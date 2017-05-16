# Kryptographie

Eine begleitende Dokumentation der Vorlesung "Kryptographie" 
Informatik.Softwaresysteme, 4. Fachsemester 

## Inhalt

1. [Theorie](#Theorie)
	1. [Elliptische-Kurven-Kryptographie](#ElliptischeKurvenKryptographie)
2. [Anwendungsentwicklung](#Anwendungsentwicklung)


# Theorie

## Elliptische Kurven Kryptographie
lorem ipsum - TO BE FILLED -


### Hasse-Intervall

```
q+1-2*q^1/2 <= #E <= q+1+2q^1/2
```

x^#E = id
Eine "id" sitzt immer in der Menge und gilt für alle beliebigen g's. Sprich egal was auch immer für ein g gewählt wird, als Gemeinsamkeit erzeugen alle an der gleichen Stelle eine "id".

Angenommen es wird **irgendein** Punkt genommen, wird dieser irgendwann intervallspezifisch gleich zu "id".
Diese könnte allerdings irgendwo zwischen 18 und 43 liegen.

Angenommen #E = 35:

g baut also eine Gruppe mit der Größe 35 oder größer.

| 0 | 1 | 2 | 3 | 4 | 5 | ... | 10 | ... | 15 | ... | 20 | ... | 25 | ... | 30 | ... | 40 |
| - | - | - | - | - | - | --- | -- | --- | -- | --- | -- | --- | -- | --- | -- | --- | -- |
| id | g | g^2 | g^3 | g^4 | id | ... | id | ... | id | ... | id | ... | id | ... | id | ... | id |

**Genau** an der Stell #E=35 liegt für **ALLE** die id.
Die eigentliche Gruppengröße bleibt vorerst verborgen.

Denken wir uns ein Element g aus. Dann wird die Menge M gebildet:
```
M = {1,g,...,g^m}
```
Dann wird berechnet:
> u = [q+1-2*q^1/2] <- ABS

> k = u + m

> g^k = 
```
		     u+m=k   g~
-----------------|-----|---{-/\-}----|
		 u    g^k            o

g^k=(x(k), y(k))

g^k * g^(2m+1) = g~

Das Intervall hat die Länge 2m+1
Das gewählte m ist in diesem Falle egal.
Die schnellste Laufzeit wäre m = (q^1/2)^1/2
```
g~ prüft genau den Intervall hinter m. Dies kann hoch multipliziert werden, um das zu testende Intervall zu verschieben.

Wenn g^k in der Menge drin sitzt, befindet sich in der Nähe auf jeden Fall eine id. Ist g^k zufälligerweise g(2) dann liegt die id 2 vor g(2). Wird g^k berechnet wird zu aller erst geprüft ob das x(k) sich in der Menge befindet. Dann prüft man ob das y(k) sich in der Menge befindet.
Lässt sich das x (oder sein inverses) nicht finden, ist der Punkt nicht in der Menge. Findet sich allerdings ein y, verweist das y auf die Position der id.

1. g(1) ausdenken (!=id)
2. M erzeugen
	- M hat m+1 Elemente
	- Falls g^j=id für 2 <= j <= m -> dann ist #g(1) bekannt. Es ist also die Gruppengröße einer Untergruppe bekannt.
3. Schritte 1. und 2. sollten öfter wiederholt werden (1 / 2 / 3 mal)
4. Durch das KGV (kleinstes gemeinsames Vielfaches) mehrerer Untergruppen lässt sich die Gruppengröße #E berechnen

Angenommen: g^a = id
Wissen wollen wir die Grupengröße von g(1).
a ist auf jeden Fall durch die Gruppengröße teilbar.
Also:
> g^a = id = g^p(1) * g^p(2) * g^p(...) * ...

Es wird g^(a/p(1)) == id geprüft!
Das neue a wird dabei zu a/p(...) gesetzt.

a wird dann so lange durch die zerlegten Primfaktoren geteilt, bis es nicht mehr möglich ist.
Dann haben wir die kleinstmögliche Gruppengröße.
Dann gilt:
> g(1) -> g(1)^(a(1)) = id

> g(2) -> g(2)^(a(2)) = id

```
        #E
---------------------
KGV(a(1)*a(2)*a(...))
```

Folgend bildet sich der "Baby-Step-Giant-Step" Algorithmus:

Eingabe: Endliche zyklische Gruppe {\displaystyle G} G, Erzeuger {\displaystyle g} g, Gruppenelement {\displaystyle a} a

Ausgabe: {\displaystyle x:=\log _{g}a} x:=\log_g a mit {\displaystyle g^{x}=a} g^x=a

1. Berechne n:=|G|, m:=[sqrt{n}]
2. Für alle j in {0, ... ,m-1}: Berechne g^{j} und speichere (j,g^j) in einer Tabelle.
3. Für alle i in {0, ... ,m-1}: Berechne a(g^{-m})^i und suche danach in der zweiten Spalte der Tabelle. Wenn gefunden, gib im+j aus.
4. Wegen a(g^{-m})^i = a(g^{-m})^{i-1}g^{-m} lässt sich das Gruppenelement im letzten Schritt leicht aus dem der vorhergehenden Iteration berechnen
