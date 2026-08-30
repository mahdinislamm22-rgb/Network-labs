# Network Labs — Cisco Packet Tracer

Zwei dokumentierte Netzwerk-Laborübungen aus meiner schulischen Ausbildung
in der Fachrichtung Informatik und Telekommunikation, umgesetzt mit
Cisco Packet Tracer.

Jede Übung besteht aus der Packet-Tracer-Datei (`.pkt`) und einer
schriftlichen Dokumentation (`.pdf`) mit Aufgabenstellung, Geräteliste,
Adressplan, Konfiguration und Testergebnissen.

---

## 1. Zugriffskontrolle zwischen zwei LANs mit Access Control Lists

**Dateien:** `ACL PROVA 1.pkt` · `Netzwerkdokumentation_ACL.pdf`

**Aufgabe:** Zwei lokale Netze (LAN A und LAN B) mit je drei Clients sind
über drei Router verbunden. Mit einer Access Control List soll verhindert
werden, dass Geräte aus LAN A auf LAN B zugreifen, während der übrige
Verkehr weiterhin erlaubt bleibt.

**Aufbau:** 3 Router, 2 Switches, 6 Clients. Eigener Adressplan mit
/27-Nutznetzen und /30-Transfernetzen zwischen den Routern.

**Umsetzung:** Standard-ACL auf dem Router nahe am Ziel, gefiltert nach
Quelladresse über die Wildcard-Maske `0.0.0.31`, anschließend mit
`ip access-group` ausgehend auf die Schnittstelle Richtung LAN B angewendet.

**Was die Übung zeigt:** Eine ACL wird von oben nach unten abgearbeitet und
die erste zutreffende Regel entscheidet. Am Ende steht implizit ein
`deny any`, deshalb ist eine abschließende `permit`-Regel notwendig. Und
eine ACL wirkt erst, wenn sie auf eine Schnittstelle angewendet wird —
ohne `ip access-group` existiert die Liste, tut aber nichts.

---

## 2. NAT und Adressumsetzung

**Dateien:** `EsercizioNAT.pkt` · `Netzwerkdokumentation_NAT.pdf`

**Aufgabe:** NAT auf einem Router konfigurieren und die Adressumsetzung
anschließend nachweisen.

**Aufbau:** 1 Router, 2 Switches, 1 Server, 2 Clients. Internes Netz mit
privaten Adressen, externes Netz mit dem Server als Gegenstelle.

**Umsetzung:** Statisches NAT für genau einen der beiden Clients. Der
zweite Client bleibt bewusst ohne Übersetzung, um einen direkten Vergleich
zu ermöglichen. Kontrolle über `show ip nat translations`.

**Nachweis:** Im Simulationsmodus wird von beiden Clients ein ICMP-Paket an
den Server gesendet und in den PDU-Details die Quell-IP-Adresse vor und
nach dem Router verglichen. Beim Client mit NAT wird die private Adresse
ersetzt, beim Client ohne NAT bleibt sie unverändert. Da alle übrigen
Bedingungen identisch sind, ist die Wirkung des NAT-Eintrags eindeutig
belegt.

---

## Kenntnisse aus diesen Übungen

TCP/IP · IP-Adressierung und Subnetting · Access Control Lists · NAT ·
Routing-Grundlagen · Cisco IOS CLI · Cisco Packet Tracer ·
Netz- und Adressplanung · technische Dokumentation

---

**Mahdin Islam Mohammed** · Siegen
mahdinislam018@gmail.com
