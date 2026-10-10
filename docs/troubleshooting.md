# Troubleshooting guide - Nivo 1

Ovaj dokument prikazuje najčešće probleme kod analognog sound mod board-a i njihova rješenja.

## 1. Problem: modul nema zvuk

### Mogući uzroci
- neispravan power rail
- prijelom u signal line
- prekršena GND veza
- op-amp pin not connected

### Rješenje
- provjeri VCC/GND na op-amp-u
- provjeri continuity na input/output jacku
- provjeri solder joints
- provjeri da li je output buffer spojen

## 2. Problem: previše šuma

### Mogući uzroci
- loš grounding
- dugačke power line trace-ovi
- nedovoljno decoupling kondenzatora
- audio input/output zasjenjen

### Rješenje
- dodaj 100nF kondenzatore što bliže op-amp-u
- kratki GS ground bus
- korištenje shielded kablova ili metalnog enclosura
- odvoji signal i power zone

## 3. Problem: DC offset na izlazu

### Mogući uzroci
- op-amp biasing issue
- pogrešan feedback network
- loš coupling capacitor

### Rješenje
- provjeri feedback rezistore
- dodaj coupling capacitor na izlazu
- provjeri da op-amp ne radi u neodgovarajućoj konfiguraciji

## 4. Problem: output je previše jak ili previše slab

### Mogući uzroci
- drive stage gain previše visok
- low output buffer drive
- gain mismatch

### Rješenje
- smanji drive gain
- dodaj trim podesi za output level
- verificaraj op-amp rail i R values

## 5. Problem: tone kontrola ne radi

### Mogući uzroci
- RC network nije pravilno spojen
- pot nije povezan ispravno
- op-amp ne prima signal corretamente

### Rješenje
- provjeri pinout op-amp-a
- provjeri da li je pot spojen između input i ground
- provjeri da li je RC komponenta ispravno orientirana

## 6. Problem: drive stage distorzira previše brzo

### Mogući uzroci
- diodes postavljene pogrešno
- gain pot previše visoko
- low signal headroom

### Rješenje
- smanji gain pot
- prebacite diode konfiguraciju
- dodajte buffer između signala i drive stage-a

## 7. Problem: mix stage ne radi balansirano

### Mogući uzroci
- signali nisu pravilno spojení
- summing resistor values nisu ispravni
- pot nije audio taper

### Rješenje
- provjeri pinout pota
- provjeri da li oba signala dolaze na summing node
- zamijeni pot sa audio taper verzijom

## 8. Problem: modul u potpunosti mijenja tonu na nepravilan način

### Mogući uzroci
- input impedance mismatch
- signal je preduga twine line without buffer
- op-amp saturiran zbog previše signala

### Rješenje
- dodaj input buffer
- smanji drive gain
- osigurač short signal path
- redizajn R/C network

## 9. Default recovery procedure

Ako je modul potpuno nestabilan:
- isključi napajanje
- odspoji izlaz
- vrati modul u bypass stanje
- ponovo provjeri power, ground i signal path
- ponovno testiraj po pojedinačnim blokovima

## 10. Recommended systematic debugging

- testiraj pojedinačno ulazni buffer
- pa drive stage
- pa tone stage
- pa mix stage
- pa output stage

To pomaže vrlo brzo pronaći problem bez miješanja blokova.

---

Ovo je praktičan troubleshooting saver za razvoj Nivo 1 modula.
