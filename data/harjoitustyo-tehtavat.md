---
path: "/harjoitustyo-tehtavat"
title: "Harjoitustyön tehtävät"
hidden: false
information_page: true
---

## Tehtävä 1: Tiedon hakeminen

Olemassa olevassa tietokannassa on tietoa kursseista ja suorituksista.
Tietokannan taulujen rakenne on seuraava:

```sql
CREATE TABLE Opiskelijat (id INTEGER PRIMARY KEY, nimi TEXT);
CREATE TABLE Opettajat (id INTEGER PRIMARY KEY, nimi TEXT);
CREATE TABLE Kurssit (id INTEGER PRIMARY KEY, nimi TEXT, laajuus INTEGER, opettaja_id INTEGER REFERENCES Opettajat);
CREATE TABLE Suoritukset (id INTEGER PRIMARY KEY, opiskelija_id INTEGER, kurssi_id INTEGER, arvosana INTEGER, paivays DATE);
```

Saat ladattua tietokannan itsellesi SQLite-tiedostona [tästä](https://cs.helsinki.fi/u/ahslaaks/kurssit.db).
Voit tutkia tietokantaa SQLite-tulkissa, jotta saat paremman kuvan sen sisällöstä.
Tietokannan sisältö on luotu satunnaisesti tätä tehtävää varten.

Tehtäväsi on laatia tietokantaa käyttävä ohjelma, jossa on seuraavat toiminnot:

1. Laske annettuna vuonna saatujen opintopisteiden yhteismäärä.
2. Tulosta annetun opiskelijan kaikki suoritukset.
3. Laske annetun kurssin kaikkien suoritusten keskiarvo.
4. Tulosta top _x_ eniten opintopisteitä antaneet opettajat.

Seuraavassa on esimerkki siitä, miten ohjelmasi tulee toimia.
Toteuta ohjelma niin, että sen toiminta vastaa tarkasti alla olevaa mallia.
Voit myös verrata ohjelmasi toimintaa esimerkkiin ja varmistaa sen avulla,
että ohjelmasi toimii oikein.

<sample-output>

<pre>
Valitse toiminto: <font color=red>1</font>
Anna vuosi: <font color=red>2014</font>
Opintopisteiden määrä: 274168
Valitse toiminto: <font color=red>2</font>
Anna opiskelijan nimi: <font color=red>Anni Virtanen</font>
kurssi         op   päiväys        arvosana
TKT3617        5    2000-03-21     3   
TKT2155        10   2000-08-22     3   
TKT1414        6    2000-11-26     2   
TKT3013        10   2000-12-04     5   
TKT7048        10   2000-12-19     3 
... (rivejä välissä)
TKT9787        2    2018-12-12     2   
TKT8115        5    2019-01-24     1   
TKT1056        6    2019-03-25     3   
TKT9986        10   2019-04-21     5   
TKT5884        10   2019-08-30     2  
Valitse toiminto: <font color=red>2</font>
Anna opiskelijan nimi: <font color=red>Uolevi Salmela</font>
Opiskelijaa ei löytynyt
Valitse toiminto: <font color=red>3</font>
Anna kurssin nimi: <font color=red>TKT4609</font>
Keskiarvo: 3.03
Valitse toiminto: <font color=red>3</font>
Anna kurssin nimi: <font color=red>TKT1111</font>
Kurssia ei löytynyt
Valitse toiminto: <font color=red>4</font>
Anna opettajien määrä: <font color=red>10</font>
opettaja             op  
Mervi Immonen        124692
Otto Mattila         110474
Ari Toivanen         87136
Jouni Mäkinen        87022
Merja Lehto          86554
Jussi Leino          85083
Katja Parviainen     83947
Leena Hiltunen       83661
Jouni Tikkanen       82821
Veeti Penttinen      82111
Valitse toiminto: <font color=red>5</font>
</pre>

</sample-output>

Ohjelman vaatimukset:

* Ohjelman kaikki toiminnot toimivat oikein.
* Kyselyissä ei haeta ylimääräistä tietoa ja tiedot haetaan yksittäisellä
  kyselyllä, kun se on luontevaa.
* Kyselyissä ei käytetä alikyselyjä.
* Käyttäjän antamat tiedot annetaan kyselyille parametreina.
* Ohjelma antaa järkevän tuloksen myös, jos tietoa ei löydy.

Voit toteuttaa ohjelman haluamallasi ohjelmointikielellä.
Kurssilla annetaan ohjausta Java- ja Python-kielissä,
joiden käyttämiseen on myös neuvoja tässä:

* [SQLite Javassa](/sqlite-java)
* [SQLite Pythonissa](/sqlite-python)

## Tehtävä 2: Tietokannan suunnittelu

Tehtäväsi on suunnitella tietokanta, jota voitaisiin käyttää YouTuben kaltaisen
videopalvelun taustalla. Suunnittele tietokanta niin, että siihen voidaan tallentaa
tietosisältö seuraavia toimintoja varten:

1. Käyttäjä voi etsiä videoita antamalla sanan, joka esiintyy videon nimessä tai kuvauksessa.
2. Käyttäjä voi arvioida videon (peukku ylös tai alas) ja videon yhteydessä näkyy
   yhteenveto käyttäjien arvioista. Sama käyttäjä voi antaa vain yhden arvion videolle.
3. Videon alla näkyy kommentteja käyttäjiltä. Myös näissä voi antaa arvion samaan
   tapaan kuin videossa (peukku ylös tai alas, vain yksi arvio samalta käyttäjältä).
4. Käyttäjä voi perustaa oman kanavan ja julkaista siellä videoita. Kanavan sisällä
   videoita voi luokitella sarjoihin.
5. Käyttäjä voi tilata toisen käyttäjän kanavan, jolloin hän saa tietoa uusista videoista.
6. Videoissa näkyy katsojien määrä ja kanavissa näkyy tilaajien määrä.
7. Käyttäjä voi luoda soittolistoja, joihin voi valita videoita eri kanavista.
   Soittolistan videoilla on tietty järjestys.
8. Käyttäjä voi lähettää viestin toiselle käyttäjälle sekä estää toista käyttäjää
   lähettämästä viestejä hänelle.

Tehtäväsi on suunnitella, mitä tauluja tietokannassa on, mitä sarakkeita kussakin taulussa on
ja miten taulut viittaavat toisiinsa. Jos yllä oleva kuvaus ei kerro jotain yksityiskohtaa,
tee jokin järkevä päätös tämän asian suhteen.

Esitä tietokannan rakenne tietokantakaaviona sekä SQL-skeemana. Suunnittele tietokanta luvun
5 periaatteiden mukaisesti ja käytä sopivissa kohdissa luvun 6.1 tekniikoita
varmistamaan, että tietokannassa oleva tieto on oikeellista.

Selosta lisäksi jokaisesta yllä olevasta vaatimuksesta (1–8), mitä tietoa tietokantaan
tallennetaan, jotta kyseinen vaatimus saadaan toteutettua.

Tässä ohjeessa on neuvoja tietokantakaavion ja SQL-skeeman tekemiseen:

* [Tietokannan kuvaaminen](/tietokannan-kuvaaminen)

Huom! Sinun ei tarvitse suunnitella, miten videot itsessään tallennetaan eikä miten palvelu
osaa suositella käyttäjälle videoita.

## Tehtävä 3: Tehokkuus

Tee ohjelma, jonka avulla voidaan suorittaa tietokannan tehokkuustesti.
Tehokkuustestin osat ovat:

1. Ohjelma luo taulun `Elokuvat`, jossa on sarakkeet `id`, `nimi` ja `vuosi`.
2. Ohjelma lisää tauluun miljoona riviä, joissa nimenä on satunnainen merkkijono
   sekä vuotena on satunnainen kokonaisluku väliltä 1900–2000.
3. Ohjelma suorittaa tuhat kertaa kyselyn, jossa haetaan elokuvien määrä vuonna _x_.
   Jokaisessa kyselyssä _x_ valitaan satunnaisesti väliltä 1900–2000.

Toteuta ohjelma niin, että vaiheessa 2 kaikki rivit lisätään saman transaktion
sisällä, jotta testi ei vie liian paljon aikaa.

Suorita ohjelman avulla kolme testiä seuraavissa tapauksissa:

* Tauluun ei lisätä indeksiä.
* Tauluun lisätään kyselyitä tehostava indeksi ennen vaihetta 2.
* Tauluun lisätään kyselyitä tehostava indeksi ennen vaihetta 3.

Ilmoita jokaisesta testistä kuhunkin vaiheeseen 1–3 kuluva aika sekä
tietokantatiedoston koko testin jälkeen. Miten voit selittää testin tulokset?

Varmista ennen testejä, että vaiheessa 3 tulee järkeviä tuloksia,
mutta älä tulosta testeissä mitään muuta kuin kunkin vaiheen ajankäyttö.

Liitä raporttiin testien tulokset sekä käyttämäsi ohjelman lähdekoodi.

Voit toteuttaa ohjelman haluamallasi ohjelmointikielellä.
Kurssilla annetaan ohjausta Java- ja Python-kielissä,
joiden käyttämiseen on myös neuvoja tässä:

* [SQLite Javassa](/sqlite-java)
* [SQLite Pythonissa](/sqlite-python)

## Tehtävä 4: Normaalimuodot

Tietokantojen teoriassa _normalisointi_ (_normalization_) on prosessi,
jonka tavoitteena on parantaa tietokannan rakennetta.

1. Ota selvää, mitä ovat 1., 2., 3., 4. ja 5. _normaalimuoto_ (_normal form_).
   Selosta jokaisesta normaalimuodosta omin sanoin ymmärrettävästi,
   mitä normaalimuoto vaatii ja mitä hyötyä siitä on.
2. Vertaa normaalimuotoja kurssin materiaalin luvussa 5 annettuihin
   tietokannan suunnitteluperiaatteisiin. Mitä yhteistä näillä periaatteilla
   on normaalimuotojen kanssa?

Tässä tehtävässä sinun tulee etsiä tietoa normaalimuodoista verkosta tai kirjallisuudesta
kurssin materiaalin ulkopuolelta. Käytä useampaa lähdettä, jotta saat hyvän kuvan asiasta.

Sopiva pituus tälle tehtävälle on noin kaksi sivua tekstiä raportissa.
Liitä mukaan lista tehtävässä käyttämistäsi lähteistä.

Huom! Kirjoita selostus niin, että sen voi ymmärtää ilman esitietoja
normaalimuodoista, tietokantojen teoriasta tai matematiikasta.
