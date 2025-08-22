# Directory Services – Fragen & Antworten

## 1. Aus technischer Sicht ist ein Verzeichnisdienst nichts anderes als
Eine **spezialisierte Datenbank**, die hierarchisch organisiert ist und für das **Speichern, Suchen und Verwalten** von Objekten optimiert ist.  

---

## 2. Nennen Sie 4 Kernaufgaben eines «Directory Services»
1. Authentifizierung von Benutzern und Geräten  
2. Autorisierung von Zugriffsrechten  
3. Zentrale Verwaltung von Ressourcen  
4. Replikation und hohe Verfügbarkeit  

---

## 3. Nennen Sie 5 Objekte (Ressourcen), welche in einem Directory vorkommen können
- Benutzer  
- Gruppen  
- Computer  
- Drucker  
- Freigaben (z. B. Fileserver)  

---

## 4. Nennen Sie 5 Merkmale eines «Directory Services»
1. Hierarchische Baumstruktur  
2. Zentrale Verwaltung von Benutzern und Ressourcen  
3. Skalierbarkeit  
4. Redundanz und Replikation  
5. Zugriff über Standardprotokolle (LDAP, Kerberos)  

---

## 5. Zusammenhang zwischen Objekt, Attribut und Wert – korrekte Antworten
-  Benutzerattribute sind Eigenschaften von Computern  
-  Benutzerattribute haben einen Namen und einen Wert  
-  Das Benutzerpasswortattribut bestehend aus Namen und Wert ist ein Benutzerattribut  
-  Der Vorname ist ein Benutzerattribut  
-  Druckerobjekte haben keine Attribute  

---

## 6. Was ist eine Objektklasse?
Eine **Objektklasse** definiert, welche Attribute ein Objekt besitzen darf oder muss.  

---

## 7. Nennen Sie zwei Nachteile eines «Directory Services»
1. Komplexität in Verwaltung und Einrichtung  
2. Abhängigkeit bei Ausfall (kein Login oder Zugriff möglich)  

---

## 8. Beschreiben Sie eine IT-Situation, welche einen «Directory Service» verlangt
Ein Unternehmen mit **vielen Mitarbeitern** benötigt zentrale Verwaltung von Benutzern, Gruppen, Geräten und Zugriffsrechten.  

---

## 9. Beschreiben Sie eine IT-Situation, welche keinen «Directory Service» verlangt
Ein **kleines Büro mit wenigen PCs**, wo Benutzer lokal verwaltet werden.  

---

## 10. Beschreiben Sie, was ein lokaler Administrator ist
Ein Konto mit **vollen Rechten nur auf einem einzelnen Computer**.  

---

## 11. Beschreiben Sie, was ein Domänenadministrator ist
Ein Konto mit **vollen Rechten in der gesamten Domäne** (Benutzer, Gruppen, Richtlinien, Geräte).  

---

## 12. Was ist die Aufgabe des Domänencontrollers?
- Ausführen des Verzeichnisdienstes (AD DS)  
- Authentifizierung, Autorisierung, Verwaltung, Replikation  

---

## 13. Wofür steht die Abkürzung DC?
- **Domain Controller**  

---

## 14. Wofür steht die Abkürzung OU bzw. OE?
- **Organizational Unit** / **Organisationseinheit**  
- Dient zur logischen Strukturierung von Objekten  
 
---

## 15. Was bedeutet „On-Premises“?
- Lokaler Betrieb der IT-Infrastruktur im eigenen Rechenzentrum.  

---

## 16. Was ist der Unterschied zwischen MS AD DS und Entra ID
- **AD DS**: On-Premises, Kerberos/LDAP, für lokale Netzwerke  
- **Entra ID**: Cloudbasiert, OAuth2/OpenID/SAML, für SaaS- und Cloud-Anwendungen  

---

## 17. Was ist und macht Intune, MDM & MAM?
- **Intune**: Cloud-Dienst für Geräte- und App-Management  
- **MDM**: Verwaltung von Endgeräten (Smartphones, Laptops)  
- **MAM**: Verwaltung von Apps und deren Daten  

---

## 18. Was ist ein Tenant?
Eine **eigene isolierte Cloud-Instanz** (Mandant), z. B. in Microsoft 365 / Entra ID.  

---

## 19. Wie nennt man eine AD-Umgebung mit Entra ID Integration?
- **Hybrid-Umgebung** (Hybrid AD)  
