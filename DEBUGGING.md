Debugging FlameDrum
=====

## 1. Strøm

### 1.1. Er begge strømforsyninger tilsluttet? 

Sørg for at der er strøm på begge strømforsyninger, ellers virker skidtet ikke.

### 1.2. Lyser indikator-lysene?

Der sidder en grøn LED på forstærkeren som skal lyse. Derudover sidder der en grøn LED på arduinoen, som også skal lyse (den kan være svær at se, fordi selve arduinoen sidder gemt under audio-skjoldet). Hvis der mangler strøm, er det vigtigt at man finder ud af hvorfor. Tjek eventuelt næste punkt og se om det hjælper.

Prøv eventuelt også at tænde og slukke strømforsyningerne hvis der mangler indikator-lys.

### 1.3. Kører blæseren? 

Hvis blæseren ikke kører mangler der strøm fra mindst en af strømforsyningerne. Husk at den ene strømforsyning har en knap, som skal tændes. Knappen er monteret for enden af nogle af strømforsyningsledningerne. Led lidt efter den i ledningsrodet, og tryk den. Hvis blæseren så virker skulle alt være godt.

### 1.4. Er forbindelsen til flammekasteren afbrudt?

Der sidder en afbryder på forbindelsen mellem flammekasteren og boksen. Sørg for at den er tændt. Forbindelsen er ikke monteret korrekt i kassen. Sørg for at begge ledninger fra flammekasteren har god forbindelse til de to relevante ledninger i kassen (den ledning går fra elektronikken, og den anden er en blå eller gul ledning fra strømforsyningen). Sørg eventuelt for at montere to samlemuffer.

## 2. Fejlfinding

### 2.1. Virker audio-skjoldet?

Man kan teste om trommerne virker ved at tilslutte sin computer til Arduinoen. Hent og installer det gratis Arduino-program, og forbind computeren til arduinoen med et USB-kabel. Når arduinoen er forbundet, vælger man fra menuen Tools, Serial Monitor og indstiller den til at læse med 9600 Baud. Når du har indstillet Baud kan det nogengange være en fordel at lukke og åbne Serial Monitor igen. 

Serial Monitor giver følgende output:

    DrumFlame 0.1
    Files found:
    C4.WAV
    BB3.WAV
    G3.WAV
    F4.WAV
    E4.WAV

Skriver den noget som helst andet er der en fejl på lydskjoldet.

### 2.2. Virker forstærkeren?

Hvis der ikke kommer nogen lyd, men audioskjoldet virker, kan det være forstærkeren den er gal med. Sikr dig at indikator-LEDDEN på forstærkeren lyser. Fjern eventuelt jack-stikket fra audioskjoldet og tilslut det til en telefon eller en anden mp3-afspiller, for at sikre dig at forstærkeren virker.

### 2.3. Virker trommerne/Funky Town?

Forsøg at spille temaet til Funky Town. 

    C4 C4 Bb3 C4 G3 G3 C4 F4 (E4) C4

Tonen E4 bør spilles automatisk, hvis resten af sekvensen er indspillet rigtigt. Vent til den er afspillet, inden du trommer det afsluttende C4.

Hvis man står ligefor kassen spilles temaet som:

    Venstre Venstre Top Venstre Højre Højre Venstre Midt (vente) Venstre

Har man tilsuttet sin computer til Arduinoen, kan man følge med i sekvensen via Serial Monitor. Efterhånden som man spiller de forskellige dele af temaet, bør Serial Monitor tælle op fra 1 til 10.

Når sekvensen er spillet korrekt, for man enten at vide at: "Finally Fire", hvilket betyder at flammekasteren burde tændes i tre sekunder. Hvis man får svaret "No cake", har man været mere end 9 sekunder om at spille temaet, og skal altså begynde forfra.

Hvis der ikke tælles op fra 1 til 10, er det trommerne som det er i vejen med.

### 2.4. Virker flammetænderen?
 
Vil man teste flammetænderen, kan man uploade følgende sketch til Arduinoen. Den tænder og slukker for flammekasteren i intervaller af 3 sekunder. Hvis det ikke virker bør man tjekke strøm-forbindelsen til flammekasteren.

    void setup() {t
      Serial.begin(9600);           
      pinMode(7, OUTPUT);
    }

    void loop() {
     finale();
     delay(3000); 
    }

    /// Fires
    void finale() {
      Serial.println("fire!");
      digitalWrite(7,HIGH);
      delay(3000);
      digitalWrite(7,LOW); 
    }


