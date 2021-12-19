# Türklingel

## Gegebenheiten:
 - 12VAC Gong
 - 5VDC bei Gong vorhanden
 
 Die Schaltung besteht aus 2 Teilen: (1 links) Erkennung 12VAC (Klingel gedrückt) und (2 rechts) Relais zur Trennung des Gongs von der 12VAC Leitung.
**Zu Teil 1:** Eingang sind die Anschlüße des Gongs mit 12VAC. Die werden mit einer 0815-Diode "gleichgerichtet" und auf einen Kondensator gegeben. Die entstandene "Gleichspannung" wird dann über einen Optokoppler übertragen. Der generiert daraus ein Signal auf 3,3VDC-Basis, welches auf dem WEMOS Board an den ESP8266 geht. Ich habe mir nicht groß Gedanken über Zeitkonstanten gemacht und die Widerstände so dimensioniert als ob 12VDC anliegen würden. Der Optokoppler geht so auf keinen Fall kaputt und hat nach unten so viel Luft, dass er trotzdem funktioniert. Bisschen Strom braucht der ja auch. Mein Klingeltrafo liefert auch eher 13VAC als 12VAC. Die 3,3VDC-Seite folgt dem Datenblatt des Optokopplers (TLP621). Im Masseteil befindet sich ein kleiner Hochpass, damit es nicht schwingt.
**Zu Teil 2:** Auf einen FET geht der Output des ESP8266. Der Widerstand R7 dort soll den Output schonen, da der FET am Gate immer nen Kondensator hat, der im Zweifel kurz mit Überstrom aus dem GPIO geladen wird. Source liegt an 5VDC mit Widerstand zur Strombegrenzung. Drain Richtung Masse enthählt den Eingang des Relais mit ner Shotky-Diode in Sperrrichtung gesichert, gegen Schaltströme. Das Relais unterbricht die 12VAC Leitung zum Gong, wenn der FET durch schaltet.
 
 So war es anfangs gedacht. Ich habe in der Grabbelkiste aber noch ein schon vorgefertigtes Relais gefunden, dass mit 5V betrieben werden kann und einen Eingang hat. Wird dieser auf Masse gezogen, dann schaltet das Relais. Dabei fließen etwa 3mA, dir vom ESP8266 versenkt werden müssten. Mit einem 4,7k Widerstand schaltet es trotzdem und senkt den Strom auf > 1mA ab. Das schont wiederum den Ausgang des ESP8266.
