# Data Arrays
In het vorige lab hebben we gezien hoe we verschillende SVG elementen kunnen tekenen met `v-for` en hoe we ons leven gemakkelijker kunnen maken met behulp van componenten. We willen nu het uiterlijk van die SVG elementen aanpassen op basis van data die we inladen. Denk bijvoorbeeld aan een bar chart per departement, waarbij de lengte van elke rechthoek bepaalt is door het aantal studenten in dat departement. De rechthoeken kunnen we al tekenen, en ook de lengte kunnen we nu aanpassen. We kunnen zelfs de rechthoek omzetten in een component. Onze data komt typisch van een file, databank of Web API, maar voor dit lab maken we gebruik van statische data. Dat betekent dat we zelf wat data gaan verzinnen en in een simpele javascript variabele gaan steken. In een volgend labo gaan we dan kijken hoe we van een file tot zo een variabele kunnen geraken. In dit labo gaan we in onze `v-for` ook loopen over objecten in de plaats van een integer `n` en gebruiken hun eigenschappen om onze SVG vorm te geven. Het helpt bijzonder veel als je weet hoe arrays en objecten werken in javascript. Als je daar moeite mee hebt, raad ik je aan om dat op voorhand eerst even te herhalen.

## 1.  Nieuw project
We starten voor dit lab opnieuw een Vue project. Dit is het laatste lab waar we dit nog overlopen. Voor alle andere labos mag je steeds een nieuw project starten op dezelfde manier. We gebruiken `vue create` in een lege folder naar keuze:

    npm create vue@latest

Als naam kies je `data-arrays`.
Vergeet niet te duiken in die nieuwe projectfolder:

    cd data-arrays

Vergeet ook niet even te controleren of je Vue project start:

    npm install
    npm run dev


## 2. Data, zegt u?

Ja. Data. Zoals jullie weten kan data in allerlei formaten voorkomen. Voor dit vak gebruiken we bijvoorbeeld vooral het .csv formaat om data voor te stellen, maar die data kan van eender welke file komen, zoals een .json file, of vaak van een database of Web API. We willen ons in dit lab echter toespitsen op de visualisatie en daarom gaan we nog niet meteen werken met een .csv bestand. We gaan daarom vandaag aan de slag met zelfverzonnen, statische data. Hoe kunnen we die voorstellen in javascript? Het meest simpele voorbeeld is een rij van getallen. Dat kan in javascript als volgt:

    data = [10, 20, 30, 40, 50]

(Je moet dit nergens invullen, volg gewoon even mee)Hier declareren we variabele `data` en we kennen daar een rij aan toe van getallen: 10, 20, 30, 40 en 50. Dat is natuurlijk al behoorlijk hip en insta-waardig, maar typisch werken we liever met een rij van objecten. Een rij van objecten ziet er bijvoorbeeld als volgt uit:

    data = [
        {
            category: 'Cat',
            value: 10
        },
        {
            category: 'Dog',
            value: 15
        },
        {
            category: 'Pig',
            value: 35
        },
        {
            category: 'Cow',
            value: 25
        }
    ]

Dit lijkt er al meer op. Nu hebben we 4 datapunten in een array gestoken (data), die elk 2 waardes bevatten: een categorie en een getal. Elk object in deze rij kan je dus bezien als de rij uit een excel tabel of een .csv bestand. Elk element uit onze data array is een rij in dat excel bestand en category en value zijn onze kolomhoofdingen. Voor dit lab gebruiken we telkens statische data, daarmee bedoelen we dat de data niet dynamisch uitgelezen wordt, maar wel "hardgecodeerd" in ons programma zit. Statisch betekent dat de data niet verandert. Typisch is dat wel zo, bijvoorbeeld bedrijven die netwerktraffiek in de smiezen houden en dat visualiseren in een dashboard. We starten zo dadelijk eenvoudig, met een rij van getallen. Als we dat onder de knieëen hebben gaan we opnieuw kijken naar een rij van objecten.

## 3. Rij van getallen
We zetten eerst een statische visualisatie op en koppelen dan daarna data aan die visualisatie.

## Basisvisualisatie
We beginnen met de laatste oefening van het laatste labo:

<svg width=700 height=175>
    <g transform="translate(0, 0)">
        <rect width=20 height=100 fill=orange />
        <text x="5" y="110" fill="orange" transform="rotate(50, 5, 110)">Pigs</text>
    </g>
    <g transform="translate(30, 70)">
        <rect width=20 height=30 fill=orange />
        <text x="5" y="40" fill="orange" transform="rotate(50, 5, 40)">Cats</text>
    </g>
    <g transform="translate(60, 40)">
        <rect width=20 height=60 fill=tomato />
        <text x="5" y="70" fill="tomato" transform="rotate(50, 5, 70)">Chickens</text>
    </g>
    <g transform="translate(90, 20)">
        <rect width=20 height=80 x=0 fill=orange />
        <text x="5" y="90" fill="orange" transform="rotate(50, 5, 90)">Dogs</text>
    </g>
</svg>

De oplossing (zonder `v-for`) daarvoor is:

    <svg width=700 height=175>
        <g transform="translate(0, 0)">
            <rect width=20 height=100 fill=orange />
            <text x="5" y="110" fill="orange" transform="rotate(50, 5, 110)">Pigs</text>
        </g>
        <g transform="translate(30, 70)">
            <rect width=20 height=30 fill=orange />
            <text x="5" y="40" fill="orange" transform="rotate(50, 5, 40)">Cats</text>
        </g>
        <g transform="translate(60, 40)">
            <rect width=20 height=60 fill=tomato />
            <text x="5" y="70" fill="tomato" transform="rotate(50, 5, 70)">Chickens</text>
        </g>
        <g transform="translate(90, 20)">
            <rect width=20 height=80 x=0 fill=orange />
            <text x="5" y="90" fill="orange" transform="rotate(50, 5, 90)">Dogs</text>
        </g>
    </svg>

Ik ga er hier vanuit dat je dit zelf in je nieuw Vue-project kan steken, en dat je ook weet waar je die code kan zetten. Als dat niet lukt, moet je het labo van de vorige les even herhalen. Ik heb ook de standaardcomponenten die meegeleverd worden in een nieuw Vue-project (TheWelcome, etc.) verwijderd.
De hoogtes van de rechthoeken zijn (van links naar rechts): `100, 30, 60` en `80`.  We willen die getallen in een array steken en werken met een `v-for`. 

### Basiscode voor App.vue
We hebben in het vorige lab gezien waar we de html en de css kunnen aanpassen voor ons Vue project (Bondig, toch. Als uitdaging: kijk eens of je de achtergrondkleur van de app kan aanpassen.). We hebben echter nog niet gezien waar we javascript code kunnen toeven. Misschien kan dat we wel gewoon tussen de `<script>` tags die we zien in `App.vue`? Laat ons dat eens proberen. Ik probeer het volgende:

    <script setup>
    console.log("Hello from App.vue");
    </script>

Start nu je applicatie en open je developer console in je browser (F12 in google chrome). We zien de boodschap verschijnen. De javascript code tussen deze tags wordt dus gewoon uitgevoerd.
Een andere optie is dat we gebruik maken van `Lifecycle hooks`. Dat is een wat complexe term maar het principe is eigenlijk simpel. Vue bestaat uit een reeks componenten (html elementen die we zelf maken, die eigen javascript hebben en eigen css). Als al die componenten tussen hun `<script>` tags code schrijven, dan moeten we ons afvragen welke code van welke component als eerste uitgevoerd zal worden. Dat is, zeker in grote applicaties, erg belangrijk. Bovendien willen we misschien code uitvoeren op bepaalde punten in het "leven" van zo een component: als een component net toegevoegd is aan onze html, als de component "sterft" (de webpagina wordt afgesloten, of we navigeren naar een andere tab waardoor de component verwijderd wordt,...), etc.
Vue biedt een aantal ingebouwde methodes aan die je zelf kan invullen zodat je code kan uitvoeren op kritieke punten in de levenscyclus van een component. De volledige lijst van die voorgekauwde methodes vindt je hier: https://vuejs.org/api/composition-api-lifecycle.html. 

Wij maken gebruik van de `onMounted()` methode. Die wordt uitgevoerd op het moment dat de component onderdeel wordt van onze html en dus getoond wordt op de webpagina. Dat kan als volgt:

    <script setup>
    import { onMounted } from 'vue';

    onMounted(() => {
    console.log("Hello from App.vue");
    })
    </script>

Deze code doet in essentie hetzelfde als de vorige, en in een kleine applicatie zoals de onze kom je weg door de code gewoon rechtstreeks tussen de `<script>` tags te zetten, maar we raden steeds aan om het op deze 'propere' manier te doen.

Let er wel op dat de functie `onMounted()` enkel wordt afgeroepen bij de start van het leven van de component, dat is dus niet de geschikte plaats voor het reageren op interacties met de gebruiker. Het is echter wel een goede plaats om eens te experimenteren met code.

Voor de rest is alles wat tussen die `<script>` tags gewoon een ruimte om javascript code te schijven. We kunnen dus ook nog extra methodes of functies declareren op onze component. Bijvoorbeeld:

    <script setup>
    import { onMounted } from 'vue';

    onMounted(() => {
    sayHello();
    })

    function sayHello()
    {
    console.log("Hello from App.vue");
    }
    </script>

Als je je trouwens afvraagt waarom die import regel daar moet staan, dat is omdat we willen aangeven dat onze `onMounted` methode de methode is die onderdeel is van het `Vue` framework. Als je die weglaat zal je code nog steeds werken, maar zal de `onMounted` functie nooit uitgevoerd worden omdat er geen plaats is waar die functie wordt aangeroepen.

Zo kunnen we dus functionaliteit toevoegen aan onze component, maar waar zit dan de data van onze component? We hebben in het vorige lab al gezien hoe we eigenschappen aan een component kunnen toevoegen met behulp van `defineProps`. Maar daar steken we liever de stukken data die van buitenaf ingevuld worden (dus vanuit de html code). Voor onze eigen, afgeschermde data die we niet willen blootstellen als een html attribuut gebruiken we simpele javascript variabelen die we gewoon tussen onze `<script>` tags zetten. We kunnen zo een variabele ook reactief maken. Denk bijvoorbeeld aan een formulier. Dat formulier bevat heel wat variabelen, zoals bijvoorbeeld een emailveld. Als dat emailveld ingevuld wordt, willen we dat die waarde ook in een variabele wordt bijgehouden. Dat concept heet databinding. Zonder databinding zou je aan je emailinputveld een stukje code moeten hangen dat uitgevoerd wordt elke keer als de waarde van dat emailveld verandert. In dat stukje coden zouden we dan onze variabele aanpassen naar de waarde die de gebruiker zonet heeft ingevuld. Parkeer die gedachte nog even, we komen daar later op terug. Voorlopig gaan we nog even verder met zuivere javascript:

    <script setup>
    import { onMounted } from 'vue';

    const myArray = [100, 30, 60, 80];
    ...


Nu hebben we een variable `myArray`, en dat is een rij van getallen. Op zich is dit nog niet zo spannend, want we gebruiken die variabele nog nergens, dus deze code zal helemaal niets zichtbaars veranderen.

### Databinding
Onze component heeft nu een stukje data! `myArray`! Wat is ie mooi! Tijd om daar gebruik van te maken. Om dit deel wat gerichter te maken verwijder ik voorlopig de labels van onze visualisatie:

    <svg width=700 height=350>
      <g transform="translate(0, 0)">
        <rect width=20 height=100 fill=orange />
      </g>
      <g transform="translate(30, 70)">
          <rect width=20 height=30 fill=orange />
      </g>
      <g transform="translate(60, 40)">
          <rect width=20 height=60 fill=tomato />
      </g>
      <g transform="translate(90, 20)">
          <rect width=20 height=80 x=0 fill=orange />
      </g>
    </svg>

<svg width=700 height=120>
    <g transform="translate(0, 0)">
    <rect width=20 height=100 fill=orange />
    </g>
    <g transform="translate(30, 70)">
        <rect width=20 height=30 fill=orange />
    </g>
    <g transform="translate(60, 40)">
        <rect width=20 height=60 fill=tomato />
    </g>
    <g transform="translate(90, 20)">
        <rect width=20 height=80 x=0 fill=orange />
    </g>
</svg>

We kunnen nu met een `v-for` loop door onze `myArray` lopen:

    <svg width=700 height=350>
      <g v-for="(number, index) in myArray" :key="index">
        <g :transform="`translate(${index * 30}, ${100-number})`">
            <rect width=20 :height=number fill=orange />
        </g>
      </g>
    </svg>

Ok - dit moeten we even uitpakken...
We beginnen met `v-for="(number, index) in myArray"`. Deze for-lus zal loopen door onze array: `myArray`. Dat betekent dat onze lus 4x uitgevoerd zal worden, want we hebben 4 getallen in onze rij staan. Daarom krijgen we 4 rechthoeken of `rect`. Wat is dan `(number, index)`? Dat is onze lusvariabele. Dit zijn variabele die enkel leven binnen onze for-lus en de waarde die daar inzit zal verschillen per iteratie. Je had ook enkel dit kunnen schrijven: `v-for="number in this.myArray"`. In dat voorbeeld zal de lus 4 ook iteraties kennen. In de eerste iteratie bevat de variabele `number` het eerste getal uit onze rij: `100`. In de tweede iteratie bevat `number` het tweede getal: `30`, enzovoort. Normaal gezien zouden we daar genoeg mee hebben, maar om de visualisatie goed te kunnen doen moeten we ook weten de <i>hoeveelste</i> rechthoek we aan het tekenen zijn, anders kunnen we de x-coordinaat van de rechthoek niet berekenen. Daarom vragen we aan Vue om naast de inhoud van de array in een variabele `number` te steken elke iteratie, om ook in een variabele bij te houden op welke iteratie we zitten. We hebben hier die variabele `index` genoemd. De namen `number` en `index` zijn zelf te kiezen. Samengevat gebeurt het volgende: Vue zal wat er tussen de for-lus staat 1x uitvoeren per waarde in `myArray`. Voor elke iteratie zullen er 2 variabele ter beschikking staan: `number` en `index`. `number` bevat een getal uit de array, en `index` bevat een getal dat begint op 0 en dan optelt per iteratie:

    1e iteratie: number = 100 en index = 0
    2e iteratie: number = 30 en index = 1
    3e iteratie: number = 60 en index = 2
    4e iteratie: number = 80 en index = 3

De rest is eigenlijk simpel. Voor elke eigenschap waar een `:` voor staat, gebruiken we deze variabele om die eigenschap te berekenen. De x-coordinaat van een rechthoek is bijvoorbeeld 0 voor de eerste rechthoek, 30 voor de tweede, 60 voor de derde, etc. Met andere woorden, de x-coordinaat is: `index * 30`. We verwerken die x-coordinaat in de `transform` eigenschap zoals we gezien hebben in het vorige lab. De y-coordinaat doet wat moeilijk omdat we rechthoeken niet netjes van linksonder beginnen te tellen qua coordinaten. Maar dat, en de rest van de code zou je nu zelf moeten kunnen ontcijferen. Durf wat experimenteren. Verander de coordinaten eens. Voeg eens een waarde of 2 toe aan `myArray` en kijk hoe je visualisatie zich automatisch aanpast. Wat gebeurt er als je waarde meer is dan 100? Waarom?

Onze visualisatie is nu gekoppeld aan data. Als we die data aanpassen, verandert ook onze visualisatie. Is dat niet tof? Ja, dat is tof.

## 4. Rij van objecten
We werken bijna nooit met een rij van getallen, maar wel met een rij van objecten. Denk eraan, een rij van objecten in javascript ziet er zo uit:

    data = [
        {
            category: 'Cat',
            value: 10
        },
        {
            category: 'Dog',
            value: 15
        },
        {
            category: 'Pig',
            value: 35
        },
        {
            category: 'Cow',
            value: 25
        }
    ]

### Databinding van eenvoudige objecten
We veranderen nu onze `myArray` in een reeks van objecten:

    ...
    const myArray = [
    {
        animal: 'Pigs',
        amount: 100
    },
    {
        animal: 'Cats',
        amount: 30
    },
    {
        animal: 'Chickens',
        amount: 60
    },
    {
        animal: 'Dogs',
        amount: 80
    }
    ];
    ...

Dit ziet er allemaal complexer uit dan het eigenlijk is. Hiervoor was een element uit onze array een getal. Zo was `myArray[1]` bijvoorbeeld `30` (denk eraan, we beginnen de index altijd te tellen vanaf 0, dus 1 is het tweede element uit de rij). Nu is `myArray[1]` een object, en dat object heeft 2 eigenschappen: `animal` en `amount`. `myArray[1]` is dus een "rij uit een excel sheet met 2 kolommen". Willen we nu die `30`, dan moeten we specifiek polsen naar de eigenschap `amount`. Dat doen we zo:

    `myArray[1].amount`

Om onze code werkende te houden moeten we dus maar een kleine aanpassing doen:

    <svg width=700 height=350>
      <g v-for="(number, index) in myArray" :key="index">
        <g :transform="`translate(${index * 30}, ${100-number.amount})`">
            <rect width=20 :height=number.amount fill=orange />
        </g>
      </g>
    </svg>

Wat me hier erg aan stoort is dat we het `number` gebruiken om te verwijzen naar een element in uit `myArray`. Daarvoor hield dat steek omdat een element uit de array een getal was. Nu is dat een complexer object. Ik zou dus ook de naam veranderen naar iets toepasselijker:

    <svg width=700 height=350>
      <g v-for="(element, index) in myArray" :key="index">
        <g :transform="`translate(${index * 30}, ${100-element.amount})`">
            <rect width=20 :height=element.amount fill=orange />
        </g>
      </g>
    </svg>

### Labels
Tijd om onze labels terug te brengen. Eerst voegen we een statisch label toe aan elke rechthoek:

    <svg width=700 height=350>
      <g v-for="(element, index) in myArray" :key="index">
        <g :transform="`translate(${index * 30}, ${100-element.amount})`">
            <rect width=20 :height=element.amount fill=orange />
            <text x="5" :y=element.amount+10 fill="orange" :transform="`rotate(50, 5, ${element.amount+10})`">Pigs</text>
        </g>
      </g>
    </svg>

Merk op dat we weer enkel attributen laten varieëren op basis van de `amount` van elk element in `myArray`. 

De laatste stap is erg simpel. We willen de text `Pigs` vervangen door de `animal` property van `element`. Die is namelijk `Pigs` voor het eerste element, `Cats` voor het tweede, enzovoort. Probeer het eerst zelf. De oplossing staat hieronder:

    <svg width=700 height=350>
      <g v-for="(element, index) in myArray" :key="index">
        <g :transform="`translate(${index * 30}, ${100-element.amount})`">
            <rect width=20 :height=element.amount fill=orange />
            <text x="5" :y=element.amount+10 fill="orange" :transform="`rotate(50, 5, ${element.amount+10})`"> {{ element.animal }}</text>
        </g>
      </g>
    </svg>

Merk op dat als we vue code willen steken in de <i>waarde</i> van een HTML element, dat we daar `{{}}` rond moeten zetten. Bij een HTML-<b>attribuut</b> gebruiken we `v-bind`, bij de waarde, of inhoud, gebruiken we `{{}}`.


<b>OPDRACHT</b>: Verander nu je Vue code zodat de balk een eigen Vue component wordt. Zorg ervoor dat je App.vue html er als volgt uitziet:

    <svg width=700 height=350>
        <g v-for="(element, index) in myArray" :key="index">
            <Bar :x="index * 30" :height="element.amount" :label="element.animal" />
        </g>
    </svg>

Hieronder overlopen we de oplossing daarvoor, stap voor stap, maar probeer het zeker eerst zelf. Je hebt nu alles geleerd om dat zelf te doen.

## 4. Gebruik van een Vue component
Maak een nieuwe file aan `Bar.vue` onder de map `components`. We zorgen dat we javascript code en html kunnen schrijven voor deze nieuwe component:

    <script setup>
    </script>

    <template>
        
    </template>

We gaan meteen enkele properties geven aan dit nieuwe componentje. Van elke rechthoeken willen we de x-coordinaat kunnen instellen. We willen ook een label kunnen instellen en de hoogte instellen van de rechthoek. Die drie zaken zullen we dus aanbieden als properties van ons custom html elementje:

    <script setup>
    defineProps({
    x: {
        type: Number,
        required: true
    },
    height: {
        type: Number,
        required: true
    },
    label: {
        type: String,
        required: true
    }
    })
    </script>

De html van onze component komt onder de `template` tags. We gebruiken de hmtml code die wel al gemaakt hadden in `App.vue`:

    <template>
        <g :transform="`translate(${x}, ${100-height})`">
            <rect width=20 :height=height fill=orange />
            <text x="5" :y=height+10 fill="orange" :transform="`rotate(50, 5, ${height+10})`"> {{ label }}</text>
        </g>
    </template>

Deze html is bijna gelijkaardig aan de html die we gebruikt hadden in `App.vue`. De verwijzingen naar `element.???` gaan hier natuurlijk niet werken, we zitten hier immers niet rechtstreeks in die `v-for` lus. Of beter gezegd, dit componentje moet overal gebruikt kunnen worden, wij gebruiken het nu toevalling in een `v-for` lus. We vervangen al die verwijzingen naar onze interne properties (x, height en label). Die worden uiteindelijk dan ingevuld in `App.vue`, in de for-lus. 

Het laatste dat we moeten doen is onze `App.vue` aanpassen zodat we ook wel degelijk `Bar` kunnen gebruiken in de html van `App.vue`. Dat doen we door de juiste import statements toe te voegen bij `App.vue`:

    <script setup>
    import Bar from "./components/Bar.vue"
    ...

Dan passen we onze html van `App.vue` aan zodat we gebruik maken van ons gloednieuw componentje:

    <template>
    <svg width=700 height=350>
        <g v-for="(element, index) in myArray" :key="index">
            <Bar :x="index * 30" :height="element.amount" :label="element.animal" />
        </g>
        </svg>
    </template>


## Conclusie
Je hebt nu een werkende datavisualisatie. We hebben een array van objecten die elk eigen data bevatten. We lezen die data in en visualiseren die in een bar chart. Bovendien maken we gebruik van Vue componenten zodat we een herbruikbaar `Bar` componentje hebben. Goed gewerkt!