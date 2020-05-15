---
path: "/harjoitustyo-ohje"
title: "Harjoitustyön ohje"
hidden: false
information_page: true
---

## Yleiset ohjeet

* Harjoitustyö muodostuu neljästä tehtävästä, joiden ratkaisut palautetaan
  raporttina yhtenä PDF-tiedostona Moodle-järjestelmään.
* Harjoitustyön deadline on 30.6. klo 23:59.
* Harjoitustyö on itsenäinen työ: raportissa oleva teksti ja koodi tulee
  olla itse kirjoittamaasi.

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
Anna vuosi: <font color=red>2015</font>
Opintopisteiden määrä: 50525
Valitse toiminto: <font color=red>2</font>
Anna opiskelijan nimi: <font color=red>Owwoihns</font>
nimi                 op   päiväys        as  
Kxnhxhjhjbbwzpex     1    2000-03-31     4   
Uejviabtdjgwpaeg     9    2000-04-09     2   
Meicnoatrpvlcqnt     3    2000-06-30     3   
Dawibpfgkjrpesut     3    2000-09-18     4   
Vjkltdnqukmuctij     9    2001-01-07     5   
... (rivejä välissä)
Orjxeqtmgtivwely     9    2018-11-30     5   
Ktaxyibbxajrrspm     5    2018-12-29     3   
Psmlkuyldphbiobp     9    2019-06-08     4   
Ocnhysdqkvfruyfy     3    2019-06-17     4   
Ifmfiuypygaslysn     2    2019-08-31     5   
Valitse toiminto: <font color=red>3</font>
Anna kurssin nimi: <font color=red>Jvwkogfmrrioemhy</font>
Keskiarvo: 2.95
Valitse toiminto: <font color=red>4</font>
Anna opettajien määrä: <font color=red>10</font>
opettaja       op  
Svmuiozq       17958
Tgufiwog       17039
Qlzxjjak       16071
Lyalkshh       15158
Lcjdpoqo       15078
Ewzywjoa       14997
Epizvfws       14994
Eukfptdb       14906
Buggubhz       14063
Rgjcxofg       14038
Valitse toiminto: <font color=red>5</font>
</pre>

</sample-output>

Ohjelman vaatimukset:

* Ohjelman kaikki toiminnot toimivat oikein.
* Jokaisessa toiminnossa suoritetaan yksittäinen SQL-kysely, jonka tulostaulu
  on sama kuin toiminnossa haluttu tulos.
* Kyselyissä ei käytetä alikyselyjä.
* Käyttäjän antamat tiedot annetaan kyselyille parametreina.

## Tehtävä 2: Tietokannan suunnittelu

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

* Taulussa ei ole indeksiä.
* Tauluun lisätään kyselyitä tehostava indeksi ennen vaihetta 2.
* Tauluun lisätään kyselyitä tehostava indeksi ennen vaihetta 3.

Ilmoita jokaisesta testistä kuhunkin vaiheeseen 1–3 kuluva aika sekä
tietokantatiedoston koko testin jälkeen. Miten voit selittää testin tulokset?

Varmista ennen testejä, että vaiheessa 3 tulee järkeviä tuloksia,
mutta älä tulosta testeissä mitään muuta kuin kunkin vaiheen ajankäyttö.

Liitä raporttiin testien tulokset sekä käyttämäsi ohjelman lähdekoodi.

## Tehtävä 4: Normaalimuodot

Tietokantojen teoriassa _normalisointi_ (_normalization_) on prosessi,
jonka tavoitteena on parantaa tietokannan rakennetta.

1. Ota selvää, mitä ovat 1., 2., 3., 4. ja 5. _normaalimuoto_ (_normal form_).
   Selosta jokaisesta normaalimuodosta omin sanoin ymmärrettävästi,
   mitä normaalimuoto vaatii ja mitä hyötyä siitä on.
2. Vertaa normaalimuotoja kurssin materiaalin luvussa 5 annettuihin
   tietokannan suunnitteluperiaatteisiin. Mitä yhteistä näillä periaatteilla
   on normaalimuotojen kanssa?

Sopiva pituus tälle tehtävälle on noin kaksi sivua tekstiä raportissa.
Liitä mukaan tehtävässä käyttämäsi lähteet.
