# Tvořím web A–Z: lekce 9

Jaro 2021, Praha

<small>11. května 2021</small>

---

# Podklady

https://github.com/tvorimweb-2021-praha-jaro/lekce_09

---

# Dnešní cíle

- Seznámit se s možnostmi připojení CSS do stránky a pravidly CSS specificity
- Zopakovat základní CSS selektory a představit další pokročilejší
- Naučit se práci se základními CSS pseudoelementy

# Způsoby připojení CSS

Zatím jsme se seznámili s připojením CSS jako externího souboru pomocí značky `link`. Je to asi nejběžnější způsob a v mnoha ohledech nejvýhodnější, ale je dobré znát i ostatní možnosti, protože i ty mají své použití. A přinejmenším se s nimi můžete setkat na jiných projektech.

1. externí soubor nebo více souborů CSS pomocí tagu `link`
   Známe již celkem důvěrně, pouze poznamenáme, že lze takto připojit i více souborů CSS (jeden pro obecné styly písma a barev, další pro konkrétní stránku), aby se zbytečně nestahovaly styly, které se na stránce nepoužijí.

   ```html
   <link rel="stylesheet" href="/styles/typography.css" />
   <link rel="stylesheet" href="/styles/contact.css" />
   ```

2. přímo v HTML prostřednictvím značky `style`
   Párová značka `style` vlastně vyznačí místo v HTML dokumentu, kam lze psát CSS. Takový to blok CSS kódu lze umístit kamkoli do dokumentu, včetně prvku `head`, což je nejběžnější užití toho zápisu. Zapisují se do něho například styly, které chceme mít na stránce vykresleny okamžitě (bez nutnosti čekat na načtení velkého souboru CSS), ale to již spíše zastaralý způsob.

   ```html
   <style>
     /* CSS komentář */
     body {
       max-width: 1600px;
     }

     p {
       margin-bottom: 1rem;
     }
   </style>
   ```

3. tzv. inline styly, přímo do otvírací značky prostřednictvím atributu `style`
   Někdy nemáme možnost zasáhnout do kódu jinak než tímto způsobem. Nejčastěji jsme k tomu nuceni při úpravě obsahu stránky přes nějaký redakční systém. Dále se tento způsob využívá při tvorbě HTML e-mailů.

   ```html
   <p style="max-width: 20rem; color: silver;">
     Text odstavce s maximální šířkou 20 rem a šedou barvou písma.
   </p>
   ```

4. pomocí jazyka JavaScript
   Uvádíme pouze pro úplnost, protože s JavaScriptem jsme se dosud nesetkali.

Pozor, poslední dva způsoby nemohou využít plnou škálu možnosti CSS (například nezapíšete stavové styly pro `:hover` či `:focus`).

note:

- předvedeme si v kódu

---

# Selektory

Existuje více jak 30 různých CSS selekterů a nespočet dalších možností, jak je kombinovat.

note:

- https://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048

---

## Pomocí názvů tagů

- prostý název HTML tagu (v CSS bez špičatých závorek!)

```css
/* odstavce vypiš tučně */

p {
  font-weight: bold;
}
```

note:

- vícenásobný selektor: tatáž pravidla se přiřadí více prvkům naráz
- zvolené prvky oddělujeme čárkou
- píšeme jeden selektor na řádek (kvůli přehlednosti)

---

## Několikanásobný selektor

```css
/* nadpisy 1.‒4 úrovně vypiš karmínovou */

h1,
h2,
h3,
h4 {
  color: crimson;
}
```

---

## Kontextový selektor

- vyjadřuje strukturu HTML

```css
footer p {
  color: white;
}
```

note:

- odstavce uvnitř patičky
- selektory čteme zprava doleva
- footer > p

---

## Třídy

- název třídy (začíná tečkou, aby se odlišil od názvu prvku)

```css
/* prvky s třídou .perex vypiš kurzívou */

.perex {
  font-style: italic;
}
```

note:

- jednu třídu může mít více prvků, bez ohledu na jejich typ
- jeden prvek může mít více tříd, na pořadí tříd v HTML nezáleží

---

## ~~Identifikátory~~ – nepoužíváme

```css
/* Tohle nedělejte! */
#navbar {
  background-color: #000;
}
```

note:

- uvádíme pro úplnost
- nepraktické, příliš vysoká specificita => `id` se omezuje na jediný prvek na stránce
- specificita vysvětlena níže

---

## Pomocí atributů

- prvek s&nbsp;konkrétním atributem

```css
/* prvkům (tedy obrázkům) s atributem `alt` přidej spodní ohraničení */
[alt] {
  border: 1px solid silver;
}
```

---

## Prvek s určitou hodnotou atributu

- prvek s&nbsp;konkrétní hodnotou atributu

```css
/* obrázky s prázdným atributem `alt` orámuj karmínově */
[alt=""] {
  border-color: crimson;
}
```

note:

- lze ještě obměňovat, např. hodnota atributu začínající/končící na konkrétní text apod. => samostudium

---

# Pseudotřídy

`:first-child`, `:last-child`, `:nth-child()`, `:nth-of-type()`, ...

---

## Pseudotřídy - `:first-child`, `:last-child`

```css=
/* První potomek elementu */
div:first-child {}

/* Poslední potomek elementu */
div:last-child {}
```

---

## Pseudotřídy - `:nth-child`

```css=
/* pravidlo platí pro druhou položku seznamu */
li:nth-child(2) {}

/* pravidlo platí pro každou třetí položku */
li:nth-child(3n) {}

/* jako předchozí, ale začíná se u druhé položky */
li:nth-child(3n + 2) {}
```

---

# Pseudoelementy

- `::first-line`, `::first-letter`
  - lze stylovat pouze font, styl textu, pozadí, margin, padding a border
- `::after`, `::before`
  - lze stylovat vše
- `::selection`
  - lze stylovat pouze color, background-color, text-decoration a pár dalších

---

# Pseudoelementy - `::before`, `::after`

```css=
div::before { content: 'Před'; }

div::after { content: 'Za'; }
```

```htmlmixed=
<div>
  Před
  <!-- Vše ostatní co bylo v divu předtím -->
  Za
</div>
```

---

# Pseudoelementy - Co můžu použít v `content`?

```css=
div::before { content: 'Text'; }

div::before { content: 'url(/cesta/k/obrazek.jpg)'; }

/* Nic, pro obrázková pozadí*/
div::before { content: ''; }

div::before { content: "<h1>Toto nejde!</h1>"; }
```

# Dědičnost

> Dědičnost v CSS je způsob, jakým se dostávají hodnoty vlastností od rodičovských elementů k potomkům.

<small>Martin Michálek, [Vzhůru Dolů](https://www.vzhurudolu.cz/prirucka/css-dedicnost)</small>

note:

- platí jen pro menšinu vlastností
- vlastnosti týkající se textu (začínají na `font-`)
- Máchal: táta českých frontendistů
- od něj jsem čerpal (kopíroval) pro další výklad
- ve sporu s kaskádou vždy prohraje, kaskáda je silnější

---

# Kaskáda

note:

- 3 principy: pořadí, specificita, důležitost

---

## Kaskáda - pořadí

1. Pořadí rozhoduje a poslední vyhraje

```css=

p {
    color: crimson;
}

p {
    color: cornflowerblue;
}

```

note:

- Kdo se směje naposled, ten se směje nejlíp.
- Ale to je spíš vzácnější případ.

---

## Kaskáda - specificita

2. Selektor s vyšší váhou (specifitou) vyhrává.

```css=

section p {
    color: crimson;
}

p {
    color: cornflowerblue;
}

```

note:

- čím konkrétněji je popsán prvek, tím má pravidlo vyšší váhu
- čím konkrétněji ~ čím vyšší specificita
- ukážeme si ve cvičení 3

---

# Specificita

Specificita je hodnota, která vyjadřuje přesnost zacílení daného selektoru (má číselnou hodnotu, více o tom v&nbsp;[článku Smashing Magazine](https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/#specificity-examples-test-yourself)).

**Pamatuj si, že pravidlo se vyšší specificitou se uplatní bez ohledu na pořadí v&nbsp;kódu.** Teprve střetnou-li se stejně „silná“ pravidla, vítězí to, které je ve stylopise později.

Porovnání se skutečným světem:

**vyndej** | cokoli | svetr | svetr ze skříně | její svetr ze skříně | její vytahaný svetr ze skříně\*

**selektor** | `*` | `li` | `ul li` | `ul .nav-item` | `.nav > .nav-item`

<small>\* Jedná se o příměr, ber s&nbsp;rezervou</small>

## Zanoření prvku

- naznačíme mezerou

```css
/* seznamu v navigaci (neplatí pro ostatní seznamy) odeber odrážky */

nav ul {
  list-style: none;
}

/* odkazy uvnitř prvků s&nbsp;třídou .perex (a jenom tam) vypiš chrpovou */

.perex a {
  color: cornflowerblue;
}
```

## Přímý potomek

- předchozí pravdla lze zpřesnit (dát jim vyšší specificitu)

```css
/* odrážky se odeberou jen na první úrovni navigace odrážek, na zanořený seznam se pravidlo nevztahuje */

nav > ul {
  list-style-type: square;
}
```

```html
<!-- Novinky a Starosti bez odrážek, ročníky s odrážkou -->
<nav>
  <ul>
    <li><a href="novinky.html">Novinky</a></li>
    <li>
      <a href="starosti.html">Starosti</a>
      <ul>
        <li><a href="2017">2017</a></li>
        <li><a href="2016">2016</a></li>
        <li><a href="2015">2015</a></li>
      </ul>
    </li>
  </ul>
</nav>
```

Jiný příklad

```css
/* odkazy uvnitř prvků s třídou .perex, které jsou jeho přímým potomkem vypiš kaštanovou */

.perex > a {
  color: maroon;
}
```

```html
<div class="perex">
  <p>Text odstavce <a href="#">odkaz na zajímavý zdroj</a>, další text</p>
  <a href="#">odkaz na celý článek</a
  ><!-- tento odkaz bude kaštanovou barvou, předchozí odkaz ne -->
</div>
```

## Vícenásobné třídy nám umožní přesnější zacílení

- používat s&nbsp;rozumem, pokud nás prosazení pravidla nutí řadit více než tři třídy, bude vhodnější přidat třídu novou

```css
/* .perex, který má současně třídu .main vykresli se slonovinovým pozadím */

.perex.main {
  background-color: ivory;
}
```

- předchozí zápis podbarví tento prvek:

```html
<p class="perex main">Úvodní odstavec nějakého článku…</p>
```

- [Specificity calculator](https://specificity.keegan.st)
- [Specificity with Fish](https://specifishity.com)
- [CSS specificity Wars](https://stuffandnonsense.co.uk/archives/css_specificity_wars.html)

---

## Kaskáda - důležitost

3. pravidlo označené jako důležité, vyhraje vždy

```css
p {
  font-size: 1rem !important;
}
```

note:

- atomový kufřík, když jiné možnosti selžou: snažte se nepoužívat
- hrozí, že se uškvaříte v importantovém pekle
- Dá se přebít !important?
- 2 případy, kdy lze použít
  1. potřebuji přebít CSS 3. strany (plugin), do nějž nemohu zasáhnout, případně nastavuje styly pomocí JS (inline styly => nejvyšší specificita)
  2. zdědila jsem prastaré a spletité CSS, které by nejlíp bylo zahodit a napsat znova, ale na to není čas=peníze
  3. Tzv. utility třídy, viz Tachyons

---

# !Poslední! povinný domácí úkol

- Zadaný v classrooms
- Ukážeme si co je třeba

![Island](https://raw.githubusercontent.com/tvorimweb-2020-praha-podzim/du_06_island/master/zadani/vysledek-3-pc.jpg)
