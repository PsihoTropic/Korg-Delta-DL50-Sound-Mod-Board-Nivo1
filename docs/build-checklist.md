# Build checklist - Nivo 1

Ovaj dokument predstavlja korak po korak checklist za izgradnju Nivo 1 sound mod board-a.

## 1. Faza 1 - Planiranje

- [ ] Odredi da li ćeš raditi external insert ili internal insert pre filtera
- [ ] Potvrdi da ćeš koristiti signal prije VCF-a
- [ ] Odaberi op-amp tip: TL072 ili NE5532
- [ ] Odaberi prototipni format: perfboard / breadboard / PCB
- [ ] Pripremi power supply i DC connector

## 2. Faza 2 - Prototip na breadboard-u

- [ ] Poveži power rails
- [ ] Dodaj decoupling kondenzatore 100nF + 10uF
- [ ] Testiraj ulazni buffer
- [ ] Testiraj drive stage bez clipping
- [ ] Dodaj diode clipping
- [ ] Proveri output amplitude
- [ ] Proveri da li ima DC offset

## 3. Faza 3 - Tone i mix test

- [ ] Dodaj tone stage
- [ ] Proveri dark / bright karakter
- [ ] Poveži mix stage
- [ ] Proveri dry/wet balans
- [ ] Zabilježi 3-5 raznih postavki

## 4. Faza 4 - Signal verification

- [ ] Mjeri input signal sa multimetrom
- [ ] Mjeri output signal sa multimetrom
- [ ] Proveri da li postoji šum
- [ ] Proveri da li postoji hum
- [ ] Proveri da li output level odgovara DL-50 filter input-u

## 5. Faza 5 - PCB / enclosure

- [ ] Napravi finalni PCB ili perfboard layout
- [ ] Oznaci front panel: Drive / Tone / Mix
- [ ] Poveži jacke i power connector
- [ ] Instaliraj u enclosure
- [ ] Dodaj GND / earth point ako je potrebno

## 6. Faza 6 - Final test

- [ ] Bypass test
- [ ] Mild drive test
- [ ] Mid drive test
- [ ] High drive test
- [ ] Provjeri filter efekat sa izabranim signalom
- [ ] Snimi ili zapiši najbolji preset

## 7. Faza 7 - Prihvatljivi rezultati

- [ ] signal ne distorzira neprirodno
- [ ] nema neobjašnjivog šuma
- [ ] nema DC offset-a
- [ ] gain je kontrolisan
- [ ] tone i mix se ponašaju stabilno

## 8. Recommended start settings

- Drive: 25%
- Tone: 50%
- Mix: 40%

## 9. Zapis rezultata

- [ ] Napiši koji preset radi najbolje za pad
- [ ] Napiši koji preset radi najbolje za lead
- [ ] Napiši koji preset radi najbolje za bass

---

Ovo je praktični checklist za održavanje konsistentnog razvoja Nivo 1 projekta.
