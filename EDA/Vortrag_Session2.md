# Vortrag Session 2 – Sprechtext (max. 2 Minuten)

## Stichpunkte pro Folie

**1 · Titel** (≈ 5 s)
- Aufbau, Eigenschaften, offene Fragen – der Reihe nach

**2 · Dataset Description** (≈ 20 s)
- 10 Versuche, 33 Messungen nach Entfernen der Duplikate
- Zwei Smartphones: Fairphone (427 Hz) und iPhone (100 Hz)
- Geräte messen verschieden: Fairphone ≈ 3× mehr Rauschen, iPhone nur bis 50 Hz → nicht direkt vergleichen
- Pro Messung: CSV je Sensor + meta-Ordner mit echter Startzeit
- Probleme: doppelte Ordner, ein falsch benannter Ordner, Aufnahmepausen

**3 · EDA Notebook** (≈ 15 s)
- Ein Notebook pro Versuch, gleiche 8 Abschnitte
- Läuft direkt auf den Rohdaten, anderer Versuch = eine Zeile ändern
- Kernidee: Vibration deutlich über dem Ruherauschen = Schlitten fährt

**4 · Visualisierungen** (≈ 20 s)
- Links V05: durchgehende Fahrt, iPhone auf dem Schlitten, Fairphone fest am Gestell
- Rechts V09: Stop-and-go, drei Wiederholungen fast identisch
- Magnetfeld = grobe Positionsanzeige

**5 · Project Canvas** (≈ 25 s)
- Hauptbefund: Versuchsaufbau verändert die Signale stärker als der Maschinenzustand
- Zwei Gruppen: A durchgehend (V02–V05), B Stop-and-go (V06, V08–V10)
- Kandidaten: V10, Ruck-Cluster in V06; Sonderfälle V01 und V07

**6 · Hypothesen** (≈ 20 s)
- H1: V10 zeigt veränderte Mechanik (mehr Vibration, andere Frequenz)
- H2: Rucke über 30 m/s² sind Handhabung
- H3: Normal = stabil innerhalb einer Gruppe

**Abschluss: offene Fragen und nächste Schritte** (≈ 15 s, noch auf der Hypothesen-Folie)
- Offene Fragen: Was wurde je Versuch verändert? Wo lagen die Handys? Welche Messung gilt sicher als „normal“?
- Nächste Schritte: Versuchsprotokoll anfragen, Referenzgruppen festlegen, erster Anomalie-Score

---

## Sprechtext (≈ 2 Minuten)

Wir zeigen kurz, was wir bis Session 2 über den Datensatz herausgefunden haben.

Der Datensatz besteht aus zehn Versuchen an der Hybridachse. Nach dem Entfernen von Duplikaten bleiben 33 Messungen, aufgenommen mit zwei Smartphones: einem Fairphone mit 427 Hertz und einem iPhone mit nur 100 Hertz. Wichtig: Das Fairphone rauscht etwa dreimal stärker, und das iPhone kann nur Frequenzen bis 50 Hertz erfassen. Deshalb vergleichen wir die Geräte nicht direkt miteinander. Jede Messung ist ein Ordner mit einer Datei pro Sensor und einem Meta-Ordner mit der echten Startzeit. Aufgefallen sind uns unter anderem doppelte und falsch benannte Ordner sowie Aufnahmepausen.

Für jeden Versuch haben wir ein eigenes Notebook mit denselben acht Abschnitten, das direkt auf den Rohdaten läuft. Die Kernidee: Liegt die Vibration deutlich über dem Ruherauschen des Handys, fährt der Schlitten.

In den Abbildungen sieht man zwei Fahrmuster. In Versuch 5 fährt der Schlitten durchgehend hin und zurück. Das iPhone fährt mit, das Fairphone liegt fest am Gestell. In Versuch 9 fährt er Stop-and-go, und die drei Wiederholungen sind fast identisch.

Unser wichtigster Befund: Der Versuchsaufbau, also wo das Handy liegt und wie gefahren wird, verändert die Signale stärker als ein möglicher Maschinenzustand. Wir bilden deshalb zwei Gruppen: durchgehende Fahrt und Stop-and-go. Erste Anomalie-Kandidaten sind Versuch 10 und ein Ruck-Cluster in Versuch 6.

Daraus leiten wir drei Hypothesen ab. Erstens: Versuch 10 zeigt eine veränderte Mechanik, weil er stärker vibriert und eine andere dominante Frequenz hat. Zweitens: Sehr große Rucke über 30 m/s² sind Handhabung, nicht die Maschine. Drittens: Normal heißt stabil innerhalb einer Gruppe.

Offen sind für uns vor allem drei Fragen: Was wurde in jedem Versuch an der Maschine verändert? Wo genau lagen die Handys? Und gibt es eine Messung, die sicher als „normal“ gilt? Deshalb fragen wir als Nächstes das Versuchsprotokoll an, legen feste Referenzgruppen fest und bauen einen ersten Anomalie-Score. Danke!
