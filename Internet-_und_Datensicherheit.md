# Internet- und Datensicherheit

Eine begleitende Dokumentation der Vorlesung "Internet- und Datensicherheit" 
Informatik.Softwaresysteme, 4. Fachsemester 

## Inhalt

1. [Theorie](#Theorie)
	1. [Grundlagen](#Grundlagen)
	2. [Diffie-Hellman](#DiffieHellman)
	3. [Euklidischer Algorithmus](#EuklidischerAlgorithmus)
	4. [RSA Signatur und Verschlüsselung](#RSA)
2. [Anwendungsentwicklung](#Anwendungsentwicklung)
	1. [Euklidscher Algorithmus in Python3](#EuklidInPython)
	2. [RSA in Python3](#RSAInPython)

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
lorem ipsum - TO BE FILLED -

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


# Anwendungsentwicklung
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
