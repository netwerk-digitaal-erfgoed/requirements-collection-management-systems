# NDE guidelines for suppliers

## Introduction

This document helps suppliers of software - like collection registration and management systems, or linked data publication platforms - to make their systems NDE-compliant and ready for use in the Dutch heritage sector.  

The guidelines in this document are required for any institution in the Dutch cultural sector, who receives funding through the NDE *Versnellingsprogramma* (Acceleration Program). Software suppliers help these organisations to meet the requirements by implementing them as features in their systems.

Organisations who provide datasets or collections according to these guidelines are considered  [*Bronhouders*](https://dera.netwerkdigitaalerfgoed.nl/index.php/Rollen#Bronhouder) (Data Providers) as defined by the *Digitaal Erfgoed Referentie Architectuur* - [DERA](https://dera.netwerkdigitaalerfgoed.nl)) (Digital Heritage Reference Architecture).

## GUIDELINES

### 1. Persistent Identifiers

Every information resource needs a web address ([URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)) that identifies it to the world. Users must be able to trust these identifiers, they should be unique and reliably serve the same resource. 

To guarantee reliability we require heritage institutions to use Persistent Identifiers (PIDs) for their resources. With a PID the link to a resource keeps working even when the organisation or object's location has changed.

There are multiple PID systems such as [Archival Resource Keys](https://arks.org) (ARKs), [Digital Object Identifiers](https://www.doi.org) (DOIs), [Handle](http://handle.net) and others. We have no preference for any specific solution. Each system has its own particular properties, strengths, and weaknesses. The [PID Guide](https://www.pidwijzer.nl/en) helps to select a PID system. 

As a heritage institution and data provider, the choice for a PID system is your responsibility. You will be limited by the PID systems supported by your software supplier. But when you change supplier, your PID system migrates with you. 

As a supplier we expect you to implement at least one persistent identification system in your software. You are of course free to support more. Take specific care that the implementation links resources to your customer (the cultural heritage institution) and not to you as a supplier. Persistency must be guaranteed even if resources are migrated to another supplier in the future.

You are required to maintain persistency even if resources have been deleted or no longer publicly available. Use [standard HTTP response status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#redirection_messages) categories 100, 200 or 300. You may redirect the PID of such resources to a new resource that replaces it, serve a deleted resource in its last incarnation and mark it as 'obsolete', or chose some other solution. You may not throw a client error response (category 400) or a server error response (category 500) to structurally handle such requests.

For convenience we compiled an [explanation of the anatomy of a PID-request](anatomyPersistentId.md) in ARK and Handle and how they differ. We also explain how ARK can be a free service (you need to do more yourself) and why Handle comes at a cost. 

We have noticed that the costs to use Handle are frequently misunderstood. A Handle prefix costs about €50 per year. 

Many institutions in the cultural heritage sector use [SURF](https://www.surf.nl/en) (the collaborative organisation for IT in Dutch education and research) to help them. SURF provides a PID-service that uses Handle and charges €493 per year (in 2024) on top of the Handle registration. For more information see: [SURF Data Persistent Identifier](https://www.surf.nl/en/data-persistent-identifier-data-always-findable-by-permanent-references). The SURF service allows you to automatically generate and administer PIDs for any resource located in SURF systems. ***It cannot provide this service for resources located anywhere else.*** 

When you chose Handle as your PID-system, NDE does not require you to make use of the SURF service. Be aware that you need to know the storage location of the resources that you want to share with the NDE network, in order to decide if the SURF PID-service provides you with value. We have encountered organisations who paid for the SURF-service while none of their linked data resources was stored there. 

### 2.  Publication of Linked Open Data

The data in a collection registration or management system is made available as [Linked Open Data](https://netwerkdigitaalerfgoed.nl/activiteiten/linked-data-2/) through a webAPI. You can find more technical information in our [Implementation Guidelines](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-collection-information).

#### 2.1 Data modelling

We distinguish between the publication of data in "generic data models" and "domain data models". The purpose of generic data models is to integrate the data in the network and make it more visible. Domain models are usually richer populated and provide users with more possibilities for further processing in for example [*dienstplatformen*](https://netwerkdigitaalerfgoed.nl/nieuws/maak-jij-erfgoedsites-en-apps-volg-de-afspraken-uit-de-architectuurblauwdruk-voor-dienstplatformen/) (Service Platforms).

When publishing data a minimum implementation of one generic model is required. Use [schema.org](https://schema.org) for this purpose.

Although the publication of data in one or more domain models is not required, we strongly suggest that you do. Domain models make reuse of the data possible. Depending on the type of data, you could consider the following examples:
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



