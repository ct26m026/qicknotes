# QuickNotes

## Setup

Projektabhängigkeiten installieren:

```bash
npm install
```

Entwicklungsserver starten:

```bash
npm run dev
```

Danach die im Terminal angezeigte lokale Adresse im Browser öffnen.

## Struktur

Die Notizlogik liegt im Composable `useNotes.js`, damit die Komponenten selbst möglichst übersichtlich bleiben. Die Persistenz liegt in `useLocalStorage.js`, damit die Zugriffe auf `localStorage` nicht über mehrere Komponenten verteilt sind.

## Reflexion

### 1. Warum darf NoteCard die Notiz-Prop nicht selbst verändern, und wie löst ihr das stattdessen?

Beim Klick auf den Löschen-Button sendet `NoteCard` ein `delete`-Event mit der ID der Notiz. `App.vue` empfängt dieses Event und ruft `deleteNote()` aus dem Composable `useNotes.js` auf.

### 2. Was passiert, wenn zwei Komponenten dasselbe useNotes() aufrufen — teilen sie sich die Notizen oder nicht?

Zwei Aufrufe von `useNotes()` erzeugen grundsätzlich eigene reaktive Zustände und teilen sich nicht automatisch dieselbe `notes`-Variable. Beide verwenden aber das selbe `localStorage`, sodass die Daten dort gespeichert werden können.

### 3. Wozu dient das Note-Interface, wenn der Code auch ohne liefe?

Das `Note`-Interface beschreibt die Struktur einer Notiz. Es legt fest, dass eine Notiz eine ID, einen Titel, einen Inhalt und eine Liste von Tags besitzt. Dadurch wird die erwartete Datenstruktur dokumentiert und der Datenfluss im Projekt verständlicher.
