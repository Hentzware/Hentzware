# HyperForge

**HyperForge** ist eine Windows-Desktopanwendung zur automatisierten Erstellung und Verwaltung von Hyper-V-Laborumgebungen. Sie richtet sich an IT-Auszubildende, Studierende und Homelabber, die Windows-Server-Labs ohne tiefgehende PowerShell-Kenntnisse aufbauen möchten.

---

## Technologien

| Ebene          | Technologie                              |
|----------------|------------------------------------------|
| UI-Framework   | WPF mit Prism (MVVM)                     |
| Runtime        | .NET 10 (Windows)                        |
| Topologie-Editor | Nodify (Node-Graph)                    |
| Hyper-V        | PowerShell SDK                           |
| Logging        | Serilog                                  |
| Auto-Update    | Velopack (via GitHub Releases)           |
| Installer      | Inno Setup                               |
| Tests          | xUnit, FluentAssertions, NSubstitute     |
| CI/CD          | GitHub Actions                           |

## Features

### Dashboard

- Systemstatus-Übersicht (Admin-Rechte, Hyper-V-Verfügbarkeit, VM- und Switch-Anzahl)
- Netzwerkübersicht aller VMs mit Status
- Schnellzugriff auf alle Funktionen
- Vorlagenkatalog für Konfigurationen

### ISO-Manager

- ISOs mounten, extrahieren und Windows-Editionen erkennen
- Eigene ISOs erstellen mit integrierter Answer-File-Einbindung
- ISO-Anpassungsassistent (mehrstufig)
- Windows-ISO-Download-Hilfe

### Answer-File-Builder

- Visueller 9-Schritte-Assistent für autounattend.xml:
  - Festplattenpartitionierung (MBR/GPT)
  - Benutzerkonten (Admin + weitere lokale Konten)
  - Regionale Einstellungen (Sprache, Zeitzone, Tastatur)
  - Netzwerk (DHCP oder statische IP, DNS, Domänenbeitritt)
  - OOBE-Einstellungen
  - First-Logon-Befehle
  - Produktschlüssel und Editionsauswahl
- XML-Generierung mit Validierung
- Befehlskatalog mit vordefinierten Kommandos

### Hyper-V-Verwaltung

**Virtuelle Maschinen:**
- VMs erstellen (Gen1/Gen2, vCPU, RAM, Festplatte, Switch, ISO)
- Starten, Stoppen, Herunterfahren, Löschen und Klonen
- VM-Gruppen für logische Organisation
- VM-Vorlagen (CPU/RAM/Disk-Presets speichern und laden)
- Batch-Operationen (mehrere VMs gleichzeitig starten, stoppen, Checkpoint erstellen)
- Automatische Statusaktualisierung alle 5 Sekunden

**Virtuelle Switches:**
- Switches erstellen (External, Internal, Private, NAT)
- NAT-Switches für Internetzugang in isolierten Netzwerken
- Subnetze pro Switch konfigurieren

**Netzwerkadapter:**
- Mehrere NICs pro VM hinzufügen und entfernen
- Live-Umschaltung auf anderen Switch ohne Neustart
- VLAN-Tagging (IDs 1--4094)
- MAC-Adressverwaltung (statisch/dynamisch)

**Checkpoints:**
- Benannte Checkpoints erstellen, anwenden und löschen
- Lab-Snapshots (Checkpoint für alle VMs gleichzeitig erstellen und wiederherstellen)

**Konnektivität & Diagnose:**
- Ping- und Port-Prüfung direkt aus der Anwendung

### Golden-Image-Verwaltung

- Sysprep auf VMs ausführen (Generalisierung + Herunterfahren)
- VM-Festplatten als Golden Image exportieren (schreibgeschützt)
- Differencing-Disk-Deployment (verknüpft mit Parent-Image)
- Golden Images über Netzwerkfreigaben importieren und exportieren

### Lab-Vorlagen

- Aktuelle Laborumgebung als JSON-Vorlage speichern (VMs + Switches)
- Vorlagen laden, bearbeiten und bereitstellen
- Import/Export über Dateien oder Netzwerkfreigaben
- Komplette Lab-Wiederherstellung aus Vorlage

### Rollen-Deployment

Automatisierte Installation und Konfiguration von Windows-Server-Rollen via PowerShell Direct:

- **Active Directory** -- Domäne erstellen, DNS, Forest/Domänen-Setup
- **DNS-Server** -- A- und PTR-Records anlegen
- **DHCP-Server** -- Scopes, Reservierungen, AD-Autorisierung
- **Dateiserver** -- SMB-Freigaben erstellen
- **IIS (Webserver)** -- Standard-Website bereitstellen
- **PKI** -- Zertifizierungsstelle einrichten
- **WSUS** -- Update-Server bereitstellen
- **RRAS** -- IP-Forwarding für Routing zwischen Subnetzen

**Weitere Operationen:**
- Domänenbeitritt und zusätzliche Domänencontroller
- Firewall-Regeln bereitstellen
- Automatische Netzwerk-Konfiguration (IP-Zuweisung für mehrere VMs)
- Software-Deployment (MSI/EXE)
- GPO-Vorlagen (Passwortrichtlinie, RDP, Windows Update, Firewall)
- Netzwerkdiagnose (ipconfig, nslookup, tracert, route)
- Dienste-Übersicht und Ereignisprotokoll-Viewer

### Topologie-Designer

- Grafischer Netzwerkplan mit VM- und Switch-Knoten
- Drag & Drop, Zoom und Pan
- IP-Konfiguration direkt an den Knoten
- VM-Steuerung aus der Topologie (Starten, Stoppen, Verbinden)
- Ping-Prüfung und Statusanzeige
- Topologien speichern und laden

### Weitere Features

- **Log-Viewer** -- Anwendungsprotokolle in Echtzeit anzeigen und filtern
- **Dark/Light Mode** -- Live-Umschaltung
- **Onboarding-Assistent** -- Ersteinrichtung mit Workspace-Pfad und Tool-Konfiguration
- **In-App-Dokumentation** -- Durchsuchbare Hilfe zu allen Modulen
- **Auto-Update** -- Automatische Aktualisierung über GitHub Releases
- **Netzwerkfreigaben** -- Golden Images und Vorlagen über UNC-Pfade teilen

### Lizenzierung

- Hybrides System: Online-Aktivierung + Offline-Token-Fallback
- Maschinengebundene Lizenzschlüssel
- Statusanzeige und Deaktivierung in den Einstellungen

## Lizenz

Copyright Hentzware. Alle Rechte vorbehalten.
