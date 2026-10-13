# 🌐 CCNA 1 v7 Exam Cheat Sheet (Introduction to Networks - ITN)

## 1. OSI- und TCP/IP-Modell & Kapselung (PDUs)
Für die Prüfung musst du die Reihenfolge der Schichten und die jeweilige **Protocol Data Unit (PDU)** auswendig kennen.

| **OSI-Schicht** | **TCP/IP-Schicht** | **PDU-Name** | **Wichtige Protokolle / Adressierung** |
| :--- | :--- | :--- | :--- |
| **7.** Application <br>**6.** Presentation <br>**5.** Session | **Application** | **Data** (Daten) | HTTP, HTTPS, DNS, DHCP, FTP, SSH |
| **4. Transport** | **Transport** | **Segment** (TCP) <br>**Datagram** (UDP) | TCP (verbindungsorientiert), UDP (verbindungslos) <br>**Quell- & Ziel-Portnummern** |
| **3. Network** | **Internet** | **Packet** (Paket) | IPv4, IPv6, ICMP, Routing-Protokolle <br>**Quell- & Ziel-IP-Adressen** (logisch) |
| **2. Data Link** | **Network Access** | **Frame** (Rahmen) | Ethernet, WLAN, PPP, LLC & MAC Sublayer <br>**Quell- & Ziel-MAC-Adressen** (physisch) |
| **1. Physical** | **Network Access** | **Bits** | Kabel (Kupfer, Glasfaser), Funkwellen, Stecker |

---

## 🔌 2. Standard-Ports (Well-Known Ports)
*   **FTP (File Transfer):** Ports 20 & 21
*   **SSH (Secure Shell):** Port 22 *(Verschlüsselt, ersetzt Telnet)*
*   **Telnet:** Port 23 *(Unverschlüsselt, Klartext)*
*   **SMTP (E-Mail senden):** Port 25
*   **DNS (Namensauflösung):** Port 53 *(Nutzt TCP und UDP)*
*   **DHCP (Automatische IP):** Port 67 (Server) / Port 68 (Client)
*   **TFTP (Trivial FTP):** Port 69 *(UDP-basiert, oft für IOS-Backups genutzt)*
*   **HTTP (Web):** Port 80
*   **POP3 (E-Mail empfangen):** Port 110
*   **IMAP (E-Mail Verwaltung):** Port 143
*   **HTTPS (Sicheres Web):** Port 443

---

## 💻 3. Cisco IOS Modi & Speicherkomponenten

### Die CLI-Modi wechseln
*   `Router>` → **User EXEC Mode:** Nur grundlegende Abfragen.
*   `Router#` → **Privileged EXEC Mode:** Befehl `enable`. Ermöglicht `show`- und `copy`-Befehle.
*   `Router(config)#` → **Global Configuration Mode:** Befehl `configure terminal`. Ändert globale Geräteeinstellungen.
*   `Router(config-if)#` → **Interface Mode:** Befehl `interface [Name]` (z.B. `interface g0/0/0`).
*   `Router(config-line)#` → **Line Mode:** Befehl `line con 0` oder `line vty 0 4`.

### Speicherarten eines Cisco-Geräts
*   **RAM:** Flüchtig. Enthält die aktive Konfiguration (`running-config`) und die Routing-Tabelle.
*   **NVRAM:** Nicht-flüchtig. Enthält die beim Start geladene Konfiguration (`startup-config`).
*   **Flash-Speicher:** Nicht-flüchtig. Enthält das Cisco **IOS-Betriebssystem** und Systemdateien.
*   **ROM:** Nicht-flüchtig. Enthält den Boot-Code (Bootstrap) und grundlegende Hardware-Diagnose (POST).

---

## 🏷️ 4. IPv4 Subnetting & Adressbereiche

### Private IPv4-Adressräume (RFC 1918)
*   **Klasse A:** `10.0.0.0` bis `10.255.255.255`
*   **Klasse B:** `172.16.0.0` bis `172.31.255.255`
*   **Klasse C:** `192.168.0.0` bis `192.168.255.255`

### Wichtige Spezialadressen
*   **Loopback (Lokaler Host-Test):** `127.0.0.1` (IPv4) / `::1` (IPv6)
*   **APIPA (Link-Local bei DHCP-Fehler):** `169.254.0.0` bis `169.254.255.255`

### Subnetting-Schnellhilfe (CIDR & Subnetzmasken)
*   `/24` = `255.255.255.0` (256 IPs gesamt, **254 nutzbare Hosts**)
*   `/25` = `255.255.255.128` (128 IPs gesamt, **126 nutzbare Hosts**)
*   `/26` = `255.255.255.192` (64 IPs gesamt, **62 nutzbare Hosts**)
*   `/27` = `255.255.255.224` (32 IPs gesamt, **30 nutzbare Hosts**)
*   `/28` = `255.255.255.240` (16 IPs gesamt, **14 nutzbare Hosts**)
*   `/30` = `255.255.255.252` (4 IPs gesamt, **2 nutzbare Hosts** – ideal für Point-to-Point-Links)

> 💡 **Regel für nutzbare Hosts:** 2ⁿ - 2 (wobei *n* die Anzahl der Host-Bits ist; minus Netzadresse und Broadcastadresse).

---

## 🌐 5. IPv6 Grundlagen
*   **Länge:** 128 Bit (dargestellt in 8 Hexadezimal-Blöcken, getrennt durch Doppelpunkte).
*   **Kompressionregeln (Prüfungsgarantie!):**
    1. Führende Nullen in jedem Block dürfen weggelassen werden (z.B. `0DB8` → `DB8`).
    2. Einmalig dürfen aufeinanderfolgende Nur-Nullen-Blöcke durch einen doppelten Doppelpunkt `::` ersetzt werden.
*   **Global Unicast Address (GUA):** Entspricht einer öffentlichen IPv4-Adresse. Beginnt typischerweise mit `2000::/3`.
*   **Link-Local Address (LLA):** Gilt nur im lokalen Subnetz, nicht routingfähig. Beginnt immer mit `fe80::/10`.
*   **All-Nodes Multicast:** `ff02::1` (spricht alle Geräte im Segment an).
*   **All-Routers Multicast:** `ff02::2` (spricht alle Router im Segment an).

---

## 🔄 6. Adressauflösung: ARP vs. ICMPv6 ND
*   **IPv4 (ARP - Address Resolution Protocol):** Löst eine bekannte IPv4-Adresse in eine MAC-Adresse auf. Nutzt **Broadcasts** (belastet das Netz).
*   **IPv6 (NDP - Neighbor Discovery Protocol):** Ersetzt ARP komplett. Nutzt **ICMPv6-Nachrichten** und **Multicasts** statt Broadcasts.
    *   *Neighbor Solicitation (NS):* "Wer hat diese IPv6-Adresse? Bitte MAC senden."
    *   *Neighbor Advertisement (NA):* "Ich habe diese IPv6-Adresse, hier ist meine MAC."
    *   *Router Solicitation (RS):* Client sucht nach einem IPv6-Router.
    *   *Router Advertisement (RA):* Router sendet Netzwerkinformationen (Präfix, Prefix-Länge, Gateway) an Clients.

---

## 🛠️ 7. Unverzichtbare Cisco CLI-Konfigurationsbefehle

### Grundkonfiguration (Switch & Router)
```switch
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# enable secret class             ! Setzt das verschlüsselte Privileged-EXEC-Passwort
R1(config)# line console 0
R1(config-line)# password cisco
R1(config-line)# login
R1(config-line)# exit
R1(config)# line vty 0 4
R1(config-line)# password cisco
R1(config-line)# login
R1(config-line)# exit
R1(config)# service password-encryption     ! Verschlüsselt Klartextpasswörter in der Konfigdatei
R1(config)# banner motd #Zutritt verboten!# ! Rechtlicher Hinweis vor dem Login
```

### IP-Adresse auf Switch-Schnittstelle konfigurieren (SVI für Management)
```switch
S1(config)# interface vlan 1
S1(config-if)# ip address 192.168.1.2 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# exit
S1(config)# ip default-gateway 192.168.1.1  ! Ermöglicht Remotzugriff aus anderen Netzen
```

### IP-Adresse auf Router-Schnittstelle konfigurieren
```switch
R1(config)# interface gigabitethernet 0/0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown                  ! Aktiviert die Schnittstelle (standardmäßig "down")
```

### Konfiguration dauerhaft speichern
```switch
R1# copy running-config startup-config       ! Kopiert vom RAM ins NVRAM
```

---

## 🔍 8. Diagnose- und Troubleshooting-Befehle
*   `show ip interface brief` → Zeigt den Status (up/down) und die IP-Adressen aller IPv4-Interfaces.
*   `show ipv6 interface brief` → Zeigt dasselbe für IPv6 (inklusive der Link-Local-Adressen).
*   `show ip route` → Zeigt die **IPv4-Routingtabelle**. (Wichtig: Einträge mit **C** stehen für direkt verbundene Netze, **S** für statische Routen).
*   `show mac-address-table` → (Nur auf Switches!) Zeigt, welche MAC-Adresse an welchem Switch-Port gelernt wurde.
*   `ping [Ziel]` → Prüft die End-zu-End-Erreichbarkeit mittels ICMP Echo Requests.
*   `traceroute [Ziel]` → Zeigt Hop-by-Hop den Pfad zum Ziel und deckt Routing-Schleifen auf.
