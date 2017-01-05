---
title       : Perustyökaluja
description : R for Data Science Chapter 3

--- type:NormalExercise lang:r xp:50 skills:1 key:ee4f3bacf1
## Perusfunktiot 

*** =instructions

Hyviä perusfunktiota ovat esimerkiksi summary() ja table(). Näihin ei tarvitse muuta kuin kertoa, mistä halutaan yhteenveto tai taulukko. 

*** =pre_exercise_code
```{r}
library(haven)
library(ggplot2)

ESS2014 <- read_sav("http://s3.amazonaws.com/assets.datacamp.com/production/course_2409/datasets/ESS2014.sav")
```

*** =sample_code
```{r}
# ESS2014 on ladattuna  

summary(ESS2014$f3_1)

table(ESS2014$f3_1)

# Tee yhteenveto muuttujasta Kuinka onnellinen yleisesti ottaen olette?


# Tee taulukko muuttujasta Kuinka onnellinen yleisesti ottaen olette?


```
***=solution
```{r}
# ESS2014 on ladattuna  

summary(ESS2014$f3_1)

table(ESS2014$f3_1)

# Tee yhteenveto muuttujasta Kuinka onnellinen yleisesti ottaen olette?
summary(ESS2014$c1)

## Tee taulukko muuttujasta Kuinka onnellinen yleisesti ottaen olette?
table(ESS2014$c1)

```

*** =sct
```{r}
test_function("summary", index=2, args="object", 
            not_called_msg = "Muista tehda `summary()`",
            args_not_specified_msg = "Muista maaritella, mista tehdaan yhteenveto - `object`?",
            incorrect_msg = "Onko summary() -suluissa aineisto$muuttujannimi? Tarkista isot ja pienet kirjaimet ja valit")
            
test_function("table", index=2, args="...", 
            not_called_msg = "Muista tehda `table()`",
            args_not_specified_msg = "Muista maaritella, mista tehdaan taulukko - `...`?",
            incorrect_msg = "Onko table() -suluissa aineisto$muuttujannimi? Tarkista isot ja pienet kirjaimet ja valit")

success_msg("Hyvin meni!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:8fac4da90d
## Argumentit


*** =instructions
Joskus funktioille annetaan monta argumenttia. Esimerkiksi keskiarvon laskeva muuttuja mean() ei osaa laskea keskiarvoa, jos kaikilta vastaajilta ei ole tietoa, ja funktiolle pitää kertoa, että jätä ne pois, jotka eivät ole vastanneet. Tämä onnistuu argumentilla na.rm=TRUE - eli puuttuvat tieto Not Applicable poistetaan eli ReMove.

*** =hint


*** =pre_exercise_code
```{r}
library(haven)
library(ggplot2)

ESS2014 <- read_sav("http://s3.amazonaws.com/assets.datacamp.com/production/course_2409/datasets/ESS2014.sav")
```

*** =sample_code
```{r}
mean(ESS2014$c1)

mean(ESS2014$c1, na.rm=TRUE)

# Laske tulomuuttujan (eli muuttujan nimi Tulot) keskiarvo. Muista kertoa funktiolle, että puuttuvat pitää jättää pois!

```

*** =solution
```{r}
mean(ESS2014$c1)

mean(ESS2014$c1, na.rm=TRUE)

# Laske tulomuuttujan keskiarvo. Muista kertoa funktiolle, että puuttuvat pitää jättää pois!

mean(ESS2014$Tulot, na.rm=TRUE)

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
test_function("mean", index=3, args="x",
            not_called_msg = "Muista laskea mean()",
            args_not_specified_msg = "Muista maaritella, mista tehdaan taulukko - `x`?",
            incorrect_msg = c("Onko ensimmainen argumentti aineisto$muuttujannimi? Ja muista kayttaa muuttujaa Tulot, ei alkuperaista tulodesiilimuuttujaa"))
            
test_output_contains("3002", incorrect_msg = "Muistitko poistaa puuttuvat tiedot?")
            
success_msg("Hyvin meni")

```


--- type:NormalExercise lang:r xp:100 skills:1 key:0ce38c3888
## Objektit


*** =instructions

Toistaiseksi olemme operoineet yhdellä objektilla, aineistolla ESS2014 ja sen osilla eli muuttujilla. Kaikkea muutakin voi kuitenkin tallentaa objektiksi muistiin. Voit esimerkiksi luoda uusia aineistoja tai uusia muuttujia aineistoon, mutta myös tallentaa funktioiden tuotoksia muistiin - joskus ei haluta vain tulostaa taulukkoa heti, vaan ehkä operoida sillä myöhemmin. 

Mitä tahansa voi tallentaa objektiksi syntaxilla 
UudenObjektinNimi <- komento/muu tallennettava asia

Tämä tallentaa siis käyttömuistiin, ei kovalevylle tai vastaavaa.

*** =hint

Vastaajan ikä kysymishetkellä 2014 on 2014-syntymävuosi (eli 2014-f3_1).

*** =pre_exercise_code
```{r}
library(haven)
library(ggplot2)

ESS2014 <- read_sav("http://s3.amazonaws.com/assets.datacamp.com/production/course_2409/datasets/ESS2014.sav")
```

*** =sample_code
```{r}
# Vaikka laskutoimituksia voi tallentaa. Kun kirjoittaa pelkän objektin nimen, tulostaa R sen sisällön konsoliin
a <- 5 + 5
a

# Funktioiden tuotoksen voi tallentaa myös

tulojenkeskiarvo <- mean(ESS2014$Tulot, na.rm=T)

# ja näillä voi sitten operoida, vaikkapa laskea keskimääräisen vuosipalkan kuukausipalkasta

tulojenkeskiarvo * 12

# Tyypillisesti halutaan laskea tai luokitella uusia muuttujia, ja liittää niitä aineistoon. Tehdään tämä ensin vuosipalkalle, eli lasketaan jokaisen vastaajan vuosipalkka

ESS2014$Vuosipalkka <- ESS2014$Tulot * 12

summary(ESS2014$Vuosipalkka)

# Laske seuraavaksi vastaajan ikä kyselyhetkellä syntymävuoden perusteella. Vinkin alta löytyy ohjetta, mutta kokeile ensin itse! 
# Muuttujien nimissä ei kannata käyttää ääkkösiä, joten liitä muuttuja aineistoon nimellä Ika


# Tee yhteenveto iästä.


```

*** =solution
```{r}
# Vaikka laskutoimituksia voi tallentaa. Kun kirjoittaa pelkän objektin nimen, tulostaa R sen sisällön konsoliin
a <- 5 + 5
a

# Funktioiden tuotoksen voi tallentaa myös
tulojenkeskiarvo <- mean(ESS2014$Tulot, na.rm=T)

# ja näillä voi sitten operoida, vaikkapa laskea keskimääräisen vuosipalkan kuukausipalkasta
tulojenkeskiarvo * 12

# Tyypillisesti halutaan laskea tai luokitella uusia muuttujia, ja liittää niitä aineistoon. Tehdään tämä ensin vuosipalkalle, eli lasketaan jokaisen vastaajan vuosipalkka

ESS2014$Vuosipalkka <- ESS2014$Tulot * 12
summary(ESS2014$Vuosipalkka)

# Laske seuraavaksi vastaajan ikä kyselyhetkellä syntymävuoden perusteella. Vinkin alta löytyy ohjetta, mutta kokeile ensin itse! 
# Muuttujien nimissä ei kannata käyttää ääkkösiä, joten liitä muuttuja aineistoon nimellä Ika
ESS2014$Ika <- 2014-ESS2014$f3_1

# Tee yhteenveto iästä.
summary(ESS2014$Ika)

```

*** =sct
```{r}

test_output_contains("summary(ESS2014$Ika)", incorrect_msg = "Muistitko tehda yhteenvedon iasta?")
test_error()
success_msg("Hyvin meni")

```



--- type:NormalExercise lang:r xp:100 skills:1 key:578d57e7e7
## Muuttujatyypit

*** =instructions

Aineistoissa voi olla eri tyyppisiä muuttujia - tärkeimpänä jatkuvia ja luokiteltuja. R-slangilla jatkuva on numeric ja luokiteltu factor. European Social Survey on toimitettu sellaisessa muodossa, että kaikki muuttujat ovat jatkuvia (mutta luokkien nimet on tallennettu aineistoon). 

Siksi luokitellut muuttujat pitää usein muuttaa oikeaan muotoon. Ensimmäisellä kerralla käytettiinkin as_factoria - nyt tallennetaan tämä muokkaus aineistoon äsken opitun <- operaattorin avulla.

Funktiot reagoivat eri tavalla erilaisiin muuttujiin -  kun R tietää, että muuttuja on luokiteltu, esimerkiksi summaryn tuotos on erilainen.
*** =hint

*** =pre_exercise_code
```{r}
library(haven)
library(ggplot2)

ESS2014 <- read_sav("http://s3.amazonaws.com/assets.datacamp.com/production/course_2409/datasets/ESS2014.sav")
```

*** =sample_code
```{r}
# Sukupuoli on tietysti luokiteltu muuttuja. Keskiarvo ei ole kovin mielekäs luku. Kerrotaan tämä siis R:lle.

summary(ESS2014$f2_1)

ESS2014$Sukupuoli <- as_factor(ESS2014$f2_1)

summary(ESS2014$Sukupuoli)

# Tee alkuperäisestä asuinympäristöstä yhteenveto.

# Luo uusi Asuinymparisto -muuttuja, joka on luokiteltu.

# Tee uudesta muuttujasta yhteenveto.
```

*** =solution
```{r}
# Sukupuoli on tietysti luokiteltu muuttuja. Keskiarvo ei ole kovin mielekäs luku. Kerrotaan tämä siis R:lle.

summary(ESS2014$f2_1)

ESS2014$Sukupuoli <- as_factor(ESS2014$f2_1)

summary(ESS2014$Sukupuoli)

# Tee alkuperäisestä asuinympäristöstä yhteenveto.
summary(ESS2014$Asuinymparisto)

# Luo uusi Asuinymparisto -muuttuja, joka on luokiteltu.
ESS2014$Asuinymparisto <- as_factor(ESS2014$f14)

# Tee uudesta muuttujasta yhteenveto.
summary(ESS2014$Asuinymparisto)

```

*** =sct
```{r}

test_output_contains("summary(ESS2014$Asuinymparisto)", incorrect_msg = "Muistitko tehda yhteenvedon uudesta siviilisaadysta?")
test_error()
success_msg("Hyvin meni")
```

