<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket – Voraussetzungen und Installation</h1>
Dieses Tutorial beschreibt die Voraussetzungen und die Installation des Open-Source-Helpdesk-Ticketingsystems osTicket.<br />



<h2>Verwendete Technologien und Umgebungen</h2>

- Microsoft Azure (Virtuelle Maschinen)
- Remote Desktop
- Internet Information Services (IIS)



<h2>Verwendete Betriebssysteme</h2>

- Windows 10</b> (21H2)



<h2>Liste der Voraussetzungen</h2>

- Microsoft Azure
- osTicket-Installation-Files.zip
- Internet Information Services (IIS)
- Hypertext Preprocessor (PHP)
- HeidiSQL (MySQL Datenbank)



<h2>Installation - Inhaltsangabe</h2>
Hier ist ein grober Überblick über die Reihenfolge der Installationen, der von osTicket benötigten Komponenten, sowie die Installation von osTicket selbst. Folglich sind die Abschnitte nach den jeweiligen Komponenten gegliedert.
<br />
<br />

- Vorbereitungen
- Installation IIS
- Installation PHP
- Installation MySQL
- Einrichtung osTicket
- Korrekturen (WICHTIG!!)



<h1>Installation - Schritt für Schritt</h1>
<br />


<h2>Vorbereitungen</h2>

<p>
Zuerst erstellen wir eine Virtuelle Maschine auf der wir osTicket installieren. Als Cloud-Anbieter benutze ich Microsoft Azure. Der erste Schritt ist es sich eine Ressourcengruppe zu erstellen. Merke dir den Namen der Ressourcengruppe für den nächsten Schritt, das Erstellen einer Virtuellen Maschine. 
<p>
Meine heißt: osTicket-RGroup
</p>
<img src="https://i.imgur.com/sDhYnw1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Im Anschluss erstellen wir eine Virtuelle Maschine (/Virtuellen Computer). 
</p>
<p>
<img src="https://i.imgur.com/jdP4nYk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<br />

Hierbei musst du auf folgende Dinge Acht geben. Alle folgenden Einstellungen befinden sich auf der ersten Seite, den "Grundeinstellungen":
  
- das Verwenden der zuvor erstellten Ressourcengruppe
- die Virtuellen Maschine taufen (einen Namen geben)
- bei "Region" eine möglichst nahe wählen (bezieht sich auf den physischen Standort deiner Virtuellen Maschine/Standort des Cloud-Centers in der deine Virtuelle Maschine Erschaffen wird. Daher je näher desto besser, da die Distanz sich später bei der Verbindung mit deinem Computer auf diese auswirken kann

<p>
<img src="https://i.imgur.com/Ftz495Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- das "Image" bezeichnet das Betriebssystem der Virtuellen Maschine. Hier wählst du Windows 10 Pro aus.
- die "Größe" bezeichnet die Rechenleistung der Virtuellen Maschine. Ich wähle die Variante mit 4 vcpus ( 4 virtuelle Central Processing Units), falls Kosten ein Faktor ist, dann kannst du auch die Variante mit 2 vcpus auswählen. Diese reicht vollkommen aus für diese Anleitung.

<p>
<img src="https://i.imgur.com/ZXwR4iq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- der Benutzername und das entsprechende Passwort stehen dir frei, hauptsache du vergisst sie nicht. Sie spiegeln die Anmeldedaten des Benutzers des Betriebssystems deiner Virtuellen Maschine. Stell dir den Account deines eigenen Computersvor, den du gerade verwendest diesen Satz zu lesen. Für diesen Account definierst du den Benutzernamen und das entsprechende Passwort. Beides benötigst du um später Zugriff auf die Virtuelle Maschine zu haben.

<p>
<img src="https://i.imgur.com/YpzCSGI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- zuletzt setze das Häckchen für das Verfügen einer Windows 10/11-Lizenz
- den Rest kannst du unberührt lassen und anschließend unten links auf "Überprüfen und erstellen" drücken. Dann nochmal auf "Erstellen".

<p>
<img src="https://i.imgur.com/jubHI6s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
___remote desktop + osticke-Inst-Files.zip___
</p>



<!--NEW SECTION -->
<h2>Installation IIS</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />



<!--NEW SECTION -->
<h2>Installation PHP</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />



<!--NEW SECTION -->
<h2>Installation MySQL</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />



<!--NEW SECTION -->
<h2>Einrichtung osTicket</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />



<!--NEW SECTION -->
<h2>Korrekturen</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
