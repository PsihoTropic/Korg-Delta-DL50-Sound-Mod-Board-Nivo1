# Detaljna elektronska shema - Nivo 1

Ovaj dokument daje detaljan schematski koncept za Nivo 1 sound mod board. Ima za cilj da se implementira kao analogni insert blok pre Korg DELTA DL-50 filtera.

## 1. Blok dijagram

```text
               +9V / +12V DC
                    |
                    v
            +------------------------+
            | POWER INPUT + FILTER   |
            | 100nF + 10uF decoupling|
            +------------------------+
                    |
                    v
          +--------------------------+
          | INPUT BUFFER            |
          | U1A: voltage follower   |
          +--------------------------+
                    |
                    v
          +--------------------------+
          | DRIVE / SATURATION      |
          | U1B + diodes + RV1      |
          +--------------------------+
                    |
                    v
          +--------------------------+
          | TONE SHAPING            |
          | U1C + RV2               |
          +--------------------------+
                    |
                    v
          +--------------------------+
          | MIX STAGE               |
          | RV3 + U2A               |
          +--------------------------+
                    |
                    v
          +--------------------------+
          | OUTPUT BUFFER           |
          | U2B: unity gain         |
          +--------------------------+
                    |
                    v
                 TO DL-50 FILTER
```

## 2. Power section

```text
            DC IN (+9V / +12V)
                    |
                    +------ 100nF ------ GND
                    |
                    +------ 10uF ------- GND
                    |
                    +------> VCC to op-amp rails

                    GND ----> op-amp ground rail
```

### Napajanje
- Minimalna verzija: +9V DC + GND
- Ako koristite dual-rail op-amp: +9V / -9V ili +12V / -12V
- Decoupling kondenzatori su obavezni: 100nF + 10uF na svaki rail

## 3. Input buffer

```text
            VCC
             |
             +--- 100nF --- GND
             |
             |
        IN JACK ----> RIN 10k-47k ----> (+) U1A
                              |
                              +----> output (U1A output)
                              |
                              +---- feedback to (-) input
```

### Funkcija
- stabilizuje ulazni signal
- čuva originalni DL-50 signal od opterećenja
- osigurava low output impedance na izlazu

### Predložene vrijednosti
- RIN = 10k - 47k
- C coupling = 1uF - 4.7uF
- op-amp = TL072 / NE5532

## 4. Drive / saturation stage

```text
         VCC
          |
          +---- 100nF ---- GND
          |
          v
       U1B op-amp
   IN ----> R1 10k ----> (+) input
                     |
                     +---- RV1 (Drive pot 100kA)
                     |
               feedback / clipping network
                     |
                 D1 1N4148
                 D2 1N4148
                     |
                 output node
```

### Drive stage koncept
- Drive pot kontrolira gain i saturaciju
- diode soft clipping daje harmonike i “warmth”
- bez distorzije se dobija čist i topao signal

### Predložene vrijednosti
- R1 = 10k - 22k
- RV1 = 100kA
- D1/D2 = 1N4148
- optional Rf = 10k - 47k

## 5. Tone shaping stage

```text
     FROM drive node
            |
            v
        U1C op-amp
            |
            +--- RV2 tone pot 50kA
            |
            +--- R3 22k
            |
            +--- C2 10nF / 47nF / 100nF
            |
            +----> output node
```

### Funkcija
- taman / warm vs svetao / bright
- dodaje karater i boju signala
- može se koristiti kao aktivni EQ ili passive RC tone shaper

## 6. Mix stage

```text
    Clean signal ----> R4 10k ----+
                                   |
                             RV3 100kA (Mix)
                                   |
   Processed signal -> R5 10k ----+
                                   |
                                   +----> U2A summing stage
                                                  |
                                               output
```

### Funkcija
- kombinira originalni signal i processed signal
- omogućava balansiran dry/wet

### Predložene vrijednosti
- R4, R5 = 10k - 22k
- RV3 = 100kA audio taper
- U2A = TL072 or NE5532

## 7. Output buffer

```text
    Mixed signal ----> U2B
                         |
                         v
                     OUT JACK
```

### Funkcija
- nizak izlazni otpor
- stabilan signal ka DL-50 filter input
- smanjuje opterećenje i šum

## 8. Finalna shema povezivanja

```text
J1 INPUT --> U1A --> U1B (drive) --> U1C (tone) --> U2A (mix) --> U2B --> J2 OUTPUT
      |                        |                        |
      +------- 100nF decoup ----+----- 100nF decoup ---+
```

## 9. Predloženi reference design

- U1A = input buffer
- U1B = drive stage
- U1C = tone shaping
- U2A = mix stage
- U2B = output buffer
- RV1 = Drive
- RV2 = Tone
- RV3 = Mix
- J1 = input
- J2 = output
- Cdec = 100nF on each rail

## 10. Napomena

Ovo je prototipska elektronska shema za analogni sound mod board. Finalna verzija se mora potvrditi na breadboard-u i oscilloscope-u prije PCB izrade.

## 11. Sljedeći koraci

1. Prototip na breadboard-u
2. Mjerenje gain i output levela
3. Testiraj hum / grounding
4. Napravi finalni PCB
5. Instaliraj u enclosure

---

Detaljnija shema treba biti validirana i po potrebi dorađena sa realnim mjerama signala i impedanse DL-50 signal path-a.
