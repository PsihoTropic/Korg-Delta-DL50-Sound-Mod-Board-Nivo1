# Insert point guide - Korg DELTA DL-50

Ovaj dokument opisuje kako pronaći tačnu tačku umetanja (insert point) za Nivo 1 sound mod board. Cilj je da modul bude ubačen pre analognog filtera, tako da se zvuk promeni da bi filter radio sa već "oblikovanim" signalom.

## 1. Cilj insert point-a

Umetanje treba da se napravi između:
- izlaza iz mixer / pre-filter signal stage
- ulaza u analogni filter (VCF)

U praktičnim uslovima, to znači da treba odvojiti signal na mjestu gdje VCF dobija signal koji je došao od oscilatora i mixer-a, a prije nego što taj signal podleže filteru.

## 2. Gdje tražiti signal

Na originalnoj DL-50 ploči, signal se obično nalazi u jednom od ovih tri mjesta:

1. Mixer output prije filtera
2. Buffer / summing stage nakon oscilatora-mixera
3. VCF input line ili pin na filter op-amp / active stage

## 3. Karakteristike tačke koju tražiš

Točka umetanja mora imati:
- line level signal (ne previše jak)
- signal bez visokog DC offset-a
- dovoljno visoku impedancu da ne optereti originalni signal
- stabilan analogni signal sa low noise

## 4. Kako utvrditi tačku

### Korak 1: odvoji ploču od napajanja
- Isključi instrument
- odspoji mrežu
- radite pažljivo na statičkom otporniku / grounding

### Korak 2: lociraj analogný filter
- tražiš VCF / filter stage na mainboard-u
- najčešće je to IC + kondenzatorski i otpornički paketi oko filter section

### Korak 3: pronađi signal prije njega
- u blizini filter input-a često postoji buffer / summing node
- signal iz mixer-a ide na filter input
- ta tačka je prava za insert

### Korak 4: mjeri napon
- multimetar u AC mode
- ako je promjena sporadična, koristite oscilloscope
- očekivani signal je obično u rangu 100mV - 1V AC, zavisno od postavke

## 5. Preporučeni pristup bez rizika

Najbezbedniji način je:
- prvo identifikovati filter input node
- zatim naći mjesto prije njega gdje signal još nije filtriran
- umetnuti modul između ta dva čvora

## 6. Fizičko umetanje modula

### Vrsta 1: pravi insert break
- prerezati signal liniju i spojiti ulaz i izlaz modula na ta dva mjesta
- najbolje za prototip, ako si siguran u tačku

### Vrsta 2: buffer extract / send return
- odvojiti signal preko kondenzatorskog impedansnog buffer-a
- kasnije vratiti izlaz u filter input

### Vrsta 3: external insert box
- najbezbedniji i najlakši za testiranje
- direktno zoveš line out / headphone out i vraćaš signal natrag u filter

## 7. Preporuka po sigurnosti

Za prototip preporuka je:
- koristiti external insert box
- pa tek nakon potvrde, raditi internal insert on board

To smanjuje rizik od oštećenja originalnog synth-a.

## 8. Mjere opreza

- ne probaj da ugradiš modul bez signal path dokumentacije
- ne spajaj GND sa naponom bez provjere
- ne koristi previše visok gain bez buffer stage-a
- na izlazu treba da bude nizak output impedance

## 9. Preporučena finalna konfiguracija

```text
Oscillators + Mixer
        |
        v
  [ PRE-FILTER INSERT ]
        |
        v
  [ Korg VCF / Filter ]
        |
        v
  [ VCA / Envelope ]
        |
        v
  [ Output ]
```

## 10. Napomena

Ukoliko se insert point ne zna potpuno, najbolji prijedlog je da se prvo radi external sound mod box, a tek potom internal insert i finalna integracija.

---

Iza ovog dokumenta ide i testiranje na perfboard-u. Nakon provjere signala i gain-a, moguće je razviti finalni PCB i enclosure.
