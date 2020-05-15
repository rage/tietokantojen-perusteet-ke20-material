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
