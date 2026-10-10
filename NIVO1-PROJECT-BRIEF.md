# KORG DELTA DL-50 SOUND MOD BOARD - NIVO 1
## FINALNI PROJEKAT ZA PRINT

---

## SADRŽAJ

1. Projektni pregled
2. Cilj i motivacija
3. Signal flow
4. Komponente
5. Šema
6. PCB raspored
7. Insert tačka
8. Build faze
9. Test procedure
10. Sound karakteristike
11. Preporuke

---

## 1. PROJEKTNI PREGLED

Nivo 1 je DIY audio insert modul namenjen za Korg DELTA DL-50 analogni sintetizator. Modul se ubacuje u signal path **pre analognog filtera** kako bi se promenio karakter zvuka pre nego što signal dođe do VCF-a.

**Cilj:** Dodati harmonike, topline i bogatiji zvuk bez menjanja osnovne DL-50 sinteze.

**Status:**完全 готov za prototipiranje i production.

---

## 2. CILJ I MOTIVACIJA

### Zašto Nivo 1?
- Originalni DL-50 ima **čistao, ali često sterilne zvuk**
- Filter je osnovan, bez dodatne karaktera
- Nema mogućnosti za "sound shaping" bez direktnog modiranja

### Šta Nivo 1 daje?
- **Topliji ton** - više harmonika i "warmth"
- **Bogatiji lead** - više "bite" i karaktera
- **Dublji bass** - více "body" i textura
- **Fleksibilnost** - Drive, Tone, Mix kontrola
- **Bypass mode** - potpuno siguran prototip bez rizika

### Prednost pristupa
- Ne diramo originalnu elektroniku
- Modul se lako testira
- Lako se proširuje u Nivo 2 (LFO/CV)
- Najbezbleniji prvi DIY projekat

---

## 3. SIGNAL FLOW

```
DL-50 Mixer / Pre-filter signal
              |
              v
        [ INPUT BUFFER ]
        (stabilizacija impedanse)
              |
              v
    [ DRIVE / SATURATION ]
    (harmonici + "warmth")
              |
              v
      [ TONE SHAPING ]
      (dark/bright kontrola)
              |
              v
       [ MIX / DRY-WET ]
       (balans originalnog i procesiranog)
              |
              v
       [ OUTPUT BUFFER ]
       (niska impedansa za filter)
              |
              v
    DL-50 Analog Filter (VCF)
```

---

## 4. KOMPONENTE

### Aktivne komponente
- **U1, U2:** TL072 ili NE5532 dual op-amp (ukupno 2 IC, 4 op-amp)
- **D1, D2:** 1N4148 diode za soft clipping

### Pasivne komponente
- **Rezistori:** 1k, 4.7k, 10k, 22k, 47k, 100k, 220k
- **Kondenzatori:** 100nF, 10uF, 1uF, 4.7uF, 10nF, 47nF
- **Potenciometri:**
  - RV1 Drive: 100k audio taper
  - RV2 Tone: 50k audio taper
  - RV3 Mix: 100k audio taper

### Konektori i power
- J1, J2: 1/4" mono jack (ili 3.5mm)
- PWR: DC barrel jack 9V-12V
- GND: GND bus / earth point

---

## 5. SHEMA

### 5.1 Power sekcija

```
+9V/+12V DC
    |
    +--- 100nF --- GND
    |
    +--- 10uF ---- GND
    |
    +------> VCC op-amp
```

### 5.2 Input buffer

```
J1 IN ---> 10k resistor ---> (+) U1A
                          |
                          +--- output
                          |
                      feedback to (-)
```

Funkcija: Stabilizuje impedansu, štiti originalni signal

### 5.3 Drive stage

```
FROM BUFFER ---> R1 10k ---> (+) U1B
                        |
                        +--- RV1 Drive pot
                        |
                  D1, D2 clipping
                        |
                      OUTPUT
```

Funkcija: Dodaje harmonike, soft saturation, warmth

### 5.4 Tone stage

```
FROM DRIVE ---> (+) U1C
                |
                +--- RV2 Tone pot
                |
            RC network (R3, C2)
                |
              OUTPUT
```

Funkcija: Dark (bass) do Bright (treble) kontrola

### 5.5 Mix stage

```
Clean signal ---> R4 10k ---|
                           RV3 Mix
Processed signal -> R5 10k -|
                           |
                        U2A summing
                           |
                         OUTPUT
```

Funkcija: Balansira originalnu i procesiranu struju

### 5.6 Output buffer

```
FROM MIX ---> (+) U2B
           |
           +--- output
           |
       feedback to (-)
```

Funkcija: Niska izlazna impedansa za filter

---

## 6. PCB RASPORED

### 6.1 Dimenzije
- **Minimalna verzija:** 100 x 60 mm
- **Preporučena verzija:** 120 x 80 mm

### 6.2 Raspored komponenti

```
┌─────────────────────────────────────────┐
│ J1 IN    [RV1 DRIVE] [RV2 TONE]        │
│                                         │
│        [U1 opamp]   [U2 opamp]          │
│                                         │
│     [RV3 MIX]    [PWR]    [J2 OUT]     │
└─────────────────────────────────────────┘
```

### 6.3 Routing pravila
- Audio linije ne pored power linija
- Decoupling kondenzatori blizu IC-eva
- Kratko feedbacka putanja
- GND pour na donjem sloju
- Kratke trace-ove za kritičan signal

---

## 7. INSERT TAČKA NA DL-50

### 7.1 Gde se ubacuje?

**Idealna tačka:** Između mixer-a i analognog filtera (VCF)

Signal ide:
```
Oscillators -> Mixer -> [INSERT OVDE] -> VCF -> Output
```

### 7.2 Kao pronađemo tačku?

1. Pronađi filter sekciju na mainboard-u
2. Tražiš signal **PRE** filter IC-a
3. Izmeri napon (trebalo bi ~100mV - 1V AC)
4. Pronađi izlaz iz mixer-a ili pre-filter buffer-a
5. Tu je insert tačka

### 7.3 Sigurnost

- **Prvo:** Test sa external insert box
- **Kasnije:** Internal insert na bordu
- **Nikada:** Diraj originalnu elektroniku bez proveravanja

---

## 8. BUILD FAZE

### Faza 1: Prototip na breadboard (1-2 sedmice)
- Testiraj input buffer
- Testiraj drive stage
- Testiraj tone stage
- Testiraj mix stage
- Testiraj output buffer
- Mjeri signal na svakom koraku

### Faza 2: Validacija na stvarnom DL-50 (1 sedmica)
- External insert box test
- Bypass test
- Mild drive test
- Full drive test
- Audio listening test

### Faza 3: PCB dizajn (2 sedmice)
- Finalni schematic
- PCB layout
- Gerber export
- Provjera design-a
- Narudžba PCB-a

### Faza 4: Montaža (1 sedmica)
- Lemljenje komponenti
- Testiranje
- Front panel montaža
- Enclosure montaža

### Faza 5: Final testing (3-5 dana)
- Power test
- Signal test
- Audio test
- Fine-tuning

**UKUPNO VREME:** 4-6 sedmica za prvi prototip

---

## 9. TEST PROCEDURE

### Test 1: Bypass (Drive=0, Tone=50%, Mix=0%)
- Zvuk ostaje identičan originalnom
- Nema dodatnog šuma
- Nema distorzije

### Test 2: Mild drive (Drive=30%, Tone=50%, Mix=50%)
- Zvuk je topao i bogat
- Bez previše agresivnosti
- Filter i dalje radi normalno

### Test 3: Mid drive (Drive=50%, Tone=60%, Mix=60%)
- Zvuk je agresivniji
- Lead ima više "bite"
- Bass je puniji

### Test 4: Full drive (Drive=80%, Tone=70%, Mix=80%)
- Zvuk je fuzzy i gritty
- Pretvara DL-50 u "warm vintage synth"
- Može biti "too much" za neke zvukove

### Test 5: Tone + Mix
- Testiraj tone u ekstremima (0% i 100%)
- Testiraj mix u ekstremima
- Potvrdi da oba rade bez problema

### Acceptance criteria
- ✓ Nema šuma
- ✓ Nema DC offset-a
- ✓ Nema pregrijavanja
- ✓ Drive radi stabilno
- ✓ Tone i mix funkcionišu kao očekivano
- ✓ Zvuk je "topao", ne "sranije"

---

## 10. SOUND KARAKTERISTIKE

### Bez modulacije (Drive=0)
- Zvuk je identičan originalnom DL-50
- Modul služi kao bypass buffer

### Warm mode (Drive 20-40%, Tone 35-60%, Mix 30-50%)
Karakteristike:
- Topao, mek zvuk
- Više harmonika nego original
- Idealno za padove i string sekcije
- Filter je još uvek kontrolisln

### Character mode (Drive 40-60%, Tone 50-70%, Mix 50-70%)
Karakteristike:
- Zvuk ima više karaktera
- Lead je živ i pun
- Bass je grub i dubak
- Filter daje dodatnu dimenziju

### Aggressive mode (Drive 70-100%, Tone 60-90%, Mix 60-100%)
Karakteristike:
- Fuzzy, gritty, dirty zvuk
- Pretvara DL-50 u "Moog-like" instrument
- Bass je ekstremno grub
- Idealno za synth punk i bass musku

---

## 11. PREPORUKE

### Za prototip
1. Počni sa external insert box (najbezblinije)
2. Testiraj sve postavke pre nego što ideš dalje
3. Snimi favorite presets
4. Tek onda go za internal insert (ako se odlučiš)

### Za PCB verziju
1. Koristi quality op-ampe (TL072 je dovoljan)
2. Dodaj decoupling na svakom op-amp-u
3. Koristi short trace-ove
4. Koristi ground plane
5. Testiraj na stvarnom DL-50 pre nego što ideš dalje

### Za enclosure
1. Metalni case je bolje od plastike (manje huma)
2. Označi front panel
3. Dodaj LED indikator (opciono)
4. Добави proper shielding ako je potrebno

### Za Nivo 2
1. Nivo 1 je temelj
2. Nivo 2 je LFO/CV modulation
3. Nivo 3 je MIDI/USB control
4. Razvoj u fazama, bez žurbe

---

## FINALNI CHECKLIST

- [ ] Sve komponente su dostupne
- [ ] Breadboard je spremna
- [ ] Multimetar je spremna
- [ ] Power supply je proverena
- [ ] DL-50 je testirana
- [ ] Insert tačka je pronađena
- [ ] Shema je razumevana
- [ ] Build faze su planirane
- [ ] Test procedure su jasne
- [ ] Alati su spremi

---

## ZAKLJUČAK

Nivo 1 je **prvi i najvažniji korak** u custom sound design-u za Korg DELTA DL-50. Ovaj projekat je:

- ✓ Siguran (bez rizika za originalni instrument)
- ✓ Praktičan (koristi dostupne komponente)
- ✓ Edukativan (uči pravu audio elektroniku)
- ✓ Proširiv (vodi ka Nivo 2 i Nivo 3)
- ✓ Rezultativan (stvarno menja zvuk na bolje)

**Kreni sa prototipom, testiraj, uči, i napravi.**

---

**Verzija:** 1.0
**Datum:** 2026-10-10
**Status:** Kompletan i spreman za build

---

## DODATNE RESURSE

- docs/schematic.md - Detaljne sheme
- docs/bom.md - Komponentna lista
- docs/insert-point-guide.md - Pronalaženje insert tačke
- docs/testing-guide.md - Test procedure
- docs/troubleshooting.md - Rešavanje problema
- docs/sound-tuning-guide.md - Tuning zvuka
- docs/build-checklist.md - Build checklist
- docs/nivo2-plan.md - Nivo 2 expansion plan

---

**SRETNO SA BUILDING-OM!**
