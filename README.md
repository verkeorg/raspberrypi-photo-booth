Rakensimme Nuori2017 -tapahtumaan Raspberry Pi -valokuva-automaatin. Pahvilaatikkoon oli asennettu Raspberry Pi -keskusyksikkö, kamera sekä kosketusnäyttö. Ohikulkijan koskettaessa ruutua, alkoi kolmen sekunnin laskenta kuvan laukaisuun. Raspberryn otettua valokuvan, se tallentui langatonta verkkoa pitkin Verken omaan Google Photos -albumiin ja kuvattu kohde pystyi halutessaan kirjoittamaan kosketusnäytölle sähköpostiosoitteensa, johon valokuva lähti automaattisesti "postikorttina". Idea automaattiin tuli Maker-lehden numeron 52 (syyskuu/2016) artikkelista "_Raspberry Pi Wi-Fi Party Photo Booth_" ([http://makezine.com/projects/raspberry-pi-photo-booth/](http://makezine.com/projects/raspberry-pi-photo-booth/)). Oheisen linkin takaa löytyy alkuperäinen ohje kaikkine tarvittavine koodeineen, joten ohjelmointitaitoja tämä projekti ei edellyttänyt. Joitain muokkauksia alkuperäiseen koodiin teimme, jotta saimme automaatin toimimaan omaan tarkoitukseemme sopivalla tavalla.

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-01-520x618.jpg) 

_Valokuva-automaatti koristeltuna Nuori2017 -tapahtumassa._ 

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-02-520x451.jpg) 

_Valokuva-automaatin vieressä läppärissä pyöri dia-show, jonne kaikki otetut valokuvat ilmestyivät automaattisesti. Oheis-ananas toimittaa tärkeää tehtävää rekvisiitan ominaisuudessa, koska meillä ei ollut hauskoja hattuja tai tekopartoja mukana._

# Valokuva-automaatin rakennusohjeet:

### Tarvikkeet:

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-03-520x378.jpg)

<div style="direction: ltr;">

<table style="direction: ltr; border-collapse: collapse; border: 1pt solid #A3A3A3;" border="1" cellspacing="0" cellpadding="0">

<tbody>

<tr>

<td></td>

<td>Tuotteen nimi</td>

<td>Hintaesimerkki ([https://vadelmapii.com/](https://vadelmapii.com/))</td>

</tr>

<tr>

<td>1</td>

<td>Raspberry Pi 3 Model B -keskusyksikkö</td>

<td>56€</td>

</tr>

<tr>

<td>2</td>

<td>Raspberry Pi Camera v2</td>

<td>34€</td>

</tr>

<tr>

<td>3</td>

<td>Raspberry Pi 7" Touchscreen Display</td>

<td>84€</td>

</tr>

<tr>

<td>4</td>

<td>EU & UK Power Supply</td>

<td>11€</td>

</tr>

<tr>

<td>5</td>

<td>16 GB NOOBS SD Card</td>

<td>12€</td>

</tr>

<tr>

<td></td>

<td>Yhteensä</td>

<td>197€</td>

</tr>

</tbody>

</table>

</div>

### Muut ei-pakolliset tarvikkeet

<div style="direction: ltr;">

<table style="direction: ltr; border-collapse: collapse; border: 1pt solid #A3A3A3;" border="1" cellspacing="0" cellpadding="0">

<tbody>

<tr>

<td>Litteät salkkumaiset pakkauslaatikot</td>

<td>2 kpl</td>

</tr>

<tr>

<td>Läppäri + virtajohto</td>

<td>1 kpl</td>

</tr>

<tr>

<td>Musta kontaktimuovi</td>

<td>laatikoiden pinta-alan perusteella</td>

</tr>

</tbody>

</table>

</div>

### Raspberry Pi 3 Model B -pohjapiirustus

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-04-520x353.png)

### Vaihe 1\. Kosketusnäytön ja kameran liittäminen keskusyksikköön

1.  Kiinnitä Raspberry Pi -keskusyksikkö kosketusnäyttöön pakkauksen mukana tulevilla ruuveilla.
2.  Kiinnitä kosketusnäytön lattakaapeli keskusyksikön "Display DSI"-liittimeen. Kiinnitys on toteutettu jousilukituksella ja ei edellytä työkaluja. Valkoista osaa nostetaan sormin ja samalla lattakaapeli ujutetaan aukeavaan koloon pohjaan asti. Lopuksi valkoinen osa painetaan tiukasti pohjaan, jolloin kaapeli lukittuu. On tärkeää laittaa lattakaapeli oikein päin: kaapelin sininen puoli ja valkoinen lukitsin vastakkain.
3.  Kytke punainen (5V/virta) ja musta (GND/maa) johto keskusyksikön ja kosketusnäytön piirilevyjen GPIO-pinneihin alla olevan kuvan mukaisesti. **HUOM! Tarkista kytkentä kosketusnäytön pakkauksen ohjekirjasesta ennen verkkovirran kytkemistä!**
4.  Kiinnitä kameran lattakaapeli keskusyksikön Camera CSI -liittimeen samoin kuin yllä, eli kaapelin sininen puoli ja valkoinen lukitsin vastakkain.
5.  Kytke virtalähde verkkovirtaan ja sen USB-liitin Raspberry Pin "Micro USB Power in" -porttiin. GPIO-johtojen kiinnitys: Punainen johto keskusyksikön 5V-pinnistä kosketusnäytön piirilevyn 5V-pinniin, musta johto keskusyksikön GND (maa) -pinnistä kosketusnäytön piirilevyn GND-pinniin. Kaksi muuta mukana tullutta johtoa (vihreä ja keltainen) ovat tässä projektissa tarpeettomia ja niitä ei tarvitse kiinnittää.

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-05-518x689.jpg) 

Tässä vielä havainnollinen video-ohje kosketusnäytön asentamiseen: https://www.youtube.com/watch?v=tK-w-wDvRTg 

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-06-520x371.jpg) 

_Raspberry Pi, kosketusnäyttö ja kamera asennettuna._

### Vaihe 2\. Asennus Raspberry Pi:n seitsemän tuuman näytöltä vs. etähallinta toiselta tietokoneelta suuremman näytön avulla

**On kaksi tapaa hallita Raspberry Pi -tietokonetta:** **Tapa 1\.** Suora hallinta**:** Kiinnitä Raspberry Pi -keskusyksikköön hiiri ja näppäimistö ja käytä näyttönä Raspberryn omaa kosketusnäyttöä.

**Edut:** Et tarvitse erillistä tietokonetta Raspberryn lisäksi. **Haitat:** Huono ergonomia ja hitaus; Selaimen käyttö, ohjelmien lataus ja ohjeiden luku seitsemän tuuman näytöltä ei ole mukavaa, et voi lukea ohjeita ja pitää Raspberry Pin käyttöjärjestelmää näkyvillä samanaikaisesti. Lisäksi sinulla pitää olla erillinen hiiri ja näppäimistö Raspberry Pi:ssä kiinni koko asennuksen ajan.

_Jos haluat suorittaa asennuksen ilman toista tietokonetta ja etäyhteyttä, jätä huomiotta VNC-etäyhteyden asennusohjeet ja hyppää ohjeissa suoraan kohtaan "Vaihe 3"._ **Tapa 2\.** Raspberryn hallinta VNC-etäyhteydellä toisella tietokoneella suurelta näytöltä (suositeltu)

**Edut:** Voit hyödyntää kannettavan tai suurinäyttöisen työpöytäkoneen ergonomiaa sekä näyttöä Raspberry Pi:n asennukseen ja hallintaan; voit pitää selainta auki suuren näytön toisella puoliskolla, josta voit lukea ohjeita ja samalla pitää samalla näytöllä Raspberry Pi:n näyttöä VNC-etäyhteysohjelman avulla ja täysin hallita Raspberry Pi -laitetta. Raspberry Pi -laite voi olla asennuksen ajan pois tieltä ihan vaikkapa kaapin päällä ja siinä ei tarvitse olla kytkettynä omaa hiirtä tai näppäimistöä. Riittää kun Raspberry on päällä ja kirjautuneena samaan WiFi-verkkoon kuin tietokone jolla sitä hallitset. **Haitat:** Tarvitset erillisen tietokoneen etähallintaa varten.

**Ota selville Raspberry Pi:n IP-osoite**

1.  Liitä Raspberry Pi paikalliseen WiFi-verkkoon
2.  Raspberryn IP-osoitteen saat selville kirjoittamalla Raspberryn komentorivillä (CTRL+ALT+T).

    > ifconfig wlan0

Vinkki: Katso artikkelin lopusta kohta "[Näin tehdään Raspberry Pi:ssä suoritettava sh-tiedosto](#naintehdaansuoritettavashtiedosto)", jos haluat lukea IP-osoitteen ilman komentorivin käyttöä. **Päivitä ja kytke päälle Raspberry Pi:n VNC-palvelin**

1.  Päivitä ja kytke päälle Raspbianiin esiasennettu etäyhteyspalvelin (RealVNC Server), jotta siihen voi ottaa yhteyden toiselta koneelta:
    1.  RealVNC-päivitys

        > sudo apt-get update sudo apt-get install realvnc-vnc-server realvnc-vnc-viewer

    2.  Enabloi VNC server Menu -> Preferences ->Raspberry Pi Configuration -> Interfaces Valitse "Enabled" kohdassa VNC
    3.  Avaa VNC Server-asetukset taskbariin ilmestyneestä kuvakkeesta: 
    
    ![](https://www.verke.org/wp-content/uploads/2017/05/rpp-07-520x114.png) 
    
    _More… > Options > Security -> Authentication -> "VNC password"_ Laita haluttu salasana.

**Asenna VNC-viewer ja ota yhteyttä Raspberry Pi:hin (Windows / Mac OS X / Ubuntu)**

1.  Kytke PC-, Mac tai Linux -tietokoneesi samaan WiFi-verkkoon Raspberry Pi:n kanssa.
2.  PC- tai Mac: lataa koneellesi ilmainen RealVNC viewer ja avaa se: https://www.realvnc.com/download/viewer/ Ubuntu: Avaa esiasennettu Remmina-etätyöpöytäsovellus
3.  Laita VNC Vieweriin/Remminaan Raspberryn IP, joka ylempänä hankittiin tietoon
4.  VNC Viewer/Remmina kysyy salasanaa, kirjoita se salasana, jonka määrittelit ylempänä Raspberry Pi:n VNC-palvelimen asetuksiin.
5.  Nyt Raspberry Pi:n työpöydän pitäisi aueta etäyhteydellä uuteen ikkunaan ja voit tästä lähtien hallita Raspberry Pi:tä omalla tietokoneellasi. Voit irroittaa Raspberry Pi:stä hiiren ja näppäimistön sekä sijoittaa sen sopivaan paikkaan pois tieltä.

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-08-520x365.png) 

_Etäyhteyden ottaminen toiselta tietokoneelta Raspberry Pi -laitteeseen VNC Vieweriä käyttämällä._

### Vaihe 3\. Käyttöjärjestelmän säätö ja TouchSelfie-skriptin yhdistäminen Google Photos -albumiin

Seuraa Maker-lehden ohjeita 1-9 (http://makezine.com/projects/raspberry-pi-photo-booth/), joiden avulla asennat ja säädät Raspberry Pin Raspbian-käyttöjärjestelmän ja TouchSelfie -skriptin:

<div style="direction: ltr;">

<table style="direction: ltr; border-collapse: collapse; border: 1pt solid #A3A3A3;" border="1" cellspacing="0" cellpadding="0">

<tbody>

<tr>

<td>Maker-lehden artikkelin ohjeiden vaihe:</td>

<td>Suomenkielinen selite</td>

</tr>

<tr>

<td>

*   1.  Configure the Pi’s operating system

</td>

<td>Säädä Raspbian -käyttöjärjestelmän asetukset.</td>

</tr>

<tr>

<td>

*   1.  Install the requiredplatforms on the Pi

</td>

<td>Asenna Raspbian-käyttöjärjestelmään projektin edellyttämät ohjelmistopaketit Raspbianin omasta ohjelmistoarkistosta.</td>

</tr>

<tr>

<td>

*   1.  Download the TouchSelfie scripts

</td>

<td>Lataa ja asenna TouchSelfie-skripti, jolla valokuva-automaatin kameraa ja käyttöliittymää hallitaan.</td>

</tr>

<tr>

<td>

*   1.  Set up your Google Photos album

</td>

<td>Valmistele Google Photos -valokuva-albumin projektin tarpeisiin.</td>

</tr>

<tr>

<td>

*   1.  Get an app-specific password

</td>

<td>Luo sovelluskohtainen salasana, jolla TouchSelfie saa pääsyn Googlen valokuva-albumiin.</td>

</tr>

<tr>

<td>

*   1.  Create API keys with Google Developer

</td>

<td>Luo API-avain, jonka avulla TouchSelfie -skripti saa pääsyn Google -valokuva-albumiin.</td>

</tr>

<tr>

<td>

*   1.  Connect TouchSelfie to Google Photos

</td>

<td>Yhdistä TouchSelfie Google Photos -palveluun.</td>

</tr>

<tr>

<td>

*   1.  Customize messages and logos

</td>

<td>Muokkaa TouchSelfien käyttöliittymän viestit ja valokuvaan upotettavat logot haluamiksesi.</td>

</tr>

<tr>

<td>

*   1.  Enable Fullscreen and Touchscreen Keyboard

</td>

<td>Aseta koko ruudun näyttötila päälle, jolloin ruudulla näkyy ainoastaan TouchSelfie -käyttöliittymä ja Raspbian-käyttöjärjestelmä on piilotettu.</td>

</tr>

</tbody>

</table>

</div>

  **Huomioita Maker-sivujen ohjeisiin:** Kohdat 4\. ja 5.

Googlen hallintasivujen käyttöliittymä on ehtinyt hieman muuttua artikkelin julkaisun jälkeen, mutta kaikki tarvittava siellä on.

Kohta 3\. ja 9.

Ladatussa TouchSelfie-skriptissä on oletuksena jäänyt koko ruudun näyttötila päälle, se kannattaa ottaa pois päältä rakentamisen ja testaamisen ajaksi. Eli tee kohdassa 3\. päinvastoin kuin kohdassa 9\. sanotaan eli laita #-merkki seuraavan rivin alkuun photobooth_gui.py -tiedostossa, jos se sieltä puuttuu:

> #root.attributes(“-fullscreen”,True)

Kohta 8.

Halutut valokuvan päällä näkyvät logot, kuvakehys tai muut kuvaelementit asetetaan laittamalla valokuvan päälle samankokoinen läpinäkyvä PNG-kuva, jossa logot on asemoitu halutulla tavalla. Tee kuvankäsittelyohjelmalla 1366x768 kokoinen PNG-tiedosto ja tallenna haluamallasi nimellä se samaan kansioon TouchSelfie-skriptin kanssa. Avaa openselfie.conf ja etsi siitä rivi: "logopng = logo.png". Korvaa logo.png oman kuvasi tiedostonimellä ja tallenna.

_Jos seinä nousee vastaan ja et pääse ohjeissa eteenpäin, ota yhteyttä allekirjoittaneeseen, niin katsotaan osaanko mahdollisesti auttaa: timi.hagelberg@hel.fi_

### Vaihe 4\. Valokuva-automaatin kotelon rakentaminen

Käytä luovuuttasi! Itse teimme kotelon ja telineen käyttäen kahta hieman eri kokoista kierrätykseen menossa olevaa kartonkipakkausta, jotka olivat salkun muotoisia. 

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-09-520x359.jpg) 

_Pienempään laatikkoon teimme aukon takaseinään kytkentöjen tarkkailua varten._ 

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-10-520x312.jpg) 

_Etuseinään teimme Raspberry Pi:n kokoisen aukon, johon kiinnitimme Raspberry Pi:n siten, että kosketusnäyttö on tukevasti kiinni pakkauksen etuseinässä halutussa kohdassa._ 

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-11-520x413.jpg) 

_Kiinnitys: Käytimme kahta tukevaa jämä-muovinpalaa, johon Raspberry Pi:n kosketusnäytön ruuvit kiinnitettiin. Kameraa varten teimme toisen aukon etuseinään ja kamera kiinnitettiin tarrateipillä, jotta kameran objektiivin saisi helposti tarvittaessa irroitettua ja kiinnitettyä yhä uudelleen._ 

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-12-520x527.jpg) 

_Pienempi laatikko koristeltiin. Isompaan laatikkoon tehtiin aukko, johon pienempi laatikko laitettiin tukevasti pystyyn._ **HUOM! On syytä laittaa valokuva-automaatin yhteyteen selkeästi tieto siitä minne kuvat tallennetaan ja mihin niitä mahdollisesti jatkokäytetään.**

### Vaihe 5\. Ota selfie!

Onneksi olkoon! Projekti on valmis ja voit ottaa valokuva-automaatin käyttöön.

### Vaihe 6\. Hifistelyä: Luo päättymätön diashow valokuva-automaatin kuvista

Laitoimme valokuva-automaatin yhteyteen kannettavan tietokoneen, joka automaattisesti esitti selaimessa https://slidesome.com -palvelussa diaesityksenä kaikkia automaatin nappaamia valokuvia loputtomasti ympäri. Uudet kuvat ilmestyivät diaesityksen loppuun automaattisesti sitä mukaa kun niitä otettiin. Slidesome-palveluun piti rekisteröityä ja sen ilmaisversio osaa hakea kuvat automaattisesti halutusta Google Photos -albumista. Maksullisessa versiossa pystyi hallitsemaan mm. esitystapaa ja esitettyjen valokuvien kokoa, mutta tähän projektiin maksuttoman version ominaisuudet olivat ihan riittäviä.

### Vaihe 7\. Hifistelyä: Tee Raspberry Pi:n työpöydälle pikakuvakkeet TouchSelfien käynnistämiseen ja IP-osoitteen näyttämiseen.

Komentojen suorittaminen komentoriviltä käsin on epäkäytännöllistä kosketusnäytön avulla, siksi usein tarvittavat komennot kannattaa toteuttaa shell-skripteinä (eli sh-skripteinä), jotka voi suorittaa työpöydälle sijoitettua pikakuvaketta klikkaamalla. sh-skripti pitää sisällään tavallisia Linux-komentoja. Tässä projektissa tarvetta sh-skripteille on näissä tilanteissa:

1.  Halutaan käynnistää TouchSelfie -skripti
2.  Halutaan saada selville Raspberry Pi:n WiFi-verkon IP-osoite, jotta siihen voidaan ottaa etäyhteys.

**Näin tehdään Raspberry Pi:ssä suoritettava sh-tiedosto, joka käynnistää TouchSelfien:**

1.  Avaa komentoterminaali painamalla <CTRL+ALT+T>, hakemisto on oletuksena kotihakemistosi
2.  Luo uusi sh-tiedosto työpöydällesi käyttäen Nano-tekstieditorilla seuraavaa komentoa

    > nano ~/Desktop/TouchSelfie.sh

    _Vinkki: ~ eli tilde-merkki kirjoitetaan PC-näppäimistöllä painamalla Å-näppäimen oikealla puolella olevaa näppäintä pitäen <ALT GR> pohjassa._
3.  Kirjoita seuraavat rivit editorilla ja tallenna+sulje lopuksi painamalla <CTRL-X>

    > #!/bin/bash python /home/pi/git/TouchSelfie/scripts/photobooth_gui.py

4.  Kirjoita komentorivillä seuraava komento, jotta skripti voidaan suorittaa

    > chmod 774 ~/Desktop/TouchSelfie.sh

5.  Suorita sh-tiedosto klikkaamalla työpöydälle ilmestynyttä pikakuvaketta.
6.  Varmista, että sh-tiedosto suoritetaan komentoina terminaalissa klikkaamalla työpöydän TouchSelfie.sh -tiedostoa oikealla hiirenpainikkeella ja valitsemalla "Properties" ja valitsemalla "Open with" kohtaan "Terminal" alla olevan kuvan mukaisesti. 

![](https://www.verke.org/wp-content/uploads/2017/05/rpp-13-520x537.png)

**<a id="naintehdaansuoritettavashtiedosto"></a>Näin tehdään Raspberry Pi:ssä suoritettava sh-tiedosto, joka kertoo nykyisen WiFi-verkon IP-osoitteen:**

1.  Avaa komentoterminaali painamalla <CTRL+ALT+T>, hakemisto on oletuksena kotihakemistosi
2.  Luo uusi sh-tiedosto työpöydällesi käyttäen Nano-tekstieditorilla seuraavaa komentoa

    > nano ~/Desktop/ShowIP.sh

3.  Kirjoita seuraavat rivit editorilla ja tallenna+sulje lopuksi painamalla <CTRL-X>

    > #!/bin/bash ifconfig wlan0 | grep inetsleep 15

4.  Kirjoita komentorivillä seuraava komento, jotta skripti voidaan suorittaa

    > chmod 774 ~/Desktop/ShowIP.sh

5.  Suorita sh-tiedosto klikkaamalla työpöydälle ilmestynyttä pikakuvaketta.
6.  Varmista, että sh-tiedosto suoritetaan komentoina terminaalissa samalla tavalla kuin edellisen osion kohdassa 6.
