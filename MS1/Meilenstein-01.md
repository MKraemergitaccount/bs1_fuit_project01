 Naamo Sami, Maik Kraemer

![[../Pictures/20250227120331.png]]


# Inhalt:
1. Plannung der VLAN- und IP-Struktur
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

![[../Pictures/20250226101747.png]]

***Verwenden Sie folgende Geräte:***
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


# Eingegebenen Befehle

***VLAN erstellen:*** 
Switch(config)# ``vlan 10`` 
Switch(config-vlan)# ``name VERWALTUNG`` 

***Port zu VLAN zuweisen:***
Switch(config)# ```interface Fa0/1```
Switch(config-if)# ``switchport mode access`` 
Switch(config-if)# ``switchport access vlan 10``

***IP zu VLAN zuweisen:***
Switch(config)# ```interface vlan vlan-i```
Switch(config-if)# ``ip address``

