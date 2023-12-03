TDD-vel fejlesszük le a következő feladatot: 

Osztály neve: EgerTávolság
Eger-X város közti távolságot egy hashMap-ben tárolom, ahol a kulcs a város neve, az érték a távolság km-ben

Minden kalkuláció előttmeghívjuk a `Pontosít.pontosít` metódust, ami a szokásos setterek segítségével beállítja, ha valamelyik város közúton közelebb vagy távolabb került pl. út karbantartás miatt. Ezt felolvas egy TXT-t, amiből látja a friss értékeket

írjon egy `bool kivitelezhető(list<string> városNevek` metódust, ha a városok kevesebb mint 500 km-re vannak egertől, egyébként hamisat

Ha a paraméter null akkor saját kivételt kell dobjon


```plantuml
@startuml
Class EgerTavolsag {
	- HashMap<String, Double> tavolsag
	+ boolean kivitelezheto(List<String> varosnevek)
	+ void setVarosTavolsag(String varos, double tavolsag)
}
Class Pontosit{
	- EgerTavolsag
	+ void pontosit()
}
EgerTavolsag ..|> Pontosit :<<pontpsotsad>>
EgerTavolsag <|.. Pontosit : s<<et Tavolsag>>

@enduml
```

```plantuml
@startuml
Class EgerTavolsag {
	- HashMap<String, Double> tavolsag
	+ boolean kivitelezheto(List<String> varosnevek)
	+ void setVarosTavolsag(String varos, double tavolsag)
}
Class Pontosit{
	- EgerTavolsag
	+ void pontosit()
}
Interface Tavolsag {
	+ {abstract} void setTavolsag(String varos, double tavolsag)
}


EgerTavolsag ..|> Tavolsag
EgerTavolsag <|.. Pontosit : <<set Tavolsag>>
Pontosit -->  Tavolsag
@enduml
```


## 2. feladat
Kezítssünk egy fibo osztály amelymp hashmap tárol néhány fibonacci számot, ahol a kulcs sortszámaaz maga at.fibo számok2, 3,


miden hívás előtt megnézzük a cache-t, ha a cacheben van olyan kulcs, 

Rossz:
```plantuml
@startuml
class Cache{
	- Hashmap<int, int> cache
	+ int fibo(int n);
	+ boolean containsKey(int key)
	+ void put(int key, int value)
	
}
class Fibo{
	- HashMap <Integer, Integet) cache
	+ void frissit(Fibo f)
}

Cache ..>Fibo : <<conainsKey,put>>
Fibo ..> Cache : <<frissit>>
@enduml
```

```plantuml
@startuml
interface Allithatosag{
+ void put(int key, int value)
{abstract} boolean containsKey(int key)
{abstract} void put (int key, int value)
}
class Cache{
	- Hashmap<int, int> cache
	+ int fibo(int n);
	+ boolean containsKey(int key)
	+ void put(int key, int value)
	+ void containsKey(int key, int value)
}
class Fibo{
	- HashMap <Integer, Integet) cache
	+ void frissit(Fibo f)
}

Cache o--|> Fibo 
Fibo ..|> Allithatosag
Fibo ..> Cache : <<frissit>>
@enduml
```

## 3. feladat
TDD segítségével fjlesssze le:
haszbáljon cagy paraméterest vagy repeated tested
ÉletkorAlapúOsztáyba Sorol
-1 vagy alatta - hib
0-2 csecsemő
, 3-6 kisgyerek, 7-12 gyerek, 13-18, 19-25 fitatl fenőtt, 25-65 felnott, 120 + hiba

```java
class EletkorAlapuOsztaly{
	String getOsztaly(int Eletkor) {}
}
```
getosztály(életkor) hívás előtt meghívjuk az aktuális elnevezés osztály egy példányából metúdust, ami visszahívja a setelneevzést(int minEletkor, int maxEletkor, String elnevezes) metódust
Ez körkörös lesz, ezért az equals ét hashcode-ban


