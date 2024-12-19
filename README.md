<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket – Voraussetzungen und Installation</h1>
Dieses Tutorial beschreibt die Voraussetzungen und die Installation des Open-Source-Helpdesk-Ticketingsystems osTicket.<br />



<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
<h2>Verwendete Technologien und Umgebungen</h2>

- Microsoft Azure (Virtuelle Maschinen)
- Remote Desktop
- Internet Information Services (IIS)



<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
<h2>Verwendete Betriebssysteme</h2>

- Windows 10</b> (21H2)



<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
<h2>Liste der Voraussetzungen</h2>

- Microsoft Azure
- osTicket-Installation-Files.zip
- Internet Information Services (IIS)
- Hypertext Preprocessor (PHP)
- HeidiSQL (MySQL Datenbank)



<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
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



<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
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
<hr>
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
<hr>
<p>
Nun müssen wir uns mit der Virtuellen Maschine verbinden und diese auch bedienen. Hierzu benutzen wir (auf Windows) die Anwendung Remotedesktopverbindung. Falls ihr eigener Computer ein MacOS ist, so müssen Sie eine App im App Store herunterladen namens Microsoft Remote Desktop.
</p>

<p>
<img src="https://i.imgur.com/oMyuNh1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/pbC7dIS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/tVsAUjz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Egal ob Remotedesktopverbindung oder Microsoft Desktop Remote müssen Sie nach dem öffnen der Anwendung die öffentliche IP-Addresse Ihrer Virtuellen Maschine eingeben sowie den Benutzername und das Passwort. Die IP-Adresse finden sie in Microsoft Azure dort, wo Sie die Maschine erstellt haben und den Benutzernamen und das Passwort meinen den von Ihnen beim Erstellen der Maschine definierten Benutzer und Passwort. Nachdem Sie sich in Ihre Maschine eingeloggt haben, downloaden Sie diesen Ordner innerhalb Ihrer Viruellen Maschine: [osTicket-Installation-Files.zip]: https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD. Und wenn Sie schon dabei sind, extrahieren Sie den Ordner an einen Ort wo Sie es leicht finden. Wenn Ich in der Zukunft von den osTicket-Installation-Files spreche, dann beziehe ich mich auf den Ordner mit dem gleichen Namen der nach Der Extraktion entsteht. Von nun an wird alles innerhalb der Virtuellen Maschine gemacht. Zusammen mit dieser und dem Ordner steht unserer Installation von osTicket nichts mehr im Weg! 
</p>



<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
<h2>Installation IIS</h2>

<p>
was ist iis:anhvjufdbvujsdbfknfovbndfsobnoifdnbad. Um es zu installieren navigieren wir innerhalb der Systemsteuerung (/Control Panel) zu Programmen, unter "Programme und Features" auf "Programm deinstallieren" und zuletzt auf der linken Seite auf "Windows-Features aktivieren oder deaktivieren".
</p>
<p>
<img src="https://i.imgur.com/CWYdrUC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/zXpecWn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/jJ6r8Lo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Suchen Sie nach "Internetinformationsdienste" und setzen Sie Häckchen. Drücken sie auf das kleine Plus neben dem Häckchen, das erneut bei "WWW-Dienste", erneut bei "Anwendungsentwicklungsfeatures" und suchen Sie nach "CGI" und setzen Sie auch hier ein Häckchen. Drücken Sie auf "OK" um die Installation zu starten. CGI steht für Common Gateway Interface und wird gebraucht für:jbiuvbufsdbvhuasogaugbjfvdfbdsf.
</p>
<p>
<img src="https://i.imgur.com/VqNSU3a.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Finden tun Sie das IIS uber... So schaut das Icon aus:
</p>
<p>
<img src="https://i.imgur.com/DuEuq2c.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/xaOwpe0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<hr>

<p>
Zuletzt installieren wir "rewrite_amd64..." aus dem osTicket-Installation-Folder. (Erklären wofür es gebraucht wird/was es ist:fndfjfsagvjuifsdabuvfjvnbjdfybujfdas)
</p>
<p>
<img src="https://i.imgur.com/RACzSvN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />



<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
<h2>Installation PHP</h2>

<p>
Was ist PHP und wofür brauchen wir es?...asdfasdfasdfgasdfga..../.
</p>
<p>
Als erstes erstellen wir einen Ordner namens "PHP" auf unserem lokalen Datenträger. Der Pfad ist folgender: "Dieser PC"-->"Lokaler Datenträger(C:)".
</p>
<p>
<img src="https://i.imgur.com/eQRc4O2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Daraufhin öffnen wir den osTicket-Installation-Files Ordner und installieren alles was PHP benötigt um flussig innerhalb des IIS zu operieren. Anfangen tun wir mit "VC_redist.x86". Bei VC_redist handelt es sich um ...adfasdfsadfgsafdgd...().
</p>
<p>
<img src="https://i.imgur.com/6t1JdFr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Jetzt kommt die Datei "PHPManagerForIIS_V1.5.0". Wie es im Namen schon steckt repräsentiert diese Datei den PHP Manager. Dieser ist zuständig für: fnvjbdsjfbvdsjfnvjsdfnbvjodsfb......(). 
</p>
<p>
<img src="https://i.imgur.com/7KIrWzj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Jetzt zur letzten, für PHP relevanten, Datei innerhalb des Installations-Ordners. Die Rede ist von "php-7.3.8-nts-Win32-VC15-x86". Darin befindet sich: najnbvufadsbzuiabfdenfjdsbvuasbfvgujasfvnfdaioa...(). Wir extrahieren den Ordner in unseren zuvor erstellten "PHP" Ordner (s. Beginn Installation PHP)
</p>
<p>
<img src="https://i.imgur.com/JmCwQke.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/6VWz9GH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<hr>

<p>
Fast geschafft! Für die letzten zwei Schritte müssen wir in IIS gehen und unsere PHP Version, die wir zuvor in den Ordner "PHP" extrahiert haben, registrieren. Sonst kann das IIS keinen Gebrauch davon machen wenn wir später osTicket installieren und einrichten wollen. Hiezu öffnen Sie IIS und müssten direkt ein Icon mit der Schrift "PHP Manager" dadrunter finden. Das klicken Sie an mit einem Doppleklick, damit sich das Fenster des PHP Managers öffnet. Jetzt klicken sie auf "Register new PHP version" und geben als Pfad den Weg zu unserem PHP Ordner ("This PC">"Windows(C:)">"PHP">) und wählen die Datei "php-cgi". Diese ist dnvjsdfbvjdsbfvujdbafjugb....(). Anschließend auf "OK" drücken.
</p>
<p>
<img src="https://i.imgur.com/7Bpudqt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/OhDS5cT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/pmvjFc5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
So sollte das ganze dann ausschauen: 
</p>
<p>
<img src="https://i.imgur.com/iDNpznJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Bevor wir uns um die Datenbank kümmern, starten wir den Webserver neu. Gehen Sie auf der linken Seite zurück zur Startseite des Server Managers und klicken sie rechts unter "Manage Server" auf "Restart".
</p>
<p>
<img src="https://i.imgur.com/0GcLTIa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />



<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
<h2>Installation MySQL</h2>

<p>
osTicket-Installation-Files Ordner mysql-5.5... installiern, weil das ist.......(). Wichtig: für Setup Type=Typical. Den Rest gleich lassen.
</p>
<p>
<img src="https://i.imgur.com/TMesfcO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/VtwS6tV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Am Ende den wizard starten.
<p/>
<p>
<img src="https://i.imgur.com/xPLUnlR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Wähle "standard Configuration", den Rest unberührt lassen und sich das eingegebene Passwort merken[stell sicher: brauchen wir das für später?? oder ist das einfach nur nen backup passwort was für die Anleitung irrelevant ist??]. Einfach "Next" drücken bis man "Execute" erreicht. Das drücken, danach auf "Finish".
<p/>
<p>
<img src="https://i.imgur.com/6eHyza0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Nächster Schritt, die Installation von "HeidiSQL..Setup" im osT-Install-Files Ordner. HeidiSQL ist .......sdfgbdsfghbsdfgh....(). Drücke "Next" durch bis du "Finish erreichst und achte bevor du darauf klickst, dass das häckchen bei "Launch HeidiSQL" gesetzt ist.
<p/>
<p>
<img src="https://i.imgur.com/3VYxQzk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Wenn sich HeidiSQL geöffnet hat, drücke auf "Skip"
<p/>
<p>
<img src="https://i.imgur.com/1WXSdK0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Der letzte Schritt für diesen Abschnitt der Anleitung behandelt das Erstellen einer neuen Datenbank, welche wir später mit unserem osTicket verbinden. Dafür rechtklicken wir auf die linke Spalte und drücken auf "New session". Ändern brauchen wir nichts, lediglich ein User und ein Passwort müssen wir uns überlegen. Beides brauchen wir später, also merke es dir oder schreibst dir auf. Drücke danach auf "Open" unten rechts.
<p/>
<p>
<img src="https://i.imgur.com/hS4oNDN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/cBDrNKd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Jetzt erstellen wir die Datenbank innerhalb der gerade erstellten Session und benennen sie osTicket. Rechtklicken Sie die Session, dann drücken Sie auf "Create new" und klicken auf "Database". Nachdem Sie den Namen "osTicket" eingegeben haben drücken Sie auf "OK".
<p/>
<p>
<img src="https://i.imgur.com/3wXGQVR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
So sollte das ganze dann aussehen:
<p/>
<p>
<img src="https://i.imgur.com/40RThgk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />




<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
<h2>Einrichtung osTicket</h2>

<p>
Alles was wir benötigen um osTicket zu benutzen haben wir zum jetzigen Zeitpunkt installiert und eingerichtet. Endlich können wir uns um die tatsächliche Installation von osTicket kümmern. Anfangen tun wir damit, den Ordner "osTicket-v1.15.8" innerhalb des Ordners osTicket-Installation-Files zu extrahieren
</p>
<p>
<img src="https://i.imgur.com/PbYS4NU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Danach kopieren wir den Ordner "upload" in dem gerade extrahiertem Ordner "osTicket-v1.15.8" und fügen ihn ein in den Ordner "wwwroot" mit dem Pfad "This PC">"Windows(C:)">"inetpub">"wwwroot". ordner wwwroot ist jdvbijhasfdbviuhdfasbvjbndfb....().
</p>
<p>
<img src="https://i.imgur.com/OK8Jno0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Nun benennen Wir den "upload" Ordner in dem "wwwroot" Ordner in "osTicket". das tun wir weil djncjbasdibvasufvdfanbbva....().
</p>
<p>
<img src="https://i.imgur.com/8B2jeQG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Endlich können wir osTicket im Browser aufrufen und beginnen, nach unseren Wünschen eine Helpdesk-Struktur aufzubauen. Öffnen Sie IIS und starten sie den Server neu (rechts auf "Restart" klicken). Dann klappen links den Server auf bis Sie einen Ordner namens "osTicket" sehen. klicken Sie in an, sodass der Ordner blau markiert ist und drücken Sie auf der rechten Seite auf "Browse *:80(http)".
</p>
<p>
<img src="https://i.imgur.com/SUqaWKw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Falls sich bei Ihnen nun ein Fenster mit dem Titel "osTicket Installer" öffnet, haben Sie bis jetzt alles richtig gemacht. Jetzt müssen wir nur noch die Schritte erledigen, die uns die Seite vorgibt und fertig sind wir. Der erste dieser Schritte besteht darin, empfohlene Erweiterungen für eine besser Erfahrung im Umgang mit der Anwendung zu aktivieren. Hierzu öffnen wir erneut den PHP Manager in IIS (s.Installation PHP), öffnen den "PHP Extension" Ordner und aktivieren die Erweiterungen "PHP IMAP Extension" und "Intl Extension". Beide besitzen auf der osTicket Installer Website ein rotes Kreuz links neben sich. Hierzu rechtklicken Sie in IIS in den PHP Extensions auf die jeweiligen Erweiterungen und drücken auf "Enable". 
</p>
<p>
<img src="https://i.imgur.com/16RIAQ1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/nj7PNf5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Laden sie die Webseite neu und beobachten Sie, dass aus den roten Kreuzen grüne Häckchen geworden sind. Falls das eintrifft drücken Sie auf "Continue".
</p>
<p>
<img src="https://i.imgur.com/chW2r2R.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Der nächste Schritt ist, die Datei "ost-sampleconfig.php" in "ost-config.php" umzubenennen. Diese Datei finden Sie in dem von uns umbenannten Ordner "osTicket" in dem Ordner "include".
</p>
<p>
<img src="https://i.imgur.com/wUZwIj6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Daruber Hinaus müssen wir die Berechtigungen für diese Datei ändern. Hierzu rechtsklicken Sie auf die Datei, drücken auf "Properties", oben auf "Security", unten auf "Advanced", links unten auf "Disable inheritance", dann auf "Remove all inherited permissions from this object". Jetzt fügen wir eine eigene Berechtigung zu und geben dieser volle Kontrolle über die Datei. Hierzu klicken Sie unten links auf "Add", oben auf "Select a principal" und dann geben Sie "Everyone" in das Feld (s. Bild) ein und drücken "OK". Vergessen Sie nicht die Box "Full Control" (s. Bild) mit einem Häckchen zu versetzen. Drücken Sie erneut auf "OK", dann "Apply" und zweimal wieder auf "OK". Gehen Sie zurück auf die Webseite und drücken Sie erneut auf "Continue"
</p>
<p>
<img src="https://i.imgur.com/lnV2va0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/vCAIJ7i.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Jetzt müssen Sie nur noch alles auf der Seite ausfüllen und anschließend auf "Install Now" drücken. Bei den "Database Settings" müssen sie sich an den Anletungsteil "Installation MySQL" zurückerinnern. Dort haben wir innerhalb einer Session eine Datenbank namens "osTicket" angelenkt und für diese Session einen User und Password eingegeben. Diese drei Daten geben Sie hierfür ein.
</p>
<p>
Auf dieser Seite sollten sie Anschließend landen, wenn alles gelaufen ist wie es sollte:
</p>
<p>
<img src="https://i.imgur.com/iUqlX6B.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Geschafft! osTicket ist erfolgreich installiert. Nun konnen Sie über die unten aufgelisteten URLs jeweils verschiedene Schnittstellen Ihres Helpdesks erreichen und herum experimentieren.
</p>
<p>
<img src="https://i.imgur.com/zJ6Q9sL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />



<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
<h2>Korrekturen</h2>

<p>
Im Verlaufe der Anleitung haben wir im Kapitel "Installation osTicket" die Berechtigungen für die Datei "ost-config.php" geändert, sodass jeder vollen Zugriff über diese hat. Gefährlich weil jdsabuvbfaubguifbgsdfigbauigbajufdg....(). Finden Sie die Datei innerhalb des "include" Ordners (s. Bild für Pfad), rechtklicken Sie auf die Datei und drücken Sie erneut auf "Properties" und oben auf "Security". Wählen Sie die Gruppe "Everyone" aus und drücken Sie auf "Edit". Nehmen Sie überall die Häckchen weg bis auf das Häckchen für das Feld "Read". Anschließend drücken Sie auf "Apply", "OK" und nochmal "OK". Nun kann die Datei von jedem eingesehen, aber nicht verändert werden.
</p>
<p>
<img src="https://i.imgur.com/9dWewTW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/LHltHxN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Zu guter letzt löschen wir den Ordner "setup" innerhalb unseres "wwwroot">"osTicket" Ordners. WEIL jkxnvjubvbsadfb.....(). Et voila! Viel Spaß mit Ihrem eigenen Ticketsystem.
</p>
<p>
<img src="https://i.imgur.com/lghZBhK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />






<p>
AUSBLICK AUF MÖGLICHE KONFIGURATION/WEITERE EINRICHTUNG
</p>

