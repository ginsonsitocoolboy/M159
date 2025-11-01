# M159 - Projekt-Setup-Sheet

In diesem Dokument werden sämtliche Angaben sowie Passwörter, welche Sie für die Installation Ihrer Umgebung benötigen, festgehalten.

![Modul_159_Architekturdiagramm](Modul_159_Architekturdiagramm.drawio.svg)



---

## 1. Übersicht Umgebung

Diese Umgebung umfasst:

- **1x Windows Server (DC)** auf AWS EC2  
- **1x Windows Server (Client)** auf AWS EC2 (da AWS keine Windows Clients anbietet)  
- **1x Windows Server (Admin Center)** auf AWS EC2 zur Verwaltung der AWS Managed AD  
- **AWS Managed AD** mit Trust zur On-Premises(EC2) AD  
- **Entra Connect** zur Synchronisation mit Entra ID sowie Entra AD  
- **Lokale AD-Domain** (zu Beginn), später **öffentliche Domain als UPN**  

---

## 2. Allgemeine Angaben

| Feld                                | Wert |
| ----------------------------------- | ---- |
| Koichiro                       |      |
| Möller                        |      |
| PE23e                         |      |
| https://github.com/ginsonsitocoolboy/M159.git |      |

---
---

## 3. AWS VPC Setup

**Hinweis:**  
Alle Instanzen liegen in einem öffentlichen Subnetz und sind über RDP (Port 3389) von außen erreichbar.  
Alle weiteren Ports sind nur innerhalb des VPCs offen.

| Komponente                      | VPC-ID                | CIDR           | Name |
| ------------------------------- | --------------------- | -------------- | ---- |
| VPC                             | vpc-0b9717ea4b3f1f559 | 10.150.0.0/24  | M159-vpc |
| M159-subnet-private1-us-east-1a | subnet-xxxxxxxxxxxxx  | 10.150.0.128/26 | M159-private1-a |
| M159-subnet-private2-us-east-1b | subnet-xxxxxxxxxxxxx  | 10.150.0.192/26 | M159-private2-b |
| M159-subnet-public1-us-east-1a  | subnet-xxxxxxxxxxxxx  | 10.150.0.0/26   | M159-public1-a |
| M159-subnet-public2-us-east-1b  | subnet-xxxxxxxxxxxxx  | 10.150.0.64/26  | M159-public2-b |


---

## 4. AWS Sicherheitsgruppen

### Sicherheitsgruppe für Domain Controller

| Regeltyp                     | Port(e)                 | Quelle  |
| ---------------------------- | ----------------------- | ------- |
| RDP                          | 3389  (TCP)             | 10.150.0.0/24  |
| LDAP                         | 389 (TCP/UDP)           | 10.150.0.0/24         |
| LDAPS                        | 636 (TCP)               | 10.150.0.0/24         |
| Kerberos                     | 88 (TCP/UDP)            | 10.150.0.0/24         |
| SMB                          | 445  (TCP)              | 10.150.0.0/24         |
| DNS                          | 53 (TCP/UDP)            | 10.150.0.0/24         |
| RPC                          | 135, 49152-65535  (TCP) | 10.150.0.0/24         |
| ICMP                         | Alle                    | 10.150.0.0/24         |
| Global Catalog               | 3268 (TCP)              | 10.150.0.0/24         |
| Global Catalog SSL           | 3269 (TCP)              | 10.150.0.0/24         |
| Kerberos Password Change/Set | 464 (TCP/UDP)           | 10.150.0.0/24         |
|                              |                         |         |

### Sicherheitsgruppe für Clients

| Regeltyp | Port(e)     | Beschreibung                             | Quelle                                           |
| -------- | ----------- | ---------------------------------------- | ------------------------------------------------ |
| RDP      | 3389        | Remote Desktop                           | 0.0.0.0                                          |
| TCP      | 88          | Kerberos Authentication                  | 10.150.0.0/24 
| TCP      | 135         | RPC Endpoint Mapper                      | 10.150.0.0/24 
| TCP      | 139         | NetBIOS Session Service                  | 10.150.0.0/24 
| TCP      | 389         | LDAP                                     | 10.150.0.0/24 
| UDP      | 53          | DNS                                      | 10.150.0.0/24 
| TCP      | 445         | SMB/CIFS (Dateifreigabe, AD-Operationen) | 10.150.0.0/24 
| TCP      | 49152-65535 | RPC Ephemeral Ports                      | 10.150.0.0/24 
| ICMP     | Alle        | Ping etc.                                | 10.150.0.0/24 

---

## 5. Active Directory Umgebung

### On-Premises Active Directory (AWS EC2)

| Feld                                  | Wert                  |
| ------------------------------------- | --------------------- |
| Active Directory Third-Level-Domäne-1 | aws.km.m159           |
| Öffentlicher UPN-Suffix (später)      | m159km.v6.rocks       |
| Domänenadministrator                  | Administrator         |
| Kennwort Domänenadministrator         | (wird lokal dokumentiert) |
| Kennwort-Demote (Herunterstufen)      | (wird lokal dokumentiert) |



### AWS Managed AD

| Feld                                  | Wert                                                 |
| ------------------------------------- | ---------------------------------------------------- |
| Active Directory Third-Level-Domäne-2 | aws.km.m159                                          |
| Trust-Typ                             | Tree-Root Trust                                      |
| AWS Managed Admin User                | admin                                                |
| AWS Managed Admin Passwort            | (wird lokal dokumentiert)                            |
| IP-Adresse                            | 10.150.0.10                                          |
| DNS-Server 1                          | 10.150.0.10                                          |
| DNS-Server 2                          | 10.150.0.11                                          |
| Trust Passwort                        | (wird lokal dokumentiert)                            |
| Subnetz 1                             | M159-subnet-private1-us-east-1a (10.150.0.128/26)    |
| Subnetz 2                             | M159-subnet-private2-us-east-1b (10.150.0.192/26)    |

---

## 6. EC2-Instanzen

| Komponente                                       | FQDN                       | Elastic IP       | Private IP (CIDR)  | Subnetz                         | DNS-Server 1 | DNS-Server 2 | Lokaler Admin | Kennwort |
| ------------------------------------------------ | -------------------------- | ---------------- | ------------------ | ------------------------------- | ------------ | ------------ | ------------- | -------- |
| IaaS/OnPrem AD DC                                | dc.aws.km.m159             | 44.198.134.10    | 10.150.0.130       | M159-subnet-private1-us-east-1a | 10.150.0.10  | 10.150.0.11  | Administrator | (lokal dokumentiert) |
| Windows Server (Client)                          | client.aws.km.m159         | 44.198.134.36    | 10.150.0.24        | M159-subnet-public1-us-east-1a  | 10.150.0.10  | 10.150.0.11  | Administrator | (lokal dokumentiert) |
| Managed AWS EC2 DC                               | ad1.aws.km.m159            | —                | 10.150.0.10        | M159-subnet-private1-us-east-1a | 10.150.0.10  | 10.150.0.11  | admin         | (lokal dokumentiert) |
| Windows Server Admin Center (Managed AWS EC2 DC) | wac.aws.km.m159            | 44.198.134.50    | 10.150.0.66        | M159-subnet-public2-us-east-1b  | 10.150.0.10  | 10.150.0.11  | Administrator | (lokal dokumentiert) |


---

## 7. Abteilungen & Benutzer

Definieren Sie je einen Benutzer dieser 3 Abteilungen 

| Abteilung | Name der Abteilung | Benutzername | Vorname | Nachname | Kennwort | Bereiche |
| --------- | ------------------ | ------------ | ------- | -------- | -------- | -------- |
| 1         | Sekretariat        |              |         |          |          | intern   |
| 2         | Buchhaltung        |              |         |          |          | intern   |
| 3         | GL                 |              |         |          |          | intern   |
| 4         | Promoter           |              |         |          |          | extern   |

## 08. Python-App-Registration (Entra-ID)

| Name                    | Wert |
| ----------------------- | ---- |
| Directory (tenant) ID   |      |
| Application (client) ID |      |
| Client Secret ID        |      |



## 09. Hinweise

- Beginnen Sie mit der lokalen Domain-Umgebung und konfigurieren Sie **später den UPN-Suffix** mit der öffentlichen Domain.  
- Achten Sie auf **richtige Portfreigaben** in den AWS Sicherheitsgruppen, insbesondere für RDP, SMB und AD-Dienste.  
- Dokumentieren Sie alle IP-Adressen, Benutzernamen und Kennwörter konsequent in dieser Vorlage.
- Diese Vorlage wurde für das Schuljahr 2025/26 komplett neu erstellt. Falls Ihnen etwas fehlt, ist die Lehrperson dankbar, wenn Sie ihr dies mitteilen.
