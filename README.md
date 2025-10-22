# Implemeter et Figma-design

Af Magnus Krahl

## Reflektioner


### 1. At være mindre perfektionistisk
Har lært mig den strategiske værdi i at kompletgøre projektet "barebones", i stedet for at  style hvert element til perfektion. Det var dette jeg havde gjort, og på trods af en ret god forside, så mangler resten af siderne.

### 2. DOM-elementer som målestokke
Har lært at bruge DOM-elementer som målestokke, ie. at intoducere elementer kun for at måle en dynamisk bredde (defineret i CSS) i JS. Eksempel:
```html
<!-- Fra FinancialProjections.astro: -->

  <div class="measurestick"></div>
  <div class="measurestickInner"></div>
```
Disse div'er bliver automatisk sat ind i det dynamiske grid-system `--padGrid:` som er defineret i `global.css`:
```css
/*Fra Global.css:*/

  --outerPadding: minmax(20px, 0.3fr);
  --padGrid: var(--outerPadding) 1fr 1fr var(--outerPadding);
```

`.measurestick` og `.measurestickInner` bliver derefter tilgængelige i JS, for at måle de nuværende bredder af kolonnerne i `--padGrid`:
```javascript
// I <script /> delen af FinancialProjections.astro:

  const measurestick = document.querySelector(".measurestick") as HTMLElement;
  const innerMeasurestick = document.querySelector(
    ".measurestickInner"
  ) as HTMLElement;  
```
Og her ses "målestok"-div'erne anvendt:
```javascript
// I <script /> delen af FinancialProjections.astro:

  function applyEntryWidth() {
    //hvis vindue bredde er mindre end 660:
    marginToApply = measurestick.clientWidth;
    let widthToApply;

    if (window.innerWidth < 660) {
      widthToApply = innerMeasurestick.clientWidth * 2;
      scroller.style.gap = marginToApply + "px";
      setNavPosition();
    } else if (window.innerWidth < 880) {
      widthToApply = innerMeasurestick.clientWidth;
      scroller.style.removeProperty("gap");
    } else {
      widthToApply = (innerMeasurestick.clientWidth * 2) / 3;
      scroller.style.removeProperty("gap");
    }

    projectEntries.forEach((projectEntry, i) => {
      projectEntry.style.width = widthToApply + "px"; //sætter bredden til alle elementer
      projectEntry.style.marginLeft = i === 0 ? marginToApply + "px" : "0"; //hvis entry er
      //den første sættes marginToApply til venstres
      projectEntry.style.marginRight =
        i === projectEntries.length - 1 ? marginToApply + "px" : "0";
      //hvis entry er længden - 1 (det sidste) sættes marginToApply til højre

      projectEntry.addEventListener("click", () => toggleActiveEntry(i));
    });
  }

```

## Tekniske problemer
Har desuden haft nogle tekniske problemer som har forhindret mig i at færdiggøre mere af opgaven.

### 1. Problemer med min hjemmecomputer
Min IDE (VSCodium på Linux) har haft en mærkelig tendens til at afinstallere sig selv, og når geninstalleret, har medført stort besvær i at få npm til at virke. En anden gang døde internettet i vores bygning. I begge tilfælde har jeg været tvunget til at bruge min bærbare (VSCode på Windows), hvilket har medført sine egne problemer:

### 2. Utrolig langsomhed på min bærbar
Det har været nær umuligt at bruge min bærbare, da den er så langsom, at det vitterligt tager en evighed at få genindlæst siden for at checke min nye kode. Ikke kun det, men det tager cirka 15 sekunder for at indlæse den figma fil vi skulle efterligne, og så lidt ekstra for at langsomt zoome ind på den komponent jeg ønsker at arbejde med.

Disse er selvfølgelige mine egne problemer som jeg vil prioritere at løse, men har hverken haft tiden eller pengene til at gøre det mens jeg har lavet denne opgave.


