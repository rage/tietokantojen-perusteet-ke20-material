---
path: "/blogi"
title: "Kurssiblogi"
hidden: false
information_page: true
---

## 26.6.2020

Kurssi on jo lähellä loppua: SQL-tehtävien ja harjoitustyön deadline
on ensi viikon tiistai (30.6. klo 23:59).

Tässä on vinkkilista harjoitustyön raportin viimeistelyyn:

**Tehtävä 1**

* Varmista, että koodin pystyy lukemaan mukavasti raportista:
  fontti on riittävän suuri ja myös pitkät rivit ovat luettavissa
  (tarvittaessa usealle riville jaettuna).
* Ei haittaa, vaikka koodi ei olisi helposti kopioitavissa.
  Harjoitustyön arvostelija käy läpi koodin kokonaiskuvan
  raportin perusteella mutta ei suorita koodia.

**Tehtävä 2**

* Tietokantakaavion kuva voi olla leveä, mutta laita se silti raporttiin
  alkuperäisessä asennossa eikä käännettynä 90 astetta.
  Arvioijan on hyvin hankala lukea kaaviota, jos se on käännetty.
* Tietokannasta riittää antaa `CREATE TABLE` -komennot, jotka luovat taulut.
  Ei tarvitse antaa esimerkiksi `SELECT`- tai `INSERT`-komentoja.

**Tehtävä 3**

* Rivien lisääminen tietokantaan tulisi kestää luokkaa kymmenen sekuntia.
  Jos se kestää paljon enemmän, varmista, että kaikki lisäykset tehdään
  yhden transaktion sisällä (alussa `BEGIN` ja lopussa `COMMIT`).
* Ilman indeksiä tulosten hakemisen tulisi kestää luokkaa pari minuuttia
  ja indeksin kanssa luokkaa pari sekuntia.
  Jos saat poikkeavia tuloksia, varmista, että suoritat lisäykset ja
  haut oikein ja mittaat ajan oikein.

**Tehtävä 4**

* Pyri siihen, että teksti on helposti ymmärrettävää. Monissa lähteissä
  asiat on ilmaistu hankalasti ja matemaattisesti, mutta näin ei ole pakko tehdä.
  Esimerkit helpottavat paljon normaalimuotojen ymmärtämistä.
* Ei haittaa, jos ylität harjoitustyön ohjeissa annetun sivumäärän,
  jos pystyt sen ansiosta selittämään asioita paremmin.

## 16.6.2020

SQL Trainerin tehtävissä 93 ja 94 tulee vertailla käyttäjien kaverilistoja.
Kuinka moinen onnistuu SQL:llä?

Hyvä askel kohti ratkaisua on koettaa ensin laskea jokaiselle
käyttäjäparille, montako yhteistä kaveria heillä on.
Koska jokainen kaverisuhde on oma rivinsä taulussa `Kaverit`,
meidän täytyy pohjimmiltaan vertailla kaverisuhteita toisiinsa
yksi kerrallaan.

Seuraava kysely käy läpi päätasolla kaikki käyttäjäparit ja
hakee heidän nimensä.
Kolmas tulostaulun sarake tulee alikyselystä,
joka käy läpi käyttäjien kaverilistat ja vertailee
niitä toisiinsa.
Tuloksena saamme jokaisesta parista tietoon yhteisten
kaverien määrät.

```sql
SELECT A.nimi, B.nimi, (SELECT SUM(C.kaveri_id=D.kaveri_id) 
                        FROM Kaverit C, Kaverit D
                        WHERE C.kayttaja_id=A.id AND D.kayttaja_id=B.id) tulos
FROM Kayttajat A, Kayttajat B;
```

Tehtävän 93 tilanteessa kyselyn tulos on seuraava:

```x
nimi        nimi        tulos     
----------  ----------  ----------
Uolevi      Uolevi      2         
Uolevi      Maija       0         
Uolevi      Liisa       1         
Uolevi      Kaaleppi    2         
Maija       Uolevi      0         
Maija       Maija       1         
Maija       Liisa       1         
Maija       Kaaleppi    0         
Liisa       Uolevi      1         
Liisa       Maija       1         
Liisa       Liisa       2         
Liisa       Kaaleppi    1         
Kaaleppi    Uolevi      2         
Kaaleppi    Maija       0         
Kaaleppi    Liisa       1         
Kaaleppi    Kaaleppi    2
```

Tulostaulusta selviää esimerkiksi,
että Uolevilla ja Kaalepilla on kaksi yhteistä kaveria
sekä että Maijalla ja Liisalla on yksi yhteinen kaveri.

Ehkä oudoin kohta kyselyssä on summa `SUM(C.kaveri_id=D.kaveri_id)`.
Tässä käytetään hyväksi SQL:n ehtojen ominaisuutta:
jos ehto on tosi, niin sen tulos on luku 1.
Alikysely vertaa toisiinsa kaverilistoja ja ehdon tulos on 1
aina, kun löytyy yhteinen kaveri.
Niinpä näiden tulosten summa kertoo, montako yhteistä kaveria on yhteensä.

Tällä idealla on mahdollista ratkaista tehtävät 93 ja 94.
Niissä pitää vielä ryhmitellä tietoa sopivasti sekä verrata yhteisten
kaverien määrää kaikkien kavereiden määrään.

## 5.6.2020

Tarkastellaan tilannetta, jossa taulussa `Elokuvat` on elokuvia
ja haluamme selvittää, mikä on suurin määrä elokuvia,
jotka ovat ilmestyneet samana vuonna. Esimerkiksi taulussa

```x
sqlite> SELECT * FROM Elokuvat;
id          nimi        vuosi     
----------  ----------  ----------
1           Lumikki     1937      
2           Fantasia    1940      
3           Pinocchio   1940      
4           Dumbo       1941      
5           Bambi       1942      
```

haluttu tulos on 2, koska vuonna 1940 ilmestyi kaksi elokuvaa.

Tämä on vähän hankalalta vaikuttava tilanne,
koska meidän tulisi tehdä sisäkkäin kyselyt
`COUNT`, joka laskee ilmestymismääriä,
ja sitten `MAX`, joka hakee suurimman arvon.
SQL ei salli kuitenkaan kyselyä `SELECT MAX(COUNT(vuosi))` tai vastaavaa.

Voimme ottaa kuitenkin lähtökohdaksi kyselyn,
joka ryhmittelee elokuvat vuoden mukaan ja hakee jokaisesta ryhmästä
elokuvien määrän:

```sql
sqlite> SELECT COUNT(*) FROM Elokuvat GROUP BY vuosi;
COUNT(*)  
----------
1         
2         
1         
1       
```

Näistä luvuista pitää vielä saada haettua suurin, mikä onnistuu alikyselyn avulla.
Tässä tapauksessa kätevä tapa on käyttää alikyselyä niin,
että sen tulos on pääkyselyn `FROM`-osassa,
jolloin alikysely luo taulun, josta pääkysely hakee tietoa:

```sql
sqlite> SELECT MAX(c) FROM (SELECT COUNT(*) c FROM Elokuvat GROUP BY vuosi);
MAX(c)    
----------
2       
```

Entä voisiko tehtävän ratkaista ilman alikyselyä?
Kyllä, koska voimme järjestää tulokset
suurimmasta pienimpään ja valita tulostaulun ensimmäisen rivin:

```sql
sqlite> SELECT COUNT(*) c FROM Elokuvat GROUP BY vuosi ORDER BY c DESC LIMIT 1;
c         
----------
2          
```

## 2.6.2020

Hyödyllinen taito SQL:ssä on osata laskea _kumulatiivinen summa_
eli jokaiselle riville summa sarakkeen luvuista
kyseiselle riville asti. Tarkastellaan esimerkiksi seuraavaa taulua:

```x
sqlite> SELECT * FROM Testi;
id          tulos
----------  ----------
1           200
2           100
3           400
4           100
```

Voimme laskea kumulatiivisen summan kahden taulun kyselyllä näin:

```x
sqlite> SELECT A.id, SUM(B.tulos) FROM Testi A, Testi B WHERE B.id <= A.id GROUP BY A.id;
id          SUM(B.tulos)
----------  ------------
1           200         
2           300         
3           700         
4           800       
```

Tässä on ideana, että summa lasketaan taulun `A` riville ja
taulusta `B` haetaan kaikki rivit, joiden `id` on pienempi tai
sama kuin taulun `A` rivillä.
Halutut summat saadaan laskettua `SUM`-funktiolla ryhmittelyn jälkeen.

Vastaavaa tekniikkaa voi käyttää muissakin tilanteissa,
jos haluamme laskea tuloksen, joka riippuu jotenkin kaikista
"pienemmistä" riveistä taulussa.

## 26.5.2020

SQL Trainerin statistiikka kesän kurssilta on nyt
[täällä](https://ahslaaks.users.cs.helsinki.fi/mooc/sql_stats.php).

Statistiikka näyttää jokaisesta tehtävästä,
moniko kurssin osallistuja on ratkonut sen tällä hetkellä.

Tällä hetkellä eniten ratkaistuja on tehtävässä 1 (458 ratkaisijaa)
ja vähiten ratkaistuja on tehtävässä 95 (20 ratkaisijaa).

## 21.5.2020

Harjoitustyön ohje on nyt julkaistu. Harjoitustyö muodostuu neljästä
tehtävästä, jotka palautetaan raporttina 30.6. mennessä.

Harjoitustyön ohjeessa kerrotaan myös, miten voit ilmoittautua kurssille.
Tämä täytyy tehdä 29.6. mennessä, jotta voit palauttaa harjoitustyön.

## 18.5.2020

Tällä viikolla kurssin ohjausta järjestetään Telegramissa erityisesti
ti 19.5. välillä 14–18 sekä pe 22.5. välillä 14–18.

Telegramissa on ollut jo hyvin keskustelua, ja neuvoja tehtäviin
voi kysyä milloin vain, mutta erityisesti noina aikoina kurssin
luennoija on paikalla kanavalla.

Jatkossa viikon ohjausajat ilmoitetaan Telegramissa maanantaisin.
Ajat saattavat vaihdella viikoittain kurssin aikana.

## 11.5.2020

SQL Trainer antaa nyt tehtävän ratkaisemisen jälkeen mahdollisuuden
katsoa tehtävän mallivastauksen.

Jokaisessa tehtävässä mallivastaus on yksi mahdollinen tapa
ratkaista tehtävä. Kuitenkin monissa tehtävissä on monia
erilaisia lähestymistapoja, eli ei kannata huolestua,
jos mallivastaus on erilainen kuin oma ratkaisu.

Jos keksit johonkin tehtävään selvästi mallivastausta paremman
ratkaisun, niin kerrothan kurssin luennoijalle!

## 7.5.2020

Kurssi alkaa tänään. Tervetuloa kurssille!
