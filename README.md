 Naamo Sami, Maik Kraemer

![[./Pictures/20250227120331.png]]


# Inhalt:
1. Planung der VLAN- und IP-Struktur
2. Soll vorgaben
3. Eingegebenen Befehle


# Planung der VLAN- und IP-Struktur 

| Gerät          | VLAN ID                                             | VLAN-Name                                                                                         | IP-Adressen                                                                                            | Subnetz  maske        | Gateway  Adresse                                                                                               | Netzwerk adresse |
| -------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | --------------------- | -------------------------------------------------------------------------------------------------------------- | ---------------- |
| Switch LJ1     | 99,     100,    51                                  | Management, Ausbilder,       LJ1                                                                  | 192.168.99.1  192.168.100.1   192.168.51.1                                                             | 255.255.255.0 /24     | 192.168.99.254  192.168.100.254 192.168.51.254                                                                 |                  |
| Switch LJ2     | 99,     100,    52                                  | Management, Ausbilder,      LJ2                                                                   | 192.168.99.2  192.168.100.2 192.168.52.1                                                               | 255.255.255.0 /24     | 192.168.99.254  192.168.100.254 192.168.52.254                                                                 |                  |
| Switch LJ3     | 99,     100,    53                                  | Management, Ausbilder,      LJ3                                                                   | 192.168.99.3  192.168.100.3 192.168.53.1                                                               | 255.255.255.0 /24     | 192.168.99.254  192.168.100.254 192.168.53.254                                                                 |                  |
| Drucker        | 99,     100,    51,      52,     53,     60         | Management, Ausbilder LJ1,          LJ2,           LJ3,                Drucker                    | 192.168.99.4 192.168.100.4 192.168.51.4  192.168.52.4 192.168.53.4 192.168.60.2                        | 255.255.255.0 /24     | 192.168.99.254  192.168.100.254 192.168.51.254  192.168.52.254  192.168.53.254  192.168.60.254                 |                  |
| Server         | 99,     100,    51,      52,     53,     70         | Management, Ausbilder, LJ1,          LJ2,           LJ3,                 Server                   | 192.168.99.5  192.168.100.5 192.168.51.5  192.168.52.5 192.168.53.5 192.168.70.2                       | 255.255.255.0 /24     | 192.168.99.254  192.168.100.254 192.168.51.254  192.168.52.254  192.168.53.254  192.168.70.254                 |                  |
| PCs LJ1        | 51                                                  | LJ1                                                                                               | 192.168.51.1/15                                                                                        | 255.255.255.0 /24     | 192.168.51.254                                                                                                 |                  |
| PCs LJ2        | 52                                                  | LJ2                                                                                               | 192.168.52.1/15                                                                                        | 255.255.255.0 /24     | 192.168.52.254                                                                                                 |                  |
| PCs LJ3        | 53                                                  | LJ3                                                                                               | 192.168.53.1/15                                                                                        | 255.255.255.0 /24     | 192.168.53.254                                                                                                 |                  |
| Zentral Switch | 99,     100,    51,      52,     53,     70,     60 | Management, Ausbilder, LJ1,          LJ2,           LJ3,                Server,           Drucker | 192.168.99.10  192.168.100.10 192.168.51.10  192.168.52.10 192.168.53.10 192.168.70.1     192.168.60.1 | <br>255.255.255.0 /24 | 192.168.99.254  192.168.100.254 192.168.51.254  192.168.52.254  192.168.53.254  192.168.70.254  192.168.60.254 |                  |

| Physikalische Schnittstelle | Logische Schnittstelle | VLAN-ID | VLAN-Name | IP-Adresse | Subnetz- maske |
| --------------------------- | ---------------------- | ------- | --------- | ---------- | -------------- |
|                             |                        |         |           |            |                |


# Soll vorgaben

### Vorgaben MS1:

![[../Pictures/20250226101747.png]]

**Verwenden Sie folgende Geräte:**
- Switch: 2960 
- Router: 1941 
- L3-Switch: 3560

***Als Anforderung an das neue Netzwerk wurden folgende Punkte definiert:***
- pro Lehrjahr 15 Azubis 
- Alle Lehrjahre sollen untereinander nicht kommunizieren können. 
- Alle Lehrjahre Zugriff auf:
	- Drucker, 
	- zentralen Server
	- Internet. 
- An Switch LJ3: 
	- Port Fa 0/20 der Drucker. 
	- Port Fa 0/21 der Server. 
- Alle Switchen: 
	- Port Fa 0/24 Management VLAN 
	- Port Fa 0/22
	- Port Fa 0/23 Ausbilder VLAN.


### Vorgaben MS2:

- Einlesen Inter-VLAN Routing
- Bearbeiten der Fragen und PT-Übung
- Herstellen der Kommunikation der VLANs im Projekt
- Abnahme Meilenstein 2 & Forms-Test


# Eingegebenen Befehle

### Befehle MS1:
```
# Config Mode:
Switche> enable
Switche# configure terminal
```

```
# VLAN erstellen:
Switch(config)#          vlan 10
Switch(config-vlan)#     name VERWALTUNG
```

```
# Port zu VLAN zuweisen:
Switch(config)#          interface Fa0/1
Switch(config-if)#       switchport mode access
Switch(config-if)#       switchport access vlan 10
```

```
# IP zu VLAN zuweisen:
Switch(config)# ```interface vlan vlan-i```
Switch(config-if)# ``ip address``
```

### Befehle MS2:
```
# Config Mode Router:
Router>                      enable
Router#                      configure terminal
```

```

Router(config)#              interface gigabitEthernet 0/1.51
Router(config)#              encapsultion dot1Q 51
```

```

Router(config-subif)#        ip address 192.168.51.254 255.255.255.0
Router(config-subif)#        exit
```

```

Router(config)#              interface gigabitEthernet 0/1.51
Router(config-subif)#        encapsulation dot1Q 51
Router(config-subif)#        ip address 192.168.51.254 255.255.255.0
Router(config-subif)#        exit
```

```

Router(config)#              interface gigabitEthernet 0/1
Router(config-if)#           no shutdown
Router(config-if)#           exit
````

```
# Config Mode Switch:
Switche>                     enable
Switche#                     configure terminal
```

```
# inter-Vlan-Routing:
Switch(config)#        interface vlan 51
Switch(config-if)#     ip address 192.168.51.254 255.255.255.0
Switch(config-if)#     no shutdown
Switch(config-if)#     exit
```

```

Switch(config)#        interface vlan 52
Switch(config-if)#     ip address 192.168.52.254 255.255.255.0
Switch(config-if)#     no shutdown
Switch(config-if)#     exit
```

```

Switch(config)#        interface vlan 53
Switch(config-if)#     ip address 192.168.53.254 255.255.255.0
Switch(config-if)#     no shutdown
Switch(config-if)#     exit
```

```

Switch(config)#        ip routing
```

### Befehle MS3:
```

R1(config)#       interface Ethernet0/0 
R1(config-if)#    ip address 10.1.1.1 255.255.255.0 
R1(config-if)#    ip access-group 1 out 
R1(config-if)#    exit 
R1(config)#       access-list 1 permit 10.1.1.0 0.0.0.255
```

### Befehle MS4:
```

R1(config)#         int gig0/0 
R1(config-if)#      ip nat inside 
R1(config)#         int S1/0 
R1(config-if)#      ip nat outside
```

# Praxisübungen:
### Praxisübung MS2 Inter-VLAN-Routing:

| Bild/Skizze                         | allg. Konfiguration | Beschreibung Arbeitsweise                                                                                                                                                                     | Nachteile                                                                                | Vorteile                                                                                                     | Art               |
| ----------------------------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | ----------------- |
| ![[./Pictures/20250326134432.png]] |                     | eine dedizierte Router-Schnittstelle mit einem VLAN verknüpft                                                                                                                                 | jedes VLAN ein Router- und Switch-Port mit der entsprechenden Verkabelung benötigt wird. | gute Kompatibilität mit alter Hardware jedes VLAN kann die volle Bandbreite des physikalischen Ports nutzen. | Legacy Routing    |
| ![[./Pictures/20250326134533.png]] |                     | SVI (Switch Virtual Interface = VLAN dem eine IP-Adresse zugewiesen wurde). Vermittlung der Frames zwischen VLANs geschieht innerhalb Gerätes                                                 | Der höhere finanzielle Aufwand                                                           | die Vermittlung erfolgt mit geringer Latenz                                                                  | Layer 3 Switch    |
| ![[./Pictures/20250326134552.png]] |                     | Auf dem Router wird, anstatt für jedes VLAN eine dedizierte Netzwerkschnittstelle zu verwenden, eine physische Schnittstelle in mehrere virtuellen Schnittstellen (Subinterfaces) unterteilt. | VLANs müssen sich die Bandbreite physikalischer Schnittstelle teilen.                    | Geräteschnittstellen und Verbindungskabel werden gespart.                                                    | Router on a Stick |



### Praxisübung MS3 ACLs :

1. Überprüfen Sie zunächst ob beide PCs Zugriff auf den Drucker 1 haben. Falls nicht, stellen Sie das zunächst sicher.  
2. Erstellen Sie als erstes eine Standard-ACL mit der Nummer 1 und binden Sie diese an das entsprechende Interface.  
3. Überprüfen Sie die Konnektivität.  
4. Erstellen Sie nun eine Erweiterte-ACL mit der Nummer 101 
   und binden Sie diese an das entsprechende Interface.  
5. Überprüfen Sie die Konnektivität.

