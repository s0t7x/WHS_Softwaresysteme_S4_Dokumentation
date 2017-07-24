# Internet- und Datensicherheit

Eine begleitende Dokumentation der Vorlesung "Internet- und Datensicherheit" 
Informatik.Softwaresysteme, 4. Fachsemester 

## Datensicherheit muss immer aktuell sein

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

## Modulo von Zahlen

Als Beispiel: `` % 5 `` bzw. ``(mod 5) ``
Wird dies auf die Potenzen von 2 angewandt, entsteht eine Zahlfolge:
|2^1|2^2|2^3|2^4|
|-|-|-|-|
|2|4|3|1|

Dabei fällt auf, dass bei beliebigen a, b aus diesen Reihen jedes Produkt ``a · b ̸= 0`` ist.
Dies gilt nur für Modulo von Primzahlen!

Bei dem Modulo 6 der Potenzen von 2 ergibt sich
beispielsweise ``2 · 3 = 6``. Jedoch ist ``6 mod 6 = 0``.

### Modulo von Primzahlen

Als Beispiel: ``% 11`` -> ``[2,4,8,5,10,9,7,3,6,1]``

Es ergeben sich 10 verschiedene Elemente und keine Null. Die Elemente sind je einmal in quasi zufälliger Reihenfolge verteilt und enden mit einer 1.
Rechenhinweis:
Anstatt mühselig einzeln ``2^5`` zu rechnen und vom Ergebnis das Modulo zu bilden, kann man auch den jeweils letzten Wert nehmen, mit zwei multiplizieren und danach Modulo rechnen.
Allgemein gilt: ``a^n mod π ̸= 0.``
Dann tauchen alle Zahlen zwischen 1 und (Primzahl−1) auf, wobei die letzte Zahl 1 ist. Anders ausgedrückt:
``a^(π−1) mod π = 1``

## Unterschied: Körper - Gruppe
### Addition
Für unsere Modulo-Operationen gilt:
- Abgeschlossenheit: ``a, b ∈ M`` → ``a + b ∈ M``
- Neutrales Element: ``e + a = a`` und ``a + e = a``
- Inverses Element: ``a + (−a) = e``

Mit diesen Eigenschaften ist die Addition von Modulo eine Gruppe. Kommt Kommutativität, ``a+b = b+a``, hinzu, so handelt es sich um eine Abelsche Gruppe.
Da wir uns in einer abzählbar endlichen Menge befinden, ist Kommutativität automatisch gewährleistet.

### Multiplikation
Wie schließen zunächst alle Nullen aus: ``M^+``
Für unsere Modulo-Operationen gilt:
- Abgeschlossenheit: ``a, b ∈ M`` → ``a · b ∈ M``
- Neutrales Element: ``1 · a = a`` und ``a · 1 = a``
- Inverses Element: ``a · (a^(-1)) = 1``, bzw. ``a/a = 1``

Abelsch wird die Gruppe, wenn gilt: a · b = b · a.

### Körper
Unsere Modulo-Operation ist ein Körper, da sie sowohl „+“ als auch „·“ kennt.
Zum Verschlüsseln ist es besser, weniger Regeln zu haben, also beispielsweise eine Gruppe ist besser geeignet als ein Körper, da letzterer mehr Regeln hat, die beim Entschlüsseln helfen.
Alle Nichtprimzahlen können bei der Multiplikation keine Gruppe bilden, da die Null ausgeschlossen wurde und bei Nichtprimzahlen die Multiplikation zum Ergebnis 0 führen kann. *(Siehe oben)*.

## Diffie-Hellmann Public-Key-Encryption
![](https://files.catbox.moe/mdon7y.png)
![](https://files.catbox.moe/x09fah.png)

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
>ggt(a,b)=ggt(a-b,b)

Angenommen *a mod(2) = 0* und *b mod(2) = 1*:
> ggt(a,b)=ggt(a/2,b)

Angenommen beide Zahlen sind nun gerade:
> ggt(a,b)=2ggt(a/2,b/2)

> ggt(a,a)=a

Werden diese Regeln rekursiv programmiert, liefert das Programm immer den größten gemeinsamen Teiler.

### Beispiel
> a=164830, b=27388

Beide werden *n-mal* durch 2 geteilt. An einem bestimmten Zeitpunkt sind entweder beide oder zumindest eine Zahl ungerade! Die Anzahl der Schritte *n* wird vermerkt.
Sind beide ungerade, wird die kleinere Zahl von der größeren abgezogen.

> a=82415, b=6847, n=2

> c=a-b=75568

Nun wird der neue Wert c erneut *n-mal* durch 2 geteilt, bis der Wert ungerade ist. Dann wird wieder die kleinere von der größeren Zahl abgezogen.

Also:
- Am Anfang werden beide Zahlen durch 2 geteilt, bis mindestens eine ungerade ist. Falls eine gerade bleibt, wird sie weiterhin durch 2 geteilt.
- Zieht man eine ungerade Zahl von einer ungeraden Zahl ab, wird das Ergebnis **definitiv** gerade sein.
- Die Summe kann dann wieder durch 2 geteilt werden, bis sie ungerade ist.
- Diese Schritte wiederholen sich bis zur Abbruchbedingung: **a == b**
	
### Anwendung in der Praxis
Angenommen *a* und *b* sind teilerfremd, also der GGT beider Zahlen ist 1!

> a * b mod n = 1

Wenn wir *a* kennen, wollen wir *b* berechnen.*a* wird später **öffentlicher Schlüssel** und *b* wird **privater Schlüssel** genannt.

> 1 = a*b+c*n = a*b mod n

bspw. 7 = öffentlicher Schlüssel; x = privater Schlüssel
> 1 = 7*x mod 60

> x = ?

> a(0)=60; b(0)=7; r=|a/b|=8; [ s=; t=; u=; v=; ]

> a = 60 - 8*7

> a=4; b=3=7-4; r=|a/b|=1;

> a=4-3=1; usw....

> s=1; t=0; u=0; v=1;

**a(n)=s(n)*a(0)+t(n)*b(0) - *bzw* - b(n)=u(n)*a(0)+v(n)*b(0)**

**Ein Beispiel in Pseudocode:**
```
EUCLID(a,b)
1  wenn b = 0
2      dann return a
3  sonst return EUCLID(b, a mod b)
```

## Euklidscher Algorithmus in Python3
```python
#!/usr/bin/python3

import sys

def euklid(a,b):
        if b == 0:
                return a
        return euklid(b, a % b)
if len(sys.argv) == 3:
    print(euklid(int(sys.argv[1]),int(sys.argv[2])))
else:
    print("Usage: euklid.py a b; where a and b have to be int")
```


## RSA Signatur und Verschlüsselung
Signieren:
```
Hash(DOCUMENT) = h;
private Key = p
public Key = ö

h^p mod n = ĥ
ĥ^ö mod n = h
```

Verschlüsseln:
```
Document = s
private key = p
public key = ö

s^ö mod n = ŝ
ŝ^p mod n = s
```

Es existiert ein bekanntes Problem, weswegen RSA keinesfalls trivial ist!
Angenommen wir haben den Wert 35 und wir wissen nicht, dass 5 * 7 = 35 ist.
> 35 = 36 - 1 = 6²-1² = (6-1) * (6+1) = 5 * 7

Durch das selbe Zerlegunsprinzip lassen sich in der Theorie auch **alle** privaten Schlüssel berechnen.
Die Verschlüsselung ist also nur so gut, wie die Unfähigkeit des Menschen eine Zahl zu zerlegen.

> 187 = 196 - 9 = (14-3) * (14+3) = 11 * 17

Grundsätzlich lässt sich nämlich **jede Zahl der Welt** in die Differenz zweier Quadrate zerlegen. Sogar **Primzahlen!**
So etwas nennt sich ein quadratisches Sieb. Damit lassen sich Primzahlen finden.

## RSA in Python3
```python
# RSA

# Imports
import random
import sys

sys.maxsize = sys.maxsize*sys.maxsize

# INPUT: Secure parameter l
def Generation(l=42):
    # Randomly select 2 primes with same Bitlength l/2
    print("Randomly selecting 2 secret primes with same bitlength. This could take a while...")
    p = Randomly_Select_Prime_w_Bitlength(int(l)/2)
    q = Randomly_Select_Prime_w_Bitlength(int(l)/2)
    # Compute
    print("Computing...")
    n = p * q
    phi = (p - 1) * (q - 1)
    # Select an arbitrary integer e with 1 < e < phi and gcd(e,phi) == 1
    print("Generating arbitrary integer...")
    e = int(Arbitrary_Int_e(phi))
    # Compute the integer d statisfying 1 < d < phi and e*d == 1 % phi
    print("Generating private Key")
    d = inverse(e, phi)
    # Return n e d
    e = "Public Key = " + (str(e))
    d = "Private Key = " + (str(d))
    n = "N = " + str(n)
    print("\n" + e)
    print(d)
    print(n + "\n")
    return e, d, n

# INPUT: RSA public key e, n, message m
def Encryption(e, n, m):
    print("Encrypting '" + m + "' with public key = " + e)
    c = [pow(ord(char),int(e),int(n)) for char in m]
    print("Encrypted Cipher:")
    print(':'.join(map(lambda x: str(x), c)))
    return ':'.join(map(lambda x: str(x), c))

# INPUT: RSA private key d, n, ciphertext c
def Decryption(d, n, c):
    print("Decrypting Cipher with private key = " + d)
    c = c.split(":")
    m = [chr(pow(int(char), int(d), int(n))) for char in c]
    print("Decrypted Cipher:")
    print(''.join(m))
    return ''.join(m)

# Miller-Rabin-Algorhthmus
def mrt(odd_int):
    odd_int = int(odd_int)
    rng = odd_int - 2
    n1 = odd_int - 1
    _a = [i for i in range(2,rng)]
    a = random.choice(_a)
    d = n1 >> 1
    j = 1
    while((d&1)==0):
        d = d >> 1
        j += 1
    t = a
    p = a
    while(d>0):
        d = d>>1
        p = p*p % odd_int
        if(d&1):
            t = t*p % odd_int
    if(t == 1 or t == n1):
        return True
    for i in range(1,j):
        t = t*t % odd_int
        if(t==n1):
            return True
        if(t<=1):
            break
    return False

def gcd(a, b):
    while b:
        a, b = b, a%b
    return a

def is_prime(n):
    for i in range(3, n):
        if n % i == 0:
            return False
    return True

def Randomly_Select_Prime_w_Bitlength(l):
    prime = random.getrandbits(int(l))
    if (prime % 2 == 1 and prime > 3):
        #if is_prime(prime):
        if (mrt(prime)):
        #if prime % 2 == 1:
            return prime
    return Randomly_Select_Prime_w_Bitlength(l)

def Arbitrary_Int_e(phi):
    e = random.randrange(1, phi)
    #_e = [i for i in range(1, phi)]
    #e = random.choice(_e)
    if(gcd(e, phi) == 1 % phi):
        return e
    return Arbitrary_Int_e(phi)

def inverse(e, phi):
    a, b, u = 0, phi, 1
    while(e > 0):
        q = b // e
        e, a, b, u = b % e, u, e, a-q*u
    if (b == 1):
        return a % phi
    else:
        print("Must be coprime!")    

def query_yes_no(question, default="yes"):
    valid = {"yes": True, "y": True,
             "no": False, "n": False}
    if default is None:
        prompt = " [y/n] "
    elif default == "yes":
        prompt = " [Y/n] "
    elif default == "no":
        prompt = " [y/N] "
    else:
        raise ValueError("invalid default answer: '%s'" % default)

    while True:
        sys.stdout.write(question + prompt)
        choice = input().lower()
        if default is not None and choice == '':
            return valid[default]
        elif choice in valid:
            return valid[choice]
        else:
            sys.stdout.write("Please respond with 'yes' or 'no' "
                             "(or 'y' or 'n').\n")

if len(sys.argv) > 1:
    if sys.argv[1] == "generate":
        if len(sys.argv) == 2:
            key = Generation()
            if query_yes_no("Save generated Keys to File?"):
                _key = '\n'.join(key)
                fo = open("Keypair.txt", "w")
                fo.write(_key)
                fo.close()
                print("Succesfully saved to 'Keypair.txt'. Keep in mind to NOT overwrite this!")

        if len(sys.argv) == 3:
            key = Generation(sys.argv[2])
            if query_yes_no("Save generated Keys to File?"):
                _key = '\n'.join(key)
                fo = open("Keypair.txt", "w")
                fo.write(_key)
                fo.close()
                print("Succesfully saved to 'Keypair.txt'. Keep in mind to NOT overwrite this!")
        elif not len(sys.argv) == 2:
            print("Missing parameters.")
    if sys.argv[1] == "encrypt":
        if len(sys.argv) == 5:
            key = Encryption(sys.argv[2], sys.argv[3], sys.argv[4])
            if query_yes_no("Save cipher to File?"):
                fo = open("cipher.txt", "w")
                fo.write(key)
                fo.close()
                print("Succesfully saved to 'cipher.txt'. Keep in mind to NOT overwrite this!")
        else:
            print("Missing parameters.")
    if sys.argv[1] == "decrypt":
        if len(sys.argv) == 5:
            Decryption(sys.argv[2], sys.argv[3], sys.argv[4])
        elif len(sys.argv) == 4:
            print("Please enter Filename: ")
            name = input()
            fo = open(name)
            cipher = fo.read()
            fo.close()
            Decryption(sys.argv[2], sys.argv[3], cipher)
        else:
            print("Missing parameters.")
else:
    print("Missing parameters.")

```

## AES - Advanced Encryption Standard
### Theorie und Grundlagen
#### Gallois-Felder
Gallois-Felder sind bestimmte Zahlenkörper, in denen alle Zahlen Polynome sind.
Ein Gallois-Feld wird mit ``GF(n)`` bezeichnet.
Für den AES interessieren wir uns für das ``GF(2n)``, spezieller für das ``GF(28)``.
Das bedeutet: *Der Koeffizient jedes Teilpolynoms hat 2 Mögliche Werte aus {0, 1} und es gibt maximal 8 Teilpolynome. So kann jedes Byte als Polynom interpretiert werden und umgekehrt.*
``B = {0011 1101} = 1 + 0x + 1x^2 + 1x^3 + 1x^4 + 1x^5 + 0x^6 + 0x^7 = x^5 + x^4 + x^3 + x^2 + 1``
#### Rechenregeln für ``GF(28)``
Für alle Gallois-Felder gibt es eigene Rechenregeln. Es muss garantiert sein, dass das Ergebnis einer Rechnung auch wieder eine Zahl des Körpers ist. Jede Rechnung muss eindeutig sein. Für uns gelten folgende Rechenregeln:

#### Addition, Subtraktion
Eine Addition oder Subtraktion ist als xor der beiden Bytes festgelegt. Hier kann das Ergebnis gar nicht außerhalb des Feldes liegen. Die Subtraktion ist äquivalent zur Addition weil xor seine eigene Umkehrfunktion ist.

#### Multiplikation
Die Multiplikation funktioniert wie eine binäre Multiplikation, nur dass das Ergebnis „modulo einem Reduktionspolynom“ gerechnet wird.
Ein RP ist ein unteilbares (primes) Polynom, das ein Bit größer
ist als die Zahlen dieses Körpers (sodass das Ergebnis wieder aus dem Körper stammt). Diese Polynome wurden mithilfe des einfachen euklidischen Algorithmus bestimmt. Zaubern wir eines aus dem Ärmel:
``{1 0001 1011} oder x8 + x4 + x3 + x + 1``
Ein Algorithmus, um das Ergebnis einer Multiplikation performant (auch auf schwacher Hardware) zu bestimmen, ist:
```
def mult(a, b, rp):
 two_pow_bitlength = 1 << rp.bit_length() - 1
 res = 0
 while b:
 if b & 1:
 res ^= a
 a <<= 1
 if a & two_pow_bitlength:
 a ^= rp
 b >>= 1
 return res
```

Multiplikation ist somit komplett in bitweisen Operationen realisiert, die bei Hardwarenähe sehr
schnell sind.

#### Inverses Element bestimmen
Zur Berechnung des inversen Elements („Kehrwert“) wird der erweiterte euklidische Algorithmus verwendet:
```
def inverse(a: int, b: int):
 (r, s, t, u, v) = (0, 1, 0, 0, 1)
 while b > 1:
 if a < b:
 (a, s, t, b, u, v) = (b, u, v, a, s, t)
 r = a.bit_length() - b.bit_length()
 (a, b, s, t, u, v) = (b, a ^ (b << r), u, v, (s ^ u << r), (t ^ v << r))
 return v
```
Der Parameter a sollte hierbei das RP sein, b ist die zu invertierende Zahl.
Division
Eine Division zweier Zahlen ist eine Multiplikation mit dem inversen Element des Nenners.
``21 / 7 = 21 * (1/7)``

### Der Algorithmus

- 128-bit Blockchiffre
- schnell
- symmetrisch
- FIPS 197
- veröffentlicht als „Rijndael-Algorithmus“

#### Verschlüsselung
##### State
AES wendet verschiedene Operationen in mehreren Runden auf einen Block an, um die Nachricht gut durcheinanderzuwerfen.
Ein ``128-bit-Block`` wird als zweidimensionales Array der Größe ``4 * 4 Byte (16Byte = 128 bit)`` verstanden.
![](https://files.catbox.moe/xekunq.png)

Ein 128-bit-Block der Eingangsnachricht wird zunächst nach dem Schema ``s[i, j] = in[i + 4j]`` in den sogenannten State kopiert. Der State ist das Array auf dem der Verschlüsselungsalgorithmus operiert. Der State ändert sich jede Runde und am Ende kommt ein verschlüsselter 128-bit-Block heraus, der analog zum input nach dem Schema ``out[i + 4j] = state[i, j]`` gebildet wird.

Was passiert dazwischen?

##### Initialisierung der Schlüssel
Eine der Operationen ist die Anwendung eines Round Keys, der jede Runde einzigartig ist. Für diesen Zweck wird ein „key schedule“ erzeugt, der angibt, welcher Schlüssel in welcher Runde hinzugefügt werden soll.
Zur Generierung des key schedules wird die ``key_expansion`` verwendet. Diese wird ausgeführt, bevor irgendetwas verschlüsselt wird. Die Round keys sind jeweils 4 Wörter ``(4 * 4 Byte)`` lang. Der gesamte key schedule enthält 11 dieser Round keys. Der Round Key wird jede Runde und abschließend ein weiteres Mal auf den State addiert ``(11 * 4 * 4 Byte = 11 * 128 Bit)``. 
###### Algorithmus:
```
def key_expansion(key: list) -> list:
 ks = [[0 for b in range(4)] for n in range(44)]
 for i in range(4):
 ks[i] = [key[4*i], key[4*i+1], key[4*i+2], key[4*i+3]]
 for i in range(4, 44): # 4 to Nb * (Nr+1)
 tmp = ks[i-1]
 if i % 4 == 0:
 tmp = sub_word(rot_word(tmp))
 for b in range(4): # for the whole word
 tmp[b] ^= rcon(i//4)[b]
 for b in range(4): # for the whole word
 ks[i][b] = ks[i-4][b] ^ tmp[b]
 return ks
```
Die ersten 4 Wörter des Key Schedules werden direkt aus dem Cipher Key übernommen. Jedes folgende Wort ist das XOR aus dem vorherigen Wort und dem Wort 4 Positionen vorher. Wenn die Position des Worts allerdings ein Vielfaches von vier ist, wird zunächst eine Transformation angewandt:

Das Wort wird um eine Position nach links rotiert (BYTE-weise) und dessen Bytes werden durch die Bytes aus der sbox ersetzt. Anschließend werden noch Werte aus einem Array mit Rundenkonstanten (rcon) dazugerechnet (xor).

##### Addieren der Schlüssel
Die Rundenschlüssel werden nach folgendem Schema auf den State addiert:

``state[i][j] = state[i][j] xor key_schedule[4*n+j][i]``

n ist hierbei die Nummer der aktuellen Runde. Der Schlüssel wird also spaltenweise addiert.

![](https://files.catbox.moe/k262u9.png)

##### Substitution
Jedes Byte des States wird durch ein anderes Byte ausgetauscht. Durch dieses Durcheinanderwerfen der Werte kann die inkrementelle Analyse verhindert werden.
Die Substitutionswerte sind das ``GF(28)``-Inverse der Zahl (siehe Theorie), auf das eine affine Transformation angewendet wurde, in konkreten Implementierungen wird dafür allerdings nur ein Array verwendet:

``state[i, j]=sbox[state[i, j]]``

Die angewendete Transformation ist folgende:

![](https://files.catbox.moe/nphx1n.png)

c ist in diesem Fall die Zahl 0x63 oder {01100011}.

##### Verschieben der Reihen
