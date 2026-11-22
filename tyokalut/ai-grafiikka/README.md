# AI-grafiikan työnkulku: yläviisto pikseligrafiikka

Työnkulku 2D-pelin hahmojen ja ympäristöjen tekemiseen tekoälyllä ilman graafikon taitoja. Kohdetyyli on moderni pikseligrafiikka yläviistosta kuvattuna: hahmot noin 48–64 px korkeita, selkeät tummat ääriviivat, rajattu mutta runsas väriskaala ja ruutupohjainen maasto (ruoho, vesi, polut, sillat).

Ohje on yleiskäyttöinen, eli sitä voi käyttää missä tahansa projektissa.

## Periaate

Tekoäly tekee raakamateriaalin, ja ihminen päättää säännöt ja kokoaa lopputuloksen. Yhtenäinen tyyli syntyy kolmella tavalla:

1. **Tyylipassi** lyödään lukkoon ennen ensimmäistäkään generointia (ks. [`tyylipassi.md`](tyylipassi.md)).
2. **Yksi ankkurihahmo** toimii tyylimallina kaikille muille.
3. **Ympäristö kootaan palasista** eikä generoida valmiina karttakuvina.

## Työkalut

| Vaihe | Työkalu | Hinta |
|---|---|---|
| Sprite-, animaatio- ja tilesetgenerointi | PixelLab (pixellab.ai): 4/8-suuntaiset hahmot, animaatiot, top-down-tilesetit, palettipakotus, oma editori ja Aseprite-liitännäinen | Kuukausitilaus, ilmainen kokeilu (hintoja ei tarkistettu) |
| Vaihtoehto yksittäisille esineille | Retro Diffusion: maksu per kuva, tyylikoulutus omista kuvista | 0,03–0,18 $ / kuva |
| Konseptit ja tunnelmakuvat | ChatGPT tai Gemini (kuvat eivät päädy peliin sellaisenaan) | Olemassa oleva tilaus |
| Pikseleiden korjailu | Aseprite (noin 20 $) tai ilmaiset LibreSprite ja Pixelorama | 0–20 $ |
| Kartan kokoaminen | Tiled (ilmainen) tai pelimoottorin tilemap-editori | 0 $ |

## Vaiheet

### 0. Tyylipassi (1–2 h, kerran)

Täytä [`tyylipassi.md`](tyylipassi.md): ruutukoko, hahmojen koko, paletti, ääriviivat, valon suunta ja kuvakulma. Kaikki myöhemmät päätökset tarkistetaan tätä vasten.

### 1. Konsepti (valinnainen)

Tee yleiskäyttöisellä kuvamallilla muutama tunnelmakuva maailmasta ja hahmoista. Kuvat ovat vain suunnan hakua, eivät pelin grafiikkaa.

### 2. Ankkurihahmo

1. Generoi yksi päähahmo PixelLabissa. Tee 10–20 varianttia ja valitse paras.
2. Korjaa se editorissa käsin: ääriviivat, silmät, siistimättömät pikselit.
3. Tallenna hahmo tiedostoon `ankkuri.png`. Siitä tulee tyylimalli kaikille muille hahmoille.

Tähän kannattaa käyttää aikaa. Jos ankkurihahmo on keskinkertainen, kaikki muutkin hahmot ovat.

### 3. Muut hahmot

1. Generoi uudet hahmot käyttäen ankkurihahmoa tyylimallina.
2. Käännä hahmo suuntiin alas, ylös ja sivulle. Toinen sivu saadaan peilaamalla, jos hahmo on tarpeeksi symmetrinen.
3. Animoi jokaiselle suunnalle idle- ja kävelyanimaatio (4–8 kuvaa).
4. Tarkista animaatiot yksi kuva kerrallaan. Tyypillisiä virheitä ovat hyppivät mittasuhteet ja väreilevät ääriviivat.

Työmäärä: 6 hahmoa × 3 suuntaa × 2 animaatiota = 36 animaatiota, joista jokainen pitää tarkistaa.

### 4. Ympäristö

Ympäristö kootaan kolmesta kerroksesta:

| Kerros | Sisältö | Miten tehdään |
|---|---|---|
| Maasto | Ruoho, vesi, polku, lattia | Autotile-tilesetit (siirtymät materiaalien välillä, esim. ruoho↔vesi) |
| Rakenteet | Seinät, sillat, aidat | Tilesetit tai erilliset spritet |
| Esineet | Puut, kivet, kalusteet, kaislat | Erilliset spritet läpinäkyvällä taustalla |

- Tee ensin **ulkoalueet**: niiden tilesetit ovat tekoälylle helpoimpia.
- **Sisätilat ovat vaikein osa.** Yläviistossa seinällä on sekä yläpinta että näkyvä etupinta, eikä tekoäly saa niitä usein yhtenäisiksi. Varaa aikaa käsityöhön tai tee seinät yksinkertaisina.
- Älä generoi kokonaisia karttoja yhtenä kuvana. Niitä ei voi muokata, niiden törmäysalueita ei voi määritellä, eivätkä ne sovi tyylillisesti hahmoihin.

### 5. Jälkikäsittely (jokaiselle assetille)

- [ ] Värit pakotettu tyylipassin palettiin
- [ ] Pikselikoko on yhtenäinen (ei eri kokoisia pikseleitä samassa kuvassa)
- [ ] Ääriviivat noudattavat tyylipassia
- [ ] Tausta on oikeasti läpinäkyvä (ei puoliläpinäkyviä reunapikseleitä)
- [ ] Toimii 1× ja kokonaislukuskaalauksella (2×, 3×)
- [ ] Tiedostonimi ja kirjanpito on päivitetty (ks. alla)

### 6. Kokoaminen

Kokoa kartta Tiledissa tai pelimoottorissa kerroksittain: maasto → rakenteet → esineet (järjestetty y-koordinaatin mukaan) → törmäysalueet.

## Kirjanpito

Pidä taulukkoa `assetit.csv`, jossa on sarakkeet `tiedosto, työkalu, malli, kehote, siemen, pvm, käsin muokattu (k/e)`. Kirjanpidosta on hyötyä, kun

- haluat tehdä samantyylisen assetin myöhemmin uudelleen
- joku kysyy grafiikan alkuperää. Opetuskäytössä ja julkaisualustoilla, kuten Steamissa, tekoälyn käyttö pitää usein ilmoittaa.

## Lisenssit

- **PixelLab:** tekijänoikeus kuuluu käyttäjälle, ja kaupallinen käyttö on sallittu. Tuotoksilla ei saa kouluttaa muita malleja (käyttöehdot 30.10.2026).
- **Retro Diffusion:** kaupallinen käyttö on sallittu usein kysyttyjen kysymysten mukaan. Varsinaisia käyttöehtoja ei saatu luettua.
- Älä käytä tyylimallina muiden pelien grafiikkaa.
