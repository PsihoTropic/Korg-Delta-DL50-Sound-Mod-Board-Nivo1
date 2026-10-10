# Nivo 2 plan - expansion path

Ovaj dokument opisuje kako se Nivo 1 mod može proširiti u Nivo 2 i dalje u modularni / digitalni control koncept.

## 1. Predlog Nivo 2

Nivo 2 dodaje kontrolu i modulaciju na postojeći sound mod board.

### Dodaci:
- LFO generator
- envelope follower
- CV outputs
- MIDI / USB control
- assignable modulation targets
- preset memory

## 2. Glavni cilj Nivo 2

Dodavanje modulacije signalu, ne samo statičke korekcije boje.

### Moguće moduli:
- LFO -> drive amount
- LFO -> tone amount
- LFO -> mix amount
- envelope follower -> drive
- random / sample & hold -> filter texture

## 3. Predložena platforma

- Teensy 4.1
- STM32 / Blue Pill
- ESP32 (ako se želi WiFi / USB)

## 4. Hardware

### Potrebno:
- DAC za CV output
- ADC za kontrolere
- potentiometri / encoders
- MIDI inputs
- USB-C / serial port
- OLED / display

## 5. Signal flow Nivo 2

```text
DL-50 pre-filter signal
      |
      v
  [ Nivo 1 sound mod ]
      |
      v
  [ CV modulation source ]
      |
      v
  [ Drive / Tone / Mix CV input ]
      |
      v
  [ Output to filter ]
```

## 6. Moguće funkcije

### LFO section
- Triangle / Saw / Square / Random
- speed control
- depth control
- target selection

### Envelope follower
- detects signal dynamics
- controls drive or mix
- creates motion / pumping effect

### CV output
- 0–5V or -5V to +5V outputs
- control of filter, drive, tone modulation

## 7. Plan razvoja Nivo 2

### Faza 1
- dodaj LFO kontrolu na Drive i Tone

### Faza 2
- dodaj CV output i kontrolu preko encoders

### Faza 3
- dodaj MIDI / USB input

### Faza 4
- dodaj preset memory i save/load

## 8. Razlog za Nivo 2

Nivo 1 je “sound shaping”.
Nivo 2 je “sound shaping + modulation”.

To znači da se DL-50 više liči na custom analog + digital hybrid instrument.

---

Ovo je plan za dalje proširenje projekta i predstavlja prirodan sljedeći korak nakon Nivo 1.
