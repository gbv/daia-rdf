# Introduction

The **DAIA Ontology** defines an encoding of document availability information
in RDF. The Ontology aligned with [Document Availability Information API
(DAIA)](http://gbv.github.io/daiaspec).

Updates and sources of this document can be found in a public git repository at
<http://github.com/gbv/daia-rdf>. The master file
[daia.md](https://github.com/gbv/daia-rdf/blob/master/daia.md) is written
in [Pandoc’s Markdown](http://johnmacfarlane.net/pandoc/demo/example9/pandocs-markdown.html).
PAIA Ontology in [in RDF/Turtle](daia.ttl), [in RDF/XML](daia.owl) and
this HTML document are generated from the master file with
[makespec](https://github.com/jakobib/makespec). The specification can be
distributed freely under the terms of CC-BY-SA.

# Overview

The Document Availability Information Ontology (DAIA ontology) defines a set of
RDF classes and RDF properties to express DAIA data in RDF. RDF data that makes
use of DAIA ontology is also referred to as DAIA/RDF.

The DAIA data model basically consists of abstract
documents, concrete holdings of documents, and document services, with an
availability status. 

RDF Serializations of DAIA Ontology are available in RDF/Turtle
([**`daia.ttl`**](./daia.ttl)) and in RDF/XML ([**`daia.owl`**](./daia.owl)).

## Namespaces

The DAIA/RDF Ontology is identified by the URI <http://purl.org/ontology/daia/>
which is also used URI namespace. Both may be changed to
<http://purl.org/ontology/daia#>. The namespace prefix `daia` is recommeded.

## Overview

DAIA ontology is based on the following RDF ontologies:

----------------------------------- ---------------------------- ---------------------------------------
 Ontology                            relevant classes            relevant properties
----------------------------------- ---------------------------- ---------------------------------------
 [Document Service Ontology] (DSO)   [dso:DocumentService]\       -
                                     [dso:Loan]\
                                     [dso:Presentation]\
                                     [dso:Interloan]\
                                     [dso:OpenAccess]\

 Service Ontology                    [service:ServiceLimitation]  [service:limits] / [service:limitedBy]\
                                                                  [service:delay]

 [Holding Ontology]                  ...                          holding:exemplar\
                                                                  holding:narrowerExemplar\
                                                                  holding:broaderExemplar\
                                                                  holding:heldby / holding:holds\
                                                                  holding:label\
                                                                  ...

 FOAF                                foaf:Organization\           foaf:primaryTopicOf\
                                                                  foaf:name\
                                     ...                          ...

 Bibliographic Ontology (bibo)       bibo:Document                -

 FRBR                                frbr:Item                    -

 DCTerms                             ...                          dct:description\
                                                                  dct:hasPart / dct:isPartOf
----------------------------------- ---------------------------- ---------------------------------------

In addition:

* [Organization ontology](http://www.w3.org/TR/vocab-org/) may be used
  to refer to organizations and institutions.
* Simple Service Status Ontology (SSSO) should be referred to.
* DAIA should be aligned with [Schema.org Ontology](http://schema.org/).

[dso:DocumentService]: http://purl.org/ontology/dso#DocumentService
[dso:Loan]: http://purl.org/ontology/dso#Loan
[dso:Presentation]: http://purl.org/ontology/dso#Presentation
[dso:Interloan]: http://purl.org/ontology/dso#Interloan
[dso:OpenAccess]: http://purl.org/ontology/dso#OpenAccess

[service:ServiceLimitation]: http://purl.org/ontology/service#ServiceLimitation
[service:limits]: http://purl.org/ontology/serviceo#limits
[service:limitedBy]: http://purl.org/ontology/service#limitedBy
[service:delay]: http://purl.org/ontology/serviceo#delay

~~~{.ditaa}
+-----------+     daia:availableFor    +---------------------+
|           |------------------------->|                     |
|           |<-------------------------|                     |
|           |     daia:availableOf     |                     |
| frbr:Item |                          | dso:DocumentService |
|           |    daia:unavailableFor   |                     |
|           |------------------------->|                     |
|           |<-------------------------|                     |
+-----------+    daia:unavailableOf    +---------------------+
~~~

## Namespaces and Ontology

The URI namespace of DAIA ontology is `http://purl.org/ontology/daia#`. The
namespace prefix `daia` is recommended. The URI of DAIA Ontology as as a whole
is <http://purl.org/ontology/daia>.

    @prefix daia: <http://purl.org/ontology/daia#> .
    @base         <http://purl.org/ontology/daia> .

The following namspace prefixes are used to refer to related ontologies:

    @prefix cc:      <http://creativecommons.org/ns#> .
    @prefix dct:     <http://purl.org/dc/terms/> .
    @prefix dso:     <http://purl.org/ontology/dso#> .
    @prefix holding: <http://purl.org/ontology/holding#> .
    @prefix frbr:    <http://purl.org/vocab/frbr/core#> .
    @prefix owl:     <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs:    <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix ssso:    <http://purl.org/ontology/ssso#> .
    @prefix service: <http://purl.org/ontology/service#> .
    @prefix holding: <http://purl.org/ontology/holding#> .
    @prefix vann:    <http://purl.org/vocab/vann/> .
    @prefix voaf:    <http://purl.org/vocommons/voaf#> .
    @prefix vs:      <http://www.w3.org/2003/06/sw-vocab-status/ns#> .
    @prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

In Turtle syntax, the ontology is defined as following:

    <> a owl:Ontology, voaf:Vocabulary ;
        dct:title "Document Availability Information Ontology"@en ;
        rdfs:label "DAIA" ;
        vann:preferredNamespacePrefix "daia" ;
        vann:preferredNamespaceUri "http://purl.org/ontology/daia#" ;
        dct:modified "{GIT_REVISION_DATE}"^^xsd:date ;
        owl:versionInfo "{VERSION}" ;
        foaf:isPrimaryTopicOf <http://purl.org/NET/DAIA> ;
        cc:license <http://creativecommons.org/licenses/by/3.0/> ;
        dct:creator "Jakob Voß" 
    .

## Classes

DAIA ontology does not define new classes but makes use of classes defined in
related ontologies.

### Documents and Holdings

...

    ssso:ServiceEvent a owl:Class ;
        rdfs:isDefinedBy <http://purl.org/ontology/ssso> .

### Storage

A storage is a place where items are stored.

    daia:Storage a owl:Class .

### Availability

...

## Properties

### availableFor

    daia:availableFor a owl:ObjectProperty ;
        rdfs:label "availableFor"@en ;
        rdfs:domain frbr:Item ;
        rdfs:range dso:DocumentService ;
        owl:inverseOf daia:availableOf ;
        rdfs:subPropertyOf dso:hasService ;
        rdfs:seeAlso daia:unavailableFor ;
        rdfs:isDefinedBy <> ;
        vs:term_status "testing" .

### availableOf
    
    daia:availableOf a owl:ObjectProperty ;
        rdfs:label "availableOf"@en ;
        rdfs:domain dso:DocumentService ;
        rdfs:range frbr:Item ;
        owl:inverseOf daia:availableFor ;
        rdfs:subPropertyOf dso:hasDocument ;
        rdfs:seeAlso daia:unavailableOf ;
        rdfs:isDefinedBy <> ;
        vs:term_status "testing" .

### unavailableFor
    
    daia:unavailableFor a owl:ObjectProperty ;
        rdfs:label "unavailableFor"@en ;
        rdfs:domain frbr:Item ;
        rdfs:range dso:DocumentService ;
        owl:inverseOf daia:unavailableOf ;
        rdfs:subPropertyOf dso:hasService ;
        rdfs:seeAlso daia:availableFor ;
        rdfs:isDefinedBy <> ;
        vs:term_status "testing" .

### unavailableOf
    
    daia:unavailableOf a owl:ObjectProperty ;
        rdfs:label "unavailableOf"@en ;
        rdfs:domain dso:DocumentService ;
        rdfs:range frbr:Item ;
        owl:inverseOf daia:unavailableOf ;
        rdfs:subPropertyOf dso:hasDocument ;
        rdfs:seeAlso daia:availableOf ;
        rdfs:isDefinedBy <> ;
        vs:term_status "testing" .

# References

- **[DSO]** [Document Service Ontology] Work in Progress 2013
  June 1999 (RFC 2616).
- **[HOLDINGS]** [Holding Ontology] Work in progress 2013
- **[SSSO]** [Simple Service Status Ontology] Work in Progress 2013
- **[URI]** [Uniform Resource Identifiers (URI): Generic Syntax](http://tools.ietf.org/html/rfc2396).
  August 1998 (RFC 2396).

# Appendixes

The following appendixes are informative only.

## Relevant differences to DAIA 0.5

The main difference of this specification to DAIA 0.5 is the inclusion of
DAIA/RDF which was formerly defined in a separate document. Major parts of the
DAIA ontology have been moved to independent micro-ontologies, involving the
change of URIs. In particular, DAIA services are now defined in the Document
Service Ontology. The following URIs are deprecated:

Removed:

* <http://purl.org/ontology/daia/Response>
* <http://purl.org/ontology/daia/timestamp>

Moved to [Document Service Ontology] (DSO):

* <http://purl.org/ontology/daia/Service>
  moved to <http://purl.org/ontology/dso#DocumentService>
* <http://purl.org/ontology/daia/Service/Openaccess>
  moved to <http://purl.org/ontology/dso#Openaccess>
* <http://purl.org/ontology/daia/Service/Interloan>
  moved to <http://purl.org/ontology/dso#Interloan>
* <http://purl.org/ontology/daia/Service/Loan>
  moved to <http://purl.org/ontology/dso#Loan>
* <http://purl.org/ontology/daia/Service/Presentation> 
  moved to <http://purl.org/ontology/dso#Presentation>

Moved to [Simple Service Status Ontology] (SSSO):

* <http://purl.org/ontology/daia/provides>
  moved to <http://purl.org/ontology/ssso#provides>
* <http://purl.org/ontology/daia/providedBy>
  moved to <http://purl.org/ontology/ssso#providedBy>
* <http://purl.org/ontology/daia/Limitation>
  moved to <http://purl.org/ontology/ssso#ServiceLimitation>
* <http://purl.org/ontology/daia/limits>
  moved to <http://purl.org/ontology/ssso#limits>
* <http://purl.org/ontology/daia/limitedBy>
  moved to <http://purl.org/ontology/ssso#limitedBy>
* <http://purl.org/ontology/daia/queue>
  moved to <http://purl.org/ontology/ssso#queue>
* <http://purl.org/ontology/daia/delay> 
  and <http://purl.org/ontology/daia/expected> 
  moved to <http://purl.org/ontology/ssso#delay>

Moved to [Holding Ontology]:

* <http://purl.org/ontology/daia/exemplar> 
  moved to ...
* <http://purl.org/ontology/daia/exemplarOf> 
  moved to ...
* <http://purl.org/ontology/daia/narrowerExemplar> 
  moved to ...
* <http://purl.org/ontology/daia/narrowerExemplarOf> 
  moved to ...
* <http://purl.org/ontology/daia/broaderExemplar> 
  moved to ...
* <http://purl.org/ontology/daia/broaderExemplarOf> 
  moved to ...
* <http://purl.org/ontology/daia/holds> 
  moved to ...
* <http://purl.org/ontology/daia/heldBy> 
  moved to ...
* <http://purl.org/ontology/daia/label> 
  moved to ...

Nur sure about:

* daia:collectedBy, daia:inCollection (?) to connect holding institution/agent 
  and abstract document which holding is exemplar of.
* daia:Storage maybe to be replaced by dct:Location, geo:SpatialThing or similar (?)

DAIA Ontology

* daia:perform, daia:baseURL ... (?)

* <http://purl.org/ontology/daia/availableOf> changed to
  <http://purl.org/ontology/daia#availableOf>.
* <http://purl.org/ontology/daia/availableFor> changed to
  <http://purl.org/ontology/daia#availableFor>.
* <http://purl.org/ontology/daia/unavailableOf> changed to
  <http://purl.org/ontology/daia#unavailableOf>.
* <http://purl.org/ontology/daia/unavailableFor> changed to
  <http://purl.org/ontology/daia#unavailableFor>.

## Integrity rules

If department and institution have same id, the department SHOULD be
ignored.

[CC-BY-SA 3.0]: http://creativecommons.org/licenses/by-sa/3.0/
[RFC 3066]: http://tools.ietf.org/html/rfc3066

[Document Service Ontology]: http://purl.org/ontology/dso
[Simple Service Status Ontology]: http://purl.org/ontology/ssso
[Holding Ontology]: http://dini-ag-kim.github.io/holding-ontology/

## Revision history

{GIT_CHANGES}

