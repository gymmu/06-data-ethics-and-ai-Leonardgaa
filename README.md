[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/KKdhufHW)
# Paper über Data-Ethics

In diesem Projekt verfassen wir ein Dokument über die ethischen
Herausforderungen im Zusammenhang mit Daten und künstlicher Intelligenz.

Die Projektarbeit setzt sich aus mehreren Teilen zusammen, die nacheinander
abgearbeitet werden.

1. Recherche zum Thema durchführen und ein Quellenverzeichnis erstellen.
2. Die Rechercheergebnisse analysieren, in Notizen zusammenfassen und die Fragestellung formulieren.
3. Die Arbeit schreiben und das Quellenverzeichnis verlinken.
4. Review zu einer anderen Arbeit verfassen.
5. Einarbeiten des Feedbacks aus dem Review für die eigene Arbeit.

## Werkzeuge

In diesem Projekt verwenden wir verschiedene Werkzeuge, wie Latex um Dokumente
zu erstellen, eine KI die uns Informationen aus verschiedenen Dokumenten
zusammen tragen kann, und Werkzeuge die Sie bereits kennen, wie Git und Nodejs.

### Latex

Die Arbeit und das Review werden jeweils mit Latex erstellt. Latex ist ähnlich
wie HTML eine Markup-Sprache, hat aber das Ziel ein PDF zu erstellen. Latex
macht es einfach und praktisch automatische Inhaltsverzeichnisse sowie
Quellenverzeichnisse zu erstellen, und ist in naturwissenschaftlichen Arbeiten
weit verbreitet. Da Latex ebenfalls auf Text basiert, eignet sich Git
hervorragend, um die eigene Arbeit zu versionieren und gleichzeitig zu sichern.

Um mit Latex arbeiten zu können, müssen Sie zuerst Latex für Ihr Betriebssystem
installieren. Hier finden die den entsprechenden Link:
[miktex](https://miktex.org/download)

Wir verwenden `latexmk` um das Dokument zu erstellen und je nach Bedarf das Quellenverzeichnis zu erstellen. Um dieses zu verwenden müssen noch [perl](https://www.perl.org/get.html) installieren.

<details>

<summary><h4>Vorsicht bei MacOS</h4></summary>

Bei MacOS ist die `MikTeX`-Installation ein weniger schwieriger. Da müssen Sie nach der Installation noch sagen wo Ihr System die Programme die `MikTeX` installiert finden kann. Das können Sie mit dem folgenden Befehl im Terminal machen:

```bash
echo export 'PATH=~/bin:$PATH' >> ~/.zprofile
```

Mehr dazu können Sie hier finden: [Miktex auf MacOS installieren](https://miktex.org/howto/install-miktex-mac) und [Miktex Pfad anpassen](https://miktex.org/howto/modify-path)

</details>

#### VSCode Extension: Latex Workshop

Damit Sie Latex einfach und bequem in VSCode verwenden können, brauchen Sie
zusätzlich noch diese Erweiterung. Drücken Sie einfach `CTRL + P` und geben Sie
den folgenden Befehl ein:

```text
ext install James-Yu.latex-workshop
```

Sie finden dann im Ordner `documents` mehrere Unterordner mit verschiedenen
Latex Projekten, die Sie verwenden können. In `documents/tutorial/tutorial.tex` finden Sie eine Einführung in Latex die Sie durcharbeiten können. Versuchen Sie zuerst das Dokument zu bauen/compilieren, und lesen Sie sich dann das PDF durch. Machen Sie danach Anpassungen am Dokument.

Das PDF sollte automatisch erstellt werden wenn Sie das Dokument speichern, Sie können aber auch oben rechts auf den grünen Pfeil klicken. Direkt daneben finden Sie einen Button der Ihnen das PDF rechts im Fenster öffnet.

Wenn Sie das PDF erstellen, dann wird `MikTeX` Sie fragen ob Sie die zusätzlichen Pakete installieren möchten. Da müssen Sie sich beim ersten mal einmal komplett durch klicken, damit von allen benötigten Paketen die neusten Versionen verfügbar sind.

### RAG (Retrieval-Augmented Generation)

Es handelt sich um eine innovative KI-Technik, die es ermöglicht, Informationen
aus unseren Dokumenten zu extrahieren. Wir können unsere Dokumente direkt
durchsuchen und die relevanten Passagen zu unserer Frage finden. Diese Passagen
werden zusammen mit der Frage an ein LLM wie ChatGPT weitergeleitet, das uns
dann eine Antwort basierend auf diesen Passagen gibt. Auf diese Weise können
wir die KI mit aktuellen Informationen versorgen, ohne auf das Training und die
Datensätze der KI-Hersteller angewiesen zu sein.

Diese Technik macht es uns sehr viel einfacher Informationen aus Dokumenten zu
extrahieren, braucht aber ein wenig Einrichtung bevor wir es verwenden können.

#### WICHTIG: API Schlüssel für OpenAI erstellen

Damit wir ChatGPT in unserem Projekt verwenden können, müssen Sie einen
API-Schlüssel erstellen und im Projekt verwenden. Den Schlüssel können Sie
[hier](https://platform.openai.com/api-keys) erstellen lassen, wenn Sie bereits
einen Account bei OpenAI haben. Sie brauchen den Schlüssel dann, und müssen
diesen in eine neue Datei `rag/.env` einfügen.

```text
VITE_OPENAI_API_KEY=<YOUR_API_KEY>
OPENAI_API_KEY=<YOUR_API_KEY>
```

**WICHTIG:** Diese Datei darf auf keinen Fall auf Github landen!

#### Webseite starten

Der ganze Code zu dem Projekt ist im Unterordner `rag/` zu finden. Wenn Sie also die folgenden Befehle ausführen, muss das Terminal im entsprechenden Ordner sein. Dazu müssen Sie den Befehl

```bash
cd rag
```

eingeben, bevor Sie die anderen Befehle laufen lassen.

Das ganze läuft in einem lokalen Webserver, diesen müssen wir mit dem folgenden
Befehl starten, öffnen Sie dazu ein Terminal und geben Sie diese beiden Befehle
ein.

```bash
npm install
npm run dev
```

Der erste Befehl installiert Ihnen alle Abhängigkeiten für das Projekt, der
zweite startet den lokalen Webserver. Den ersten Befehl brauchen Sie nur beim
ersten mal einzugeben, danach reicht `npm run dev`.

#### Datenbank erstellen

Damit unser lokal Webserver überhaupt etwas machen kann, müssen wir zuerst noch
eine Datenbank erzeugen. Dabei werden die Dokumente in `rag/data/` angeschaut und
indexiert. Wie müssen zuerst also ein PDF Dokument in `rag/data/` ablegen. Und dann
den folgenden Befehl ausführen. Öffnen Sie dazu ein neues Terminal.

```bash
npm run create_db
```

Sie können auch andere Formate wie `.md` oder `.txt` Dateien in den Ordner `rag/data/` ablegen. Diese werden automatisch gelesen und verarbeitet. Beides sind einfache Textformate, in denen Sie Notizen, oder auch andere Dinge, speichern können.

Sie können auch Webseiten lesen lassen. Dafür können Sie einfach eine Liste mit Webseiten angeben, diese finden Sie in `rag/config/websites.json`.

#### Lokalen Webserver starten

Zusätzlich zur Webseite, brauchen Sie noch einen Webserver, der direkt Zugriff auf NodeJS hat, und dadurch auch auf die Datenbank die Sie erstellt haben. Diesen Server können Sie mit dem folgenden Befehl starten.

```bash
npm run server
```
