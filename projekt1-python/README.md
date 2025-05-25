# Projekt 1 Python

## Übersicht

| | Bitte ausfüllen |
| -------- | ------- |
| Variante | Eigenes Projekt |
| Datenherkunft | Format: csv und JSON, vorbereitete Datensätze die ich beziehen konnte |
| Datenherkunft | https://www.energiedashboard.admin.ch/strom/produktion |
| ML-Algorithmus | nur begrenzt ML, da Datensatz sehr speziell war |
| Repo URL | https://github.com/rueeggnic/mdmproject1 |

## Dokumentation

### Data Scraping

Da ich mit Scraping begonnen habe, dann aber gemerkt habe, dass ich die Daten so wie ich sie brauche vom Energiedashboard, bzw. der dahinterliegenden Statistik entnehmen kann, brauchte ich für das eigentliche Projekt keinen Spider. Da dies aber ein wichtiger Bestandteil des Projektes war, wollte ich doch noch einen erstellen. Also habe ich unabhängig vom Projekt einen Beispielspider kreiiert, um das scraping auch noch zu vervollständigen. Der erstellte Scraper ist an das Vorlesungsbeispiel geknüpft.

![Spider](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/projekt1-python/images/Spider.png)

Die Daten konnte ich also von vom Energiedachboard beziehen. Entweder waren das csv Daten oder eine JSON API.

![Energiedashboard](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/projekt1-python/images/json_api_energiedashboard.png)

### Training

Im Zentrum des Projekts stand kein klassisches Machine-Learning-Modell, sondern ein regelbasiertes Simulationsmodell. Statt zu trainieren, habe ich bestehende Energieproduktionsdaten (PV, Wind, Kernkraft) mit Zufluss- und Verbrauchsdaten kombiniert. Die Hauptlogik bestand darin, über eine Zeitreihe hinweg den Füllstand der Speicherseen und die benötigte Speicherkraft zu simulieren. Dabei war es wichtig, die Eingangsparameter (z. B. PV-Faktor) dynamisch veränderbar zu machen, um verschiedene Szenarien zu berechnen. Obwohl kein ML-Training nötig war, habe ich zentrale Konzepte wie Feature-Kombination, Zeitreihenverarbeitung und realitätsnahe Modellierung angewendet.

![prediction](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/projekt1-python/images/prediction.png)

### ModelOps Automation

Ein Ziel war es, das Modell nicht nur einmal manuell laufen zu lassen, sondern in eine einfache automatisierbare Struktur zu bringen. Ich habe die Modelllogik in eine Funktion (run_simulation) überführt, sodass sie von aussen aufgerufen werden kann – etwa durch andere Programme oder eine Weboberfläche. Zusätzlich habe ich eine einfache API mit Flask aufgebaut. Die Parameterübergabe erfolgt automatisiert über HTTP-Requests, was eine direkte Integration in ein User Interface oder ein größeres automatisiertes System erlaubt. Diese Kapselung ist ein wichtiger Schritt in Richtung ModelOps: das Modell ist klar trennbar, reproduzierbar und reaktiv auf Nutzereingaben.

![github](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/projekt1-python/images/Github_secrets.png)

### Deployment

Für das Deployment habe ich eine lokale Flask-Webanwendung erstellt. Über ein einfaches HTML-Formular können Nutzer drei Parameter eingeben (PV-, Wind-, und Kernkraft-Faktor) und erhalten nach dem Absenden eine visuelle Ausgabe der Simulation direkt im Browser. Dieses Setup ist lokal lauffähig. Um das dann zu deployen, habe ich das Projekt genommen und über die GitHub Actions auf Azure deployed.

![Azure](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/projekt1-python/images/Azure_resource_group.png)

Das Deployment ist über eine WebApp abrufbar. Drei Eingaben können getätigt werden, wobei sich bei jeder Eingabe nach "Simulation starten" das Diagramm respektive die Diagramme verändern. Die Diagramme werden nicht direkt im WebApp erstellt. Das sichtbare im WebApp ist eigentlich statisch, d.h. es ist ein Bild das aus dem Diagramm im Backend kreiiert wird und die Seite updatet.

![WebApp](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/projekt1-python/images/WebApp.png)
