# NDE requirements

## Introduction

This document helps vendors of software - like collection registration and management systems, or linked data publication platforms - to make their systems NDE-compliant and ready for use in the Dutch heritage sector.  

The guidelines in this document are required for any institution in the Dutch cultural sector that receives funding through the NDE *Versnellingsprogramma* (Acceleration Program). Software vendors help these organisations to meet these requirements by implementing them as features in their systems.

Organisations who provide datasets or collections according to these guidelines are considered  [*Bronhouders*](https://dera.netwerkdigitaalerfgoed.nl/index.php/Rollen#Bronhouder) (Data Providers) as defined by the *Digitaal Erfgoed Referentie Architectuur* - [DERA](https://dera.netwerkdigitaalerfgoed.nl)) (Digital Heritage Reference Architecture).

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).

Please refer to our [Implementation Guidelines](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-collection-information) for more detailed technical information.
## Compatibility requirements

### 1. Persistent Identifiers

Every information resource needs a web address ([URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)) that identifies it to the world. Users must be able to trust these identifiers, they should be unique and reliably serve the same resource. 

To guarantee reliability heritage institutions must use Persistent Identifiers (PIDs) for their resources. With a PID the link to a resource keeps working even when the organisation or object's location has changed.
#### 1.1 PID Implementations

There are multiple PID systems such as [Archival Resource Keys](https://arks.org) (ARKs), [Digital Object Identifiers](https://www.doi.org) (DOIs), [Handle](http://handle.net) and others. You may chose the implementation. Each system has its own particular properties, strengths, and weaknesses. The [PID Guide](https://www.pidwijzer.nl/en) helps you make a choice. 

As a heritage institution and data provider, you must chose a PID system. You may be limited by the PID systems supported by your software vendor. But when you change vendor, your PID system migrates with you. 

As a vendor you must implement at least one PID system in your software. You may support more. The PID-system must link resources to your customer (the cultural heritage institution) and not to you as a vendor. Persistency must be guaranteed when resources are migrated to another vendor in the future.
#### 1.2 Linking to removed resources

Removed resources are all resources that have been deleted, made invisible, or that are for any other reason no longer structurally available . You must maintain persistency for removed resources. To handle such requests you must use [standard HTTP response status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#redirection_messages) categories 100, 200 or 300. You may redirect the PID of a removed resource to a new resource that replaces it, serve a deleted resource in its last incarnation and mark it as 'obsolete', or chose another solution. 

Unless an actual error occurs, you must not throw a client error response (category 400) or a server error response (category 500) to point to removed resources.
### 2.  Publication of Linked Open Data
#### 2.1 Data modelling

We distinguish between the publication of data in "generic data models" and "domain data models". The purpose of generic data models is to integrate the data in the cultural heritage network and make it more visible. Domain models are usually more richly populated and provide users with more possibilities for further processing in [*dienstplatformen*](https://netwerkdigitaalerfgoed.nl/nieuws/maak-jij-erfgoedsites-en-apps-volg-de-afspraken-uit-de-architectuurblauwdruk-voor-dienstplatformen/) (Service Platforms).

You must use the generic model [schema.org](https://schema.org) when serving linked data that is available in only one model. 

We recommend you also serve data in one or more domain data models. Domain models make reuse of data much more likely. Depending on the type of data, you may consider the following examples:
- Museum collections and catalogues: [CIDOC-CRM](https://cidoc-crm.org) and its derivative [Linked-Art](https://linked.art/model/).
- Data from archives: [RiC-O](https://www.ica.org/standards/RiC/RiC-O_v0-2.html)
- Libraries: [BIBFRAME](https://www.loc.gov/bibframe/) or [RDA Elements](https://www.rdaregistry.info/Elements/)

You may also implement any model suggested by [CLARIAH](https://www.clariah.nl) in the [Awesome Ontologies for Digital Humanities](https://github.com/CLARIAH/awesome-humanities-ontologies) repository.

When publishing linked data that is available in multiple models you may implement the [W3C draft for content negotiation by profile](https://www.w3.org/TR/dx-prof-conneg/)
#### 2.2 Serving data

The Implementation Guidelines mentioned earlier consider three levels when [publishing linked data](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-linked-data):
1. Basic level: data dumps
2. Web compliance level: resolvable URIs
3. Advanced level: queryable Linked Data

You must publish linked data both as level 1 and 2. 

The metadata of any dataset you serve must be published separately. The metadata contains the description of the data dump and must be modelled in [schema.org](https://schema.org).  You are required to serve the metadata through a persistent identifier and may chose the protocol to handle the request. The metadata must be published under an open data license.

To publish linked data as a data dump (level 1) you should use [RDF](https://www.w3.org/RDF/) or [JSON-LD](https://json-ld.org) as a format.  You are required to serve the data dump through a persistent identifier and may chose the protocol to handle the request. 

To publish web compliant linked data (level 2) you must use persistent identifiers (see above) to resolve the individual linked data resources contained in your data. You may chose the protocol to handle the request. 

We strongly recommend that vendors implement level 3 in their products and allow users to also query linked data collections. For compliance with level 3 you must use a [SPARQL](https://www.w3.org/TR/rdf-sparql-query/) endpoint.

> Note, by complying with both level 1 and 2 you allow users to access both the individual linked data objects (level 2) and the entire dataset (level 1) without having to maintain a full linked data infrastructure needed to provide querying (level 3). Since you effectively move the burden to query data to the user, we view this as a minimal requirement and strongly urge you to go further. Compliancy with level 3 will very likely play a large role in the allocation of future NDE funding.
#### 2.3 Data licenses

You must publish metadata with an open license. The actual access to a digital object, such as an image or audio file, can be restricted. You must specify additional license statements for use and reuse of the objects in the metadata. Use the [schema:license](https://schema.org/license) property to relate a license to an information resource. 

Remember that you have to relate a license to the dataset, the object metadata, and the reproduction. These licenses may differ.
### 3. Implementation of the NDE *termennetwerk* (Terminology Network)

To connect the linked data that you publish with other data sources you may use terms. Terms are descriptions of concepts or entities, such as subjects, people or places. Each term has a URI as an identifier. Because a URI is a unique web address it makes unambiguously clear which term is meant. Terms and their URIs are managed in terminology sources, such as thesauri, reference lists or classification systems. Examples are [AAT](https://www.getty.edu/research/tools/vocabularies/aat/), [GeoNames](https://www.geonames.org/) or [WO2 Thesaurus](https://data.niod.nl/WO2_Thesaurus.html) (in Dutch).

You may use your own terminology sources. However you reduce the ability to connect to sources from different institutions when using terms that are not part of internationally standardised terminology sources. We recommend using as many standardised terminology sources as possible. If you are considered an authority in your domain, you may also chose to publish your terminology sources for use by others. Please refer to our [Implementation Guidelines on publishing terminology sources](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-terminology-sources). 

As a vendor you must implement configurable terms for certain fields in your heritage application. You may chose the fields. If you allow users to configure the data type of a field in your application, we recommend adding a data type for terms. That way users are not limited and can decide which fields they want to configure for certain sets of terms.

It is not recommended that you import the lists of terms in your system. A limitation is that the user does not use current data and you must periodically synchronise with the data sources of each set of  terms. Wherever possible you should query terminology sources real-time. To help you avoid having to establish multiple connections to a range of data sources serving terms, we recommend using the [NDE Network of Terms](https://termennetwerk.netwerkdigitaalerfgoed.nl/faq). 
### 4. Registration at the NDE dataset register


### 5. Serving images through IIIF



