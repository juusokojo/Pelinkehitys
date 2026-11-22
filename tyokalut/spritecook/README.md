# SpriteCook

**Mitä:** AI-pohjainen grafiikkageneraattori pelinkehittäjille. Tuottaa pikseligrafiikkaa ja tarkempaa grafiikkaa: hahmospritejä, animaatioita (idle, walk, run, jump, attack), tilesettejä (top-down, platformer, isometrinen), UI-kokonaisuuksia, esineitä ja saumattomia tekstuureja. Lisäksi taustanpoisto.

**Lähteet:** <https://www.spritecook.ai/agents> · <https://github.com/SpriteCook/claude-plugin> · <https://www.spritecook.ai/pricing>
(Tiedot luettu 22.11.2026.)

## Miten se toimii agenttien kanssa

SpriteCook tarjoaa hostatun MCP-palvelimen. Koodiagentti (Claude Code, Codex, Cursor, OpenCode, ChatGPT) kutsuu sen työkaluja: generoi, tarkistaa jobin tilan ja tallentaa tiedostot suoraan projektikansioon. Mukana tulee myös joukko skillejä (työnkulut spriteille, tileseteille, animaatioille, UI-kiteille ja Godot-viennille).

- MCP-osoite: `https://mcp.spritecook.ai/mcp/claude`
- Tunnistautuminen: SpriteCook-tilin OAuth ensimmäisellä käyttökerralla. API-avainta tai ympäristömuuttujia ei tarvita.
- Älä liitä API-avaimia tai tokeneita chattiin.

## Käyttöönotto

### Claude Code (plugin, suositeltu)

```bash
git clone https://github.com/SpriteCook/claude-plugin.git
cd claude-plugin
claude --plugin-dir .
```

Päivitys: `claude plugin update spritecook@spritecook` ja sitten `/reload-plugins`.

### Claude Code (pelkkä MCP, ilman skillejä)

Kopioi [`mcp.json`](mcp.json) pelin projektin juureen nimellä `.mcp.json`, tai:

```bash
claude mcp add --transport http spritecook https://mcp.spritecook.ai/mcp/claude
```

Plugin on yleensä parempi valinta, koska skillit ohjaavat agenttia oikeisiin työnkulkuihin.

### Claude-työpöytäsovellus

Code-välilehti → Customize → + → Create plugin → Add marketplace → Add from a repository → liitä `https://github.com/SpriteCook/claude-plugin` → Sync → asenna SpriteCook ja yhdistä tili.

### Esimerkkikehotteita

- "Use SpriteCook to generate a 64x64 transparent pixel-art slime enemy and save the result in my project."
- "Use SpriteCook to check my credit balance."

## Hinnat (ilman ALV:tä)

| Paketti | Hinta | Krediitit/kk | Huomioita |
|---|---|---|---|
| Free | 0 $ | 40 | 10 tallennettua assettia, 1 projekti, **ei yksityisiä assetteja**, ei moottorivientejä |
| Starter | 12 $/kk | 1 000 | Yksityiset assetit, Unity/Godot/sprite sheet -viennit |
| Adventurer | 30 $/kk | 3 000 | 2K/4K-resoluutio, 5 rinnakkaista generointia |
| Archmage | 100 $/kk | 12 000 | Korkein jonoprioriteetti |

Kulutus: kuva 8–12 krediittiä (oletusmalli 12), animaatio 20–26. Ilmaisilla krediiteillä saa siis noin 3 kuvaa tai 1–2 animaatiota kuukaudessa. Lisäkrediitit 1–1,2 senttiä kpl, eivät vanhene.

## Lisenssi

Kaupallinen käyttö sallittu kaikissa paketeissa, myös ilmaisessa, eikä mainintaa vaadita. SpriteCookin käyttöehdot ja taustalla olevien AI-mallien tarjoajien ehdot pätevät lisäksi. Käyttöehtoja ei ole vielä luettu: tarkista ennen julkaisua. Plugin-koodi on MIT-lisensoitu.

## Rajoitukset

- Animointi vaatii SpriteCookissa olevan `asset_id`:n. Paikalliset kuvat pitää ensin ladata palveluun.
- Pitkät jobit palauttavat ensin `queued`-tilan. Agenttia pitää pyytää tarkistamaan tila uudelleen.
- Latauslinkit vanhenevat. Ne saa uusittua pyytämällä tarkistusta uudelleen.
- Ilmaisversiossa assetit eivät ole yksityisiä ja tallennustilaa on vain 10 assetille.

## Arvio

**Vahvuudet**
- Matala kynnys: ei API-avaimia, toimii suoraan Claude Coden sisältä ja tallentaa tiedostot projektiin.
- Kattaa koko 2D-pelin perusgrafiikan (hahmot, animaatiot, tilesetit, UI) ja vie Godot-/Unity-muotoon.
- Kaupallinen käyttö sallittu.

**Riskit ja avoimet kysymykset**
- **Tyylin yhtenäisyys.** AI-generoidun grafiikan suurin ongelma on yleensä se, että eri assetit eivät näytä samalta peliltä. Presetit ja "shared concept" -UI-kitit yrittävät ratkaista tämän; toimivuus pitää testata.
- **Pikseligrafiikan tarkkuus.** AI-pikseligrafiikassa on usein epäsiistejä pikseleitä, vääriä paletteja ja ei-kokonaislukuskaalausta. Varaudu käsin siistimiseen (esim. Aseprite).
- **Kustannus skaalautuu nopeasti.** Ilmaisversio riittää vain kokeiluun. Oikeaan peliin tarvitaan käytännössä vähintään Starter (12 $/kk), ja iterointi kuluttaa krediittejä.
- **Riippuvuus palvelusta.** Animointi toimii vain palvelussa olevista asseteista. Pidä kaikki lopulliset tiedostot omassa repossa.
- **Yksityisyys.** Ilmaisversiolla tehdyt assetit eivät ole yksityisiä. Älä käytä sitä keskeneräisen pelin tunnistettaviin hahmoihin, jos tämä haittaa.

## Seuraava askel

Pieni koe ilmaisilla krediiteillä: yksi hahmo (64×64, läpinäkyvä tausta) ja sen kävelyanimaatio. Arvioi tyylin laatu, kuinka paljon käsityötä tarvitaan ja miten tiedostot tuodaan pelimoottoriin. Kirjaa tulokset tähän tiedostoon.
