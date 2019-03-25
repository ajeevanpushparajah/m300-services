##### Ajeevan Pushparajah | ST16B |M300
------------------------------------------------------------

# Plattformübergreifende Dienste in ein Netzwerk integrieren


![TitelBild](https://cdn.pixabay.com/photo/2013/07/13/13/41/bash-161382_1280.png)


## Inhaltsverzeichnis
* 00 - [Einleitung](#Einleitung)  
* 01 - [SSH](#SSH)
* 02 - [Vagrant](#Vagrant)
* 03 - [Firewall](#Firewall)
* 04 - [Reverse Proxy](#ReverseProxy)
* 05 - [Sicherheitsmassnahmen](#Sicherheitsmassnahmen)


# Einleitung  

Dies ist ein Wissensdatenbank in welchem, an neues gelerntes wissen Dokumentiert und fortlaufend weitergeführt werden. 
Sämtliche Versuche, werden mit den abgesetzten Commands so dokumentiert, sodass man die wieder nachstellen kann. 


# SSH
## Key auf dem MAC OSX erstellen

#### 1. Terminal öffnen 
#### 2. Folgenden Befehl mit der Account E-Mail von GitHub einfügen:
$ ssh-keygen -t rsa -b 4096 -C "ajeevan.pushparajah@swissitpartner.ch"
#### 3. Neuer SSH-Key wird erstellt:
Generating public/private/ rsa key pair.
#### 4. Bei der Abfrage, unter welchem Namen der Schlüssel gespeichert werden soll, die Enter-Taster drücken:
Enter a file in which to save the key (~/.ssh/id_rsa): [Press enter]
#### 5. Nun kann ein Passwort für den Key festgelegt werden. Ich empfehle dieses zu setzen und anschliessend dem SSH-Agent zu hinterlegen, sodass keine erneute Eingabe (z.B. beim Pushen) notwendig ist:
  Enter passphrase (empty for no passphrase): [Passwort]
  Enter same passphrase again: [Passwort wiederholen]

# Vagrant

## Software  Installation

https://www.vagrantup.com

## Virtuelle Maschine erstellen

#### 1. Terminal (Bash) öffnen
#### 2. In gewünschtem Verzeichnis einen neuen Ordner für die VM anlegen:
$ cd desktop/tbz/modul/m300/
$ mkdir meinevagrantvm
$ cd meinevagrantvm 
#### 3. Vagrantfile erzeugen, VM erstellen und entsprechend starten:
 $ vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name ubuntu/xenial64  #Vagrant-Box vom Netzwerkshare hinzufügen
  $ vagrant init ubuntu/xenial64        #Vagrantfile erzeugen
  $ vagrant up --provider virtualbox    #Virtuelle Maschine erstellen starten
#### 4. Die VM ist nun in Betrieb (erscheint auch in der Übersicht innerhalb von VirtualBox) und kann via SSH-Zugriff bedient werden:
 $ cd Pfad\zu\meiner\Vagrant-VM      #Zum Verzeichnis der VM wechseln
  $ vagrant ssh                       #SSH-Verbindung zur VM aufbauen

1. VirtualBox starten
2. Links oben, innerhalb der Anwendung, auf `Neu` klicken
3. Im neuen Fenster folgende Informationen eintragen:
   *  Name:           `M300_Ubuntu_XX.04_Desktop`
   *  Typ:            `Linux`
   *  Version:        `Ubuntu (64-bit)`
   *  Speichergrösse: `2048 MB`
   *  Platte:         `[X] Festplatte erzeugen`
4. Auf `Erzeugen` klicken
5. Weiteres Fenster öffnet sich, folgende Informationen eintragen:
   *  Dateipfad:                       standard
   *  Dateigrösse:                     `10.00 GB`
   *  Dateityp der Festplatte:         `VMDK (Virtual Maschine Disk)`
   *  Storage on physical hard disk:   `dynamisch alloziert`
6. Ebenfalls auf `Erzeugen` klicken, dann im Hauptmenü die VM anwählen (blau markiert) und den Punkt `Ändern` aufrufen
7. Im Abschnitt `Massenspeicher` den SATA-Controller anwählen und auf das CD+Symbol klicken
8. Unter `Medium auswählen` das zuvor heruntergeladene Systemabbild (ISO-Datei) anwählen
9. Alle Änderungen speichern und die VM starten
10. Den Installationsanweisungen der OS-Installation folgen und anschliessend zu Abschnitt "VM einrichten" gehen

#### 4.1. Anschliessend können ganz normale Bash-Befehle abgesetzt werden:

Befehl          | Zweck                       |  
--------------- | ----------------            |  
$ ls -l /bin    | #Bin-Verzeichnis anzeigen   |
$ df -h         | #Freier Festplattenspeicher |
$ free -m       | #Freier Arbeitsspeicher     |
                
#### 5. VM über VirtualBox-GUI ausschalten      

## Vagrant Befehle 

# Firewall

## Firewall (UFW) installieren 
 sudo apt-get install ufw

## Wichtige Befehle 

Befehl            | Zweck                                            |  
---------------   | ----------------                                 |  
Sudo ufw enable   | # Startet den Firewall                           |
Sudo ufw disable  | # Beendet den Firewall                           |
Sudo ufw status   | # Status Firewall & die Regeln werden angezeigt  |

![Firewall Status](img/ufwstatus.png)

# ReverseProxy


## Installation

#### Module installieren
sudo apt-get install libapache2-mod-proxy-html
sudo apt-get install libxml2-dev

#### Module in Apache aktivieren 
sudo a2enmod proxy
sudo a2enmod proxy_html
sudo a2enmod proxy_http 

#### Datei im Ordner Apache2 ergänzen 
/etc/apache2/apache2.conf -> ServerName localhost 
sudo service apache2 restart

# Sicherheitsmassnahmen


## Benutzer

Benutzer          | Funktion                                                                                                  |  
---------------   | ----------------------------------------------------------------------------------------------------------|  
root              | # Der Systemverwalter unter Linux                                                                         |
nobody            | # Wird von Prozessen als Benutzererkennung verwendet, wenn nur ein Minimum an Rechten vergeben werden soll|
cupsys            | # Benutzer des Druckdienstes CUPS                                                                         |
www-data          | # Benutzer des Webservers Apache                                                                          |
## Authentisierung
Die Authentisierung stellt den Nachweis einer Person dar, dass sie tatsächlich diejenige Person ist, die sie vorgibt zu sein. Eine Person legt also Nachweise vor, die ihre Identität bestätigen sollen. Je nach der eingesetzten Authentisierungsmethode kann die Person ihre Identität unter anderem auf folgenden Wegen behaupten:

* sie hat geheime Informationen, die nur ihr bekannt sind (z.B. Passwort)
* sie besitzt einen Identifizierungsgegenstand (z.B. Personalausweis)
* sie ist selbst das Identifizierungsobjekt (z.B. biometrische Merkmale wie Fingerabdruck).

## Authorisierung

Die Autorisierung ist die Einräumung von speziellen Rechten. War die Identifizierung einer Person erfolgreich, heißt es noch nicht automatisch, dass diese Person bereitgesellte Dienste und Leistungen nutzen darf. Darüber entscheidet die Autorisierung.