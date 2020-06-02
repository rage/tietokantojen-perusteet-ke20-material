---
path: "/blogi"
title: "Kurssiblogi"
hidden: false
information_page: true
---

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
sqlite> SELECT A.id, SUM(B.tulos) FROM Testi A, Testi B
        WHERE B.id <= A.id GROUP BY A.id;
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
