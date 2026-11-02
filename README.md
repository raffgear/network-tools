# Netzwerk Tools

**Netzwerk Tools** ist eine Windows-Desktopanwendung für Netzwerkdiagnose, Adapterkonfiguration und den schnellen Zugriff auf häufig benötigte Netzwerk- und Windows-Werkzeuge. Die Oberfläche und die Module sind mit AutoHotkey v2 umgesetzt.

Die App ist modular aufgebaut: `IP-App.ahk` erstellt das Hauptfenster; `Tab_*.ahk` enthält die Logik der Reiter; eigenständige Werkzeugfenster liegen unter `tools/`.

## Funktionen

### Netzwerkkarten

- Erkennt Netzwerkadapter und zeigt IP-Adresse, Subnetzmaske, Gateway, DNS-Server und DHCP-Status.
- Ermöglicht die Auswahl eines Adapters sowie DHCP- oder statische IPv4-Konfiguration.
- VLAN-Anzeige und -Konfiguration, sofern Adapter und Treiber dies unterstützen.
- Profile, Notizen und zuletzt verwendeter Adapter werden im Benutzerzweig der Registry unter `HKEY_CURRENT_USER\Software\IP-App` gespeichert.
- Adapterinformationen werden asynchron geladen, nachdem das Hauptfenster sichtbar ist.

### Öffentliche IP

Ermittelt die öffentliche IP-Adresse und zeigt verfügbare Geolokalisierungs- und Providerinformationen an.

### Erreichbarkeit

Ping, Traceroute und Test-NetConnection mit einstellbarem Zielport. Diese Diagnosefunktionen öffnen ein sichtbares Konsolenfenster.

### Netzwerk

- Browser-Internet-Speedtest
- Prüfung der Erreichbarkeit eines TCP-Ports
- IP-Scanner für Geräte im lokalen Netzwerk
- TCP-Portscanner
- DNS-Abfrage und DNS-NAPTR-/SRV-Abfrage
- Verbindungsmonitor mit Prozessinformationen
- Subnetz-Rechner mit CIDR-Präfix, Netzadresse, Broadcast-Adresse, Hostbereich und Scan-Range
- Passwortgenerator mit wählbaren Zeichengruppen und einstellbarer Länge
- FRITZ!Box- und LANCOM-Firmware-Downloader mit Suche, Datei-, Größen- und Änderungsanzeige

Die Firmware-Downloader lesen Verzeichnislisten von den offiziellen Anbieter-Websites. Downloads können in einen wählbaren Zielordner gespeichert und anschließend im Explorer angezeigt werden.

### Windows

Verknüpfungen zu Netzwerk- und Internet-Einstellungen, Task-Manager, Diensten, Geräte-Manager, Firewall, Netzwerkverbindungen, Ereignisanzeige, Systeminformationen, Ressourcenmonitor und Datenträgerverwaltung.

### Notizen

Eine einfache Notizfläche. Notizen werden in der Registry des aktuellen Benutzers gespeichert.

## Voraussetzungen

- Windows 10 oder Windows 11
- AutoHotkey v2
- Administratorrechte: Das Hauptskript prüft beim Start auf erhöhte Rechte und beendet sich andernfalls. Diese Rechte werden für Adapterkonfigurationen benötigt.
- Internetverbindung für öffentliche IP-/Geolokalisierungsabfragen, Speedtest und Firmware-Verzeichnisse

Einige Funktionen benötigen passende Windows-Komponenten oder Adaptertreiber. VLAN-Unterstützung hängt vom Netzwerkadapter ab.

## Start

1. AutoHotkey v2 installieren.
2. `IP-App.ahk` über das Kontextmenü **Als Administrator ausführen** starten.
3. Das Hauptfenster erscheint, bevor Adapterliste und Adapterdetails im Hintergrund geladen werden.

Die übrigen Reiter und Netzwerktools sind nutzbar, während die lokale Adapterabfrage läuft.

## Projektstruktur

```text
IP-App/
├── IP-App.ahk                     Hauptfenster, Tabs, Ereignisse und Startablauf
├── Gemeinsam.ahk                  gemeinsame Funktionen, Daten und Konfiguration
├── Tab_Netzwerkkarten.ahk          Adapter, Profile und Netzwerkkonfiguration
├── Tab_Oeffentliche_IP.ahk         öffentliche IP und Standortdaten
├── Tab_Erreichbarkeit.ahk          Ping, Traceroute und Porttest
├── Tab_Tools.ahk                   Einbindung der Netzwerk- und Windows-Tools
├── Tab_Notizen.ahk                 Notizen
├── Tab_About.ahk                   Anwendungsinformationen
└── tools/                          eigenständige Werkzeugmodule und Helfer
```

## Daten und Datenschutz

Profile, Notizen und der zuletzt gewählte Adapter werden unter `HKEY_CURRENT_USER\Software\IP-App` gespeichert; dafür wird keine separate Profildatei angelegt. Funktionen mit externen Diensten benötigen Internetzugang. AVM und LANCOM erhalten beim Abruf ihrer Firmware-Verzeichnisse die üblichen Verbindungsdaten, darunter die IP-Adresse des Rechners.

## Hinweise

- Netzwerkeinstellungen werden erst geändert, wenn die Adapterkonfiguration ausdrücklich mit **Übernehmen** angewendet wird.
- Änderungen an IP-, DNS- oder VLAN-Einstellungen können die Netzwerkverbindung unterbrechen.
- Verfügbarkeit, Versionen und Struktur externer Firmware-Verzeichnisse können sich ändern.
- Die App-Oberfläche ist deutschsprachig.

## Erster Commit

Vorschlag für die Commit-Nachricht:

```text
feat: add Windows network tools desktop application
```

Deutsche Alternative:

```text
feat: Windows-Anwendung für Netzwerktools hinzufügen
```

---

# Network Tools

**Network Tools** is a Windows desktop application for network diagnostics, adapter configuration, and quick access to commonly used network and Windows utilities. The interface and modules are written in AutoHotkey v2.

The app is modular: `IP-App.ahk` creates the main window, `Tab_*.ahk` files contain tab logic, and standalone utility windows are located in `tools/`.

## Features

### Network adapters

- Detects network adapters and displays IP address, subnet mask, gateway, DNS servers, and DHCP status.
- Supports adapter selection and DHCP or static IPv4 configuration.
- Displays and configures VLAN settings when supported by the adapter and driver.
- Stores profiles, notes, and the last selected adapter in the current user's Registry at `HKEY_CURRENT_USER\Software\IP-App`.
- Loads adapter information asynchronously after the main window is displayed.

### Public IP

Retrieves the public IP address and displays available geolocation and provider information.

### Reachability

Ping, traceroute, and Test-NetConnection with a configurable destination port. These diagnostics open a visible console window.

### Network

- Browser-based internet speed test
- TCP port reachability check
- IP scanner for devices on the local network
- TCP port scanner
- DNS lookup and DNS NAPTR/SRV lookup
- Connection monitor with process information
- Subnet calculator with CIDR prefix, network and broadcast addresses, host range, and scan range
- Password generator with selectable character groups and configurable length
- FRITZ!Box and LANCOM firmware downloaders with search, file, size, and modification details

The firmware downloaders read directory listings from the vendors' official websites. Downloads can be saved to a selected folder and then shown in Explorer.

### Windows

Shortcuts to Network & Internet settings, Task Manager, Services, Device Manager, Firewall, Network Connections, Event Viewer, System Information, Resource Monitor, and Disk Management.

### Notes

A simple notes area. Notes are stored in the current user's Registry.

## Requirements

- Windows 10 or Windows 11
- AutoHotkey v2
- Administrator privileges: the main script checks for elevation at startup and exits otherwise. Elevated access is needed for adapter configuration.
- Internet access for public IP/geolocation lookups, the speed test, and firmware directories

Some features require suitable Windows components or adapter drivers. VLAN support depends on the network adapter.

## Launch

1. Install AutoHotkey v2.
2. Right-click `IP-App.ahk` and choose **Run as administrator**.
3. The main window appears before the adapter list and details are loaded in the background.

Other tabs and network tools can be used while local adapter information is loading.

## Project structure

```text
IP-App/
├── IP-App.ahk                     Main window, tabs, events, and startup flow
├── Gemeinsam.ahk                  Shared functions, data, and configuration
├── Tab_Netzwerkkarten.ahk          Adapter, profiles, and network configuration
├── Tab_Oeffentliche_IP.ahk         Public IP and location data
├── Tab_Erreichbarkeit.ahk          Ping, traceroute, and port test
├── Tab_Tools.ahk                   Includes network and Windows utilities
├── Tab_Notizen.ahk                 Notes
├── Tab_About.ahk                   Application information
└── tools/                          Standalone utility modules and helpers
```

## Data and privacy

Profiles, notes, and the last selected adapter are stored under `HKEY_CURRENT_USER\Software\IP-App`; no separate profile file is created. Features using external services require internet access. AVM and LANCOM receive standard connection data, including the computer's IP address, when their firmware directories are queried.

## Notes

- Network settings are changed only when the adapter configuration is explicitly applied with **Übernehmen**.
- Changing IP, DNS, or VLAN settings may interrupt the network connection.
- Availability, versions, and structure of external firmware directories may change.
- The application interface is in German.

## Initial commit

Suggested commit message:

```text
feat: add Windows network tools desktop application
```

German alternative:

```text
feat: Windows-Anwendung für Netzwerktools hinzufügen
```
