# Schedule I Cheat Menu by Keks

Ein stilvolles ImGui Menü für Unity-Spiele mit modernem Dark-Mode Design.

## Features

- Modernes, schlichtes Dark-Mode Design
- Animationen beim Öffnen/Schließen des Menüs
- Abgerundete Ecken für ein modernes Aussehen
- Tastenkürzel zum Umschalten (EINFG-Taste / INSERT)
- Als DLL kompiliert für einfache Integration in Unity

## Aufbau des Projekts

Das Projekt besteht aus:
- ImGui Integration für DirectX 11
- Benutzerdefiniertes Theme mit blauem Akzent
- Animation mit Fade-In/Out Effekt
- DLL für Unity-Integration

## Kompilieren der DLL

1. Öffne das Projekt in Visual Studio
2. Wähle die Konfiguration "Release" und die Plattform "x64"
3. Baue das Projekt (F7 oder Build -> Build Solution)
4. Die DLL wird im Ordner "x64/Release" erstellt

## Verwendung der DLL

1. Kopiere die erstellte DLL in den Hauptordner deines Unity-Spiels
2. Verwende einen DLL-Injector, um die DLL in den Unity-Spielprozess zu injizieren
3. Drücke die EINFG-Taste (INSERT), um das Menü zu öffnen/schließen

## Anpassen des Menüs

Das Menü kann in der Datei "Schedule I Cheat by Keks.cpp" angepasst werden:
- Design und Farben in der Funktion `KeksMenu::SetupImGuiStyle()`
- Menüelemente in der Funktion `KeksMenu::Render()`
- Animationsverhalten in `KeksMenu::ApplyAnimations()`

## Hinweise

- Die DLL muss für jede Unity-Version neu kompiliert werden
- Das Projekt verwendet DirectX 11 Hooks und ist daher nur mit Unity-Spielen kompatibel, die DirectX 11 verwenden
- Das Menü kann durch Anpassen der `KeksMenu::Render()` Funktion erweitert werden 
