---
path: "/blogi"
title: "Kurssiblogi"
hidden: false
information_page: true
---

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
