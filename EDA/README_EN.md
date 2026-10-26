# EDA Versuch05 & Versuch06 – What we are actually doing here

Industrial AI · HKA WS 2026/27 · work phase until Session 2

*(German version: `README.md`)*

---

## 1. The real-world problem

In a factory hall at IPR there is a **Hybridachse**, a linear axis. A heavy steel **carriage** (Schlitten) sits on a long rail on the floor, with the base of a robot arm mounted on top. The carriage moves back and forth along the rail on a **gear rack** (Zahnstange). In this experiment the motor shaft was turned with a **cordless drill** (see the photos).

Machines like this wear out: screws loosen, bearings degrade, parts start rattling. The industrial goal is **predictive maintenance**, which means noticing that something is changing *before* the machine breaks.

The course question (lecture slide 16):

> *How can we use the measurement data to identify unusual system states?*

## 2. How it was measured: smartphones as sensors

Instead of expensive industrial sensors, **two smartphones** were placed on or near the machine and recorded with the app **phyphox**:

- **Fairphone 4** (Android)
- **iPhone 12**

A smartphone has several motion sensors built in:

| Sensor | What it measures | What it tells us here |
|---|---|---|
| **Accelerometer** | Acceleration in 3 directions (x, y, z), including gravity | Vibration of the machine, jerks when starting and stopping |
| **Linear acceleration** | The same, with gravity removed by the phone's software | Easier to read movement from |
| **Gyroscope** | How fast the phone rotates | Tilting and wobbling |
| **Magnetometer** | The magnetic field (like a compass) | Changes near steel parts, so it roughly shows *where* the carriage is |

The x, y, z axes refer to the phone itself: x and y lie across the screen, z points out of the screen. When the phone lies flat, gravity (≈ 9.8 m/s²) shows up on z. When the carriage moves along the rail, the movement shows up mostly on **y**.

## 3. How the data is organised

```
Hybridachse/
├── Versuch01 … Versuch10        ← 10 experiments; something was probably changed between them
│   └── FP_01, FP_02, FP_03      ← recordings (repeats) with the Fairphone
│   └── IP_01, IP_02, IP_03      ← recordings with the iPhone
│       ├── Accelerometer.csv    ← one table per sensor: time + x, y, z
│       ├── Gyroscope.csv
│       ├── Linear Acceleration.csv
│       ├── Magnetometer.csv
│       └── meta/
│           ├── device.csv       ← which phone, which OS, which sensor chips
│           └── time.csv         ← clock time when the recording started and paused
```

- **Versuch:** one experiment, meaning one set of conditions.
- **Recording (Messung):** one run, about 40–90 s long.
- **Repeat:** the same experiment run again (_01, _02, _03). Repeats show how much variation is "normal".

### How the files connect

- **Inside one recording:** every CSV has a `Time (s)` column that starts at 0. It lets you line the sensors up in time. At second 12.3 you can look at acceleration, rotation and magnetic field together.
- **Between two phones:** each phone has its own clock that starts at 0, so the CSV times alone don't match up. The connection is `meta/time.csv`, which stores the **real clock time** of the start.
  - Example V05: FP_01 started at 12:22:29.215 and IP_01 at 12:22:29.926.
  - Shifting the iPhone by 0.711 s puts both on one common timeline. The start times are listed in section 01 of each notebook, where you can see which recordings ran at the same time.
- **Between experiments:** nothing in the data connects them. Nobody recorded what was changed between V05 and V06. That is the most important open question.

## 4. What one recording looks like

Every recording follows the same physical story, and you can see it in the data:

```
 phone lying still → drill starts → carriage drives out → stops at the end → drives back → stops → still
 ─────────────────   ↑jerk          ~~~~~vibration~~~~~   ↑jerk            ~~~~~~~~~~~~   ↑jerk   ──────
```

- **Standing still:** the acceleration is almost flat, just sensor noise.
- **Driving:** a continuous vibration from the motor, the gears and the rail.
- **Starting and stopping:** short, strong spikes, the **impulses** (jerks).
- **Magnetic field:** changes smoothly while the carriage travels, because the phone moves past different steel parts. That's why we use it as a rough **position indicator**.

## 5. What the notebooks do

The lecture asks for an **EDA** (exploratory data analysis) before Session 2. The goal is not to detect anomalies yet. The goal is to **understand the data well enough** to know what "normal" looks like.

There is **one notebook per Versuch** (`V01.ipynb` … `V10.ipynb`). Each stands on its own and needs nothing except the raw data. All have the same structure. Versuch03 is split into two folders (`Versuch03_Fairphone`, `Versuch03_iPhone`); `V03.ipynb` loads both together.

**For another Versuch, change `VERSUCH`:** in the first code cell, set `VERSUCH = 'Versuch05'` to e.g. `'Versuch04'`. Everything else runs unchanged, and the figures automatically get the matching prefix (`V04_…`).

### Structure of a Versuch notebook

1. **Settings** (first code cell): path to the raw data (`DATA_ROOT`), the Versuch (`VERSUCH`), colours and plot style.
2. **Helper functions** (second code cell), six small functions:

| Function | What it does |
|---|---|
| `load()`, `load_versuch()` | Reads all recordings of a Versuch and unifies both phones' column names to `t, x, y, z`. Duplicate folders are skipped. |
| `drive_phases()` | Detects when the carriage is moving (see below) |
| `impulses()` | Finds jerks above 2 m/s² (starting and braking) |
| `spectrum_drive()` | Frequency spectrum during steady travel, without the jerks at the edges |
| `main_axis()` | Axis with the most motion, usually y (travel direction) |

3. **Sections 01–08**, following the tasks for Session 2. After each section, a **Befund** text summarises the numbers in the table or figure directly above it.

| Section | Plain-language question | What the notebook shows |
|---|---|---|
| 01 Describe the dataset | Which recordings and devices are there? | Table: device, start time, duration, recording pauses, sensors |
| 02 Characterise measurements | How often is it sampled, what values, how do the phones lie? | Sampling rates and gaps, value ranges, phones at rest (orientation, resting noise, gyro offset) |
| 03 Visualise signals | What does it look like? | Fig. 1: overview per recording. Fig. 2: frequency spectrum |
| 04 Compare measurements | How do the repeats differ? | Feature table, eight numbers per recording |
| 05 Data quality | Is anything missing or broken? | Table of problem files only, recording pauses |
| 06 Normal behaviour | How similar are the repeats? | Mean and coefficient of variation (CV) of the features. Fig. 3: envelopes overlaid |
| 07–08 | What do we suspect, what is unclear? | Hypotheses, open questions |

**Two terms not to mix up:**
- **Ruhe-Rauschen** (resting noise, section 02): standard deviation of the acceleration while the phone lies still, in mm/s². A property of the **phone**.
- **Fahr-Vibration** (drive vibration, section 04): median vibration level while the carriage moves, in m/s². A property of the **machine** (and of where the phone lies).

### The key trick: detecting travel phases

The most important helper is `drive_phases()`. It answers the question: *When is the carriage moving?*

1. Filter the slow changes out of the acceleration, so only the vibration is left.
2. Smooth it into a "vibration level over time" curve (the **envelope**).
3. Wherever the curve is clearly above the phone's resting noise, the carriage is moving.

The thresholds (3× above the quietest 5 % of the recording, at least 0.5 s) are rules of thumb. Fig. 1 shows the detected travel phases shaded grey, so you can check them.

Once we know *when* it moves, section 04 computes eight numbers per recording:

| Feature | Meaning |
|---|---|
| Dauer | Length of the recording |
| Fahrzeit | How long the carriage moves in total (about 40 s in every recording) |
| Fahrabschnitte | Number of travel phases longer than 2 s: 2 = continuous out and back, 5 = stop-and-go |
| Fahr-Vibration | Median vibration level while moving |
| Impulse | Number of jerks above 2 m/s² |
| max \|a\| | Strongest jerk |
| dominante Frequenz | Strongest "tone" in the spectrum above 20 Hz. The machine "hums" at 45.5, 86 and 121.6 Hz, probably from the drill and the gears |
| \|B\|-Spanne | How much the magnetic field changes, i.e. how far the phone travels past steel parts |

These numbers are the **features**. Later (Sessions 3–4), an anomaly detector compares features: *"This recording is far from the normal ones, so something is wrong."*

## 6. Why the devices matter

`00_Metadaten_Geraete.ipynb` is a **simple overview of all Versuche**. It reads only the metadata (`meta/device.csv`, `meta/time.csv`), no sensor data:

- **Table of all recording folders:** device, start time, duration, pauses.
- **Duplicates:** same phone and same start time to the millisecond, i.e. the same recording saved twice.
- **Mislabelled folders:** the folder name doesn't match the device in the metadata.
- **Device check:** whether the same Fairphone and iPhone were used every time.

How the phones *measure* (noise, orientation, sampling rate) is in section 02 of each Versuch notebook.

When two recordings differ, there are three possible causes:

1. **The machine changed.** That is what we want to detect.
2. **The phone is a different one.** A measurement effect we want to rule out.
3. **The phone was placed elsewhere.** Also a measurement effect.

So the phones themselves were checked:

- **Same phones every time?** Almost certainly yes. All metadata is identical within each model. It isn't a proof, because no serial number is stored.
- **Do they measure the same?** No:
  - The Fairphone is about 2–3× noisier at rest.
  - The iPhone samples only 100 times per second, so it can't capture tones above 50 Hz correctly. 86 Hz shows up falsely as 14 Hz (aliasing).
  - Each phone has a small calibration error. At rest the Fairphone measures gravity as ≈ 9.95 instead of 9.81 m/s² when lying display-down (g_z in section 02).

**Consequence:** compare Fairphone recordings only with Fairphone recordings, not with iPhone recordings. Or divide each value by that phone's own resting noise so they become comparable.

## 7. What we found in V05 and V06

**Versuch05**
- The **iPhone rode on the carriage**: its magnetic field changes during the whole travel.
- The **Fairphone lay still on the machine frame**, near the end of the rail. Its magnetic field barely changes, but its vibration gets stronger when the carriage comes close.
- The carriage drove **continuously**: out, short stop, back.

**Versuch06**
- Fairphone only, this time **on the carriage**.
- The carriage drove **stop-and-go**: 3 segments out, 2 back, with jerks at every stop and start.

**The catch:** between V05 and V06, *three* things changed at once: the driving style, where the Fairphone lay and possibly the machine condition. So we **cannot** simply say that V06 is the anomaly. The differences can be explained by the setup alone.

To know for sure, we need the **test protocol**: what was changed in each Versuch, and where each phone lay. That is the most important question for the lecturer.

## 8. The big picture across the semester

| Session | Goal |
|---|---|
| **1 (done)** | First look at the data |
| **2 (now)** | Understand the data properly: what normal looks like, which data issues exist, what affects the signals |
| **3** | Build an anomaly detector: compute features per travel phase, compare each recording against the "normal" group, flag outliers |
| **4** | Evaluate and present |

Our part (V05 and V06) gives the team two reference patterns: **continuous driving** and **stop-and-go**.

There is also a first possible anomaly candidate: in V06/FP_02 there is a cluster of 4 jerks at ≈ 49 s that no other repeat has.

---

## Contents of this folder

| File / folder | Contents |
|---|---|
| `V01.ipynb` … `V10.ipynb` | One notebook per Versuch, points 01–08 |
| `00_Metadaten_Geraete.ipynb` | Simple overview of all recordings from the metadata: devices, start times, duplicates |
| `figures/` | Figures as PNG: per Versuch `Vxx_1_uebersicht`, `Vxx_2_spektrum`, `Vxx_3_normalverhalten` |
| `Vortrag_Session2.md` | Speaking script (German) for the Session 2 presentation |
| `README.md` | This explanation in German |

**Running:** all notebooks are independent of each other and can run in any order.

**Adjust the path:** the first code cell of each notebook contains `DATA_ROOT`, the path to the raw data. It is the only line that needs to change on another computer.

**Requirements:** Python with `pandas`, `numpy`, `scipy`, `matplotlib`.

*Note: the notebooks' explanatory text and figure labels are in German; code comments are in English.*
