

<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

**Hochschule Karlsruhe · Wintersemester 2026/2027** 

### **Industrial AI** 

**Datenvorverarbeitung, Feature-Erzeugung und Transformation** 

Session 2 im Gesamtprozess: Schritte 02–04 · Vorbereitung der Modellierung. 

# **02** 



<!-- Start of picture text -->
Relativer Wert<br>1<br>0.5<br>0<br>0 10 20 30<br>Zeit (s)<br>Synthetisches Lehrbeispiel<br><!-- End of picture text -->

###### **Session 2** 

180 Minuten · EDA, Features & Teamarbeit 

**Dr.-Ing. Yannic Wolf** CTO & Geschäftsführer Industrial AI GmbH 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**01 / 54** 

**EINSTIEG · 2–5 MIN** 

###### **Ablauf der Session** 



###### 4 Teams · zwei zusammenhängende Arbeitsblöcke mit 45 und 55 Minuten 

**0–25 Einstieg und Projektstand 25–45 Überblicksvortrag 45–90 Teamarbeit · Block 1** 0–5 Einstieg Gesamtprozess und Weg zur EDA vertiefen und Datenregeln 5–25 Berichte aus der Sample-Feature-Matrix dokumentieren Zwischenphase **90–100 Pause 100–125 Vertiefung und Ausblick 125–180 Teamarbeit · Block 2** tsfresh, DTW, Transformation Features umsetzen und 10 Minuten und nächste Zwischenphase Modellierung vorbereiten 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**02 / 54** 

**STATUSBERICHTE · 5–25 MIN** 

###### **Projektstand aus der Zwischenphase** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

4 Teams × 5 Minuten · jeweils 4 Minuten Bericht und 1 Minute Rückfragen. 

**01 Datenverständnis** Datenstruktur, Zeitbasis und relevante Datenprobleme zusammenfassen. 

**02 EDA-Ergebnis** 

Einen aussagekräftigen Plot mit Beobachtung und Hypothese erläutern. 

**03 Arbeitsstand** Erledigte Aufgaben, offene Fragen und den nächsten Prüfschritt benennen. 

Die offenen Fragen aus den Berichten bestimmen die Schwerpunkte der Teamarbeit. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**03 / 54** 

**GESAMTPROZESS · 25–27 MIN** 

###### **Grundstruktur einer datengetriebenen Anwendung** 





<!-- Start of picture text -->
Rohdaten +<br>01 Dateneingang Messwerte, Zeitstempel und Kontext einlesen.<br>Datenbeschreibung<br>02 Datenvorverarbeitung Zeitbasis, Datenqualität und Fenster festlegen. Gültige Signalabschnitte<br>03 Feature-Erzeugung Signale in numerische Merkmale überführen. Featurematrix X<br>04 Feature-Transformation Features imputieren, skalieren oder auswählen. Modellfähige Merkmale Z<br>05 Modelltraining Modellparameter auf Trainingsdaten bestimmen. Angepasstes Modell<br>06 Modellevaluation Leistung auf getrennten Daten und Fehler prüfen. Vergleich + Einsatzgrenzen<br>Vorhersagen / Scores im<br>07 Modellbereitstellung Verarbeitungskette ausführen und überwachen.<br>Betrieb<br>Hervorgehoben: Schwerpunkt Session 2 · 01: Session 1 · 05–06: Session 3 · 07: Session 4<br>Quellen: scikit-learn · Leakage and preprocessing<br><!-- End of picture text -->

Datentrennung vorab festlegen. Gelernte Verarbeitungsschritte innerhalb der Trainingsdaten anpassen. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**04 / 54** 

**KURZRÜCKBLICK · 27–29 MIN** 

###### **ML-Grundlagen · Samples, Features und Zielwerte** 





<!-- Start of picture text -->
X: 6 Samples × 3 Features y: 6 Zielwerte Train-Test-Split: gleiche Zeilen in X und y<br>f ₁ f ₂ f ₃<br>Training · Modell anpassen<br>x ₁ 10 2 5 0<br>(X_train, y_train) → f<br>x ₂ 12 4 7 1<br>x ₃ 9 3 6 0<br>x ₄ 14 5 8 1 Test · neue Samples bewerten<br>x ₅ 11 2 6 0<br>X_test → f → ŷ_test<br>x ₆ 13 4 9 1<br>ŷ_test mit y_test vergleichen<br>Featurevektor x ₂  = [12, 4, 7]<br><!-- End of picture text -->

###### **X: 6 Samples × 3 Features** 

Trennregel passend zu Zeit und Gruppen wählen. 

###### **Sample-Feature-Matrix X** 

###### **Featurevektor xᵢ** 

###### **Zielvektor y** 

n Zeilen = Samples; p Spalten = Features. Hier: X mit Form 6 × 3. 

Alle p Merkmale eines Samples i; als Zeile in X gespeichert. 

Ein Zielwert yᵢ je Sample: Klasse oder Zahl. Zuordnung zu X erhalten. 

Synthetisches Beispiel für überwachtes Lernen · Klassen 0/1 · Testdaten für die abschließende Bewertung zurückhalten. 

Quellen: scikit-learn · Samples, features and targets · <u>scikit-learn · Cross-validation</u> 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**05 / 54** 

**IDEENSAMMLUNG · 29–32 MIN** 

###### **Von Zeitreihen zur Sample-Feature-Matrix** 



###### **Zeitreihen: 12 Zeitpunkte × 2 Kanäle** 



<!-- Start of picture text -->
A<br>B<br>0 1 2 3 4 5 6 7 8 9 10 11<br>Messpunkt-Index<br><!-- End of picture text -->

Synthetische Lehrbeispiele · relative Werte und vereinfachte Zeitachsen. 

Wie würdet ihr aus diesen Zeitreihen eine Sample-Feature-Matrix erstellen? 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**06 / 54** 

**02 → 03 · BEOBACHTUNGSEINHEIT · 29–32 MIN** 

###### **Von Zeitreihen zur Sample-Feature-Matrix** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

###### **Zeitreihen: 12 Zeitpunkte × 2 Kanäle** 

###### **X: 3 Samples × 4 Features** 



<!-- Start of picture text -->
w1 w2 w3<br>A je Fenster<br>B<br>oo —-<br>0 4 8 12<br>Messpunkt-Index<br><!-- End of picture text -->

|ID|A.mean|A.std|B.mean|B.std|
|---|---|---|---|---|
|w1|1|0,71|2|0|
|w2|2|0,71|3|0|
|w3|2|1,41|4|0|



ID ≠ Feature 

Separate Metadaten: record_id, Fensterstart, Fensterende 

###### **Sample = Beobachtung** 

###### **Feature = Spalte** 

###### **Zielwert y separat** 

Hier: ein abgeschlossenes Fenster einer Messung. 

Dieselbe Definition, Einheit und Reihenfolge für jede Zeile. 

Bei überwachtem Lernen gehört zu jeder Zeile ein passender Zielwert. 

Synthetische Lehrbeispiele · relative Werte und vereinfachte Zeitachsen. 

Quellen: scikit-learn · Samples, features and targets 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**07 / 54** 

**FRAGE INS PLENUM · 32–35 MIN** 

###### **Zeitreihen strukturieren** 



Welche Entscheidungen müsst ihr treffen, bevor aus einer Zeitreihe mehrere Samples werden? 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**08 / 54** 

**02 → 03 · FENSTERBILDUNG · 32–35 MIN** 

###### **Fensterlänge und Schrittweite bestimmen die Zeilen** 





<!-- Start of picture text -->
Länge 4 · Schrittweite 2 Länge 6 · Schrittweite 6<br>0 1 2 3 4 5 6 7 8 9 10 11 0 1 2 3 4 5 6 7 8 9 10 11<br>w1 w1<br>w2 w2<br>w3<br>w4<br>w5<br>5 Matrixzeilen 2 Matrixzeilen<br><!-- End of picture text -->

Überlappende Fenster teilen Rohwerte. 

Längere Fenster fassen mehr Verlauf zusammen. 

###### **Zeitskala** 

###### **Informationsverlust** 

###### **Abhängigkeit** 

Fensterdauer an Ereignisdauer und Große Fenster können kurze Ereignisse Entscheidungsrhythmus ausrichten. abschwächen. 

Mehr Fenster erzeugen zusätzliche, oft stark ähnliche Zeilen. 

Synthetische Lehrbeispiele · relative Werte und vereinfachte Zeitachsen. 

Quellen: pandas · Rolling windows 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**09 / 54** 

**FRAGE INS PLENUM · 35–38 MIN** 

###### **Messungen vergleichen** 



Wie würdet ihr Messungen mit unterschiedlicher Länge und unterschiedlichen Zeitstempeln vergleichbar machen? 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**10 / 54** 

**02 · VERGLEICHBARKEIT · 35–38 MIN** 

###### **Messlängen und Sensorzeitachsen unterscheiden sich** 





<!-- Start of picture text -->
Unterschiedliche Messlängen Unterschiedliche Zeitstempel<br>A<br>A · n=8<br>0 1 2 3 4<br>Oooococooo one ee<br>B<br>B · n=5 ? ? ?<br>Oo oo 2<br>0,4 2,4 4,4<br>unbeobachtet<br>Zeit (s)<br>Fenster / Zyklus / Gesamtversuch festlegen. Über Zeit und Versuch zuordnen.<br><!-- End of picture text -->

**Länge Synchronisation** Abschneiden, Auffüllen und Aggregation Gleiche Zeilennummern können verschiedene verändern die Aussage. Zeitpunkte beschreiben. Synthetische Lehrbeispiele · relative Werte und vereinfachte Zeitachsen. Quellen: pandas · Time-based joins · <u>pandas · Rolling windows</u> 

###### **Regel** 

Zeitbasis, Toleranz und verfügbare Werte dokumentieren. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**11 / 54** 

**FRAGE INS PLENUM · 38–41 MIN** 

###### **Unvollständige Messungen** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

###### Ein Sensor fällt zeitweise aus. Wie würdet ihr mit den betroffenen Samples umgehen? 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**12 / 54** 

**02 → 04 · DATENABDECKUNG · 38–41 MIN** 

###### **Unvollständige Fenster erzeugen ungültige Features** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

###### **Beispiel: vollständige B-Fenster erforderlich** 



<!-- Start of picture text -->
ID A.mean B.mean B.std B.coverage<br>w1 1 2 0 100 %<br>w2 2 NaN NaN 50 %<br>w3 2 NaN NaN 0 %<br>w4 3 4 0 100 %<br><!-- End of picture text -->

###### **Lücken → ungültige Zellen** 

**Konstanter Kanal → std = 0** 

**Abdeckung separat mitführen** 

###### Ausschluss oder begründete Imputation 

###### **NaN** 

###### **Konstante Spalten** 

###### **Nachvollziehbarkeit** 

Fehlende Messungen sind von gültigen Nullwerten zu unterscheiden. 

Bei Standardisierung ist eine Regel für σ = 0 erforderlich. 

Maske, Abdeckung und verworfene Fenster protokollieren. 

Synthetische Lehrbeispiele · relative Werte und vereinfachte Zeitachsen. 

Quellen: scikit-learn · Leakage and preprocessing · <u>pandas · Interpolation</u> 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**13 / 54** 

**FRAGE INS PLENUM · 41–43 MIN** 

###### **Vorhersagen vorbereiten** 



Wir treffen bei t = 6 eine Vorhersage für t = 9. Welche Informationen dürfen in das Sample eingehen? 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**14 / 54** 

**03 · ENTSCHEIDUNGSZEITPUNKT · 41–43 MIN** 

###### **Features und Zielwerte brauchen einen Zeitbezug** 





<!-- Start of picture text -->
Verfügbar bis zur Entscheidung Spätere Beobachtungen<br>Eingangsfenster [2, 6) Prognoseziel bei t + h = 9<br>0 2 4 6 8 9 10 12<br>Entscheidung t = 6<br>X-Zeile: Features aus dem Eingangsfenster y: separat zugeordnetes Ziel<br>Schlüssel: Versuch + Fensterende + Zieldefinition<br><!-- End of picture text -->

**Verfügbarkeit Zieldefinition Zuordnung** Eingangsdaten müssen zum gewählten Prognosehorizont oder Ereigniszuordnung X, y und Gruppen über stabile IDs gemeinsam Entscheidungszeitpunkt vorliegen. fachlich festlegen. filtern und sortieren. Synthetisches Prognosebeispiel · bei Anomalieerkennung sind bestätigte Labels optional und gesondert zu prüfen. Quellen: scikit-learn · Samples, features and targets · <u>scikit-learn · Lagged features</u> 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**15 / 54** 

**FRAGE INS PLENUM · 43–45 MIN Übertragbarkeit prüfen** 



Wie würdet ihr Trainings- und Testdaten trennen, um die Übertragbarkeit auf neue Messungen zu prüfen? 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**16 / 54** 

**03 → 06 · DATENTRENNUNG · 43–45 MIN** 

###### **Überlappende Fenster beeinflussen den Modellvergleich** 



###### **Ein Versuch: Fenster teilen Rohdaten** 

**Ziel: auf neue Versuche übertragen** 



<!-- Start of picture text -->
0 1 2 3 4 5 6 7 8 9 10 11<br>Train · w1 [0,6)<br>Test · w2 [4,10)<br>Gemeinsame Messpunkte<br><!-- End of picture text -->



<!-- Start of picture text -->
Versuch A → Training<br>Versuch B → Test<br><!-- End of picture text -->

Trennung nach Versuch vor der Fensterbildung 

###### **Abhängigkeit** 

###### **Einsatzbezug** 

###### **Trainingsgrenze** 

Zufällige Zeilensplits können fast gleiche Fenster Für neue Versuche nach Versuch gruppieren; für auf beide Seiten verteilen. Zukunftsprognosen zeitlich trennen. 

Imputation, Skalierung und Auswahl innerhalb der Trainingsdaten anpassen. 

Synthetische Lehrbeispiele · relative Werte und vereinfachte Zeitachsen. 

Quellen: scikit-learn · Cross-validation · <u>scikit-learn · Leakage and preprocessing</u> 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**17 / 54** 

**02 → 03 · ARBEITSBLOCK 1 · 45–90 MIN** 

###### **Teamarbeit · EDA und Datenqualität** 



##### 45 min 

**01 Analyse vertiefen** 

Messungen vergleichen; Trends, wiederkehrende Muster und Streuung untersuchen. 

Bearbeitet die offenen Fragen aus eurem Statusbericht. Setzt eigene Prioritäten und arbeitet bis zur Pause 

durchgehend im Team. 

**02 Datenregeln prüfen** Zeitbasis, Fehlwerte und Auffälligkeiten prüfen; Entscheidungen begründen. 

Sample definieren: Messung, Fenster, Zeitpunkt und gemeinsame FeatureSpalten. 

**03 Ergebnisse sichern** 

Bis zur Pause: EDA-Notebook, zwei Plots und ein Schema für die Sample-Feature-Matrix. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**18 / 54** 

**90–100 min Pause** 



**Anschließend: technische Vertiefung und Ausblick auf die nächste Zwischenphase.** Lasst einen Plot geöffnet, an dem ihr weiterarbeiten möchtet. 

## **10 min** 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**19 / 54** 

**FRAGE INS PLENUM · 100–104 MIN** 

###### **Die Featurematrix weiterverarbeiten** 



Eine Featurematrix enthält Lücken und stark unterschiedliche Größenordnungen. Wie würdet ihr sie für ein Modell vorbereiten? 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**20 / 54** 

**04 · FEATURE-TRANSFORMATION · 100–104 MIN** 

###### **Featurematrix für das Modell vorbereiten** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

**Entscheidung Anpassung auf Trainingsdaten Anwendung auf neue Daten** `Imputation` Ersatzwerte und gültige Spalten festlegen Gespeicherte Ersatzwerte verwenden `Skalierung` μ und σ je Feature bestimmen z = (x − μ_train) / σ_train `Auswahl / PCA` Spaltenauswahl oder Projektion lernen Identische Spalten / Projektion nutzen Quellen: scikit-learn · Leakage and preprocessing 

fit auf Trainingsdaten; transform auf Validierungs-, Test- und Betriebsdaten. Alle Schritte gemeinsam versionieren. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**21 / 54** 

**03 · TECHNISCHE VERTIEFUNG · 104–106 MIN** 

###### **tsfresh · Automatische Feature-Erzeugung** 



tsfresh berechnet ausgewählte statistische Merkmale für jede definierte Zeitreihe oder jedes Fenster. 

**01 Eingang** Tabelle mit id, time und value. Jede id bezeichnet hier ein vorbereitetes Fenster. **02 Berechnung** Feature-Funktionen auswählen, z. B. mean, standard_deviation und maximum. 

**03 Ausgang** Eine Zeile pro Fenster; eine Spalte pro berechnetem Feature. 

Quellen: tsfresh · Feature extraction · <u>tsfresh · Data formats</u> 

Synthetisches Fenster [0, 1, 2, 1] → mean = 1 · std ≈ 0,707 · maximum = 2 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**22 / 54** 

**03 · TECHNISCHE VERTIEFUNG · 106–110 MIN** 

###### **tsfresh · Fenster in eine Featurematrix überführen** 



```
from tsfresh import extract_features
fc = {
```

```
    'mean': None, 'standard_deviation': None,
```

###### **windows** 

Vorbereitete Tabelle: id, time, value; endliche Werte innerhalb gültiger Fenster. 

```
    'maximum': None,
```

```
}
```

```
X = extract_features(
```

```
    windows, column_id='id', column_sort='time',
    column_value='value', default_fc_parameters=fc,
    n_jobs=0, disable_progressbar=True,
```

```
)
```

###### **Ergebnis** 

X.index enthält Fenster-IDs. Spalten heißen z. B. value__mean. 

###### **Prüfung** 

Ein Fenster manuell nachrechnen; ungültige Feature-Werte gezielt behandeln. 

Ausführbares synthetisches Beispiel: feature-methods.py · keine Spaltenvorgabe für den Projektdatensatz. 

Quellen: tsfresh · Extraction settings · <u>tsfresh · Data formats</u> 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**23 / 54** 

**FRAGE INS PLENUM · 110–113 MIN Ähnliche Signalverläufe** 



Zwei Signale verlaufen ähnlich, sind aber zeitlich versetzt oder unterschiedlich schnell. Wie würdet ihr ihre Ähnlichkeit bewerten? 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**24 / 54** 

**03 · TECHNISCHE VERTIEFUNG · 110–113 MIN** 

###### **Dynamic Time Warping · Verläufe vergleichen** 



###### **Zeitliche Zuordnung mit DTW** 



<!-- Start of picture text -->
2<br>A<br>1<br>0<br>0 1 2 3 4 5<br>2<br>B<br>1<br>0<br>0 1 2 3 4 5<br>Sample-Index · relative Werte<br><!-- End of picture text -->

###### **Fragestellung** 

Gleiche Form bei unterschiedlichem zeitlichem Ablauf? 

###### **Zuordnung** 

DTW ordnet Werte entlang eines monotonen Pfads zu; Wiederholungen sind möglich. 

###### **Ergebnis** 

Die Distanz zur Referenz kann ein Feature oder ein Anomalie-Score sein. 

###### **Punktweise Distanz = 2 · DTW = 0** 

Synthetisches Beispiel · Punktdistanz: √Σ(Aᵢ − Bᵢ)² = 2 · DTW: √Σ Pfadkosten = 0 · Radius 1 

Quellen: tslearn · Dynamic Time Warping 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**25 / 54** 

**03 · TECHNISCHE VERTIEFUNG · 113–117 MIN** 

###### **DTW berechnen und die Anpassung begrenzen** 



```
from tslearn.metrics import dtw_path
a = [0, 1, 2, 1, 0, 0]
b = [0, 0, 1, 2, 1, 0]
path, distance = dtw_path(
    a, b, global_constraint='sakoe_chiba',
    sakoe_chiba_radius=1,
)
```

###### **Zeitliche Grenze** 

Radius 1 erlaubt im Beispiel |i − j| ≤ 1. 

###### **Fachliche Grenze** 

Zeitfehler können durch Warping verdeckt werden; Amplitude und Skalierung prüfen. 

```
# distance == 0.0
```

###### **Referenzwahl** 

Referenz und Parameter auf Entwicklungsdaten festlegen; getrennt evaluieren. 

Kostenrekursion: Cᵢ `ⱼ` = (aᵢ − b `ⱼ` )² + min(Cᵢ ₋₁ , `ⱼ` , Cᵢ, `ⱼ` ₋₁ , Cᵢ ₋₁ , `ⱼ` ₋₁ ) · DTW = √Cₙₘ 

Quellen: tslearn · dtw_path 

DTW passt, wenn Zeitvariation zulässig ist. Bei zeitkritischen Fehlern die zeitliche Abweichung gesondert bewerten. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**26 / 54** 

**ÜBERGANG ZU 05–06 · BASELINE UND EVALUATION · 117–120 MIN** 

###### **Referenzdaten, Score und Schwelle** 

01 

02 

**Score** 

**Normalbereich** 

Welche Versuche gelten begründet als vergleichbar und unauffällig? 

In der Demo: std_8 pro gültigem Zeitpunkt. 



03 

**Regel** 

Score oberhalb einer vorab gewählten Schwelle markieren. 

Quellen: scikit-learn · Novelty detection 

Ohne bestätigte Referenz bleiben die Ergebnisse explorative Kandidaten zur Prüfung. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**27 / 54** 

**AUSBLICK AUF DIE ZWISCHENPHASE · 120–125 MIN** 

###### **Arbeitsauftrag bis Session 3** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

Beginnt die Umsetzung im folgenden Arbeitsblock und führt sie bis Session 3 eigenständig fort. 

Feature- und Transformationsregeln festhalten; eine einfache Baseline auf Trainingsdaten **01 05 · Baseline trainieren** anpassen. 

**02 06 · Varianten evaluieren** Einen Ansatz gezielt verändern; dieselbe Datentrennung für den Vergleich nutzen. 

**03 07 · Einsatz vorbereiten** Datenvertrag, gespeicherte Verarbeitungsschritte und Überwachungsbedarf beschreiben. 

Zu Session 3: reproduzierbare Verarbeitung, Baseline-Vergleich und Review-Protokoll. Deployment wird in Session 4 vertieft. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**28 / 54** 

**03 → 04 · ARBEITSBLOCK 2 · 125–180 MIN** 

###### **Teamarbeit · Features und Modellierungsplan** 



##### 55 min 

**01 Features umsetzen** 

Kleine Sample-Feature-Matrix berechnen. Eine Zeile am Signal nachrechnen; IDs sichern. 

Setzt eure FeatureIdee um und bereitet die erste 

Modellierungsiteration vor. Arbeitet bis zum Ende der Session im Team. 

**Transformation 02 prüfen** 

**03 Weiterarbeit planen** 

Fehlende Features und Skalierung prüfen; Anpassung auf Trainingsdaten begrenzen. 

Aufgaben, Verantwortliche, Abnahmekriterien und einen Review-Termin dokumentieren. 

Zum Ende: Feature-Code, geprüfte Transformationsregel und Plan für Training und Evaluation. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**29 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Ab Sekunde 16 schwingt das Signal stärker** 





<!-- Start of picture text -->
Ein Versuch verändert sich<br>Relativer Wert<br>1<br>Beobachten<br>Die Ausschläge werden größer. Der Mittelwert<br>bleibt ähnlich.<br>Erklären<br>0<br>Belastung? Veränderte Struktur? Messfehler?<br>Prüfen<br>Welche zusätzliche Information trennt diese<br>Erklärungen?<br>-1<br>0 8 16 24 32<br>Zeit (s)<br><!-- End of picture text -->

Synthetisches Lehrbeispiel · relative Einheiten · unabhängig vom Projektdatensatz. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**30 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Darstellungen für die Zeitreihenanalyse** 



**01 Zeitverlauf** Wann beginnt die Änderung? Welche Phase liegt davor und danach? 

**02 Verteilung** Wie ändern sich Lage und Streuung innerhalb vergleichbarer Phasen? 

**03 Versuchsvergleich** 

Bleibt das Muster bei gleichem Ablauf oder Betriebszustand bestehen? 

Quellen: FPP3 · Time series graphics 

Jeder Plot beantwortet eine konkrete Frage und führt zu einem nächsten Prüfschritt. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**31 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Trend, Periodik und Saisonalität** 



<!-- Start of picture text -->
Trend + Wiederholung<br>Relativer Wert<br>1.5<br>0.5<br>-0.5<br>0 8 16 24 32<br>Zeit (s)<br>Wiederholung<br>Relativer Wert<br>0.5<br>0<br>-0.5<br>0 8 16 24 32<br>Zeit (s)<br><!-- End of picture text -->



###### **Trend** 

Das Niveau verändert sich über den beobachteten Zeitraum. 

###### **Periodik** 

Ein Muster kehrt in ähnlichen Abständen wieder. 

###### **Saisonalität** 

Kalendergebundene Wiederholung braucht passende Zeitabdeckung. 

Synthetisches Lehrbeispiel · relative Einheiten · unabhängig vom Projektdatensatz. 

Quellen: FPP3 · Time series graphics 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**32 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Autokorrelation und zeitliche Abhängigkeit** 



<!-- Start of picture text -->
Regelmäßige synthetische Referenz<br>Relativer Wert<br>0.5<br>0<br>-0.5<br>0 8 16 24 32<br>Zeit (s)<br>Autokorrelation der Referenz<br>ACF<br>1<br>0<br>-1<br>0 8 16 24 32<br>Lag (Samples)<br><!-- End of picture text -->



###### **Lag k** 

Vergleicht eine Reihe mit ihrer um k Schritte verschobenen Version. 

###### **ACF bei 16** 

Die Demo wiederholt sich nach 16 Samples = 4 Sekunden. 

###### **Einordnen** 

Trend, kurze Reihen und Zustandswechsel beeinflussen die ACF. 

Synthetische Referenz · ACF aus den gezeigten 128 Werten berechnet. 

Quellen: FPP3 · Time series graphics 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**33 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Zeitachse und Abtastung prüfen** 



**01 Reihenfolge** 

Pro Versuch sortieren; doppelte Zeitpunkte und Rücksprünge klären. 

**02 Abstände** 

Verteilung von Δt prüfen. Ein Lag von 8 Zeilen hat nur bei konstantem Δt eine feste Dauer. 

**03 Grenzen** 

Versuche und Unterbrechungen getrennt behandeln; Fenster innerhalb gültiger Abschnitte bilden. 

Quellen: pandas · Rolling windows · <u>pandas · Series.shift</u> 

Ein regelmäßiges Raster und eine dokumentierte Zeitbasis machen Features interpretierbar. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**34 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Regeln für fehlende und auffällige Werte** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

|**Befund**|**Mögliche Entscheidung**|**Beleg sichern**|
|---|---|---|
|`Zeitbasis`|Sortierung, Abstände und Versuchstrennung prüfen|Zeitstempel + Fensterdefinition|
|`Kurze Lücke`|Begrenzt füllen, falls fachlich plausibel|Rohwerte + Fehlwertmaske|
|`Lange Unterbrechung`|Abschnitt trennen; Fenster verwerfen|Dauer + Ausschlussgrund|
|`Einzelne Spitze`|Ursache prüfen; zunächst markieren|Original + Kontext|
|`Neues Niveau`|Betriebsphase und Kalibrierung prüfen|Vorher/Nachher-Vergleich|



Quellen: NIST · Detection of outliers · <u>pandas · Interpolation</u> 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**35 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Features aus Hypothesen ableiten** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

**Vermutetes Muster Kandidat Wichtige Grenze** `Niveau verschiebt sich` Rolling Mean / Median Fenster kann Übergang verwischen `Streuung nimmt zu` Rolling Std Spitzen und Betriebszustand wirken mit `Dynamik verändert sich` Lag-Wert / Differenz Zeitraster bestimmt Bedeutung `Schwingung wird stärker` RMS oder Streuung RMS reagiert auch auf Offset Quellen: pandas · Rolling windowspandas · Rolling windows· Rolling windows Rolling windows Unsere Demo-Hypothese führt zur lokalen Standardabweichung. 

Quellen: pandas · Rolling windowspandas · Rolling windows· Rolling windows Rolling windows 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**36 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Datenverfügbarkeit zum Entscheidungszeitpunkt** 



Konvention: Wir entscheiden bei t, bevor xₜ verfügbar ist. 

**Größe bei t Verwendete Werte Beispiel bei t = 4** `x: 2, 4, 6, 8, 10` Index: 0, 1, 2, 3, 4 x ₄ = 10 ist noch unbekannt `lag₁(t)` xₜ ₋₁ 8 `mean₃(t)` xₜ ₋₃ … xₜ ₋₁ (4 + 6 + 8) / 3 = 6 `std₃(t), ddof = 0` xₜ ₋₃ … xₜ ₋₁ √(8/3) ≈ 1,63 

Quellen: pandas · Series.shift · <u>scikit-learn · Lagged features</u> 

Für eine Diagnose nach Eingang von xₜ darf xₜ Teil des Fensters sein. Zeitpunkt und Ziel explizit festlegen. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**37 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Lag- und Rolling-Features mit pandas** 

```
# x: one regular, ordered recording
past = x.shift(1)
features = pd.DataFrame({
    'lag_1': past,
    'mean_8': past.rolling(8, min_periods=8).mean(),
    'std_8': past.rolling(8, min_periods=8).std(ddof=0),
})
```

```
valid = features.notna().all(axis=1)
```



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

###### **Fenster** 

8 Samples bei 4 Hz: 2 Sekunden Demo-Kontext. 

###### **Abdeckung** 

Die ersten 8 Zeilen und unvollständige Fenster bleiben ungültig. 

###### **Pro Versuch** 

Den Code für jeden gültigen Abschnitt getrennt ausführen. 

Python · pandas · Demo-Parameter; Sampling und Fenster für das Projekt begründen. 

Quellen: pandas · Rolling windows · <u>pandas · Series.shift</u> 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**38 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Einfluss der Fensterlänge** 



###### **Nachlaufende Standardabweichung** 



<!-- Start of picture text -->
Relativer Wert<br>0.6<br>0.3<br>0<br>0 8 16 24 32<br>8 Samples 32 Samples Zeit (s)<br><!-- End of picture text -->

###### **8 Samples** 

Reagiert rascher; variiert mit der Phase des Signals. 

###### **32 Samples** 

Mittelt über mehr Zyklen; Übergänge wirken länger nach. 

###### **Wahl begründen** 

Ereignisdauer, Abtastrate und zulässige Verzögerung verbinden. 

Synthetisches Lehrbeispiel · relative Einheiten · unabhängig vom Projektdatensatz. 

Quellen: pandas · Rolling windows 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**39 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Anwendung einer schwellenbasierten Baseline** 



###### **Score des zweiten Versuchs** 



<!-- Start of picture text -->
Relativer Wert<br>0.6<br>Konstruierte Änderung<br>0.3<br>0<br>0 8 16 24 32<br>std_8 Referenzschwelle Zeit (s)<br><!-- End of picture text -->

###### **Kalibrieren** 

Demo-Schwelle: 95. Perzentil der gültigen Referenz-Scores. 

###### **Anwenden** 

Dieselbe Regel auf den zweiten Demo-Versuch anwenden. 

###### **Zurück zum Signal** 

Markierte Abschnitte im Rohsignal und Kontext prüfen. 

Synthetisches Lehrbeispiel · relative Einheiten · unabhängig vom Projektdatensatz. 

Quellen: scikit-learn · Novelty detection 

Ein erhöhter Score begründet eine Untersuchung. Die Ursache bleibt eine fachliche Frage. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**40 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Datentrennung für den Modellvergleich** 



**01 Versuche trennen** 

- Fenster desselben Versuchs bleiben zusammen. Gruppierung am späteren Einsatz ausrichten. 

**02 Zeit beachten** 

Für zukünftige Einsätze auf späteren Daten prüfen. Überlappung an Grenzen vermeiden. 

**03 Regeln festlegen** 

Features und Schwellen auf Entwicklungsdaten wählen. Den finalen Test reservieren. 

Quellen: scikit-learn · Cross-validation · <u>scikit-learn · Lagged features</u> 

Heute: Trennregel dokumentieren. Session 3: Backtesting, Metriken und Fehleranalyse. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**41 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Aufgaben und Abnahmekriterien** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

**Verantwortung → Aufgabe Fertig, wenn … Review** `Zeitbasis und Referenz` A → B Prüfbericht + begründete Versuchsliste vorliegen `prüfen Feature-Funktion bauen` B → C Fenster, Einheiten und Fehlwertregel geprüft sind Score-Plot und feste Schwelle reproduzierbar `Baseline anwenden` C → A sind `Gemeinsames Review` Alle Befund, Grenze und nächster Versuch feststehen 

Quellen: Schwaber & Sutherland · Scrum Guide 

Gemeinsames Done: frischer Lauf, dokumentierte Parameter, geprüfter Plot und festgehaltene Grenzen. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**42 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Beobachtungen und Hypothesen dokumentieren** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

**Schritt Eintrag im EDA-Log** `Beobachtung` Größere Ausschläge im Demo-Intervall 16–24 s. `Hypothese` Die lokale Streuung bildet diese Änderung ab. `Alternative` Ein anderer Betriebszustand erzeugt dieselbe Änderung. `Nächster Check` Streuung in vergleichbaren Phasen und Versuchen vergleichen. Ein EDA-Ergebnis verbindet Beleg, Erklärung und Konsequenz für die Modellierung. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**43 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Feature-Definition dokumentieren** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

|**Feld**<br>**Demo-Entscheidung**|
|---|
|`Zweck`<br>Erhöhte lokale Streuung sichtbar machen|
|`Eingang`<br>Ein gültiger, regelmäßiger Signalabschnitt|
|`Zeitbezug`<br>8 frühere Werte; xₜbleibt ausgeschlossen|
|`Fehlwerte`<br>Nur vollständige Fenster auswerten|
|`Ausgang`<br>std_8 in derselben Einheit wie das Eingangssignal|
|Eine andere Person im Team kann das Feature mit denselben Regeln reproduzieren.|



**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**44 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Iterationsziel, Abstimmung und Review** 

01 

02 

**Iterationsziel** 

**Kurze Abstimmung** 

Eine begründete Baseline auf getrennten Versuchen reproduzieren. 

Was ist fertig? Was blockiert? Welche Übergabe braucht ihr? 



03 

**Review** 

Code ausführen, Befunde prüfen, nächste Änderung wählen. 

Quellen: Schwaber & Sutherland · Scrum Guide 

Teamregel: Eine Person verantwortet die Aufgabe; eine zweite prüft das Ergebnis. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**45 / 54** 

**ANHANG · OPTIONALE VERTIEFUNG** 

###### **Ergänzung: Baselines für Prognosen** 



Für Energie- oder Verbrauchsreihen: Ziel ist der nächste Wert xₜ. 

|**Baseline**|**Vorhersage bei t**|**Voraussetzung**|
|---|---|---|
|`Naiv`|x̂ₜ= xₜ₋₁|Letzter Wert ist bekannt|
|`Saisonal naiv`|x̂ₜ= xₜ₋ₘ|Periode m ist fachlich begründet|
|`Mittelwert`|x̂ₜ= Mittelwert der Trainingswerte|Referenzzeitraum ist geeignet|
|Quellen:<br>FPP3·Forecasting toolbox|||



Prognosen: Fehler zu später beobachteten Werten messen. Anomalien: markierte Ereignisse fachlich prüfen. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**46 / 54** 

**ANHANG · ZUM AUSFÜLLEN IM TEAM** 

###### **Arbeitsblatt · EDA → Feature → Iteration** 

###### **Befund** 

###### **Hypothese** 

###### **Datenregel** 

Plot / Messung / Abschnitt Beobachtung: … 

Erklärung: … Alternative: … 

Zeitbasis: … Lücken / Ausreißer: … 

###### **Aufgaben** 

###### **Vergleich** 

###### **Iterationsziel** 

Owner / Reviewer: … Abhängigkeit: … 

Prüfbares Ergebnis: … Termin: … 

Trennregel: … Prüfkriterium / Grenze: … 



###### **Feature** 

###### **Baseline** 

Eingang / Einheit: … Fenster / Zeitpunkt: … 

Referenz: … Score / Regel: … 

###### **Done** 

###### **Review** 

Frischer Lauf / Plot: … Termin / Teilnehmende: Parameter / Grenzen: … … Nächste Entscheidung: 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**47 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Session 2 · Von Signalen zu Modellmerkmalen** 



#### 02 

###### **Vorverarbeitung** 

Datenqualität und Zeitbasis prüfen. Beobachtungseinheit und Fenster definieren. 

03 

###### **Feature-Erzeugung** 

Pro Sample fachlich begründete Merkmale berechnen und in gemeinsamen Spalten ablegen. 

04 

###### **Transformation** 

Fehlende Features behandeln, Größenordnungen anpassen und Auswahl begründen. 

Block 1: Datenbasis und Feature-Idee. Block 2: Featurematrix, Transformationsregel und Modellierungsplan. 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**48 / 54** 

**ANHANG · ARBEITSREFERENZ** 

###### **Feature-Erzeugung und Transformation** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

|**Schritt**|**Eingang → Ausgang**|**Beispiel**|
|---|---|---|
|`03 · Erzeugung`|Signalabschnitt → Merkmale|Mittelwert, Streuung, Maximum|
|`03 · Erzeugung`|Signalabschnitt → Trend|Steigung über das definierte Fenster|
|`04 · Transformation`|Merkmale → skalierte Merkmale|z = (x − μ_train) / σ_train|
|`04 · Transformation`|Viele Merkmale → Teilmenge|Konstante oder redundante Features prüfen|
|Die Feature-Definition bestimmt|die gemessene Eigenschaft. Die Transforma|tion bestimmt ihre Darstellung für das Modell.|



**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**49 / 54** 

**ANHANG · PRIMÄRQUELLEN · RECHERCHIERT AM 25.10.2026** 

###### **Quellen · Analyse & Daten** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

###### **<u>FPP3 · Time series graphics</u>** 

https://otexts.com/fpp3/graphics.html 

###### **<u>NIST · Detection of outliers</u>** 

https://www.itl.nist.gov/div898/handbook/eda/section3/eda35h.htm 

###### **<u>pandas · Interpolation</u>** 

https://pandas.pydata.org/docs/reference/api/pandas.Series.interpolate.html 

###### **<u>pandas · Rolling windows</u>** 

https://pandas.pydata.org/docs/reference/api/pandas.Series.rolling.html 

###### **<u>pandas · Series.shift</u>** 

https://pandas.pydata.org/docs/reference/api/pandas.Series.shift.html 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**50 / 54** 

**ANHANG · PRIMÄRQUELLEN · RECHERCHIERT AM 25.10.2026** 

###### **Quellen · Baselines & Zusammenarbeit** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

###### **<u>FPP3 · Forecasting toolbox</u>** 

https://otexts.com/fpp3/toolbox.html 

###### **<u>scikit-learn · Lagged features</u>** 

https://scikit-learn.org/stable/auto_examples/applications/plot_time_series_lagged_features.html 

###### **<u>scikit-learn · Cross-validation</u>** 

https://scikit-learn.org/stable/modules/cross_validation.html 

###### **<u>scikit-learn · Novelty detection</u>** 

https://scikit-learn.org/stable/modules/outlier_detection.html 

###### **<u>Schwaber & Sutherland · Scrum Guide</u>** 

https://scrumguides.org/scrum-guide.html 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**51 / 54** 

**ANHANG · PRIMÄRQUELLEN · RECHERCHIERT AM 25.10.2026** 

###### **Quellen · Sample-Feature-Matrix** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

###### **<u>scikit-learn · Samples, features and targets</u>** 

https://scikit-learn.org/stable/getting_started.html 

###### **<u>pandas · Time-based joins</u>** 

https://pandas.pydata.org/docs/reference/api/pandas.merge_asof.html 

###### **<u>scikit-learn · Cross-validation</u>** 

https://scikit-learn.org/stable/modules/cross_validation.html 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**52 / 54** 

**ANHANG · PRIMÄRQUELLEN · RECHERCHIERT AM 25.10.2026 Quellen · tsfresh** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

###### **<u>tsfresh · Feature extraction</u>** 

https://tsfresh.readthedocs.io/en/latest/text/introduction.html 

###### **<u>tsfresh · Data formats</u>** 

https://tsfresh.readthedocs.io/en/latest/text/data_formats.html 

###### **<u>tsfresh · Extraction settings</u>** 

https://tsfresh.readthedocs.io/en/latest/text/feature_extraction_settings.html 

###### **<u>tsfresh · Quick start</u>** 

https://tsfresh.readthedocs.io/en/latest/text/quick_start.html 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**53 / 54** 

**ANHANG · PRIMÄRQUELLEN · RECHERCHIERT AM 25.10.2026** 

###### **Quellen · DTW und Transformation** 



<!-- Start of picture text -->
Industrial_AI<br><!-- End of picture text -->

###### **<u>tslearn · Dynamic Time Warping</u>** 

https://tslearn.readthedocs.io/en/stable/user_guide/dtw.html 

###### **<u>tslearn · dtw_path</u>** 

https://tslearn.readthedocs.io/en/stable/gen_modules/metrics/tslearn.metrics.dtw_path.html 

###### **<u>scikit-learn · Leakage and preprocessing</u>** 

https://scikit-learn.org/stable/common_pitfalls.html 

**`Industrial AI`** · HKA · WS 2026/2027 · Session 2 · Dr.-Ing. Yannic Wolf 

**54 / 54** 

