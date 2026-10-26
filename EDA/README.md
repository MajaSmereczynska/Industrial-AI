# EDA Versuch05 & Versuch06 – Was wir hier eigentlich machen

Industrial AI · HKA WS 2026/27 · Arbeitsphase bis Session 2

---

## 1. Das Problem aus der Praxis

In einer Halle bei IPR steht eine **Hybridachse**, eine Linearachse. Auf einer langen Schiene am Boden sitzt ein schwerer Stahl-**Schlitten**, auf dem der Fuß eines Roboterarms montiert ist. Der Schlitten fährt über eine **Zahnstange** vor und zurück. Im Versuch wurde die Motorwelle mit einem **Akkuschrauber** gedreht (siehe Fotos).

Solche Maschinen verschleißen: Schrauben lockern sich, Lager werden schlechter, Teile fangen an zu klappern. Das industrielle Ziel ist **Predictive Maintenance**, also Veränderungen erkennen, *bevor* etwas kaputtgeht.

Die Leitfrage der Vorlesung (Folie 16):

> *Wie können anhand der Messdaten ungewöhnliche Systemzustände identifiziert werden?*

## 2. Wie gemessen wurde: Smartphones als Sensoren

Statt teurer Industriesensoren wurden **zwei Smartphones** auf bzw. neben die Maschine gelegt. Aufgezeichnet wurde mit der App **phyphox**:

- **Fairphone 4** (Android)
- **iPhone 12**

Ein Smartphone hat mehrere eingebaute Bewegungssensoren:

| Sensor | Was er misst | Was er uns hier sagt |
|---|---|---|
| **Beschleunigungssensor** | Beschleunigung in 3 Richtungen (x, y, z), inkl. Schwerkraft | Vibration der Maschine, Rucke beim Anfahren und Bremsen |
| **Lineare Beschleunigung** | Dasselbe, Schwerkraft per Software herausgerechnet | Bewegung leichter ablesbar |
| **Gyroskop** | Wie schnell sich das Handy dreht | Kippen und Wackeln |
| **Magnetometer** | Magnetfeld (wie ein Kompass) | Ändert sich in der Nähe von Stahlteilen und zeigt so grob, *wo* der Schlitten ist |

Die Achsen x, y, z beziehen sich auf das Handy selbst: x und y liegen in der Bildschirmebene, z zeigt aus dem Bildschirm heraus. Liegt das Handy flach, erscheint die Schwerkraft (≈ 9,8 m/s²) auf z. Fährt der Schlitten entlang der Schiene, zeigt sich die Bewegung hauptsächlich auf **y**.

## 3. Wie die Daten organisiert sind

```
Hybridachse/
├── Versuch01 … Versuch10        ← 10 Versuche; dazwischen wurde vermutlich etwas verändert
│   └── FP_01, FP_02, FP_03      ← Messungen (Wiederholungen) mit dem Fairphone
│   └── IP_01, IP_02, IP_03      ← Messungen mit dem iPhone
│       ├── Accelerometer.csv    ← eine Tabelle pro Sensor: Zeit + x, y, z
│       ├── Gyroscope.csv
│       ├── Linear Acceleration.csv
│       ├── Magnetometer.csv
│       └── meta/
│           ├── device.csv       ← welches Handy, welches Betriebssystem, welche Sensorchips
│           └── time.csv         ← Uhrzeit von Start und Pause der Aufnahme
```

- **Versuch:** ein Experiment, also ein Satz an Bedingungen.
- **Messung:** ein Durchlauf von etwa 40–90 s.
- **Wiederholung:** derselbe Versuch noch einmal (_01, _02, _03). Wiederholungen zeigen, wie viel Variation „normal“ ist.

### Wie die Dateien zusammenhängen

- **Innerhalb einer Messung:** Jede CSV hat eine Spalte `Time (s)`, die bei 0 beginnt. Darüber lassen sich die Sensoren zeitlich übereinanderlegen. Bei Sekunde 12,3 kann man Beschleunigung, Drehung und Magnetfeld gemeinsam betrachten.
- **Zwischen zwei Handys:** Jedes Handy hat eine eigene Uhr, die bei 0 startet. Die CSV-Zeiten allein passen also nicht zusammen. Die Verbindung ist `meta/time.csv`, wo die **echte Uhrzeit** des Starts steht.
  - Beispiel V05: FP_01 startete um 12:22:29,215, IP_01 um 12:22:29,926.
  - Verschiebt man das iPhone um 0,711 s, liegen beide auf einer gemeinsamen Zeitachse. Die Startzeiten stehen in Abschnitt 01 jedes Notebooks. Dort sieht man, welche Messungen gleichzeitig liefen.
- **Zwischen Versuchen:** In den Daten verbindet nichts die Versuche miteinander. Es ist nicht festgehalten, was zwischen V05 und V06 verändert wurde. Das ist die wichtigste offene Frage.

## 4. Wie eine Messung aussieht

Jede Messung folgt demselben physikalischen Ablauf, und man sieht ihn in den Daten:

```
 Handy liegt still → Schrauber startet → Schlitten fährt hin → Halt am Ende → fährt zurück → Halt → still
 ─────────────────   ↑Ruck               ~~~~Vibration~~~~    ↑Ruck          ~~~~~~~~~~~~   ↑Ruck   ─────
```

- **Stillstand:** Die Beschleunigung ist fast flach, nur Sensorrauschen.
- **Fahrt:** gleichmäßige Vibration von Motor, Zahnrädern und Schiene.
- **Anfahren und Bremsen:** kurze, starke Spitzen, die **Impulse** (Rucke).
- **Magnetfeld:** ändert sich gleichmäßig, während der Schlitten fährt, weil das Handy an verschiedenen Stahlteilen vorbeikommt. Deshalb nutzen wir es als grobe **Positionsanzeige**.

## 5. Was die Notebooks machen

Die Vorlesung verlangt bis Session 2 eine **EDA** (explorative Datenanalyse). Ziel ist noch nicht, Anomalien zu erkennen, sondern die Daten **gut genug zu verstehen**, um zu wissen, wie „normal“ aussieht.

Es gibt **ein Notebook pro Versuch** (`V01.ipynb` … `V10.ipynb`). Jedes steht für sich allein und braucht außer den Rohdaten keine anderen Dateien. Alle sind gleich aufgebaut. Versuch03 liegt in zwei Ordnern (`Versuch03_Fairphone`, `Versuch03_iPhone`); `V03.ipynb` lädt beide gemeinsam.

**Für einen anderen Versuch `VERSUCH` ändern:** In der ersten Code-Zelle `VERSUCH = 'Versuch05'` z. B. auf `'Versuch04'` setzen. Der Rest läuft unverändert, und die Abbildungen bekommen automatisch das passende Präfix (`V04_…`).

### Aufbau eines Versuchs-Notebooks

1. **Einstellungen** (erste Code-Zelle): Pfad zu den Rohdaten (`DATA_ROOT`), der Versuch (`VERSUCH`), Farben und Plot-Stil.
2. **Hilfsfunktionen** (zweite Code-Zelle), sechs kleine Funktionen:

| Funktion | Was sie macht |
|---|---|
| `load()`, `load_versuch()` | Liest alle Messungen eines Versuchs ein und vereinheitlicht die Spaltennamen beider Handys auf `t, x, y, z`. Doppelte Ordner werden übersprungen. |
| `drive_phases()` | Erkennt, wann der Schlitten fährt (siehe unten) |
| `impulses()` | Findet Rucke über 2 m/s² (Anfahren und Bremsen) |
| `spectrum_drive()` | Frequenzspektrum während der gleichmäßigen Fahrt, ohne die Rucke an den Rändern |
| `main_axis()` | Achse mit der meisten Bewegung, meist y (Fahrtrichtung) |

3. **Abschnitte 01–08** entlang der Aufgaben bis Session 2. Nach jedem Abschnitt fasst ein **Befund**-Text die Zahlen aus der Tabelle bzw. Abbildung direkt darüber zusammen.

| Abschnitt | Frage in einfachen Worten | Was das Notebook zeigt |
|---|---|---|
| 01 Datensatz beschreiben | Welche Messungen und Geräte gibt es? | Tabelle: Gerät, Startzeit, Dauer, Aufnahmepausen, Sensoren |
| 02 Messungen charakterisieren | Wie oft wird gemessen, welche Werte, wie liegen die Handys? | Abtastraten und Lücken, Wertebereiche, Handys in Ruhe (Lage, Ruhe-Rauschen, Gyro-Offset) |
| 03 Signale visualisieren | Wie sieht es aus? | Abb. 1: Übersicht je Messung. Abb. 2: Frequenzspektrum |
| 04 Messungen vergleichen | Wie unterscheiden sich die Wiederholungen? | Merkmalstabelle, acht Kennzahlen pro Messung |
| 05 Datenqualität | Fehlt etwas oder ist etwas kaputt? | Tabelle nur mit problematischen Dateien, Aufnahmepausen |
| 06 Normalverhalten | Wie ähnlich sind die Wiederholungen? | Mittelwert und Variationskoeffizient (CV) der Merkmale. Abb. 3: Hüllkurven übereinandergelegt |
| 07–08 | Was vermuten wir, was ist unklar? | Hypothesen, offene Fragen |

**Zwei Begriffe, die man nicht verwechseln sollte:**
- **Ruhe-Rauschen** (Abschnitt 02): Standardabweichung der Beschleunigung, während das Handy still liegt, in mm/s². Das ist eine Eigenschaft des **Handys**.
- **Fahr-Vibration** (Abschnitt 04): mittlere Vibrationsstärke, während der Schlitten fährt, in m/s². Das ist eine Eigenschaft der **Maschine** (und des Ablageorts).

### Der zentrale Trick: Fahrphasen erkennen

Die wichtigste Hilfsfunktion ist `drive_phases()`. Sie beantwortet die Frage: *Wann fährt der Schlitten?*

1. Aus der Beschleunigung die langsamen Änderungen herausfiltern, sodass nur die Vibration übrig bleibt.
2. Diese zu einer Kurve „Vibrationsstärke über der Zeit“ glätten (die **Hüllkurve**).
3. Wo die Kurve deutlich über dem Ruherauschen des Handys liegt, fährt der Schlitten.

Die Schwellen (3× über den ruhigsten 5 % der Messung, mindestens 0,5 s) sind Erfahrungswerte. In Abb. 1 sieht man die erkannten Fahrphasen grau hinterlegt und kann sie prüfen.

Wenn wir wissen, *wann* er fährt, berechnet Abschnitt 04 acht Kennzahlen pro Messung:

| Merkmal | Bedeutung |
|---|---|
| Dauer | Länge der Aufnahme |
| Fahrzeit | Wie lange der Schlitten insgesamt fährt (in jeder Messung etwa 40 s) |
| Fahrabschnitte | Anzahl Fahrphasen über 2 s: 2 = durchgehend hin und zurück, 5 = Stop-and-go |
| Fahr-Vibration | Mittlere Vibrationsstärke während der Fahrt |
| Impulse | Anzahl der Rucke über 2 m/s² |
| max \|a\| | Stärkster Ruck |
| dominante Frequenz | Stärkster „Ton“ im Spektrum über 20 Hz. Die Maschine „brummt“ bei 45,5, 86 und 121,6 Hz, vermutlich durch Akkuschrauber und Zahnräder |
| \|B\|-Spanne | Wie stark sich das Magnetfeld ändert, also wie weit das Handy an Stahlteilen vorbeifährt |

Diese Kennzahlen sind die **Merkmale (Features)**. Später (Session 3–4) vergleicht ein Anomaliedetektor die Merkmale: *„Diese Messung liegt weit weg von den normalen, also stimmt etwas nicht.“*

## 6. Warum die Geräte wichtig sind

`00_Metadaten_Geraete.ipynb` ist ein **einfacher Überblick über alle Versuche**. Es liest nur die Metadaten (`meta/device.csv`, `meta/time.csv`), keine Sensordaten:

- **Tabelle aller Messordner:** Gerät, Startzeit, Dauer, Pausen.
- **Duplikate:** gleiches Handy und gleiche Startzeit auf die Millisekunde, also dieselbe Aufnahme zweimal gespeichert.
- **Falsch benannte Ordner:** Ordnername passt nicht zum Gerät in den Metadaten.
- **Geräteprüfung:** ob immer dasselbe Fairphone und iPhone verwendet wurden.

`00_Zeitablauf.ipynb` liest dieselben Metadaten und zeigt **Start- und Endzeiten** aller Versuche auf einer Zeitachse, fasst gleichzeitige Fairphone-/iPhone-Messungen zu Durchgängen zusammen und listet die **Pausen** zwischen Versuchen und Wiederholungen. Lange Pausen zeigen, wo ein Umbau der Maschine (Zustandswechsel) möglich war.

`00_Vergleich_Uebersicht.ipynb` zeigt **Abb. 1, 2 und 3 aller zehn Versuche untereinander** (Übersicht, Spektrum, Vibrationshüllkurve), je eine Abbildung für Fairphone und iPhone, dazu eine Tabelle mit der Stärke der Frequenzlinien 45,5 / 86 / 121,6 Hz. Alle Zeilen einer Abbildung haben dieselben Achsen, und das Magnetfeld ist als Änderung seit Messbeginn (Δ|B|) dargestellt, damit man die Versuche direkt vergleichen kann.

Wie die Handys *messen* (Rauschen, Lage, Abtastrate), steht in Abschnitt 02 jedes Versuchs-Notebooks.

Wenn sich zwei Messungen unterscheiden, kann das drei Ursachen haben:

1. **Die Maschine hat sich verändert.** Das wollen wir erkennen.
2. **Das Handy ist ein anderes.** Ein Messeffekt, den wir ausschließen wollen.
3. **Das Handy lag woanders.** Ebenfalls ein Messeffekt.

Deshalb wurden die Handys selbst geprüft:

- **Immer dieselben Handys?** Sehr wahrscheinlich ja. Alle Metadaten sind innerhalb jedes Modells identisch. Ein Beweis ist das nicht, weil keine Seriennummer gespeichert ist.
- **Messen sie gleich?** Nein:
  - Das Fairphone rauscht in Ruhe etwa 2–3× stärker.
  - Das iPhone misst nur 100-mal pro Sekunde und kann Töne über 50 Hz nicht korrekt erfassen. 86 Hz erscheint fälschlich als 14 Hz (Aliasing).
  - Jedes Handy hat einen kleinen Kalibrierfehler. Das Fairphone misst die Schwerkraft in Ruhe als ≈ 9,95 statt 9,81 m/s², wenn es mit dem Display nach unten liegt (g_z in Abschnitt 02).

**Folge:** Fairphone-Messungen nur mit Fairphone-Messungen vergleichen, nicht mit iPhone-Messungen. Oder jeden Wert durch das Ruherauschen des jeweiligen Handys teilen, damit sie vergleichbar werden.

## 7. Was wir in V05 und V06 gefunden haben

**Versuch05**
- Das **iPhone fuhr auf dem Schlitten mit**: Sein Magnetfeld ändert sich über die ganze Fahrt.
- Das **Fairphone lag ortsfest auf dem Maschinengestell**, nahe dem Ende der Schiene. Sein Magnetfeld bleibt fast konstant, aber die Vibration wird stärker, wenn der Schlitten näher kommt.
- Der Schlitten fuhr **durchgehend**: hin, kurzer Halt, zurück.

**Versuch06**
- Nur das Fairphone, diesmal **auf dem Schlitten**.
- Der Schlitten fuhr **Stop-and-go**: 3 Abschnitte hin, 2 zurück, mit Rucken bei jedem Halt und Anfahren.

**Der Haken:** Zwischen V05 und V06 haben sich *drei* Dinge gleichzeitig geändert: die Fahrweise, der Ablageort des Fairphones und eventuell der Maschinenzustand. Wir **können also nicht** einfach sagen, V06 sei die Anomalie. Die Unterschiede lassen sich allein durch den Versuchsaufbau erklären.

Um das sicher zu wissen, brauchen wir das **Versuchsprotokoll**: Was wurde in jedem Versuch verändert, und wo lag jedes Handy? Das ist die wichtigste Frage an den Dozenten.

## 8. Das große Bild über das Semester

| Session | Ziel |
|---|---|
| **1 (erledigt)** | Erster Blick auf die Daten |
| **2 (jetzt)** | Daten richtig verstehen: wie normal aussieht, welche Datenprobleme es gibt, was die Signale beeinflusst |
| **3** | Anomaliedetektor bauen: Merkmale pro Fahrphase berechnen, jede Messung mit der „normalen“ Gruppe vergleichen, Ausreißer markieren |
| **4** | Bewerten und präsentieren |

Unser Teil (V05 und V06) liefert dem Team zwei Referenzmuster: **durchgehende Fahrt** und **Stop-and-go**.

Außerdem gibt es einen ersten möglichen Anomalie-Kandidaten: In V06/FP_02 gibt es bei ≈ 49 s ein Cluster aus 4 Rucken, das keine andere Wiederholung hat.

---

## Inhalt dieses Ordners

| Datei / Ordner | Inhalt |
|---|---|
| `V01.ipynb` … `V10.ipynb` | Ein Notebook pro Versuch, Punkte 01–08 |
| `00_Metadaten_Geraete.ipynb` | Einfacher Überblick über alle Messungen aus den Metadaten: Geräte, Startzeiten, Duplikate |
| `00_Zeitablauf.ipynb` | Start-/Endzeiten, Durchgänge und Pausen zwischen den Versuchen, Zeitachse des Messtags |
| `00_Vergleich_Uebersicht.ipynb` | Abb. 1–3 aller Versuche untereinander (je Gerät) + Tabelle der Frequenzlinien, gleiche Achsen zum direkten Vergleich |
| `figures/` | Abbildungen als PNG: je Versuch `Vxx_1_uebersicht`, `Vxx_2_spektrum`, `Vxx_3_normalverhalten` |
| `Vortrag_Session2.md` | Sprechtext für die Präsentation in Session 2 |
| `README.md` / `README_EN.md` | Diese Erklärung auf Deutsch / Englisch |

**Ausführen:** Alle Notebooks sind unabhängig voneinander und können in beliebiger Reihenfolge laufen.

**Pfad anpassen:** In der ersten Code-Zelle jedes Notebooks steht `DATA_ROOT`, der Pfad zu den Rohdaten. Das ist die einzige Zeile, die auf einem anderen Rechner geändert werden muss.

**Benötigt:** Python mit `pandas`, `numpy`, `scipy`, `matplotlib`.
