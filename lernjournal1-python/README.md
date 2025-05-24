# Lernjournal 1 Python

## Repository und Library

| | Bitte ausfüllen |
| -------- | ------- |
| Repository (URL)  | https://github.com/rueeggnic/MDM-Lernjournal.git
| Kurze Beschreibung der App-Funktion | Text umdrehen und Originaleingabetext mit einem Sentiment bewerten |
| Verwendete Library aus PyPi (Name) | textblob |
| Verwendete Library aus PyPi (URL) | https://pypi.org/project/textblob/|
| ... | |
| ... | |

## App, Funktionalität
Die Applikation bietet dem User die Möglichkeit einen Text auszugeben, der dann umgedreht wird. Der Text wird nach Sentiment bewertet.

### Funktionen Aufgaben bearbeiten
Der User kann den Text anpassen und neu senden um den Text wieder zu drehen. Das Sentiment wird neu bewertet.

#### Ansicht im Web-UI:

![WebUI](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/lernjournal1-python/images/Ansicht_Webui.png)

#### Code der Application:

![WebUI](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/lernjournal1-python/images/Code_der_Applikation.png)

## Dependency Management

Für das Dependency Management haben wir pip-tools verwendet. In der Datei requirements.in definiere ich nur die Hauptpakete wie flask und textblob. Mit dem Befehl pip-compile wird daraus automatisch eine vollständige requirements.txt mit allen Abhängigkeiten und Versionsangaben generiert. Diese Datei wird für das Deployment auf Azure genutzt und stellt sicher, dass die Anwendung jederzeit reproduzierbar und stabil bleibt.

### requirements.in Inhalt:

![WebUI](https://raw.githubusercontent.com/rueeggnic/MDM-Lernjournal/main/lernjournal1-python/images/requirementsin.png)

### requirements.txt Inhalt (Teil-Auszug):

blinker==1.9.0
    # via flask
click==8.2.1
    # via
    #   flask
    #   nltk
colorama==0.4.6
    # via
    #   click
    #   tqdm
flask==3.1.1
    # via -r requirements.in
itsdangerous==2.2.0
    # via flask
jinja2==3.1.6
    # via flask
joblib==1.5.1
    # via nltk
markupsafe==3.0.2
    # via
    #   flask
    #   jinja2
    #   werkzeug
nltk==3.9.1
    # via textblob
regex==2024.11.6
    # via nltk
textblob==0.19.0
    # via -r requirements.in
tqdm==4.67.1
    # via nltk
werkzeug==3.1.3
    # via flask


## Deployment

az webapp up --name lernjournal1-rueegnic --plan lernjournal1-plan --resource-group lernjournal1 --runtime "PYTHON:3.12" --sku F1 --logs


az webapp up `
  --name lernjournal1-rueegnic `
  --plan lernjournal1-plan `
  --resource-group lernjournal1 `
  --runtime "PYTHON:3.12" `
  --sku F1 `
  --logs

