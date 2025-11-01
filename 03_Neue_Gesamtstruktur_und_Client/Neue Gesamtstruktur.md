
## Gesamtstruktur 
Hier habe ich alle Rolen schon hinzugefügt und den Domain Controller 
![alt text](image.png)
![alt text](Enable-recycling.png)
![alt text](ClientinDomain.png)
Ich habe den Client M159Client über die Systemeinstellungen der Domäne aws.km.m159 hinzugefügt, indem ich die Domäne ausgewählt und die Anmeldedaten des Domain-Administrators eingegeben habe. Danach wurde der Computer erfolgreich der Domäne beigetreten.
#### 9.9.9.9 (Quad9) vs. 8.8.8.8 (Google DNS)
 
- **Datenschutz:** Quad9 ist Non-Profit (Schweiz) und speichert keine Nutzerdaten → besserer Datenschutz.  
- **Sicherheit:** Quad9 blockiert automatisch schädliche Domains.  
- **Geschwindigkeit:** Google DNS ist meist minimal schneller.  
- **Fazit:** Quad9 = sicherer & privater, Google = etwas schneller.
- ![alt text](image-1.png)



Ich habe im Active Directory überprüft, ob die Computer und Gruppen korrekt in der Domäne registriert sind.
Der Domain Controller (EC2AMAZ) und der Client M159Client erscheinen unter den Computern.
Zusätzlich habe ich die Gruppen RDP_Admins und RDP_Users erstellt und die entsprechenden Benutzer (Administrator → Admins, Guest → Users) hinzugefügt.
- ![alt text](image-2.png)
- ![alt text](image-4.png)
- ![alt text](image-3.png)
- ![alt text](image-5.png)

Ich habe auf dem Client die Gruppen RDP_Admins und RDP_Users zu den Remote Desktop Users hinzugefügt, damit sich diese Gruppen per RDP anmelden können.
Anschließend habe ich erfolgreich mit dem Benutzer Koichiro getestet, dass der Login über Remote Desktop funktioniert.