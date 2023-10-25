# NDE richtlijnen voor leveranciers

## Inleiding

Dit document geeft een uitwerking van de richtlijnen voor NDE-compatibiliteit om leveranciers van collectie registratie systemen en linked data publicatieplatformen bij het inrichten van de benodigde functionaliteit voor een NDE-compatibel systeem. 

De in dit document benoemde richtlijnen zijn vereist voor instellingen in de culturele sector die via het NDE Versnellingsprogramma gefinancierd worden. De leveranciers helpen de instellingen te voldoen aan de richtlijnen door ze te implementeren in hun systemen. 

Instellingen die datasets en collecties conform deze richtlijnen aanleveren worden gezien als [Bronhouders](https://dera.netwerkdigitaalerfgoed.nl/index.php/Rollen#Bronhouder) conform de definitie van de *Digitaal Erfgoed Referentie Architectuur* ([DERA](https://dera.netwerkdigitaalerfgoed.nl)).
## Richtlijnen

### 1. Persistente identifiers

### 2.  Publicatie van Linked Open Data

De data in het collectie registratie systeem wordt via een webAPI beschikbaar gesteld als [Linked Open Data](https://netwerkdigitaalerfgoed.nl/activiteiten/linked-data-2/). Aanwijzingen voor de technische implementatie zijn te vinden in de [Implementation Guidelines](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-collection-information).

#### 2.1 Data modellering

NDE maakt onderscheid tussen de publicatie van de data in "generieke data modellen" en "domein data modellen". De generieke data modellen zorgen voor de integratie en zichtbaarheid van de data binnen het netwerk. Domein modellen zijn rijker en bieden gebruikers meer mogelijkheden bij de verdere verwerking in [dienstplatformen](https://netwerkdigitaalerfgoed.nl/nieuws/maak-jij-erfgoedsites-en-apps-volg-de-afspraken-uit-de-architectuurblauwdruk-voor-dienstplatformen/).

Het aanbieden van de data in minimaal één generiek model is verplicht. Gebruik hiervoor [schema.org](https://schema.org). 

Het aanbieden van de data in één of meer domein modellen is niet verplicht, maar wordt wel sterk gestimuleerd. Deze modellering maakt immers het hergebruik van de data mogelijk. Afhankelijk van het soort data zijn de volgende domein modellen aan te raden:
- Museale collecties en catalogie: [CIDOC-CRM](https://cidoc-crm.org) en het afgeleide model [Linked-Art](https://linked.art/model/)
- Archief collecties: [RiC-O](https://www.ica.org/standards/RiC/RiC-O_v0-2.html)
- Bibliotheken: [BIBFRAME](https://www.loc.gov/bibframe/) of [RDA Elements](https://www.rdaregistry.info/Elements/)

Ook de door [CLARIAH](https://www.clariah.nl) geadviseerde modellen in [Awesome Ontologies for Digital Humanities](https://github.com/CLARIAH/awesome-humanities-ontologies) voldoen aan de NDE richtlijnen.

#### 2.2 Uitleveren

In de [implementation guidelines voor het uitleveren van Linked Open Data](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-linked-data) wordt gesproken over drie niveaus:
1. data dumps
2. linked data resources
3. doorzoekbare linked data

NDE verwacht van instellingen binnen de culturele sector minimaal niveau 2. De linked data is op resource niveau opvraagbaar en voorzien van een persistent adres (zie ook: [[README#1. Persistente identifiers]]). Enkel het beschikbaar maken van een data dump (al dan niet op een persistent webadres) is **niet** voldoende.

Niveau 3, het aanbieden van doorzoekbare linked data, wordt alle leveranciers sterk aangeraden. Gebruik daarvoor een endpoint dat [SPARQL](https://www.w3.org/TR/rdf-sparql-query/) queries kan verwerken.

### 3. Implementatie van het NDE termennetwerk


### 4. Registratie van datasets in het NDE dataset register

### 5. Beschikbaarstelling van afbeeldingen via IIIF



