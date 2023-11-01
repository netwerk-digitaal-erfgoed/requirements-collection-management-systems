# NDE requirements

## Introduction

This document helps vendors of software - like collection management systems, and linked data publication platforms - to make their systems NDE compliant and ready for use in the Dutch heritage sector.  

The guidelines in this document are required for any institution in the Dutch cultural sector that receives funding through the NDE *Versnellingsprogramma* (Acceleration Program). Software vendors help these organisations to meet the requirements by implementing them as features in their systems.

Organisations who provide datasets or collections according to these guidelines are considered  [*Bronhouders*](https://dera.netwerkdigitaalerfgoed.nl/index.php/Rollen#Bronhouder) (Data Providers) as defined by the *Digitaal Erfgoed Referentie Architectuur* - [DERA](https://dera.netwerkdigitaalerfgoed.nl)) (Digital Heritage Reference Architecture).

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).

Please refer to our [Implementation Guidelines](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-collection-information) for further detailed technical information.

## Compatibility requirements

### 1. Persistent Identifiers

Every information resource needs a web address ([URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)) that identifies it to the world. Users must be able to trust these identifiers, they should be unique and reliably serve the same resource. 

Heritage institutions must use Persistent Identifiers (PIDs) for their resources to guarantee reliability. With a PID the link to a resource keeps working even when the organisation, or the object's location, has changed.

#### 1.1 PID Implementations

There are multiple PID systems such as [Archival Resource Keys](https://arks.org) (ARKs), [Digital Object Identifiers](https://www.doi.org) (DOIs), [Handle](http://handle.net) and others. You may chose the implementation. Each system has its own particular properties, strengths, and weaknesses. Our [PID Guide](https://www.pidwijzer.nl/en) helps you make a choice. 

As a heritage institution you must chose a PID system. You may be limited by the PID systems supported by your software vendor. But when you change vendor, your PID system migrates with you. 

As a vendor you must implement at least one PID system in your software. You may support more. When implementing the PID-system you must link resources to your customer (the cultural heritage institution) and not to you as a vendor. Persistency must be guaranteed when resources are migrated to another vendor in the future.

#### 1.2 Linking to removed resources

Removed resources are all objects that have been deleted, made invisible, or that for any other reason are no longer structurally available . You must maintain persistency for removed resources. To handle such requests you must use [standard HTTP response status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#redirection_messages) categories 100, 200, or 300. You may redirect the PID of a removed resource to a new resource that replaces it, serve a deleted resource in its last incarnation and mark it as 'obsolete', or chose another solution. 

Unless an actual error occurs, you must not throw a client error response (category 400) or a server error response (category 500) to point to removed resources.

### 2.  Publication of Linked Open Data

#### 2.1 Data modelling

We distinguish between the publication of data in "generic data models" and "domain data models". The purpose of generic data models is to integrate the data in the cultural heritage network and make it more visible. Domain models are usually more richly populated and provide users with more possibilities for further processing in [*dienstplatformen*](https://netwerkdigitaalerfgoed.nl/nieuws/maak-jij-erfgoedsites-en-apps-volg-de-afspraken-uit-de-architectuurblauwdruk-voor-dienstplatformen/) (Service Platforms).

You must use the generic model [schema.org](https://schema.org) when you chose to serve linked data in only one model. 

We recommend you also serve data in one or more domain models. Domain models make reuse of data much more likely and may contain a wealth of information. Depending on the type of data, you may consider the following examples:
- Museum collections and catalogues: [CIDOC-CRM](https://cidoc-crm.org) and its derivative [Linked-Art](https://linked.art/model/).
- Data from archives: [RiC-O](https://www.ica.org/standards/RiC/RiC-O_v0-2.html)
- Libraries: [BIBFRAME](https://www.loc.gov/bibframe/) or [RDA Elements](https://www.rdaregistry.info/Elements/)

You may also implement any model suggested by [CLARIAH](https://www.clariah.nl) in the [Awesome Ontologies for Digital Humanities](https://github.com/CLARIAH/awesome-humanities-ontologies) repository.

You should implement the [W3C draft for content negotiation by profile](https://www.w3.org/TR/dx-prof-conneg/) when publishing linked data that is available in multiple models.

#### 2.2 Serving data

The [Implementation Guidelines](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-collection-information) mentioned earlier consider three levels when [publishing linked data](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-linked-data):
1. Basic level: data dumps
2. Web compliance level: resolvable URIs
3. Advanced level: queryable Linked Data

You must publish linked data both as level 1 and 2. 

To publish linked data as a data dump (level 1) you should use [RDF](https://www.w3.org/RDF/) or [JSON-LD](https://json-ld.org) as a format.  You are required to serve the data dump through a [persistent identifier](###%201.%20Persistent%20Identifiers). To handle requests you must provide an API that complies with the [Open API Specification](https://spec.openapis.org/oas/latest.html). 

To publish web compliant linked data (level 2) you must use persistent identifiers (see above) to resolve the individual linked data resources contained in your data. To handle requests you must provide an API that complies with the [Open API Specification](https://spec.openapis.org/oas/latest.html). 

We strongly recommend that vendors implement level 3 in their products and allow users to also query linked data collections. For compliance with level 3 you must use a [SPARQL](https://www.w3.org/TR/rdf-sparql-query/) endpoint.

> Note, when you comply with levels 1 and 2 you allow users to access the individual linked data objects and the full dataset, while you avoid maintaining a linked data infrastructure that you would need to provide for querying. The drawback of this approach is that you move the burden to facilitate querying to the user. For this reason we view compliance with level 1 and 2 as a minimal requirement. We strongly urge you to go further and implement level 3. Compliancy with level 3 will very likely play a large role in the allocation of future NDE funding.

#### 2.3 Serving metadata

To increase the findability of datasets of heritage institutions, you must also publish the metadata of any dataset you serve. The metadata contains the description of the dataset and must be modelled in [schema.org](https://schema.org). We created a data model for the description of datasets and have adopted the class https://schema.org/Dataset. You must comply with the model as documented in the [NDE Requirements for Datasets](https://netwerk-digitaal-erfgoed.github.io/requirements-datasets) and specifically the [section Dataset information](https://netwerk-digitaal-erfgoed.github.io/requirements-datasets/#dataset-information).

You are required to serve the metadata through a [persistent identifier](###%201.%20Persistent%20Identifiers). To handle requests you must provide an API that complies with the [Open API Specification](https://spec.openapis.org/oas/latest.html). 

You must publish metadata with an open data license. You may chose the most suitable license.

The actual access to digital objects, such as images, audio files, or linked data resources, may be restricted. You must specify additional license statements for use and reuse of the objects in the metadata. Use the [schema:license](https://schema.org/license) property to relate a license to an information resource. 

Remember that you must relate a license to the dataset, the object metadata, and the reproduction. These licenses may differ.

### 3. Implementation of the NDE *termennetwerk* (Terminology Network)

To connect the linked data that you publish with other data sources you should use terms. Terms are descriptions of concepts or entities, such as subjects, people or places, and are managed in terminology sources, such as thesauri, reference lists or classification systems. Examples are [AAT](https://www.getty.edu/research/tools/vocabularies/aat/), [GeoNames](https://www.geonames.org/) or [WO2 Thesaurus](https://data.niod.nl/WO2_Thesaurus.html) (in Dutch).

You may use your own terminology sources. However, you reduce the ability to connect to sources from different institutions when using terms that are not part of internationally standardised terminology sources. We recommend using as many standardised terminology sources as possible. If you are considered an authority in your domain, you should publish your own terminology source for use by others. Please refer to our [Implementation Guidelines on publishing terminology sources](https://netwerk-digitaal-erfgoed.github.io/cm-implementation-guidelines/#publishing-terminology-sources). 

As a vendor you must implement configurable terms for fields in your heritage application. You may chose the specific fields. If you allow users of your application to configure the data type of a field, you should add a data type for terms. That way users are not limited in the (number of) fields that they want to configure for certain sets of terms.

It is not recommended that you import the lists of terms in your system. A limitation of such imports is that the user does not view the current data and you must periodically synchronise with the sources of each set of  terms. Wherever possible you should query terminology sources real-time. We recommend using the [NDE Network of Terms](https://termennetwerk.netwerkdigitaalerfgoed.nl/faq)to help you avoid having to establish multiple connections to a range of data sources serving terms, . 

### 4. Registration with the NDE dataset register

We have created the [NDE dataset register](https://datasetregister.netwerkdigitaalerfgoed.nl/?lang=en) to help users in the cultural heritage sector find relevant datasets to link with. You must use this to register the [metadata of datasets you serve](####%202.3%20Serving%20metadata). 

Although the register provides a manual registration option for users, as a vendor you are required to use the [Dataset Register API](https://datasetregister.netwerkdigitaalerfgoed.nl/apidoc.php?lang=en) to implement an automated registration feature in your software. The API description is available based on an [Open API](https://www.openapis.org) specification via the [Swagger UI](https://datasetregister.netwerkdigitaalerfgoed.nl/api/static/index.html).

We recommend you also use any other (open) registers to promote  datasets. A good example is the Netherlands government open data register: [data.overheid.nl](https://data.overheid.nl).

### 5. Serving images through IIIF

You must implement the [IIIF Image API](https://iiif.io/api/image/3.0/) to publish images contained in your system. The Image API supports requests for specific parts, sizes and orientations of images based on a URL scheme. It gives viewers the ability to request only those tiles needed for the current viewport and zoom level, instead of forcing them to load the complete high resolution image. You may chose the highest zoom level, size, and number of parts, of any image you serve, since these are directly related to the available storage in your system, the results of the digitisation process at the institution, and other customer wishes. 

We use the [IIIF Image API Validator](https://iiif.io/api/image/validator/) to test compliance.

While the Image API provides access to individual images, it does not describe the relationship between groups of images, such as the individual scans that make up the pages of a book. Besides the IIIF Image API you must also publish a IIIF manifest through the [IIIF Presentation API](https://iiif.io/api/presentation/3.0/). A IIIF manifest is a JSON-LD document that describes the structure and metadata of a digital object or collection of objects, such as images, audio, or video. It is comprises several key components, including pages, canvases, table of contents (ranges), and annotations.

We use the [IIIF Presentation API Validator](https://presentation-validator.iiif.io) to test compliance.