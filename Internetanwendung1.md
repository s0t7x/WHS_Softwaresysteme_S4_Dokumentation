# Internetanwendungen 1

Eine begleitende Dokumentation der Vorlesung "Internetanwendungen 1" 
Informatik.Softwaresysteme, 4. Fachsemester 

## Hinweise

Thema der Vorträge: "Sicherheit"

Praktikumsanmeldung im QIS-Portal

Moodle-Schlüssel: INA1

## Grundlagen

### Was sind Internetanwendungen?
 
>***Internetanwendungen*** sind eine Untergruppe der ***Netzwerkanwendungen*** und gehören zu den ***verteilten Systemen***.Es sind konkrete Anwendungen!
Zu den ***Internetanwendungen*** gehört die Untergruppe der ***Web-Anwendungen***.

- Anwendungen, welche das Internet für Ihre Kernfunktionen verwenden.
- Protokolle der TCP/IP-Familie
- Konkrete Anwendungen

#### Beispiele
	- E-mail, WWW
	- SNMP
	- Telnet
	- SSH
	- FTP


### 8 Trugschlüsse der verteilten Systeme
*L Peter Deutsch* und *James Gosling* definierten 8 Annahmen, welche bei der Entwicklung von verteilten Systemen falsch unvorteilhaft sein könnten.
Diese sind:
1. **The network is reliable**
2. **Latency is zero**
3. **Bandwidth is infinite**
4. **The network is secure**
5. **Topology does not change**
6. **There is one administrator**
7. **Transport cost is zero**
8. **The network is homogeneous** 


## Architektur

### Middleware
Ziele von Middleware sind die **Modularisierung, Schematisierung und Abstraktion** von Anwendungskomponenten.

Nutzt eine Software keine Middleware, so implementiert sie **Socketprogrammierung**.
Dies kann sinnvoll sein um in **Kleinstprogrammen** für eine **geringe Datenrate, vollständige Kontrolle über die Kommunikation und höhere Effiziens** zu sorgen.
**Socketprogrammierung** ist jedoch **fehleranfällig und verfügt über mangelhafte Wartbarkeit**.

Eine **Middleware** stellt wenig **spezialisierte Dienste** zur Verfügung, die meist die Verteilung von Anwendungen unterstützen und arbeitet **plattformübergreifend** auf **Standardschnittstellen**. *(Oft TCP/IP-Stack)*.
Darüber hinaus stellt sie Schnittstellen wie z.B. ein **Framework** oder eine **API** zur Verfügung.

Von einer Middleware werden oft **typische Kerndienste** bereitgestellt. Die **Art und Anzahl** hängt jeodch stark von der Aufgabe der Middleware ab.
Hauptsächlich dienen jedoch **Kommunikationsfunktionen** zur **Abstraktion der Kommunikation** und zur **Verbergung der Low-Level-Kommunikation** innerhalb der Anwendung.

**Middleware** ermöglicht das **Auffinden verteilter Ressourcen** und **erlaubt deren gemeinsame Nutzung**.
**Speicherfunktion in nicht-flüchtigem Speicher** ermöglichen **Persistenz** für z.B. *Objektserialisierung, Schnittstellen zu Dateisystemen und Datenbanken, oder OR-Mapping (Object-Relational Mapping)*.

**Verteilte Transaktionen** werden **automar**, auch über mehrere Knoten hinweg, ausgeführt.

**Kommunikations-** und **Anwendungsorientierte Middleware** stellen ihre Abstraktionen transparent zur verfügung.

- **Zugriffstransparent:**
	Eine Anwendung kann auf lokale und entfernte Ressourcen mit identischen Operatoren zugreifen. Die Middleware vermittelt den Aufruf.
- **Positionstransparenz:**
	Es kann auf Ressourcen zugegriffen werden, ohne ihren Ort zu kennen.
- **Replikationstransparenz:**
    Es können mehrere Instanzen einer Ressource verwendet werden, ohne, dass die Anwendung dies wissen muss. (Clustering, Leistung, Verfügbarkeit)
- **Fehlertransparenz:**
	Der Anwendung bleiben Fehler in anderen Komponenten (Software, Hardware) verborgen, sodass sie weiterarbeiten kann.
- **Mobilitätstransparenz:**
	Ressourcen können innerhalb des Systems verschoben werden, ohne dass die Anwendung dadurch beeinträchtigt wird.
- **Leistungstransparenz:**
	Das System kann neu konfiguriert werden, um die Leistung zu verbessern.
- **Skalierungstransparenz:**
	Das System kann vergrößert werden, ohne dass Struktur oder Algorithmen geändert werden müssen.

### Client-Server-Modell
Das **Client-Server-Modell** verfügt über eine eundeutige, statische Rollenverteilung.
Meist kommuniziert ein **kurzlebiger Clientprozess** mit einem **lannglebigem Server**.
Hierbei **bedient der Server** meist **mehrere Clientprozesse**.

Ein **typisches Besipiel** ist die **Browser-Webserver** Verbindung.

Eine von mehreren Varianten des Client-Server-Konzeptes ist ein **Kooperierender Server**.
Dabei wird ein Server benötigt, **welcher zur Bearbeitung von Anfrage-Funktionen eines weiteren Servers, selber zum Client wird und den anderen Server abfragt.**
Dieses Konzept lässt sich beliebig kaskadieren.

Kooperierende Server sind z.B. ein **Proxy** oder ein **Broker**.

Der **Broker** ist ein Vermittler. Er **leitet Anfragen** an den **richtigen Server weiter** und zwar **ohne, dass der Client den Server kennen muss**.


## Model View Controller
![](http://puu.sh/wMI5h/8b4fb27361.png)

![](http://puu.sh/wMI6r/fded56dadd.png)
