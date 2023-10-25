# NDE guidelines for suppliers

## Introduction

This document helps suppliers of software - like collection registration and management systems, or linked data publication platforms - to make their systems NDE-compliant and ready for use in the Dutch heritage sector.  

The guidelines in this document are required for any institution in the Dutch cultural sector, who receives funding through the NDE *Versnellingsprogramma* (Acceleration Program). Software suppliers help these organisations to meet the requirements by implementing them as features in their systems.

Organisations who provide datasets or collections according to these guidelines are considered  [*Bronhouders*](https://dera.netwerkdigitaalerfgoed.nl/index.php/Rollen#Bronhouder) (Data Providers) as defined by the *Digitaal Erfgoed Referentie Architectuur* - [DERA](https://dera.netwerkdigitaalerfgoed.nl)) (Digital Heritage Reference Architecture).

## GUIDELINES

### 1. Persistent Identifiers

### 2.  Publication of Linked Open Data

The data in a collection registration or management system is made available as [Linked Open Data](https://netwerkdigitaalerfgoed.nl/activiteiten/linked-data-2/) through a webAPI. You can find more technical information in our [Implementation Guidelines](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-collection-information).

#### 2.1 Data modelling

We distinguish between the publication of data in "generic data models" and "domain data models". The purpose of generic data models is to integrate the data in the network and make it more visible. Domain models are usually more rich and provide users with more possibilities for further processing in [*dienstplatformen*](https://netwerkdigitaalerfgoed.nl/nieuws/maak-jij-erfgoedsites-en-apps-volg-de-afspraken-uit-de-architectuurblauwdruk-voor-dienstplatformen/) (Service Platforms).

When publishing data a minimum implementation of one generic model is required. Use [schema.org](https://schema.org) for this purpose.

Although the publication of data in one or more domain models is not required, we strongly suggest that you do. Domain models make reuse  of the data possible. Depending on the type of data, you could consider the following examples:
- Museum collections and catalogues: [CIDOC-CRM](https://cidoc-crm.org) and its derivative [Linked-Art](https://linked.art/model/).
- Data from archives: [RiC-O](https://www.ica.org/standards/RiC/RiC-O_v0-2.html)
- Libraries: [BIBFRAME](https://www.loc.gov/bibframe/) or [RDA Elements](https://www.rdaregistry.info/Elements/)

Also the implementation of any model suggested by [CLARIAH](https://www.clariah.nl) in the [Awesome Ontologies for Digital Humanities](https://github.com/CLARIAH/awesome-humanities-ontologies) repository fully complies with NDE guidelines.

#### 2.2 Serving data

The Implementation Guidelines mentioned above consider three levels when [publishing linked data](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-linked-data):
1. Basic level: data dumps
2. Web compliance level: resolvable URIs
3. Advanced level: queryable Linked Data

We expect institutions to implement at least level 2. Users can request individual linked data resources through a persistent identifier (see above). Making data available through a data dump at basic level does **not** comply with these guidelines.

We strongly suggest that suppliers implement level 3 in their products and enable users to also query linked data collections. Use an endpoint that can process [SPARQL](https://www.w3.org/TR/rdf-sparql-query/) queries.

### 3. Implementation of the NDE *termennetwerk* (Terminology Network)

### 4. Registration at the NDE dataset register

### 5. Serving images through IIIF



