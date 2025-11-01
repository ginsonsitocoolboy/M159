# DIT und GPO 
Teil 1: Passwortrichtlinien
Ich habe in der Default Domain Policy die Passwortkomplexität deaktiviert und das Erzwingen einer Passwortänderung entfernt. Diese Änderungen gelten nur für die Testumgebung.
![alt text](image.png)
![alt text](image-1.png)
![alt text](image-2.png)

Teil 2: Netzlaufwerke per GPO
Ich habe GPOs erstellt, um Netzlaufwerke automatisch zu verbinden. Dabei gibt es ein gemeinsames Laufwerk „Pool“ und je ein Abteilungslaufwerk für interne und externe Abteilungen. Die GPOs wurden direkt mit den passenden OUs verknüpft.
![alt text](image-3.png)
![alt text](image-4.png)

Teil 3: Desktop-Verknüpfung (positive Filterung)
Ich habe ein GPO erstellt, das eine Desktop-Verknüpfung zum Web-CRM anlegt. Dieses GPO ist auf oberster Ebene verknüpft und über Sicherheitsfilterung nur für die internen Gruppen aktiv.

![alt text](image-6.png)
![alt text](image-7.png)

Teil 4: WMI-Filter (Windows 10)
Ich habe einen WMI-Filter erstellt, der nur Windows-10-Clients erkennt. Das GPO „Textdatei kopieren“ kopiert eine Datei von der Freigabe Pool nach %temp% bei allen Benutzern der OU Promoter. Die Auswertung habe ich mit gpresult /h gpo.html exportiert.
![alt text](image-8.png)
![alt text](image-9.png)

Teil 5: Drucker verteilen
Ich habe zwei fiktive Drucker eingerichtet: Drucker_Farbe und Drucker_SW. Beide wurden freigegeben und per GPO über UNC-Pfad verteilt. Die Funktion habe ich getestet, indem ich die Drucker gelöscht und mit gpupdate /force neu hinzugefügt habe.
![alt text](image-10.png)
<video controls src="2025-11-01 23-40-10 (1).mp4" title="Title"></video>

Teil 6: 7-Zip per GPO
Ich habe ein MSI-Paket von 7-Zip auf einer Freigabe bereitgestellt und ein GPO zur automatischen Installation auf Domain-Computern erstellt. Nur Computer in der Security Group „7-Zip“ erhalten die Software. Die erfolgreiche Installation habe ich über das Eventlog überprüft.
![alt text](image-11.png)
![alt text](image-12.png)
![alt text](image-5.png)
