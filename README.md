<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket – Voraussetzungen und Installation</h1>
Dieses Tutorial beschreibt die Voraussetzungen und führt Sie durch die Installation des Open-Source-Ticketingsystems osTicket.
<br />


Klicke hier: [Dokumentation](https://example.com)
<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
<h2>Verwendete Technologien und Umgebungen</h2>

- Microsoft Azure (Virtuelle Maschine)
- Remote Desktop
- Internet Information Services (IIS)
- HeidiSQL
- Hypertext Preprocessor (PHP)



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
<p>
Hier ist ein grober Überblick über die Reihenfolge der Installationen, der von osTicket benötigten Komponenten, sowie die Installation von osTicket selbst. Folglich sind die Abschnitte nach den jeweiligen Komponenten gegliedert.
</p>
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

<h2>Vorbereitungen</h2>

<p>
Zuerst erstellen wir eine virtuelle Maschine, auf der wir osTicket installieren. Als Cloud-Anbieter benutze ich Microsoft Azure. Der erste Schritt ist es, sich eine Ressourcengruppe zu erstellen. Merke dir den Namen der Ressourcengruppe für den nächsten Schritt, das Erstellen einer virtuellen Maschine.
<p>
Meine heißt: osTicket-RGroup.
</p>
<img src="https://i.imgur.com/sDhYnw1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Im Anschluss erstellen wir eine virtuelle Maschine (/virtuellen Computer). 
</p>
<p>
<img src="https://i.imgur.com/jdP4nYk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<hr>
Hierbei musst du auf folgende Dinge Acht geben. Alle folgenden Einstellungen befinden sich auf der ersten Seite, den "Grundeinstellungen":

- Das Verwenden der zuvor erstellten Ressourcengruppe.
- Die virtuelle Maschine taufen (einen Namen geben).
- Bei "Region" eine möglichst nahe wählen (bezieht sich auf den physischen Standort deiner virtuellen Maschine/Standort des Cloud-Centers in der deine virtuelle Maschine Erschaffen wird. Daher je näher, desto besser, da die Distanz später, bei der Verbindung mit deinem Computer, sich auf diese auswirken kann).

<p>
<img src="https://i.imgur.com/Ftz495Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- Das "Image" bezeichnet das Betriebssystem der virtuellen Maschine. Hier wählst du Windows 10 Pro aus.
- Die "Größe" bezeichnet die Rechenleistung der virtuellen Maschine. Ich wähle die Variante mit 4 vcpus (4 virtuelle Central Processing Units). Falls Kosten ein Faktor sind, dann kannst du auch die Variante mit 2 vcpus auswählen. Diese reicht vollkommen aus für diese Anleitung.

<p>
<img src="https://i.imgur.com/ZXwR4iq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- Der Benutzername und das entsprechende Passwort stehen dir frei, Hauptsache du vergisst sie nicht. Sie spiegeln die Anmeldedaten des Benutzers des Betriebssystems deiner virtuellen Maschine dar. Stell dir den Account deines eigenen Computers vor, den Account den du gerade verwendest, um diesen Satz im Browser zu lesen. Für diesen Account definierst du den Benutzernamen und das entsprechende Passwort. Beides benötigst du, um später Zugriff auf die virtuelle Maschine zu haben.

<p>
<img src="https://i.imgur.com/YpzCSGI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- Zuletzt setze das Häkchen für das Verfügen einer Windows 10/11-Lizenz.
- Den Rest kannst du unberührt lassen und anschließend unten links auf "Überprüfen und erstellen" drücken. Dann nochmal auf "Erstellen".

<p>
<img src="https://i.imgur.com/jubHI6s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<hr>

<br />
<p>
Nun müssen wir uns mit der virtuellen Maschine verbinden und diese auch bedienen. Hierzu benutzen wir (auf Windows) die Anwendung Remotedesktopverbindung. Falls ihr eigener Computer ein macOS ist, so müssen Sie eine App im App Store herunterladen namens Microsoft Remote Desktop.
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
Egal ob Remotedesktopverbindung oder Microsoft Desktop Remote müssen Sie nach dem Öffnen der Anwendung die öffentliche IP-Adresse Ihrer virtuellen Maschine eingeben, sowie den Benutzernamen und das Passwort. Die IP-Adresse finden sie in Microsoft Azure dort, wo Sie die Maschine erstellt haben und den Benutzernamen und das Passwort meinen den von Ihnen, beim Erstellen der Maschine, definierten Benutzer und Passwort. Nachdem Sie sich in Ihre Maschine eingeloggt haben, downloaden Sie diesen Ordner innerhalb Ihrer virtuellen Maschine: [I'm a reference-style link][osTicket-Inst-Ordner] bbbb [osTicket-Installation-Files.zip]: https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD. Und wenn Sie schon dabei sind, extrahieren Sie den Ordner an einen Ort wo Sie ihn leicht finden. Wenn ich in der Zukunft von einem osTicket-Installation-Files spreche, dann beziehe ich mich auf den Ordner, mit dem gleichen Namen, der nach der Extraktion entsteht. Von nun an wird alles innerhalb der virtuellen Maschine gemacht. Zusammen mit dieser und dem Ordner steht unserer Installation von osTicket nichts mehr im Weg! gggggggggggggggggggggggggggggg ggggggggggggggggggggggggggggggggggggggggggggggggggggggggggggggggggggggggggggggg
</p>
[osTicket-Inst-Ordner](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD)


<!--NEW SECTION -->
<!--NEW SECTION -->
<!--NEW SECTION -->
<h2>Installation IIS</h2>

<p>
IIS (Internet Information Services) ist ein Webserver von Microsoft, der es ermöglicht, Webseiten und Webanwendungen bereitzustellen und zu hosten. Es dient als Plattform zur Verwaltung von Webdiensten und unterstützt verschiedene Protokolle wie HTTP, HTTPS und FTP. Um es zu installieren, navigieren wir innerhalb der Systemsteuerung (/Control Panel) zu Programmen, unter "Programme und Features" auf "Programm deinstallieren" und zuletzt auf der linken Seite auf "Windows-Features aktivieren oder deaktivieren".
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
Suchen Sie nach "Internetinformationsdienste" und setzen Sie das Häkchen. Drücken Sie auf das kleine Plus neben dem Häkchen, das erneut bei "WWW-Dienste", erneut bei "Anwendungsentwicklungsfeatures" und suchen Sie nach "CGI" und setzen Sie auch hier ein Häkchen. Drücken Sie auf "OK" um die Installation zu starten. CGI steht für Common Gateway Interface und ist eine Schnittstelle, die es einem Webserver ermöglicht, mit externen Programmen oder Skripten zu kommunizieren, um dynamische Inhalte zu erstellen. Es wird häufig verwendet, um serverseitige Skripte wie PHP oder Perl auszuführen, die zur Verarbeitung von Benutzeranfragen oder zur Interaktion mit einer Datenbank erforderlich sind. In unserem Fall benötigen wir CGI, um sicherzustellen, dass osTicket seine serverseitigen Skripte korrekt ausführen kann und die Webanwendung reibungslos funktioniert.
</p>
<p>
<img src="https://i.imgur.com/VqNSU3a.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Finden tun Sie das IIS über die Suchleiste unten links. So schaut das Icon aus:
</p>
<p>
<img src="https://i.imgur.com/DuEuq2c.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/xaOwpe0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<hr>

<p>
Zuletzt installieren wir "rewrite_amd64_en-US" aus dem osTicket-Installation-Folder. Diese Datei installiert das URL Rewrite-Modul für IIS, das es ermöglicht, URLs flexibel umzuschreiben und weiterzuleiten. Dieses Modul ist essenziell, um benutzerfreundliche, suchmaschinenoptimierte URLs zu erstellen oder Anfragen gezielt an bestimmte Skripte oder Seiten weiterzuleiten. Im Zusammenhang mit osTicket sorgt das Rewrite-Modul dafür, dass die URLs korrekt verarbeitet werden und die Webanwendung reibungslos funktioniert, indem es die gewünschten Endpunkte für Benutzer und Server erreichbar macht.
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
Bei PHP (Hypertext Preprocessor) handelt es sich um eine serverseitige Skriptsprache, die speziell für die Entwicklung dynamischer Webseiten und Webanwendungen entwickelt wurde. Sie ermöglicht es, serverseitige Logik auszuführen, Benutzerdaten zu verarbeiten und Inhalte dynamisch zu generieren. Im Kontext von osTicket benötigen wir PHP, da die Anwendung auf PHP basiert und diese Sprache verwendet, um ihre Funktionalitäten wie das Erstellen und Verwalten von Support-Tickets bereitzustellen.
</p>
<p>
Als erstes erstellen wir einen Ordner namens "PHP" auf unserem lokalen Datenträger. Der Pfad ist folgender: "Dieser PC"-->"Lokaler Datenträger(C:)".
</p>
<p>
<img src="https://i.imgur.com/eQRc4O2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Daraufhin öffnen wir den osTicket-Installation-Files Ordner und installieren alles, was PHP benötigt, um flüssig innerhalb des IIS zu operieren. Anfangen tun wir mit "VC_redist.x86". Die Datei „VC_redist.x86“ installiert die "Microsoft Visual C++ Redistributable", eine Sammlung von Laufzeitbibliotheken, die von Anwendungen benötigt werden, die mit Visual C++ entwickelt wurden. PHP und viele seiner Erweiterungen sind auf diese Laufzeitbibliotheken angewiesen, um korrekt zu funktionieren. In Bezug auf osTicket ist die Installation dieser Datei notwendig, da sie sicherstellt, dass PHP und alle dazugehörigen Komponenten ordnungsgemäß ausgeführt werden können.
</p>
<p>
<img src="https://i.imgur.com/6t1JdFr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Jetzt kommt die Datei "PHPManagerForIIS_V1.5.0". Wie es im Namen schon steckt hinter dieser Datei der PHP Manager. Dieser ist zuständig für eine einfache Verwaltung von PHP-Installationen auf dem IIS-Server. Es hilft dabei, PHP-Versionen zu konfigurieren, Einstellungen zu optimieren und Erweiterungen zu verwalten, um PHP effektiv mit IIS zu integrieren.
</p>
<p>
<img src="https://i.imgur.com/7KIrWzj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Jetzt zur letzten, für PHP relevanten, Datei innerhalb des Installations-Ordners. Die Rede ist von "php-7.3.8-nts-Win32-VC15-x86". Darin befindet sich die ausführbaren Dateien und Kernkomponenten von PHP in Version 7.3.8, die für die Ausführung von PHP-Skripten benötigt werden. Darüber hinaus handelt es sich dabei um eine spezielle Version von PHP, da sie ohne Thread-Safety (NTS) konfiguriert ist, was für die Nutzung in Serverumgebungen wie IIS optimiert ist, da IIS diesen Teil selbst verantwortet. Wir extrahieren den Ordner in unseren zuvor erstellten "PHP" Ordner (s. Beginn Installation PHP).
</p>
<p>
<img src="https://i.imgur.com/JmCwQke.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/6VWz9GH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<hr>

<p>
Fast geschafft! Für die letzten zwei Schritte müssen wir in IIS gehen und unsere PHP Version, die wir zuvor in den Ordner "PHP" extrahiert haben, registrieren. Sonst kann das IIS keinen Gebrauch davon machen, wenn wir später osTicket installieren und einrichten wollen. Hierzu öffnen Sie IIS und müssten direkt ein Icon mit der Schrift "PHP Manager" darunter finden. Das klicken Sie an mit einem Doppelklick, damit sich das Fenster des PHP Managers öffnet. Jetzt klicken sie auf "Register new PHP version" und geben als Pfad den Weg zu unserem PHP Ordner ("This PC">"Windows(C:)">"PHP">) und wählen die Datei "php-cgi". Die „php-cgi“-Datei ermöglicht es unserem IIS-Server, PHP-Skripte mithilfe von CGI auszuführen. Sie sorgt dafür, dass PHP korrekt verarbeitet wird und die Webanwendung wie osTicket funktioniert. Stellen Sie es sich vor wie die Straße auf der die PHP-Skripte zur Schnittstelle des CGI fahren.
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
Bevor wir uns um die Datenbank kümmern, starten wir den Webserver neu. Gehen Sie auf der linken Seite zurück zur Startseite des Server-Managers und klicken sie rechts unter "Manage Server" auf "Restart".
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
Nun öffnen wir den osTicket-Installation-Files Ordner und installieren die Datei "mysql-5.5.62-win32". Diese enthält die Installationsdateien für MySQL Version 5.5.62, eine relationale Open-Source-Datenbank, die häufig für die Speicherung und Verwaltung von Daten in Webanwendungen verwendet wird. In unserem Fall stellt es für osTicket eine Datenbank bereit, in der Benutzerdaten, Tickets und andere Anwendungsdaten gespeichert werden. Wichtig: beim Fenster für das Setup wählen wir als "Type" "Typical" aus. Den Rest gleich lassen und am Ende den Wizard starten.
</p>
<p>
<img src="https://i.imgur.com/TMesfcO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/VtwS6tV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/xPLUnlR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Wähle "standard Configuration" und lass den Rest unberührt. Einfach "Next" drücken bis man "Execute" erreicht, es drücken und schließlich auf "Finish". 
<p/>
<p>
<img src="https://i.imgur.com/6eHyza0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Nächster Schritt, die Installation von "HeidiSQL_12.3.0.6589_Setup" im osTicket-Installation-Files Ordner. Diese enthält die Installationsdateien für HeidiSQL, ein grafisches Verwaltungswerkzeug für relationale Datenbanken wie MySQL. Mit HeidiSQL können wir Datenbanken bequem erstellen und verwalten, ohne dass dafür eine Kommandozeile (PowerShell) nötig ist. Drücke "Next" durch bis hin zu "Finish". Achte bevor du darauf klickst, dass das Häkchen bei "Launch HeidiSQL" gesetzt ist. Wenn sich HeidiSQL geöffnet hat, drücke auf "Skip".
<p/>
<p>
<img src="https://i.imgur.com/3VYxQzk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/1WXSdK0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Der letzte Schritt für diesen Abschnitt der Anleitung behandelt das Erstellen einer neuen Datenbank, welche wir später mit unserem osTicket verbinden. Dafür Rechtsklicken wir auf die linke Spalte und drücken auf "New session". Ändern brauchen wir nichts, lediglich ein User und ein Passwort müssen wir uns überlegen. Beides brauchen wir später zum Verbinden mit osTicket, also merken oder aufschreiben. Drücken Sie danach auf "Open".
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
Alles was wir benötigen für eine reibungslose, funktionsfähige Version von osTicket haben wir zum jetzigen Zeitpunkt installiert und eingerichtet. Endlich können wir uns um die tatsächliche Installation von osTicket kümmern. Anfangen tun wir damit, den Ordner "osTicket-v1.15.8" innerhalb des Ordners osTicket-Installation-Files zu extrahieren. Innerhalb dieses Ordners befinden sich die Dateien und Skripte der osTicket-Webanwendung in der Version 1.15.8, die für die Installation benötigt werden. Alle wichtigen Komponenten wie PHP-Skripte, Konfigurationsdateien und Ressourcen, die zur Bereitstellung und Nutzung des Ticketsystems erforderlich sind finden sich hier.
</p>
<p>
<img src="https://i.imgur.com/PbYS4NU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Danach kopieren wir den Ordner "upload" in dem gerade extrahiertem Ordner "osTicket-v1.15.8" und fügen ihn ein in den Ordner "wwwroot" mit dem Pfad "This PC">"Windows(C:)">"inetpub">"wwwroot". Der Ordner „inetpub“ ist das Standardverzeichnis, das der IIS-Webserver verwendet, um alle Webdateien zu speichern und zu verwalten. Innerhalb von „inetpub“ dient der Ordner „wwwroot“ als das Hauptverzeichnis für öffentlich zugängliche Webseiten und Webanwendungen. Dateien (/Ordner), die in „wwwroot“ abgelegt werden, können über den Webserver bereitgestellt und von Benutzern im Browser aufgerufen werden.
</p>
<p>
<img src="https://i.imgur.com/OK8Jno0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Nun benennen wir den "upload" Ordner in dem "wwwroot" Ordner in "osTicket". Das dient der klaren Identifizierung und sinnvollen Namensgebung. Wie vorhin angedeutet befindet sich dieser gerade umbenannter Ordner "osTicket" in dem Hauptverzeichnis für öffentlich zugängliche Webseiten (Google, Wikipedia, YouTube, etc.) innerhalb unseres Webservers (IIS). Heißt unser "osTicket"-Ordner repräsentiert die Webseite, die durch die beinhaltenden Dateien erstellt wird, sprich unsere osTicket-Webseite.
</p>
<p>
<img src="https://i.imgur.com/8B2jeQG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Endlich können wir osTicket im Browser aufrufen und beginnen, nach unseren Wünschen eine Helpdesk-Struktur aufzubauen. Öffnen Sie IIS und starten Sie den Server neu (rechts auf "Restart" klicken). Dann klappen Sie links den Server auf bis Sie einen Ordner namens "osTicket" sehen. Klicken Sie in an, sodass der Ordner blau markiert ist und drücken Sie auf der rechten Seite auf "Browse *:80(http)".
</p>
<p>
<img src="https://i.imgur.com/SUqaWKw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Falls sich bei Ihnen nun ein Fenster mit dem Titel "osTicket Installer" öffnet, haben Sie bis jetzt alles richtig gemacht. Jetzt müssen wir nur noch die Schritte erledigen, die uns die Seite vorgibt und fertig sind wir. Der erste dieser Schritte besteht darin, empfohlene Erweiterungen für eine besser Erfahrung im Umgang mit der Anwendung zu aktivieren. Hierzu öffnen wir erneut den PHP Manager in IIS (s.Installation PHP), öffnen den "PHP Extension" Ordner und aktivieren die Erweiterungen "PHP IMAP Extension" und "Intl Extension". Beide besitzen auf der osTicket Installer Website ein rotes Kreuz links neben sich. Hierzu Rechtklicken Sie in IIS in den PHP Extensions auf die jeweiligen Erweiterungen und drücken auf "Enable". Diese Erweiterungen lassen sich auch im Nachhinein konfigurieren.
</p>
<p>
<img src="https://i.imgur.com/16RIAQ1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/nj7PNf5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Laden Sie die Webseite neu und beobachten Sie, dass aus den roten Kreuzen grüne Häkchen geworden sind. Falls das eintrifft drücken Sie auf "Continue".
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
Darüber hinaus müssen wir die Berechtigungen für diese Datei ändern. Hierzu Rechtsklicken Sie auf die Datei, drücken auf "Properties", oben auf "Security", unten auf "Advanced", links unten auf "Disable inheritance", dann auf "Remove all inherited permissions from this object". Jetzt fügen wir eine eigene Berechtigung hinzu und geben dieser volle Kontrolle über die Datei. Hierzu klicken Sie unten links auf "Add", oben auf "Select a principal" und dann geben Sie "Everyone" in das Feld (s. Bild) ein und drücken "OK". Vergessen Sie nicht die Box "Full Control" (s. Bild) mit einem Häkchen zu versetzen. Drücken Sie erneut auf "OK", dann "Apply" und wieder (zweimal) auf "OK". Gehen Sie zurück auf die Webseite und drücken Sie auf "Continue". Die Erklärung für das alles kommt im nächsten Kapitel.
</p>
<p>
<img src="https://i.imgur.com/lnV2va0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/vCAIJ7i.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Jetzt müssen Sie nur noch alles auf der Seite ausfüllen und anschließend auf "Install Now" drücken. Bei den "Database Settings" müssen sie sich an den Anleitungsteil "Installation MySQL" zurückerinnern. Dort haben wir innerhalb einer Session eine Datenbank namens "osTicket" angelegt und für diese Session einen User und Password eingegeben. Diese drei Daten geben Sie hierfür ein.
</p>
<p>
Auf dieser Seite sollten sie anschließend landen, wenn alles gelaufen ist wie es soll:
</p>
<p>
<img src="https://i.imgur.com/iUqlX6B.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Geschafft! osTicket ist erfolgreich installiert. Nun können Sie über die unten aufgelisteten URLs jeweils verschiedene Schnittstellen Ihres Helpdesks erreichen und herumexperimentieren.
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
Im Verlaufe der Anleitung haben wir im Kapitel "Installation osTicket" die Berechtigungen für die Datei "ost-config.php" geändert, sodass jeder vollen Zugriff über diese hat und haben den Namen der Datei geändert. Da stellt sich die Frage, warum? Was spiegelt diese Datei wider? Und warum ändern wir den Namen nicht wieder zu ost-sampleconfig (ja, der Name bleibt)? Die Datei "ost-sampleconfig" ist die Konfigurationsdatei, die osTicket während der Installation verwendet, um die individuellen Einstellungen wie Datenbankverbindungen zu speichern. Das Umbenennen ist notwendig, da osTicket als Konfigurationsdatei nur nach einer Datei mit dem Namen "ost-config.php" Ausschau hält und akzeptiert. Dem zufolge bleibt der Name bei ost-config.php und heißt zu Beginn ost-sampleconfig, da es sich zu Beginn um eine nicht konfigurierte, standardisierte Datei handelt, die noch zu konfigurieren gilt. Ebenfalls der Grund für das Ändern der Sicherheitsregeln geht aus diesem Hintergrund hervor. Damit osTicket Zugriff hat auf die Einstellungen und Konfigurationen hat, müssen wir die Sicherheitsregeln ändern. Im Gegensatz zum Namen machen wir diesen Schritt aber rückgängig, da wir momentan jedem vollen Zugriff gewähren, sodass es auch jedem möglich ist an der Datei herumzubasteln. Finden Sie die Datei innerhalb des "include" Ordners (s. Bild für Pfad), Rechtklicken Sie auf die Datei und drücken Sie erneut auf "Properties" und oben auf "Security". Wählen Sie die Gruppe "Everyone" aus und drücken Sie auf "Edit". Nehmen Sie überall die Häkchen weg bis auf das Häkchen für das Feld "Read". Anschließend drücken Sie auf "Apply", "OK" und nochmal "OK". Nun kann die Datei von jedem eingesehen, aber nicht verändert werden.
</p>
<p>
<img src="https://i.imgur.com/9dWewTW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/LHltHxN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Zu guter Letzt löschen wir den Ordner "setup" innerhalb unseres "wwwroot">"osTicket" Ordners. Nach der Installation von osTicket wird dieser nicht mehr benötigt und stellt ein potenzielles Sicherheitsrisiko dar, da er den Zugriff auf Installationsskripte ermöglicht. Durch das Entfernen des Ordners wird verhindert, dass unbefugte Personen Änderungen an der Installation vornehmen oder das System erneut einrichten können, konträr zu unseren Vorstellungen. Et voilà! Sie haben es geschafft!
</p>
<p>
<img src="https://i.imgur.com/lghZBhK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />






<p>
Nach der erfolgreichen Installation von osTicket gibt es zahlreiche Möglichkeiten zur weiteren Konfiguration und Einrichtung. Dazu gehören das Anlegen von Benutzern und Rollen, das Einrichten von E-Mail-Integrationen für die automatische Ticket-Erstellung und die Anpassung von Ticketfeldern und Workflows. Außerdem können benutzerdefinierte SLA-Pläne, Helpdesk-Formulare und Automatisierungsregeln erstellt werden, um den Support-Prozess zu optimieren. All das sind weiter mögliche Konfigurationen und Einrichtungsmöglichkeiten für Ihr Ticketsystem!! Viel Spaß beim weiteren Einrichten!
</p>

