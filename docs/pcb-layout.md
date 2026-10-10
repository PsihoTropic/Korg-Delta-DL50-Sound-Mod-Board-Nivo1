# PCB layout predlog - Nivo 1

Ovaj dokument opisuje predlog PCB rasporeda za DIY sound mod board za Korg DELTA DL-50. Layout je zamišljen kao jednostavna, stabilna ploča za prototip, a ne kao finalni komercijalni PCB.

## 1. Osnovna konfiguracija

### Dimenzije
- 100 x 60 mm (standardni prototip)
- 120 x 80 mm (više prostora za power i routing)

### Layer
- 2-layer PCB
- top layer = signal
- bottom layer = ground / power pickup

## 2. Layout organizacija

```text
┌──────────────────────────────────────────────┐
│          TOP SIDE: AUDIO + CONTROLS         │
│                                              │
│     J1 INPUT        RV1 DRIVE      RV2 TONE │
│     ┌───────┐       ┌───────┐      ┌───────┐ │
│     │ JACK  │       │ POT   │      │ POT   │ │
│     └───────┘       └───────┘      └───────┘ │
│                                              │
│                 U1 (TL072 / NE5532)           │
│              ┌───────────────┐              │
│              │  IC  Dual     │              │
│              └───────────────┘              │
│                                              │
│                 RV3 MIX                     │
│                 ┌───────┐                   │
│                 │ POT   │                   │
│                 └───────┘                   │
│                                              │
│     J2 OUTPUT                               │
│     ┌───────┐                               │
│     │ JACK  │                               │
│     └───────┘                               │
│                                              │
└──────────────────────────────────────────────┘
```

## 3. Praktični raspored komponenti

### Lijeva strana
- J1 AUDIO INPUT
- signal input buffer section
- R_in, C_in, op-amp pin routing

### Centralna zona
- U1 op-amp package (TL072 or NE5532)
- vrata za drive, tone, mix
- diode clipping network

### Desna strana
- RV1 Drive
- RV2 Tone
- RV3 Mix
- J2 Output
- power connector

## 4. Power routing

```text
      +9V / +12V DC
            |
            +-------------+--------- GND
            |             |
           C1            C2
           100nF         10uF
            |             |
           VCC -------- GND
```

### Preporuka
- VCC i GND treba da ideju vrlo kratko do op-amp pinova
- stavi decoupling kondenzatore što bliže IC-ovima
- ne koristi dugačke power trace-ove ako nije potrebno

## 5. Audio routing

```text
J1 input
   |
   v
 buffer
   |
   v
 drive stage + diode clip
   |
   v
 tone stage
   |
   v
 mix stage
   |
   v
 output buffer
   |
   v
J2 output
```

## 6. Pozicija potova

### RV1 Drive
- postavi na prednjoj ploči, lako dostupno
- audio taper
- 100kA

### RV2 Tone
- obično 50kA audio taper
- postaviti u sredini front plate

### RV3 Mix
- 100kA audio taper
- idealno na desnoj strani front panela

## 7. PCB routing smjernice

- audio lines ne idu pored power lines
- signal path treba biti kratki i direktni
- uzmi ground pour na donjem sloju
- route op-amp feedback kratko i direktno
- decoupling kondenzatori odmah uz IC pinove

## 8. Dodatni raspored ako želiš metalni case

```text
┌──────────────────────────────────────┐
│ [J1 IN]   [RV1 DRIVE] [RV2 TONE]   │
│                                      │
│        [U1 OPAMP BOARD]             │
│                                      │
│ [RV3 MIX]        [PWR]     [J2 OUT] │
└──────────────────────────────────────┘
```

## 9. Sigurnosni savjeti

- koristi 3.5mm ili 1/4" jacke, ali predvidi dovoljnu udaljenost
- odvoji audio i power zone
- ako koristiš metalni enclosure, dodaj earth / shielding point
- dodaj GND star ground point na zadnjim/bočnim panelima

## 10. Predložena oznaka komponenti

```text
J1 = Input
J2 = Output
RV1 = Drive
RV2 = Tone
RV3 = Mix
U1 = TL072 / NE5532
C1 = 100nF decoupling
C2 = 10uF power smoothing
D1, D2 = 1N4148 clipping diodes
```

## 11. Verzija za proizvodnju

Ako ideš u finalni PCB:
- dodaj silkscreen oznake za pinove i komponentne reference
- koristi pad spacing za 1/4W ili 1/8W rezistore
- predvidi 2 mm kroz rupe za PCB mount posterior
- proba čvrstoća i GND continuity

## 12. Napomena

Ovo je predlog prototipa, ne finalna proizvodna verzija. Za finalnu instalaciju radi se validacija na stvarnoj jedinici i potvrda sa oscilloscope-om i DMM-om.

---

Ako želiš dalje, mogu dodati i:
- `pcb-top-view.svg`-like ASCII layout
- `pcb-gerber-inspired.md`
- `board-dimensions.pdf` opis u markdown obliku
- detaljno gore/dolje routing crtanje sa oznakama pinova
