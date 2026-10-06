# 🥪 WG Sandwich-Bestellsystem – nur GitHub

## Was du bekommst

- GitHub Pages als Webseite
- `login.txt` für Benutzer
- `produkte.txt` für Sandwiches
- `bestellungen.txt` für Bestellungen
- Admin-Dashboard
- manuelles Leeren
- automatisches Leeren per GitHub Actions
- kein eigener Server

## 1. Dateien ins Repository

Alle Dateien in dieses Repository kopieren.

GitHub Pages muss auf den Ordner mit `index.html` zeigen. Am einfachsten liegen
`index.html`, `style.css`, `app.js` und `config.js` direkt im Hauptverzeichnis.

## 2. GitHub Token erstellen

Du brauchst einen Fine-grained Personal Access Token.

Für das Repository nur die Berechtigung:

`Contents: Read and write`

geben.

Den Token anschließend in `config.js` eintragen.

Beispiel:

```js
const CONFIG = {
  githubToken: "github_pat_...",
  owner: "deinname",
  repo: "wg-sandwiches",
  branch: "main"
};
```

## 3. login.txt

```text
max:1234
anna:passwort
admin:admin123:admin
```

Das Format ist:

```text
BENUTZER:PASSWORT
```

oder für einen Admin:

```text
BENUTZER:PASSWORT:admin
```

## 4. produkte.txt

```text
Schinken-Käse|3,50 €
Salami|3,50 €
Käse|3,00 €
Thunfisch|4,00 €
```

Du kannst Sandwiches direkt in dieser Datei hinzufügen, entfernen oder ändern.

## 5. GitHub Pages aktivieren

Repository → Settings → Pages

Bei "Build and deployment":

`Deploy from a branch`

Branch:

`main`

Ordner:

`/ (root)`

auswählen.

## 6. Automatisches Löschen

`.github/workflows/clear-orders.yml` leert `bestellungen.txt` automatisch.

Die Action läuft über GitHub, also brauchst du dafür keinen eigenen Server.

WICHTIG:
GitHub Actions nutzt UTC. Die Beispiel-Cronzeit ist auf 12 Uhr deutsche
Sommerzeit ausgelegt. Für die Winterzeit muss die Cronzeit angepasst werden.

GitHub kann geplante Actions außerdem mit Verzögerung starten. Wenn exakt
12:00 Uhr wichtig ist, ist eine serverseitige Cronlösung zuverlässiger.

## ⚠️ Wichtig zum Token

Der Token steht in `config.js` und ist dadurch für Besucher der Seite
auslesbar. Das ist absichtlich so, weil das System komplett ohne Backend
funktionieren soll.

Verwende dafür ein eigenes Repository und einen Token, der möglichst nur
dieses Repository bearbeiten darf.

Wenn du den Token später widerrufen willst:
GitHub → Settings → Developer settings → Personal access tokens.
