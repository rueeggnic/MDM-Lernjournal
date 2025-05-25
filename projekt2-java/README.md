# Projekt 2 Java

## Übersicht

| | Bitte ausfüllen |
| -------- | ------- |
| Variante | Vorhandener Datensatz  |
| Datensatz (wenn selbstgewählt) | Format: PNG Bilder, Grösse 256x256, Recycling Bilder in verschiedenen Kategorien |
| Datensatz (wenn selbstgewählt) | [URL](https://www.kaggle.com/datasets/alistairking/recyclable-and-household-waste-classification) |
| Modell (wenn selbstgewählt) | - |
| ML-Algorithmus | Vorlesung |
| Repo URL | https://github.com/rueeggnic/MDMProjekt2 |



## Dokumentation

### Daten

Die Daten sind von einem vordefinierten Datensatz von Kaggle. Da gibt es die Recyclingbilder in einer riesigen Datenbank mit extrem vielen Unterordnern. Da ich für das Projekt 2 weniger Datensätze wollte da sonst die Trainingszeiten viel zu hoch sind, habe ich die Datensätze auf 6 Klassen reduziert und für jede Klasse 250 Bilder bereit gestellt. Später habe ich dann, zwei Klassen noch zusammengefügt. Ich hatte eine Petflachen Wasser und eine Gruppe Petflaschen Soda (also Süssgetränke). Die Klassen waren im Verhältnis zu den anderen zu nahe aneinander, also habe ich mich entschieden eine Klasse zu streichen. Wobei ich habe diese Klassen dann in PET zusammengefügt und jeweils mit 125 Bilder von Pet Wasser und mit 125 Bilder von Pet Soda ergänzt, sodass beide Klassen inhaltlich als eine Klasse berücksichtigt werden.

![Datensatz](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/projekt2-java/images/Datensatz.png)

### Training

Das Training des Modells erfolgte in der Java-Klasse Training.java mithilfe der Deep Java Library (DJL). Dabei wurde ein neuronales Netz für die Klassifikation von Abfallarten trainiert (z. B. PET, Aluminium, Papier, Kehricht, Glasflaschen).

Zu Beginn wurde die Eingabeform definiert und der Trainer mit der richtigen Input-Shape initialisiert. Anschliessend erfolgte das eigentliche Training mit der Methode EasyTrain.fit(), wobei die Trainings- und Validierungsdaten verwendet wurden.

Während des Trainings wurden in der Konsole laufend Kennzahlen wie Loss und Accuracy pro Epoche ausgegeben. Zum Beispiel erreichte das Modell nach wenigen Prozent Trainingsfortschritt bereits eine Accuracy von ca. 57 % auf dem Validierungsdatensatz. Die Trainingsmetriken wurden durch den LoggingTrainingListener automatisch mitprotokolliert. Ich habe die Trainings mehrfach durchgeführt. Leider war ich da ein bisschen frustriert, trotz der klaren Abgrenzung der Klassen ist die Accuracy nie über 85% gekommen.

Nach dem Training wurde das Modell gespeichert und steht anschliessend für die Inference und das Deployment zur Verfügung.

![Training](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/projekt2-java/images/Training.png)

### Inference / Serving

Die trainierten Daten habe ich über einen Localhost getestet. Danach habe ich die Daten mittles Dockerimage auf Docker gebracht. Auch da konnte ich die Applikation über den Localhost Port 8080 testen. Danach habe ich die lokalen Dateien von Docker Desktop auf Dockerhub gepusht.

![dockerhub](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/projekt2-java/images/dockerhub.png)

Um das alles auf Azure zu deployen, habe ich im Azure bereits alles eingereichtet, d.h. Resourcengruppe erstellt und über die Einrichtung WebApp aufgeschaltet.

![Deployment](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/projekt2-java/images/Azure_deployment.png)

### Deployment

Das Deployment ist über Azure erfolgt. Die Daten habe ich dann bereits über eine Containerisierung auf Docker Hub gepusht, sodass ich das dann auf Azure bringen konnte.

![WebApp](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/projekt2-java/images/WebApp.png)
