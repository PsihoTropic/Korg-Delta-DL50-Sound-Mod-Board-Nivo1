# Bill of Materials (BOM) - Nivo 1

Ovaj dokument prikazuje predložene komponente za jednostavan, protipski "sound mod board" za Korg DELTA DL-50. Svi delovi su odabrani za analognu audio obradu i jednostavno prototipiranje.

## 1. Op-amp i aktivne komponente

| Referenca | Komponenta | Vrednost | Količina | Napomena |
|-----------|------------|----------|----------|----------|
| U1A | TL072 / NE5532 | dual op-amp | 1 | input buffer |
| U1B | TL072 / NE5532 | dual op-amp | 1 | drive stage |
| U1C | TL072 / NE5532 | dual op-amp | 1 | tone stage |
| U2A | TL072 / NE5532 | dual op-amp | 1 | mix stage |
| U2B | TL072 / NE5532 | dual op-amp | 1 | output buffer |

Napomena: u praksi mogu se koristiti 2x TL072 ili 2x NE5532 dual IC pa se tako smanjuje broj komponenti.

## 2. Potenciometri

| Referenca | Komponenta | Vrednost | Količina | Napomena |
|-----------|------------|----------|----------|----------|
| RV1 | audio taper potentiometer | 100k | 1 | Drive |
| RV2 | audio taper potentiometer | 50k | 1 | Tone |
| RV3 | audio taper potentiometer | 100k | 1 | Mix |

## 3. Diode i clipping

| Referenca | Komponenta | Vrednost | Količina | Napomena |
|-----------|------------|----------|----------|----------|
| D1 | 1N4148 | switching diode | 1 | soft clipping |
| D2 | 1N4148 | switching diode | 1 | soft clipping |
| D3 | 1N5819 | Schottky | 1 | opcionalni, agresivniji overdrive |
| D4 | 1N5819 | Schottky | 1 | opcionalni, agresivniji overdrive |

## 4. Pasivne komponente - rezistori

| Količina | Vrednost | Potreba |
|----------|----------|---------|
| 5-10 | 1k | bias / feedback |
| 5-10 | 4.7k | bias / tone network |
| 5-10 | 10k | buffer / input |
| 5-10 | 22k | tone / mix |
| 5-10 | 47k | feedback / drive |
| 5-10 | 100k | drive / mix |
| 5 | 220k | opcionalni gain / tone |

## 5. Pasivne komponente - kondenzatori

| Komponenta | Vrednost | Količina | Napomena |
|------------|----------|----------|----------|
| C1 | 100nF | 4-6 | decoupling |
| C2 | 10uF | 2-4 | smoothing |
| C3 | 1uF | 2-4 | coupling stage |
| C4 | 4.7uF | 2-4 | coupling/output |
| C5 | 10nF | 2-4 | tone shaping |
| C6 | 47nF | 2-4 | filter / tone stage |

## 6. Audio konektori

| Referenca | Komponenta | Količina | Napomena |
|-----------|------------|----------|----------|
| J1 | 1/4" mono jack | 1 | input |
| J2 | 1/4" mono jack | 1 | output |
| PWR1 | DC barrel jack / screw terminal | 1 | power |

## 7. Power section

| Komponenta | Vrednost | Količina | Napomena |
|------------|----------|----------|----------|
| regulator / adapter | 9V - 12V DC | 1 | individual PSU recommended |
| 7805 / LM317 / dual regulator | po potrebi | 1 | ako se koristi dodatni rail |
| reverse polarity protection diode | 1N5819 | 1 | optional |

## 8. Case + PCB

| Komponenta | Opis | Količina |
|------------|-------|----------|
| perfboard / PCB | prototyping plate | 1 |
| enclosure | aluminum or plastic box | 1 |
| screws / standoffs | mounting | 4+ |
| panel labels | front plate labels | 1 project |

## 9. Predložena finalna konfiguracija

### Minimalna verzija
- 1x TL072 dual IC
- 1x NE5532 dual IC
- 3x poti
- 2x diode clipping
- 2x jacks
- power section

### Naprednija verzija
- 2x TL072 dual IC
- dodatni tone EQ stage
- 1x LED indikator
- 1x bypass switch / footswitch

## 10. Napomena

Ovo je BOM za protipski sound mod board. U finalnoj verziji se mogu dodati:
- bypass switch
- LED power indicator
- small panel labels
- ground shielding
- metal enclosure

---

Ako želiš, sljedeći korak je detaljan `insert-point-guide.md` za pronalaženje tačne tačke umetanja u Korg DELTA DL-50 signal path.
