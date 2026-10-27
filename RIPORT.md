# A dékáni hivatal „működő” kapcsolati űrlapja – hibariport

Repó: https://github.com/<felhasznalo>/umfst-bh01-kapcsolati-urlap
Készítette: <név>, <csoport>

## 1. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Képernyőolvasó (pl. NVDA vagy VoiceOver) használatával az oldal megnyitásakor a magyar szöveget angol kiejtéssel olvassa fel, ami érthetetlenné teszi a tartalmat.
- **Gyökérok (melyik sor, melyik szabály sérül):** Az `index.html` 2. sorában az `<html>` gyökerelemből hiányzik a nyelvet meghatározó attribútum. Ezzel sérül a WCAG 3.1.1 (Language of Page - Oldal nyelve) szabálya.
- **Javítás (commit link, előtte/utána kódrészlet):** https://github.com/Huni98/umfst-bh01-kapcsolati-urlap/commit/4afcd2fcaacf8f2a594860820483695556980b5e
  - Előtte: `<html>`
  - Utána: `<html lang="hu">`
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** Képernyőolvasóval (javítás után már a magyar hangot és kiejtést használja) és W3C HTML validátorral.
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** WCAG 3.1.1 (Érthetőség) – A segédtechnológiák számára elengedhetetlen a dokumentum alapnyelvének megadása a helyes működéshez és a megfelelő hangmotor kiválasztásához.

## 2. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Képernyőolvasóval (pl. NVDA) a fejlécre navigálva a logónál a fájl nevét („logo.png”) olvassa fel, így a látássérült felhasználó nem tudja, mit ábrázol a kép.
- **Gyökérok (melyik sor, melyik szabály sérül):** Az `index.html` 11. sorában lévő `<img>` elemből hiányzik az `alt` attribútum. Ezzel sérül a WCAG 1.1.1 (Non-text Content - Nem szöveges tartalom) szabálya.
- **Javítás (commit link, előtte/utána kódrészlet):** https://github.com/Huni98/umfst-bh01-kapcsolati-urlap/commit/fb1889046ce9a9761080317a33b652c7549c312e
  - Előtte: `<img src="logo.png" width="120" height="40">`
  - Utána: `<img src="logo.png" alt="ÁOK Dékáni Hivatal logó" width="120" height="40">`
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** Lighthouse Accessibility audittal és képernyőolvasóval (javítás után már az alternatív szöveget olvassa fel).
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** WCAG 1.1.1 (Észlelhetőség) – Minden vizuális információt hordozó képhez kötelező értelmes szöveges alternatívát (`alt`) biztosítani.

## 3. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Képernyőolvasóval az űrlap mezőire navigálva csak a helykitöltő (placeholder) szöveg hallható. Amint a felhasználó elkezd gépelni, ez eltűnik, így a mező azonosítója elveszik, a képernyőolvasó nem tudja visszamondani, mit töltünk éppen ki.
- **Gyökérok (melyik sor, melyik szabály sérül):** Az `index.html` 17–24. soraiban az űrlapmezőkhöz nem tartoznak szemantikus `<label>` elemek, csak `placeholder`-t használnak. Ezzel sérül a WCAG 1.3.1 (Info and Relationships) és a 3.3.2 (Labels or Instructions) szabálya.
- **Javítás (commit link, előtte/utána kódrészlet):** https://github.com/Huni98/umfst-bh01-kapcsolati-urlap/commit/aabde4d92e95bc1b982adfc2ba1902b583590de8
  - Előtte: `<input type="text" name="nev" placeholder="Teljes név" required>`
  - Utána: 
    `<label for="nev">Teljes név</label>`
    `<input type="text" id="nev" name="nev" placeholder="Teljes név" required>`
    *(A többi mezőnél is ugyanígy id és for attribútumokkal kiegészítve)*
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** Képernyőolvasóval (gépelés közben és visszalépve is felolvassa a mező nevét) és Lighthouse Accessibility audittal (a "Form elements do not have associated labels" hiba megszűnt).
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** Szemantika előbb: A `placeholder` soha nem helyettesíti a `<label>` elemet! Címkék nélkül az űrlap kitöltése akadályba ütközik a képernyőolvasót használók számára.

## 4. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Mobilböngészőben az e-mail mezőbe kattintva a sima betű-billentyűzet jelenik meg a @ jelet tartalmazó kiosztás helyett, és az űrlap helytelen formátumú e-mail címet (pl. „alma”) is zokszó nélkül elfogad.
- **Gyökérok (melyik sor, melyik szabály sérül):** Az `index.html` fájlban az e-mail mezőnél `type="text"` attribútum szerepel. Ezzel sérül a HTML5 űrlap-specifikációja és a WCAG 1.3.5 (Identify Input Purpose - Beviteli cél azonosítása) ajánlása.
- **Javítás (commit link, előtte/utána kódrészlet):** https://github.com/Huni98/umfst-bh01-kapcsolati-urlap/commit/f4688dba708b354395db7df9bb7f7743d4d42cab
  - Előtte: `<input type="text" id="email" name="email" placeholder="E-mail cím" required>`
  - Utána: `<input type="email" id="email" name="email" placeholder="E-mail cím" required>`
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** Mobilos nézetben (megjelenik a megfelelő e-mail billentyűzet), illetve böngészőben hibás adat megadásával (a beépített HTML5 validáció bejelez és megakadályozza a küldést).
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** Szemantika előbb: Mindig a legspecifikusabb HTML5 űrlapmező-típust (`type="email"`) kell használni a jobb felhasználói élmény (mobilos billentyűzet) és az automatikus kliensoldali validáció kihasználása érdekében.

## 5. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Billentyűzettel (Tab) történő navigáció során a Küldés gombra kétszer kell lépni, hogy átugorjunk rajta, emellett a W3C validátor futtatásakor szerkezeti hibát kapunk a form utolsó sorainál.
- **Gyökérok (melyik sor, melyik szabály sérül):** Az `index.html` 25. sorában egy `<button>` elem van beágyazva egy `<a>` link elembe. A HTML specifikáció tiltja az interaktív elemek egymásba ágyazását, emiatt a böngésző mindkét elemet fókuszálhatónak látja. Sérül a W3C szabvány és a WCAG 4.1.2 (Name, Role, Value) kritérium is.
- **Javítás (commit link, előtte/utána kódrészlet):** https://github.com/Huni98/umfst-bh01-kapcsolati-urlap/commit/4c3b3eb12b8c1ed940f7ae89fded4e8048dcc11b
  - Előtte: `<a href="#"><button>Küldés</button></a>`
  - Utána: `<button type="submit">Küldés</button>`
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** W3C HTML validátorral (a szintaktikai hiba megszűnt) és billentyűzetes Tab-bejárással (a gomb már csak egyszer kap fókuszt).
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** Szemantika előbb: Interaktív elemeket sosem ágyazunk egymásba. Egy űrlap beküldéséhez a legtisztább és szabványos megoldás a `<button type="submit">` használata.

## 6. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Az oldal megnyitásakor a főcím („Kapcsolatfelvétel”) fekete marad ahelyett, hogy zöld színnel jelenne meg.
- **Gyökérok (melyik sor, melyik szabály sérül):** A `style.css` 3. sorában a szín megadásánál elírás (brit angol írásmód) történt: `colour` szerepel a szabványos `color` helyett. A CSS motor nem ismeri fel ezt a tulajdonságot, így eldobja a szabályt.
- **Javítás (commit link, előtte/utána kódrészlet):** https://github.com/Huni98/umfst-bh01-kapcsolati-urlap/commit/33dc9a2e876ec311c9743743880982686c34b986
  - Előtte: `.cim { colour: #0e7c66; font-size: 2rem; }`
  - Utána: `.cim { color: #0e7c66; font-size: 2rem; }`
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** W3C CSS validátorral (nincs már szintaktikai hiba) és a böngésző megtekintésével (a cím vizuálisan zöld színűvé vált).
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** CSS szintaxis pontossága. A CSS tulajdonságokat szigorúan a szabványos (többnyire amerikai angol) elnevezésekkel kell használni.

## 7. hiba
- **Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia):** Billentyűzettel (Tab) történő navigáció során egyáltalán nem látható, hogy éppen melyik beviteli mezőn vagy gombon áll a fókusz.
- **Gyökérok (melyik sor, melyik szabály sérül):** A `style.css` 6. sorában az `outline: none;` tulajdonság eltávolítja az alapértelmezett böngészős fókuszkeretet úgy, hogy nincs helyette más egyedi vizuális jelzés beállítva. Ezzel sérül a WCAG 2.4.7 (Focus Visible) kritérium.
- **Javítás (commit link, előtte/utána kódrészlet):** https://github.com/Huni98/umfst-bh01-kapcsolati-urlap/commit/a127a8e6392469cfeddd4c6614ea737ff02d1e13
  - Előtte: `input:focus, select:focus, textarea:focus, button:focus { outline: none; }`
  - Utána: 
    ```css
    input:focus, select:focus, textarea:focus, button:focus { 
      outline: 2px solid #0e7c66; 
      outline-offset: 2px;
    }
    ```
- **Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó):** Tab-bejárással tesztelve minden beviteli mező és a gomb is jól látható vizuális fókuszkeretet kap. A Lighthouse Accessibility auditja nem jelez hibát a hiányzó fókuszstílus miatt.
- **Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium):** WCAG 2.4.7 (Kezelhetőség) – Sose távolítsuk el az `outline`-t úgy, hogy nem biztosítunk helyette jól látható, akadálymentes alternatív fókuszkijelölést a billentyűzettel navigáló felhasználók számára.

## Összegzés
- **Mit tanultam:** Az akadálymentes webfejlesztés (a11y) alapja a helyes HTML szemantika. A vizuális megjelenés önmagában nem garantálja a használhatóságot; kötelező a megfelelő attribútumok (`lang`, `alt`, `type`), a logikai felépítés (`label` és `input` összekapcsolása), valamint a billentyűzetes navigáció (látható fókusz) biztosítása, hogy az oldal minden felhasználó és segédtechnológia számára maradéktalanul elérhető legyen.
- **Melyik alapelv sérült a leggyakrabban:** A „Szemantika előbb, stílus később” alapelv, illetve az ehhez szorosan kapcsolódó WCAG akadálymentességi irányelvek. A hibák túlnyomó része (címkék hiánya, nem megfelelő input típus, interaktív elemek egymásba ágyazása, fókusz eltávolítása, hiányzó alternatív szöveg) abból fakadt, hogy a kód mellőzte a szabványos jelentéstartalmat és a hozzáférhetőségi szabályokat.
