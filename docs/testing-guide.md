# Testing guide - Nivo 1

Ovaj dokument opisuje kako testirati Nivo 1 sound mod board da bi se potvrdilo da signal radi ispravno i da nema neželjenih efekata kao šum, DC offset ili prevelika distorzija.

## 1. Osnovni alati

- multimetar
- oscilloscope (preporučljivo)
- audio amplifier / monitor
- signal generator ili sintetizator za test
- headphone / speaker za slušanje

## 2. Test 1 - power rail validation

### Provjeri:
- da ima +VCC i GND ispravno
- da nema kratkog spoja
- da decoupling kondenzatori rade
- da op-amp i power rails nisu pregrijani

### Očekivanje:
- stabilno napajanje bez naglog pada
- nema pregrijavanja

## 3. Test 2 - bypass test

### Postavke:
- Drive = 0
- Tone = 50
- Mix = 0

### Cíl:
- da modul prođe signal bez promjene, kao bypass

### Očekivanje:
- originalni sound ostaje čist
- nema dodatnog šuma
- nema distortiona

## 4. Test 3 - drive validation

### Postavke:
- Drive = 30%
- Tone = 50%
- Mix = 50%

### Cíl:
- da se provjeri da li drive stage dodaje harmonike i da li maskira signal bez kršenja output headroom-a

### Očekivanje:
- zvuk je topao i bogat, ne “grubi”
- nema clipping bez kontrolisanog karaktera

## 5. Test 4 - tone validation

### Postavke:
- Drive = 40%
- Tone = 20%, 50%, 80%
- Mix = 50%

### Očekivanje:
- pri nižem tone signalu ton je tamniji
- pri višem tone signalu je više bright

## 6. Test 5 - mix validation

### Postavke:
- Drive = 50%
- Tone = 60%
- Mix = 0%, 50%, 100%

### Očekivanje:
- 0% = originalni signal
- 50% = balansiran
- 100% = fully processed signal

## 7. Test 6 - output validation

### Provjeri:
- output signal ne prelazi safe level za filter input
- output signal ima nisku impedancu
- nema DC offset

### Očekivanje:
- signal je audio signal, bez DC offset-a
- ima odgovarajuću amplitudu za filter input

## 8. Test 7 - final audio listening

### Provjeri u realnom korištenju:
- bass tone
- lead tone
- pad tone
- pluck / attack
- filter resonant effect

### Očekivanje:
- modul ne “uništava” originalni synth
- daje više boje i harmonika
- filter dalje radi sa dodatnim timbre-om

## 9. Common problems

### Problem: šum je previše jak
- provjeri grounding
- provjeri decoupling kondenzatore
- provjeri da li je signal path duž

### Problem: output je previše jak
- smanji drive gain
- dodaj output attenuator
- proveri load i output buffer

### Problem: signal se “puni” ili “klipa”
- proveri clipping network
- smanji drive pot
- proveri op-amp power rail

### Problem: tone ne radi kako treba
- proveri RC network values
- proveri da nema previše high-frequency gain

## 10. Final acceptance criteria

Projekt je prihvatljiv ako:
- signal prolazi bez šuma
- nema DC offset-a
- nema pregrijavanja op-amp-a
- drive radi stabilno u svim pozicijama
- tone i mix performiraju konzistentno
- finalni sound je “topliji”, ne “sranije”

---

Ovo je praktični test plan za Nivo 1 i treba ga koristiti za validaciju svih verzija modula.
