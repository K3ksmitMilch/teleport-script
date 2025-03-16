# Teleport Script für RAGE:MP
Dieses Scripts soll stets Streng Geheim bleiben. Daher bitte ich, dieses Script nicht ohne mein Erlaubnis zuteilen. 
Sonst lest bitte vorher in LICENSE.txt nach, da stehen noch mehr Richtlinen die Bitte eingehalten werden sollen.




# RAGE:MP Client-Side Event Logger

Ein komplexer clientseitiger Eventlogger für RAGE:MP, der verschiedene Events protokolliert und eine Funktion zum Ausschließen bestimmter callRemote-Events bietet.

## Features

- Protokollierung verschiedener RAGE:MP-Client-Events
- Protokollierung von callRemote-Events mit Parametern
- Möglichkeit, bestimmte callRemote-Events von der Protokollierung auszuschließen
- Konfigurierbare Log-Level (INFO, WARNING, ERROR, DEBUG)
- Farbige Konsolenausgabe
- Performance-Tracking für callRemote-Events
- Chat-Befehle zur Steuerung des Loggers

## Installation

1. Kopiere die Datei `eventlogger.js` in dein RAGE:MP-Client-Skriptverzeichnis.
2. Importiere den Eventlogger in deinem Skript:

```javascript
const eventLogger = require('./eventlogger.js');
```

## Verwendung

### Grundlegende Protokollierung

```javascript
// Protokolliere eine Nachricht
eventLogger.log("INFO", "Custom", "Dies ist eine benutzerdefinierte Lognachricht");

// Verschiedene Log-Level
eventLogger.log("INFO", "System", "Informationsnachricht");
eventLogger.log("WARNING", "System", "Warnungsnachricht");
eventLogger.log("ERROR", "System", "Fehlernachricht");
eventLogger.log("DEBUG", "System", "Debug-Nachricht");
```

### Verwaltung der ausgeschlossenen callRemote-Events

```javascript
// Füge ein Event zur Ausschlussliste hinzu
eventLogger.excludeCallRemote("player:someEvent");

// Entferne ein Event aus der Ausschlussliste
eventLogger.includeCallRemote("player:someEvent");

// Hole die Liste der ausgeschlossenen Events
const excludedEvents = eventLogger.getExcludedCallRemotes();
console.log(excludedEvents);
```

### Statistiken

```javascript
// Zeige Statistiken in der Konsole an
eventLogger.printStats();

// Hole Statistiken als Objekt
const stats = eventLogger.getStats();
console.log(stats);
```

### Ereignisprotokollierung ein-/ausschalten

```javascript
// Schalte die Protokollierung für eine bestimmte Kategorie ein/aus
eventLogger.toggleEventLogging("player", true); // Einschalten
eventLogger.toggleEventLogging("render", false); // Ausschalten

// Schalte ein bestimmtes Log-Level ein/aus
eventLogger.toggleLogLevel("DEBUG", true); // Einschalten
eventLogger.toggleLogLevel("INFO", false); // Ausschalten
```

### Statistiken zurücksetzen

```javascript
// Setze alle Statistiken zurück
eventLogger.clearStats();
```

## Chat-Befehle

Der Eventlogger registriert die folgenden Chat-Befehle:

- `/logstats` - Zeigt Statistiken in der Konsole an
- `/logexclude [eventName]` - Fügt ein Event zur Ausschlussliste hinzu
- `/loginclude [eventName]` - Entfernt ein Event aus der Ausschlussliste
- `/loglist` - Zeigt die Liste der ausgeschlossenen Events an
- `/logclear` - Setzt alle Statistiken zurück
- `/logtoggle [category] [true/false]` - Schaltet die Protokollierung für eine Kategorie ein/aus
- `/loglevel [level] [true/false]` - Schaltet ein Log-Level ein/aus

## Konfiguration

Die Konfiguration kann in der Datei `eventlogger.js` angepasst werden:

```javascript
const config = {
    // Allgemeine Einstellungen
    enabled: true,
    logToConsole: true,
    logToFile: false, // Hinweis: Dateiprotokollierung ist im Client-Kontext möglicherweise eingeschränkt
    logFilePath: "eventlogger.log",
    
    // Log-Level (true = aktiviert, false = deaktiviert)
    logLevels: {
        INFO: true,
        WARNING: true,
        ERROR: true,
        DEBUG: false
    },
    
    // Zu protokollierende Events
    logEvents: {
        player: true,
        vehicle: true,
        streaming: true,
        render: false, // Standardmäßig deaktiviert, da es sehr spammy sein kann
        browser: true,
        gui: true,
        keys: true,
        callRemote: true,
        custom: true
    },
    
    // Performance-Tracking
    trackPerformance: true,
    slowEventThreshold: 50, // ms
    
    // Liste der callRemote-Events, die von der Protokollierung ausgeschlossen werden sollen
    excludedCallRemotes: [
        "player:updatePosition",
        "player:syncData",
        "vehicle:updatePosition",
        "stats:update",
        "ping:update",
        // Füge hier weitere Events hinzu
    ]
};
```

## Beispiel: Integration in ein bestehendes Skript

```javascript
// Importiere den Eventlogger
const eventLogger = require('./eventlogger.js');

// Füge ein benutzerdefiniertes Event hinzu
mp.events.add("myCustomEvent", (data) => {
    // Protokolliere das Event
    eventLogger.log("INFO", "Custom", `myCustomEvent triggered with data: ${JSON.stringify(data)}`);
    
    // Führe die eigentliche Event-Logik aus
    // ...
});

// Füge häufig aufgerufene Events zur Ausschlussliste hinzu
eventLogger.excludeCallRemote("player:frequentUpdate");

// Registriere einen benutzerdefinierten Tastendruck
mp.keys.bind(0x42, false, () => { // B key
    eventLogger.log("INFO", "Keys", "B key pressed");
    // Deine Logik hier...
});
```

## Erweiterte Verwendung

### Benutzerdefinierte Events protokollieren

Du kannst den Eventlogger verwenden, um benutzerdefinierte Events zu protokollieren:

```javascript
// Protokolliere ein benutzerdefiniertes Event
function onPlayerAction(action) {
    eventLogger.log("INFO", "PlayerAction", `Player performed action: ${action}`);
}
```

### Performance-Überwachung

Der Eventlogger verfolgt automatisch die Performance von callRemote-Events, wenn `trackPerformance: true` gesetzt ist. Du kannst die Performance-Statistiken mit `eventLogger.printStats()` anzeigen lassen.

## Hinweise

- Die Dateiprotokollierung ist im Client-Kontext von RAGE:MP möglicherweise eingeschränkt. Der Logger verwendet stattdessen `mp.storage`, um Logs zu speichern, falls aktiviert.
- Das Rendern von Frames (`render`-Event) ist standardmäßig deaktiviert, da es sehr viele Logs erzeugen kann.
- Für eine bessere Performance sollten häufig auftretende Events zur Ausschlussliste hinzugefügt werden.

## Lizenz

Frei verwendbar für RAGE:MP-Projekte. 
