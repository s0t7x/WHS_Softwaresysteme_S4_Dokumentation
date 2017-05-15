# Internet- und Datensicherheit

Eine begleitende Dokumentation der Vorlesung "Internet- und Datensicherheit" 
Informatik.Softwaresysteme, 4. Fachsemester 

## Inhalt

1. [Theorie](#Theorie)
	1. [Grundlagen](#Grundlagen)
	2. [Diffie-Hellman](#DiffieHellman)
	3. [Euklidischer Algorithmus](#EuklidischerAlgorithmus)
2. [Anwendungsentwicklung](#Anwendungsentwicklung)

# Theorie

## Grundlagen

### Datensicherheit muss immer aktuell sein

**Ein Arbeitsplatz, in dem das Thema "Datensicherheit" todgeschwiegen wird, sollte kein Arbeitsplatz sein!**
Prinzipiell ist das Thema unvermeidlich! Datensicherheit beschäftigt und **wird** immer beschäftigen.

Es brauch nur eine kleine Lücke und es ist sofort möglich, einen riesen schaden aus zu lösen.

Warum sollten also Protokolle wie z.B. SMB (Datentransfer bei Windows) standardmäßig aktiviert sein?
Im Endeffekt sollte doch nur das aktiviert sein, was wirklich unausweichlich genutzt werden soll / muss.

In einer Firma muss also immer über das Thema "Datensicherheit" debatiert werden. Auf Schwachstellen sollte immer geachtet werden.
Nimmt ein Arbeitskollege ständig USB-Sticks mit rein oder raus? Wird Zeit ihm zu sagen, dass er das unterlassen soll!

Hygiene ist das A und O! Wir Menschen leben nicht wegen der Medizin fast 100 Jahre. Nein, wir leben so lange, weil wir wichtige fortschritte in der Hygiene gemacht haben. Warum sollte es an Systemen anders sein?

Unter Software-Hygiene fällt also:
	- Nur nutzen / aktivieren was gebraucht wird
		- In diesem Sinne, sollten Anwendungen nur dann ausführbar sein, wenn sie auch ausgeführt werden. Alles andere sollte gesperrt sein!
	- Virenscanner tragen nicht zur Hygiene bei! (Nicht effektiv)
	- Fehler sollten **nie** geheim bleiben! Veröffentlichungen von Fehlern tragen zur Sicherheit bei!
	
## Diffie-Hellmann Public-Key-Encryption


## Euklidischer Algorithmus (Erweiterter Euklid)
Wie oft ist 95 durch 30 in einer Ganzzahl teilbar?
> 95/30=3
Der Rest ist 5!
95 und 5 sollen den gleichen Teiler haben: hier also 30.
Nun wird die größere der beiden Zahlen durch die kleinere geteilt.
> 30/5=6
Hier ist der Rest 0. Der größte gemeinsame Teiler ist also 5!

> ggt(a,b)=ggt(b,a)
sei a > b:
>>ggt(a,b)=ggt(a-b,b)

Angenommen *a mod(2) = 0* und *b mod(2) = 1*:
>> ggt(a,b)=ggt(a/2,b)

Angenommen beide Zahlen sind nun gerade:
>> ggt(a,b)=2ggt(a/2,b/2)

>> ggt(a,a)=a

Werden diese Regeln rekursiv programmiert, liefert das Programm immer den größten gemeinsamen Teiler.

### Beispiel
