# Kennismaking SVG en Vue

## 1. Klaarzetten Vue-project
De details voor het opzetten van een Vue-project (en de nodige installaties) zien jullie in het vak Web-Expert, wij beperken ons hier tot de basis om je op gang te krijgen. We volgen hier deze gids: https://vuejs.org/guide/quick-start.html. Lees aandachtig! Sla niets over! Alle stappen staan uitgelegd, maar het is gemakkelijk om een stap te missen. Ik werk in Visual Studio Code, maar je mag een IDE naar keuze gebruiken. Meer informatie over het gebruik van Vue in VS code vind je hier: https://code.visualstudio.com/docs/nodejs/vuejs-tutorial.

Vooreerst moet je node.js geinstalleerd hebben op je machine. Normaal gezien heb je dat al gedaan in andere vakken, maar je kan node hier installeren: https://nodejs.org/en. Je kan dat controleren door in een terminal het volgende commando in te geven:

    node --version

 Gebruik het 'create' commando om een nieuw project aan te maken. Dat project krijgt zijn eigen mapje. We raden aan om dit commando uit te voeren in een folder die je speciaal aanmaakt voor dit vak. Voer het volgende commando uit:

    npm create vue@latest

Het zou kunnen dat je de vraag krijgt om een package te installeren (bijvoorbeeld creatue-vue@3.8.0). Druk op `y` om te aanvaarden.
Vervolgens moet je een projectnaam kiezen. Ik koos voor `first-svg`. Op alle opties die volgen mag je `no` selecteren.

De output vertelt ons exact wat onze volgende 3 commando's moeten zijn, dus vergeet niet die output te lezen. Het commando heeft namelijk een folder aangemaakt met daarin ons project. De naam van die folder is ook de naam van ons project (first-svg). Navigeren via de terminal doen we met `cd` (kort voor "change directory", zoals je hoort te weten), dus we navigeren naar onze projectfolder:

    cd first-svg  

Als je een leeg Vue project maakt, dan worden alle pakketten die het project nodig heeft gedocumenteerd in een manifest, maar nog niet automatisch gedownload. Dat is om de projectfolder klein te houden. Typisch, als je je werkt deelt (of instuurt voor een examen), stuur je je oplossing door zonder al die pakketten. Vue houdt zijn pakketten bij in de folder `node_modules`. Je kan die map ten allen tijden verwijderen, en dat doe je ook best voor je je werk doorstuurt. Om ons project te laten werken moeten we dus eerst het commando uitvoeren dat kijkt naar het manifest en alle pakketten ook effectief download. Dat doen we met het volgende commando:

    npm install

Dit commando zou je dus altijd moeten uitvoeren de eerste keer als je ergens een vue project krijgt, of download. Als de map `node_modules` verwijderd is, dan zal dit commmando de map opnieuw aanmaken. Dit kan overigens ook even duren. Tijd om ons project even te testen. We kunnen ons project opstarten met het volgende commando:

    npm run dev

De uitvoer ziet er dan bijvoorbeeld zo uit:

      VITE v4.5.0  ready in 405 ms

    ➜  Local:   http://localhost:5173/
    ➜  Network: use --host to expose
    ➜  press h to show help


Daar vind je het adres waar je website op draait. In dit voorbeeld is dat `http://localhost:5173/`. Open een web browser en surf naar dat adres om je website te zien. Nadat je je harde werk bewonderd heb, keer je terug naar terminal in VS code en gebruik je CTRL+C om de uitvoer stil te leggen. Bevestig met 'Y'.

Oef! Pak wat te drinken, geef jezelf een schouderklopje. Goed werk.

### Verkenning van het project
Opnieuw laten we de basis van Vue over aan andere vakken, maar hier is een snel overzicht van het project. We beginnen bij wat de gebruiker ziet en werken zo terug.

- Onder projectmap vindt je index.html. Dat is de webpagina die we zien als we het project laten runnen. Daar zie je dat de body van de html enkel bestaat uit een div met de id `app`. Waar komt die `app` vandaan?
- Onder de map src vind je App.vue, dat lijkt een goed startpunt. Bovenaan die file zie je een hoopje html tussen `<template>` tags. Dit is de html die geinjecteerd wordt in onze index.html op de plaats waar ons `app` divje staat. We zien dat onze website bestaat uit een afbeelding van het Vue-logo en een element genaamd `TheWelcome`. 
- In Vue kunnen we eigen HTML-component definiëren. We noemen dat Vue componenten. In het bestand TheWelcome.vue kan je bekijken hoe het TheWelcome element er uitziet. We kunnen dus met andere woorden zelf nieuwe HTML elementen/snippets uitvinden, definiëren en die dan hergebruiken. 

### Snoeien
Het TheWelcome componentje hebben we niet nodig. Pas de App component aan zodat de html er als volgt uitziet:

    <template>
    <header>
        
    </header>

    <main>
    </main>
    </template>

Er schiet nu niet veel meer over. Verwijder ook gerust de HelloWorld.vue, TheWelcome.vue en TheWelcomeItem bestandjes uit je project (laat de map components nog even staan). Als je nu opnieuw het project probeert te runnen met `npm run dev` krijg je de volgende foutboodschap:

    [vite] Internal server error: Failed to resolve import "./components/HelloWorld.vue" from "src\App.vue". Does the file exist?
    
Dat komt omdat de App-component nog een verwijzing heeft naar een component genaamd HelloWorld, maar die hebben we net verwijderd. De verwijzing vindt je in App.vue:

    <script setup>
    import HelloWorld from './components/HelloWorld.vue'
    import TheWelcome from './components/TheWelcome.vue'
    </script>

Daar zie je dat de App component het HelloWorld componentje wilt importeren (en TheWelcome ook). We verwijderen deze referenties. Je blijft dan over met het volgende:

    <script setup>
    </script>

Als je nu je project opnieuw opstart krijg je enkel nog een witte pagina te zien. Dat was voorlopig genoeg Vue. We kunnen nu de html van de webpagina aanpassen door het App-componentje aan te passen. We hebben dus in feite nog niets gewonnen met Vue, maar het nut van Vue zal wel snel duidelijk worden als we data gaan inlezen voor onze visualizaties. Probeer nu zelf de html aan te passen:

    <template>
    <main>
    <h1>DataViz</h1>
      <p>Ik vind Vue wel leuk, maar niet zo leuk als Blender.</p>
    </main>
    </template>

Als je het Vue project niet afgesloten had met CTRL+C dan zal de verandering ook live doorgevoerd worden op de website als je het bestandje opslaat. Dat noemen ze ook wel hot-reload of dynamic reloading. Je website zou er nu ruwweg zo moeten uitzien (de screenshot is wat ouder):

![Hello Vue!](First-Vue.PNG)

## 2. SVG
We kennen ondertussen het concept van Scalable Vector Graphics (SVG) van Illustrator. We weten dat die niet opgebouwd zijn uit statische pixels maar dat het eigenlijk berekeningen zijn op basis van primitieve vormen zoals rechthoeken, cirkels, etc. HTML 5 ondersteunt zelf ook het gebruik van SVG elementen. Je hebt dus in principe voor dit onderdeel geen Vue nodig, SVG elementen zitten standaard ingebakken in HTML. Als je bovenstaande niet gedaan hebt kan je hier meevolgen door zelf even een index.html bestandje aan te maken en rechtstreeks te werken in de body.

### Hello Circle
We starten met een cirkel, want cirkels zijn hip. Vooraleer we een cirkel kunnen tekenen moeten we echter beginnen met aan HTML te laten weten dat we SVG elementen willen toevoegen door een SVG canvas toe te voegen. Dat doen we door een SVG tag toe te voegen aan de body. Daaraan moeten we ook meteen een breedte en hoogte meegeven:

    <svg width=700 height=350>
    </svg>

Als je zonder Vue werkt kan je deze tags rechtstreeks in de body zetten. Als je meegevolgd hebt met Vue, dan zijn we nog steeds onze aanpassingen aan het maken in de App-component:

    <template>
    <main>
        <h1>DataViz</h1>
        <p>Ik vind Vue wel leuk, maar niet zo leuk als Blender.</p>

        <svg width=700 height=350>
        </svg>
    </main>
    </template>

Nu dan: Cirkel. Dat is eigenlijk heel simpel, je gebruikt een cirkel element binnen je svg groep:

    <svg width=700 height=350>
        <circle>
        </circle>
    </svg>

Helaas ga je zo nog niets kunnen zien want onze cirkel heeft nog geen afmetingen. Een cirkel heeft onder andere de volgende eigenschappen:
- cx: dit is de x-coördinaat van het middelpunt van de cirkel
- cy: dit is de y-coördinaat van het middelpunt van de cirkel
- r: dit is de straal van de cirkel

We voegen waardes voor die eigenschappen toe aan onze cirkel:

    <svg width=700 height=350>
        <circle cx=250 cy=50 r=50>
        </circle>
    </svg>

Als je nu uitvoert krijg je je eerste zwarte cirkel! Hoezee!

<svg width=700 height=100>
    <circle cx=250 cy=50 r=50>
    </circle>
</svg>

### Meer cirkels!

Breid nu zelf de bovenstaande code uit zodat je meer cirkels op je scherm krijgt:

<svg width=960 height=100>
    <circle cx=50 cy=50 fill=orange r=20 />
    <circle cx=150 cy=50 fill=orange r=5 />
    <circle cx=250 cy=50 fill=orange r=10 />
    <circle cx=350 cy=50 fill=orange r=30 />
    <circle cx=450 cy=50 fill=orange r=15 />
</svg>


Merk op: de bovenstaande code maakt gebruik van de `fill` eigenschap om de kleur van de cirkel te wijzigen.

### Het element `g`
Een veelgebruikt element voor SVG graphics in HTML 5 is het `g` element, oftewel het group element. Op zich doet dat element niet veel, vergelijkbaar met het `div` element. We kunnen het gebruiken om SVG elementen te groeperen:

    <svg width=700 height=350>
        <g>
          <circle cx=250 cy=50 r=50>
          </circle>
        </g>
    </svg>

Deze toevoeging zal niets veranderen aan je website. Maar nu kunnen we attributen toevoegen aan het groepselement zodat alle elementen binnen die groep beïnvloed worden. Zo kunnen we de hele groep 200 pixels naar rechts bewegen:

    <svg width=700 height=350>
        <g transform="translate(200, 0)">
          <circle cx=250 cy=50 r=50>
          </circle>
        </g>
    </svg>
    
Denk eraan dat ons 'canvas' maar 700 pixels breed is. Als je daar buitentreedt zal je cirkel niet, of maar gedeeltelijk, zichtbaar zijn.

### Nog meer cirkels!
Uiteindelijk gaan we dit soort SVG elementen tekenen op basis van data die we inlezen. Als we exact weten hoeveel datapunten we moeten visualiseren kunnen we de cirkels dus zo handmatig toevoegen, maar dat is geen robuuste oplossing. Bovendien weten we op voorhand niet hoeveel datapunten er zullen zijn, ofwel zijn die variabel. Het is dus nuttig om een arbitraire hoeveelheid cirkels te kunnen tekenen. Soms hebben we bijvoorbeeld 25 cirkels nodig, eentje voor elke student in de klas, of soms hebben we er misschien 200 nodig, eentje voor elke student in de richting.

Daarvoor kunnen we gebruik maken van de Vue for-lus. Met de vue for-lus willen we typisch loopen over een array van data, maar die hebben we nu nog niet. Gelukkig kunnen we ook een Vue for-lus gebruiken voor een reeks getallen. Dat ziet er dan bijvoorbeeld zo uit (je moet dit niet invullen, volg gewoon even mee):

    <span v-for="n in 10">{{ n }}</span>

Deze code zal Vue vertalen in HTML. Deze regel wordt dankzij de `v-for` 10 keer uitgevoerd (`n in 10`). N is de index. Die begint bij 1 en loopt op tot 10. Vue maakt er dus dit van:

    <span>1</span>
    <span>2</span>
    <span>3</span>
    ...
    <span>10</span>

Alles wat binnen `{{` staat wordt door Vue gezien als code, dus niet als HTML. Voor meer informatie, zie: https://vuejs.org/guide/essentials/list.html.

We tekenen opnieuw de gele cirkels. Vul in op je svg canvas::

    <circle cx=50 cy=50 fill=orange r=20 />
    <circle cx=150 cy=50 fill=orange r=5 />
    <circle cx=250 cy=50 fill=orange r=10 />
    <circle cx=350 cy=50 fill=orange r=30 />
    <circle cx=450 cy=50 fill=orange r=15 />

Voor het gemak van deze oefening zetten we eerst de straal van elk van deze cirkels gelijk:

    <circle cx=50 cy=50 fill=orange r=15 />
    <circle cx=150 cy=50 fill=orange r=15 />
    <circle cx=250 cy=50 fill=orange r=15 />
    <circle cx=350 cy=50 fill=orange r=15 />
    <circle cx=450 cy=50 fill=orange r=15 />

`cy` is altijd 50. `r` is altijd 15. `fill` is altijd `orange`. Maar `cx` verschilt per cirkel. `cx` is 50, 150, 250, 350, ... We zouden de n'de `cx` kunnen herschrijven als

    50 + (n-1) * 100

Waarbij `n` begint bij 1 en dan oploopt. Dat geeft:

    50 + (1-1) * 100 = 50 + 0 * 100 = 50

Voor de eerste cirkel, en voor de  rest:

    50 + (2-1) * 100 = 50 + 1 * 100 = 150
    50 + (3-1) * 100 = 50 + 2 * 100 = 250
    ...

Dat kunnen we vertalen naar een `v-for`! Maak ook gebruik van een `g` element voor je `v-for`. De oplossing staat hieronder, maar probeer zeker eerst zelf.

    <svg width=700 height=350>
      <g v-for="n in 5">
        <circle v-bind:cx="n*100" cy=50 r=15 fill="orange" />
      </g>
    </svg>

Waarom staat er een `v-bind` voor die `cx`? Die laat aan Vue weten dat de `cx` niet zomaar een waarde bevat, maar wel een berekende waarde: een formule. Dit is een signaal aan Vue dat dit HTML is die nog eerst onderhanden moet genomen worden en als code moet worden uitgevoerd. Je kan `v-bind:cs` ook afkorten naar `:cx`.
Het zou kunnen dat je de volgende fout tegenkomt: 

    Elements in iteration expect to have 'v-bind:key'

De uitleg voor deze fout is erg technisch maar het komt erop neer dat vue een unieke sleutel nodig heeft voor elke iteratie (elke n). Je kan dat sterk vergelijken met de primary key die je kent van relationele databases. Uiteraard is elke n al uniek, want elke n is in elke iteratie een ander getal, maar vue kan die redenering niet maken. We kunnen vue wat helpen door de volgende toevoeging:

    <svg width=700 height=350>
      <g v-for="n in 5" :key="n">
        <circle v-bind:cx="n*100" cy=50 r=15 fill="orange" />
      </g>
    </svg>

In dit geval is de key evident: n is in elke iteratie verschillend. Maar typisch itereren we over objecten, en dan is het vaak niet zo simpel voor Vue om te weten wat de unieke identifier is van elk object.

Als je moeite hebt met for-lussen, raad ik je altijd aan om die zelf eens uit te schrijven. Met andere woorden: speel zelf eens Vue: verwijder de for-lus en schrijf elke iteratie manueel neer, zo krijg je inzicht in de werking van de for-lus.

## 3. Smiley

Tijd om eens een smiley-face zonder glimlach te maken. We maken een SVG canvas van 960x500. Vervolgens tekenen we een cirkel op (480, 250), in het midden dus. We maken weliswaar gebruik van een groep om de cirkel op die plaats te zetten, dus niet van de eigenschappen `cx` en `cy`, maar wel de `transform` eigenschap van een groep. Ten slotte maken we de cirkel geel. Als straal pakken we 245 zodat we wat marge hebben. Voorlopig ziet er dat dan uit als volgt:

    <svg width=960 height=500>
        <g transform="translate(480, 250)">
          <circle r=245 fill=yellow>
          </circle>
        </g>
    </svg>

<svg width=300 height=100>
    <g transform="translate(150, 50)">
        <circle r=45 fill=yellow>
        </circle>
    </g>
</svg>

We kunnen nog een 'stroke' toevoegen aan deze cirkel met behulp van de eigenschappen `stroke` en `stroke-width`:

    <svg width=960 height=500>
        <g transform="translate(480, 250)">
          <circle r=245 fill=yellow stroke=black stroke-width=10>
          </circle>
        </g>
    </svg>

<svg width=300 height=100>
    <g transform="translate(150, 50)">
        <circle r=45 fill=yellow stroke=black stroke-width=3>
        </circle>
    </g>
</svg>

Voordat je verder leest, probeer nu eerst eens zelf om oogjes toe te voegen. Blijf binnen hetzelfde groepselement (`g`) werken. De oplossing vind je hieronder.

    <svg width=960 height=500>
        <g transform="translate(480, 250)">
          <circle r=245 fill=yellow stroke=black stroke-width=10>
          </circle>
          <circle cx=-130 cy=-100 r=40 fill=black />
          <circle cx=130 cy=-100 r=40 fill=black />
        </g>
    </svg>

<svg width=300 height=100>
    <g transform="translate(150, 50)">
        <circle r=45 fill=yellow stroke=black stroke-width=3>
        </circle>
          <circle cx=-20 cy=-10 r=8 fill=black />
          <circle cx=20 cy=-10 r=8 fill=black />
    </g>
</svg>

Let op, bovenstaande smiley is html die rechtstreeks in dit document staat en dus op een veel kleinere afmeting is gemaakt, het is dus mogelijk dat het voorbeeld hier niet exact overeenkomt met jouw oplossing.

Probeer nu eens de smiley 3x te herhalen, eerst zonder `v-for` lus:

<svg width=300 height=100>
    <g transform="translate(50, 50)">
        <circle r=45 fill=yellow stroke=black stroke-width=3>
        </circle>
          <circle cx=-20 cy=-10 r=8 fill=black />
          <circle cx=20 cy=-10 r=8 fill=black />
    </g>
    <g transform="translate(150, 50)">
        <circle r=45 fill=yellow stroke=black stroke-width=3>
        </circle>
          <circle cx=-20 cy=-10 r=8 fill=black />
          <circle cx=20 cy=-10 r=8 fill=black />
    </g>
    <g transform="translate(250, 50)">
        <circle r=45 fill=yellow stroke=black stroke-width=3>
        </circle>
          <circle cx=-20 cy=-10 r=8 fill=black />
          <circle cx=20 cy=-10 r=8 fill=black />
    </g>
</svg>

Doe dat eerst manueel. Maak daarna gebruik van een `v-for` lus. Let op: De x- en y-coordinaat staat op dit moment binnen onze transform eigenschap:

    <g transform="translate(50, 50)">

Helaas is het niet voldoende om dit te doen:

    <g v-bind:transform="translate(50 + n *100, cy)">

Als `n` onze lusvariabele is. (De `v-bind:` is nodig om vue te laten weten dat we in dit attribuut code hebben gestoken. Je kan die, zoals in het vorige voorbeeld ook afkorten tot `:`).

De waarde van transform is namelijk een string (=tekst): `'translate(50, 50)'`. Als we daar rechtstreeks n inzetten wordt die geinterpreteerd als tekst. We gaan daarom de tekst opdelen. In javascript kan je tekst 'optellen' om die aan elkaar te hangen. Dus `'translate(150, 50)'` is hetzelfde als `'translate(' + '150, 50)'` of `'translate(' + 150 + ', ' + 50 + ')'`. Om de interpretatie als tekst te mijden schrijven we dus: `'translate(' + (50 + n * 100) + ', 50')'`. Je kan ook gebruik maken van javascript template literals voor kortere notate (zie: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals). Dat ziet er dan zo uit:

    <g :transform="`translate(${50 + n *100}, 50)`">

Wat is nu de smiley in dit geval? Dat is het `g` element, en de x- en y-coördinaat van de smiley staat in de transform eigenschap van die groep. Dit is de code van bovenstaand voorbeeld (met `v-for`):

    <svg width=700 height=350>
      <g v-for="n in 3" :key="n">
        <g :transform="`translate(${50 + (n-1) *100}, 50)`">
            <circle r=45 fill=yellow stroke=black stroke-width=3>
            </circle>
              <circle cx=-20 cy=-10 r=8 fill=black />
              <circle cx=20 cy=-10 r=8 fill=black />
        </g>
      </g>
    </svg>

En wat als ik nu een kleine smiley wil, een middelgrote en een grote? Probeer zelf eens te spelen met de waardes om dat voor elkaar te krijgen.

<svg width=300 height=100>
    <g transform="translate(50, 50)">
        <circle r=20 fill=yellow stroke=black stroke-width=1>
        </circle>
          <circle cx=-8 cy=-5 r=4 fill=black />
          <circle cx=8 cy=-5 r=4 fill=black />
    </g>
    <g transform="translate(150, 50)">
        <circle r=35 fill=yellow stroke=black stroke-width=2>
        </circle>
          <circle cx=-15 cy=-8 r=6 fill=black />
          <circle cx=15 cy=-8 r=6 fill=black />
    </g>
    <g transform="translate(250, 50)">
        <circle r=45 fill=yellow stroke=black stroke-width=3>
        </circle>
          <circle cx=-20 cy=-10 r=8 fill=black />
          <circle cx=20 cy=-10 r=8 fill=black />
    </g>
</svg>

Waarom zijn we dit aan het doen? Omdat we graag SVG elementen willen aanpassen op basis van data die we inlezen. Denk bijvoorbeeld aan een bar-chart waarbij we rechthoeken hoger of korter maken op basis van data. In datavisualisatie werken we dus vaak met dezelfde SVG elemenen die we willen aanpassen met kleine waardes. We hebben gelukkig een framework dat ons daarbij kan helpen. Welkom terug, Vue!

## 4. Vue Componenten
Met Vue kunnen we eigen html-componenten definiëren. Dat betekent dat we eigenlijk willen dat onze html er ruwweg als volgt uiziet:

    <svg>
        <face> ... </face>
        <face> ... </face>
        <face> ... </face>
    </svg>

of:

    <svg>
        <g v-for="...">
            <face>...</face>
        </g>
    </svg>

idealiter kunnen we dan ook nog eigenschappen meegeven om de gezichtjes onderling aanpasbaar te maken:

    <svg>
        <face cx=150 cy=0 r=20> ... </face>
        ...

### Face.vue
Maak in de map components een nieuw bestandje aan: `Face.vue`. Als je kijkt naar App.vue, dan kan je zien dat zo een Vue component bestaat uit 3 onderdelen:

- template
- script
- style

Er zijn er nog meer dan dat en we hebben ze niet allemaal nodig. Onder template staat de html voor de component. We kunnen daar dus de html copy-pasten van onze smiley (vergeet die wel niet tussen de `template` tags te steken):

    <template>
        <g transform="translate(150, 50)">
            <circle r=45 fill=yellow stroke=black stroke-width=3>
            </circle>
            <circle cx=-20 cy=-10 r=8 fill=black />
            <circle cx=20 cy=-10 r=8 fill=black />
        </g>
    </template>

`script` gaan we zo dadelijk nodig hebben, maar voorlopig kunnen we dat nog leeg laten:

    <script setup>
    </script>


Het laatste onderdeel, `style`, is voor css en hebben we hier niet nodig.

Alles wat we nu gedaan hebben heeft geen enkele invloed op onze webpagina. Dat komt omdat alle html code voor onze pagina nog steeds in `App.vue` staat. Tijd om onze gloednieuwe `Face` component te gebruiken. 

Toen we ons project voor het eerst opstartten gebruikte `App.vue` al een andere component: `HelloWorld.vue`. Dat zag er toen zo uit:

    <script setup>
    import HelloWorld from './components/HelloWorld.vue'
    import TheWelcome from './components/TheWelcome.vue'
    </script>

We zien dat er dus 2 zaken nodig zijn om de `Face` component te kunnen gebruiken. Het eerste is een `import` statement, het andere is de component ook effectief gebruiken in onze html. We passen dus `App.vue` aan:

    <script setup>
    import Face from './components/Face.vue'
    </script>

Nu moeten we onze component nog gebruiken. We veranderen de inhoud van ons svg canvas:

    ...
    <svg width=960 height=500>
        <Face />  
    </svg>
    ..

Run opnieuw je project en je zal zien dat je nog steeds een smiley hebt. Misschien is dat niet zo spannend voor de doorsnee gebruiker, maar wij weten beter! De html maakt nu gebruik van een html element dat we zelf uitgevonden en gedefinieerd hebben!

## 5. Componenten & Data

We zijn al een stap verder! We hebben nu een eigen html element. Helaas kunnen we nog niet veel met dit element. De volgende HTML zal bijvoorbeeld drie gezichtjes tekenen, maar telkens op dezelfde plaats waardoor we maar 1 gezichtje zien:

    <svg width=960 height=500>
        <Face />  
        <Face />  
        <Face />  
    </svg>

### Coordinaten
Aan een cirkelelement konden we data doorgeven zoals `cx` en `fill`. Waarom zouden we dat ook niet kunnen voor ons eigen elementje? We zouden dus graag data doorgeven aan ons html element: de x-coordinaat van het gezicht. Het eerste wat we moeten doen is de code van onze Face component uitbreiden zodat die ook `props`, oftewel properties, blootstelt. Dat doen we in onze Face.vue onder onze script tags:

    <script setup>
    defineProps({
    x: {
        type: Number,
        required: true
    },
    y: {
        type: Number,
        required: true
    }
    })
    </script>

Dit zorgt ervoor dat ons html element 2 eigenschappen heeft: `x` en `y` (van het type Number, of getal) waar we een getal aan kunnen toewijzen. We hebben tegen Vue ook gezegd dat die vereist zijn (required). We kunnen daar waarden aan toewijzen op dezelfde manier als andere html eigenschappen. We passen dus `App.vue` aan als volgt:

    <template>
    <div id="app">
        <svg width=700 height=350>
            <Face x=100 y=100 />
        </svg>
    </div>
    </template>

We zijn hier iets vergeten. Vue heeft wat hulp nodig en moet weten welke eigenschappen doorgegeven moeten worden aan componenten. We moeten daarvoor een Vue directive toevoegen, dat is dus wat extra boekhouding. Gelukkig is dat heel simpel om te doen: we marken de eigenschappen met onze oude bekende: `v-bind:`.

    <template>
    <div id="app">
        <svg width=700 height=350>
            <Face v-bind:x=100 v-bind:y=100 /> 
        </svg>
    </div>
    </template>

Helaas werkt dit niet. Weet je ook waarom?

De html van ons `Face` componentje is nog altijd dezelfde. We maken nergens gebruik van de `x` en `y` eigenschappen die we hebben gedeclareerd. Met andere woorden: we hebben nu wel een `x` en `y` gegeven aan onze component, maar we hebben nog niet duidelijk gemaakt hoe die eigenschappen de html van `Face` zullen beinvloeden. Laat ons dat even aanpassen. De x- en y-coordinaat staat op dit moment binnen onze transform eigenschap:

    <g transform="translate(150, 50)">

Helaas is het niet voldoende om dit te doen:

    <g transform="translate(x, y)">

Weet je nog waarom? Probeer weer eerst even zelf. De oplossing staat hieronder:

    <template>
        <g :transform="`translate(${x}, ${y})`">
            <circle r=45 fill=yellow stroke=black stroke-width=3>
            </circle>
            <circle cx=-20 cy=-10 r=8 fill=black />
            <circle cx=20 cy=-10 r=8 fill=black />
        </g>
    </template>

Vergeet niet de `:` of `v-bind:` voor de transform. Samengevat: elke keer als Vue ziet dat er een `Face` html element wordt gebruikt, zal Vue daar de html copy-pasten die tussen de `template` tags staat in Face.vue. Vue weet ook dat Face 2 attributen heeft: `x` en `y`. Als er in die geplakte html ergens de `x` of `y` voorkomt, zal die vervangen worden door wat er bij het `Face` elementje is meegegeven.

### Andere properties

Tijd om een versnelling hoger te schakelen. We gaan nog extra properties toevoegen aan Face:

    <script setup>
    defineProps({
    x: {
        type: Number,
        required: true
    },
    y: {
        type: Number,
        required: true
    },
    r: {
        type: Number,
        required: true
    },
    strokeWidth: {
        type: Number,
        required: true
    },
    eyeOffsetX: {
        type: Number,
        required: true
    },
    eyeOffsetY: {
        type: Number,
        required: true
    },
    eyeRadius: {
        type: Number,
        required: true
    }
    })
    </script>

We gebruiken die properties ook op de gepaste manier in de html van onze Face-component:

    <template>
        <g :transform="`translate(${x}, ${y})`">
            <circle :r=r fill=yellow stroke=black :stroke-width=stroke-width>
            </circle>
            <circle :cx=-eyeOffsetX :cy=-eyeOffsetY :r=eyeRadius fill=black />
            <circle :cx=eyeOffsetX :cy=-eyeOffsetY :r=eyeRadius fill=black />
        </g>
    </template>

Let op de `:` (de afgekorte variant van `v-bind:`)!

Ten slotte geven we de correcte waardes door vanaf `App.vue`:

    <template>
    <div id="app">
        <svg width=700 height=350>
        <Face 
            v-bind:x=50 
            v-bind:y=150
            v-bind:stroke-width=3
            v-bind:eyeOffsetX=20
            v-bind:eyeOffsetY=10
            v-bind:eyeRadius=8
            v-bind:r=45
            /> 
        </svg>
    </div>
    </template>

Hier gebruiken we opnieuw `v-bind` in de plaats van `:`, daar is geen specifieke reden voor. Denk eraan dat je die uitwisselbaar kan gebruiken, dus `:` was even goed.

We kunnen nu gemakkelijker bijvoorbeeld 3 gezichten naast elkaar zetten. Probeer het eerst zo. Maak daarna gebruik van een `v-for`. De oplossing met `v-for` vind je hieronder, maar probeer het eerst zelf!


    <svg width=700 height=350>
      <g v-for="n in 3">
        <Face 
          v-bind:x="50 + (n-1) * 100"
          v-bind:y=150
          v-bind:stroke-width=3
          v-bind:eyeOffsetX=20
          v-bind:eyeOffsetY=10
          v-bind:eyeRadius=8
          v-bind:r=45
          />
      </g>
    </svg>

Let op:
Je kan een property binnen je component gebruiken als volgt: `cx=-eyeOffsetX` maar je kan die eveneens tussen `""` zetten: `cx="-eyeOffsetX"`. Nu komt de verwarring: we hadden toch net moeite met die `""` bij het gebruik van transform? Dat komt omdat transform een string verwacht en vue ook net graag die " voor expressies. Zo kan je bijvoorbeeld schrijven: `cx="50 + eyeOffsetX/2"`. Dat conflicteert soms, zoals het geval is bij de transform, en dan moeten we andere oplossingen zoeken zoals de string opdelen.

## 6. Uitdaging
Probeer hier nu een paar stapjes in verder te gaan. 

- Begin eens met het toevoegen van een `Eye` component die dan gebruikt wordt door de `Face` component die we gemaakt hebben.
- Maak een rij van gezichtjes, allemaal met een andere afmetingen en oogjes, met behulp van een `v-for`.