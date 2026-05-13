# peltola-pesis

Kevyt pesäpallo-scorebug Twitch/OBS-striimiin. Overlay on tarkoitettu käytettäväksi OBS:n Browser Source -lähteenä ja control panel yhdelle puhelimella päivittävälle henkilölle.

## Tiedostot

- `overlay.html` - vasemman yläkulman pesäpallo-scorebug
- `control.html` - mobiiliystävällinen kontrollipaneeli
- `firebase-config.example.js` - Firebase-konfiguraation pohja
- `.gitignore` - estää oman `firebase-config.js`-tiedoston committaamisen

## Firebase-käyttöönotto

1. Luo uusi Firebase-projekti nimellä `peltola-pesis`.
2. Lisää projektiin Web app.
3. Luo Realtime Database.
4. Ota Authentication käyttöön ja aktivoi Email/Password sign-in.
5. Lisää scorekeeper-käyttäjä Authentication -> Users -näkymässä.
6. Kopioi `firebase-config.example.js` tiedostoksi `firebase-config.js`.
7. Liitä Web appin Firebase config `firebase-config.js`-tiedostoon.
8. Julkaise tiedostot esimerkiksi GitHub Pagesiin tai muuhun staattiseen hostaukseen.

## Realtime Database rules

Kehitystestaukseen voi käyttää tätä väliaikaisesti:

```json
{
  "rules": {
    ".read": true,
    ".write": "auth != null"
  }
}
```

Tällä overlay saa lukea tilanteen ilman kirjautumista, mutta vain kirjautunut control panel saa kirjoittaa.

## Käyttö

Control panel:

```text
control.html?game=main
```

Overlay OBS:ään:

```text
overlay.html?game=main
```

Testitausta selaimessa:

```text
overlay.html?game=main&debug=1
```

## Datamalli

```json
{
  "games": {
    "main": {
      "homeName": "KIPA",
      "awayName": "VETO",
      "homeRuns": 3,
      "awayRuns": 2,
      "homeSetWins": 1,
      "awaySetWins": 0,
      "period": 2,
      "periodCount": 2,
      "inningPairsPerPeriod": 4,
      "inningNumber": 3,
      "inningHalf": "T",
      "battingTeam": "away",
      "outs": 1,
      "showOverlay": true
    }
  }
}
```


## Viimeisimmät hienosäädöt

- Overlay on vasemmassa yläkulmassa.
- Vuoroparin alempi vuoro näytetään muodossa `T`, esimerkiksi `1A` ja `1T`.
- Setupissa voi määrittää jaksojen määrän ja vuoroparien määrän per jakso.
- Control panel ei päästä vuoroparia asetetun maksimin yli.
- Palojen ruudut näkyvät vain sisällä olevan joukkueen rivillä.
- Control panelin lopussa on erillinen manuaalinen pistetaulukon nollaus.
