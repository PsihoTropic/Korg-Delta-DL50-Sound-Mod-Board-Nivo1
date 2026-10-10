# Korg DELTA DL-50 Sound Mod Board - Nivo 1

## Predlog projekta

Ovaj projekat predstavlja DIY sound mod board za Korg DELTA DL-50 u Nivo 1 konfiguraciji. Ideja je da se modul ubaci kao insert segment PRE Korgovog analognog filtera, čime se menja karakter zvuka pre nego što signal stigne do VCF-a. Ovo je najbezbedniji i najpraktičniji prvi korak za customizaciju zvuka bez direktnog diranja originalne elektronike.

## Osnovna ideja

Signal iz DL-50 se odvaja odmah pre analognog filtera / VCF ulaza i prolazi kroz dodatni audio blok:

- input buffer
- drive / saturation stage
- tone shaping stage
- mix / dry-wet stage
- output buffer

Nakon toga signal se vraća u originalni signal path u filter.

To daje:
- više harmonika
- topliji i bogatiji zvuk
- mešavinu čistog i saturisanog signala
- modifikovani karakter bez potpune zamene originalne sinteze

## Signal flow

```text
DL-50 Oscillators / Mixer
          |
          v
   [ INPUT BUFFER ]
          |
          v
   [ DRIVE / SATURATION ]
          |
          v
   [ TONE SHAPING ]
          |
          v
   [ MIX / DRY-WET ]
          |
          v
   [ OUTPUT BUFFER ]
          |
          v
 DL-50 Analog Filter (VCF)
```

## Elektronski princip

### 1. Input buffer

Ulazni signal sa DL-50 treba da se pušta kroz unity-gain buffer kako bi:
- se izbegao opterećenje originalnog kola
- se održala stabilna impedansa
- se smanjiš shum i međusobni uticaj između modula i sintetizatora

Preporučena konfiguracija:
- op-amp: TL072 ili NE5532
- konfiguracija: voltage follower

### 2. Drive / saturation

Najvažniji deo modula. U ovoj fazi se postavlja karakter signala.

Preporučena realizacija:
- op-amp gain stage
- diode soft clipping (1N4148 ili 1N5819)
- gain control kroz pot 10k - 100k
- po potrebi transistor / op-amp overdrive

### 3. Tone shaping

Dodaje kontrolu boje signala: od tamnog (warm) do svetlog (bright).

Moguci oblici:
- passive RC low-pass / high-pass mix
- active tone stage
- equalizer stage

### 4. Mix / dry-wet

Kontrolira odnos originalnog clean signala i saturisanog signala.

Dva osnovna pristupa:
- passive mix
- active summing amplifier

Preporučena psihološka vrednost:
- 0 = čist signal
- 50% = balansiran
- 100% = potpuno processed signal

### 5. Output buffer

Na izlazu se postavlja second buffer kako bi se osiguralo:
- nizak izlazni otpor
- čisti signal ka filteru
- spremnost za dodatni modul (CV / effect bus)

## Predložena shema

### Napajanje

- 9V do 12V DC adapter
- po potrebi dual supply +/- 9V / +/- 12V ako se koriste op-ampovi sa dual power rail

### Predložena topologija napajanja

```text
DC IN --> 9V/12V adapter
      --> 7805 / 79xx / regulator stage (po potrebi)
      --> +9V / GND / -9V
```

U praksi za jednostavno audio kolo preporučuje se:
- +9V i GND za jednostavniji op-amp split
- ili +/-12V ako se koristi više ambijentalnih op-amp konfiguracija

## Predložene komponente

### Op-ampovi
- TL072 x3
- NE5532 x3 (alternativa)

### Diode za clipping
- 1N4148 x2
- 1N5819 x2 (po izboru za više agresivnu saturaciju)

### Potenciometri
- 10k / 50k / 100k audio taper
- Drive pot: 100kA
- Tone pot: 50kA
- Mix pot: 100kA
- Level pot: 10kA (po izboru)

### Kondenzatori
- 100nF MLCC za decoupling
- 10uF elektro za power smoothing
- 1uF, 4.7uF, 22uF za coupling / tone stage

### Rezistori
- 1k, 4.7k, 10k, 22k, 47k, 100k, 220k

### Konektori
- 2x 1/4" mono jack IN/OUT
- 2x power input headers
- GND terminal / bus

## Predložena elektronska topologija

```text
IN JACK
  |
  v
[BUFFER U1A]
  |
  v
[DRIVE STAGE U1B]
  |
  +-- DIODES --> soft clip
  |
  v
[TONE STAGE U1C]
  |
  v
[MIX STAGE]
  |
  v
[OUTPUT BUFFER U2A]
  |
  v
OUT JACK
```

## PCB predlog

PCB je predložen kao mala jednostavna ploča sa:
- 2 audio jack konektora
- 3 potentiometra
- 1 power connector
- op-amp package
- decoupling kondenzatori
- signal routing prema perfboard / PCB 2-layer design

### Dimenzije predloga
- 100 x 60 mm
- ili 120 x 80 mm ako se želi više prostora za power/gnd

### Smestaj komponenti
- left side: in/out jacks
- middle: op-amp IC
- right side: pots + power rail

## Pinout / oznake

### Audio konektori
- J1 = Input
- J2 = Output

### Potenciometri
- RV1 = Drive
- RV2 = Tone
- RV3 = Mix

### Napajanje
- PWR1 = +9V / +12V
- GND = common ground

## Povezivanje sa DL-50

### Opcija A: External insert box (preporučeno)

```text
DL-50 line out / headphone out
          |
          v
   [ SOUND MOD BOARD ]
          |
          v
   amplifier / mixer
```

### Opcija B: Internal insert pre-VCF

```text
DL-50 mixer output
          |
          v
   [ SOUND MOD BOARD ]
          |
          v
   DL-50 filter input
```

Ova opcija daje veću integraciju sa originalnim filterom, ali zahteva precizno spajanje na signal path.

## Signal path preporuka

Najbolji rezultat se dobija kada modul bude umetnut u signal path pre analognog filtera, jer tada:
- drive i saturation uticaju timbre pre filtera
- filter “vidi” već promenjen signal
- rezultat je glasniji, “warmer”, i prirodniji

## Opis uticaja na zvuk

### Clean / bypass
- skoro isti zvuk kao originalni DL-50
- filter radi originalno, bez dodatnog karaktera

### Warm / mild drive
- zvuk je topliji
- harmonici postaju bogatiji
- filter ostaje pristupačan i kontrolisan

### Mid drive
- leadovi postaju agresivniji
- padovi su dublji i bogatiji
- bass se više “razvija”

### High drive / saturation
- signal već postaje “dirty” i “fuzzy”
- filter daje više “bite" i širi harmonike
- idealno za bass sintetizatore i leadove

## Projektni zapis

Ovaj mod je zamišljen kao:
- edukativni DIY audio projekt
- low-risk mod za DL-50
- uvod u custom sound design
- jednostavan prototip koji se kasnije razvija u modulacioni ekosistem

## Sledeći koraci

1. Potvrditi tačan insert point na DL-50 ploči
2. Prototip na breadboard-u
3. Merenje istorodnog signala i impedanse
4. Napraviti PCB verziju
5. Proveriti prisustvo šuma i hum
6. Finalna instalacija u metalni ili plastični enclosure

## Napomena

Ovo je dizajn i dokumentacija za DIY izvedbu. Za finalnu instalaciju i stabilnost, preporučuje se:
- zemljanje u skladu sa originalnim sintetizatorom
- decoupling kondenzatori na napajanju
- op-amp buffer stage na ulazu i izlazu
- finalna proba sa multimetrom i oscilloscope

## Pravac daljeg razvoja

Nakon Nivo 1, moguće je dodati:
- LFO modulation
- CV interface
- MIDI / USB kontrolu
- preset memory
- drive amount modulation
- external effects send / return

## Reference

- Korg DL-50 analog signal path
- Classic transistor / op-amp saturation circuits
- TL072 / NE5532 audio preamp design
- passive tone network and active sum stage

## License

Ovaj projekat je dokumentacioni i DIY primer. Koristi se isključivo za edukaciju, prototipiranje i vlastite eksperimente.

---

Ako želiš, u sledećem koraku mogu da kreiram i:
- `schematic.pdf`-like textual schematic
- `pcb-layout.md` sa spatial arrangement
- `bom.csv` ili `bill-of-materials.md`
- `README.md` krajnje uređen za repo
- detaljan `insert-point-guide.md` za DL-50 signal path
