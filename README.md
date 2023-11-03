# API registriranih vozil v Sloveniji (ni aktiven)

## API ni več aktiven, ker se je izkazalo, da ni ravno uporaben za izvajanje neke statistike, kar je bil primarni cilj vsega skupaj. Tukaj je povezava do boljše rešitve za ta namen -> https://github.com/marcell7/vozila-slo-app

_________________________________________________________________________________________________________________________________________________________________________________________________________________

API za pridobitev podatkov o vseh registriranih avtomobilih v Sloveniji.
Trenutni podatki so od leta 2016 do 2022. Aktualni podatki za leto 2023 se posodobijo konec leta.


## išči po VIN številki

```
GET https://api-aw46ycnrva-ey.a.run.app/api/v0/vehicles?vin=jhmrxxxxxxxxxxxxx
```

S tem klicem lahko z vnosom VIN številke poiščeš podatke o vozilu.

### Request

> 
> **Query**
> 
> |Key|Value|Description|
> |---|---|---|
> |vin|jhmrxxxxxxxxxxxxx|VIN številka vozila, ki ga iščemo|
> 

## išči po večih VIN številkah (max 25)

```
GET https://api-aw46ycnrva-ey.a.run.app/api/v0/vehicles?vin=jhmrxxxxxxxxxxxxx&vin=wvwzxxxxxxxxxxxxx
```

Če želiš preveriti podatke za več vozil hkrati, lahko v klic nanizaš več VIN številk. Maksimalno dovoljeno število v enem klicu je 25. Če jih potrebuješ več, moraš to narediti z ločenimi klici.

### Request

> 
> **Query**
> 
> |Key|Value| Description                               |
> |---|-------------------------------------------|---|
> |vin|jhmrxxxxxxxxxxxxx| VIN številka vozila, ki ga iščemo         |
> |vin|wvwzxxxxxxxxxxxxx| VIN številka drugega vozila, ki ga iščemo |
> 

## poizvedba po bazi po različnih parametrih

```
GET https://api-aw46ycnrva-ey.a.run.app/api/v0/query?gorivo=bencin&model_simple=jazz
```

Omogočeno je tudi klicanje poizvedb s filtriranjem.

Filtri, ki jih trenutno lahko določamo:

- Filtriramo lahko po enakosti polja: gorivo = "bencin"
- Filtre enakosti lahko tudi združujemo z ostalimi: gorivo = "bencin" in model_simple = "jazz"
    

Parameter limit predstavlja število vrnjenih zapisov. Maksimalno število je 25.

Parameter offset pa je VIN številka zadnjega zapisa v predhodnem odgovoru. Ta parameter uporabimo, če naša poizvedba vrne >25 zapisov. Recimo, da naša poizvedba vsebuje 50 zapisov. To pomeni, da jih bomo v odgovoru dobili max. 25, če le to z limit parametrom nismo določili drugače.

Če bi želeli dobiti naslednjih 25 v tej poizvedbi, moramo z offset parametrom poslati VIN zadnjega zapisa v prejšnjem odogovoru. Če offset parametra ne bi specificirali, bi ponovno dobili enakih 25 zapisov.

### Request

> 
> **Query**
> 
> |Key|Value|Description|
> |---|---|---|
> |gorivo|bencin||
> |model_simple|jazz||
> 

## poizvedba po bazi po različnih parametrih z offset-om

```
GET https://api-aw46ycnrva-ey.a.run.app/api/v0/query?gorivo=bencin&model_simple=jazz&offset=jhmgxxxxxxxxxxxxx
```

Če bi želeli dobiti naslednjih 25 v tej poizvedbi, moramo z offset parametrom poslati VIN zadnjega zapisa v prejšnjem odogovoru. Če offset parametra ne bi specificirali, bi ponovno dobili enakih 25 zapisov.

### Request

> 
> **Query**
> 
> |Key|Value|Description|
> |---|---|---|
> |gorivo|bencin||
> |model_simple|jazz||
> |offset|jhmgxxxxxxxxxxxxx|Zadnja vin številka v predhodnem izpisu|
>

---

## Primer izpisa podatkov:
``` json
{
    "result": {
        "aktivnost": [2022, 2021, 2020], // leta v katerih je bilo vozilo registrirano
        "barva_detail": "kovinski - rjava - srednja", // podrobnejši opis barve vozila
        "barva_simple": "rjava", // barva vozila
        "drzava_izvora": "japonska", // država izvora vozila
        "gorivo": "bencin", // gorivo vozila
        "katgorija": "m1", // kategorija vozila
        "km": null, // število prevoženih kilometrov
        "lastnik_p_f": "p", // ali je lastnik fizična ali pravna oseba (f - fizična, p - pravna)
        "lastnik_starost": null, // starost lastnika vozila
        "masa": 1594.0, // masa vozila
        "model_detail": "cr-v / 1.5 / 2wd", // podrobnejši opis modela vozila
        "model_simple": "cr-v", // model vozila
        "motor_moc": 127.0, // moč motorja v kw
        "motor_v": 1498.0, // prostornina motorja v ccm
        "prevrteni_km": 0, // ali je imelo vozilo prevrtene kilometre (od leta 2016) (0 - ne, 1 -ja)
        "prva_registracija": "2020-04-23", // datum prve registracije vozila (leto-mesec-dan)
        "prva_registracija_leto": 2020, // leto prve registracije vozila
        "prva_registracija_mesec": 4, // mesec prve registracije vozila
        "prva_registracija_obmocje": "ljubljana", // območje prve registracije vozila
        "prva_registracija_slo": "2020-04-23", // datum prve registracije v Sloveniji
        "prva_registracija_slo_leto": 2020, // leto prve registracije v Sloveniji
        "prva_registracija_slo_mesec": 4, // mesec prve regisracije v Sloveniji
        "razpon_km": "+0", // prevoženi kilometri (glej *)
        "teh_pregled_izv_enota": null, // izvajalna enota tehničnega pregleda
        "teh_pregled_status": null, // status tehničnega pregleda
        "uporabnik_je_lastnik": 0, // ali je uporabnik vozila tudi lastnik (0 - ne, 1 - ja)
        "uporabnik_obcina": "ljubljana", // občina uporabnika vozila
        "uporabnik_p_f": "f", // ali je uporabnik vozila fizična ali pravna oseba (p - pravna, f - fizična)
        "uporabnik_regija": "osrednjeslovenska", // regija uporabnika vozila
        "uporabnik_spol": "m", // spol uporabnika vozila (m - moški, z - ženska)
        "uporabnik_starost": 56, // starost uporabnika
        "uvozeno": 0, // ali je bilo vozilo uvoženo (0 - ja, 1 - ne)
        "vin": "jhmrw1740kx206111", // vin številka vozila
        "warn_km": 0, // opozorila gelde prevoženih kilometrov (0 - ni opozorila, 1 - je opozorilo; glej **)
        "warn_teh_pregled": 0, // opozorilo glede tehničnih pregledov (0 - ni opozorila, 1 - je opozorilo; glej ***)
        "znamka": "honda", // znamka vozila
        "his": { // zgodovina vozila (podatki so od leta 2016 dalje)
            "km": null,
            "lastnik_p_f": {
                "2020": "p",
                "2021": "p",
                "2022": "p"
            },
            "lastnik_starost": null,
            "teh_pregled_izv_enota": {
                "2020": "avtocenter as d.o.o. pe avto serbinek"
            },
            "teh_pregled_status": {
                "2020": "brezhiben"
            },
            "uporabnik_je_lastnik": {
                "2020": 0,
                "2021": 0,
                "2022": 0
            },
            "uporabnik_obcina": {
                "2020": "ljubljana",
                "2021": "ljubljana",
                "2022": "ljubljana"
            },
            "uporabnik_p_f": {
                "2020": "f",
                "2021": "f",
                "2022": "f"
            },
            "uporabnik_regija": {
                "2020": "osrednjeslovenska",
                "2021": "osrednjeslovenska",
                "2022": "osrednjeslovenska"
            },
            "uporabnik_spol": {
                "2020": "m",
                "2021": "m",
                "2022": "m"
            },
            "uporabnik_starost": {
                "2020": 54,
                "2021": 55,
                "2022": 56
            }
        }
    },
    "status": "successful"
}
// * razpon_km predstavlja različne intervale po prevoženih kilometrih.
// To je namenjeno lažjemu iskanju. Možnosti so: +0, +10000, +50000, +100000, +150000, +200000, +300000
// Primer: Avto s 5000km spada v kategorijo +0, ker ima več kot 0 in manj kot 10000 prevoženih km.
//
// **  opozorila glede prevoženih kilometrov.
// V prvotnih podatkih je pri kilometrih kar nekaj napak. Ta parameter nam pove, če je potrebno biti pozoren pri zabeleženih kilometrih. ker gre lahko za napako.
// Parameter ima tudi vrednost 1, če ima avto prevrtene kilometre.
//
// *** opozorilo glede tehničnih pregledov.
// Opozorilo, če je vozilo v svoji zgodovini imelo kdaj neuspešen tehnični ali pogojno brezhiben pregled

 ```
Generated with [Postdown][PyPI].

[PyPI]:    https://pypi.python.org/pypi/Postdown
