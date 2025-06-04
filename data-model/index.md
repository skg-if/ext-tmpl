---
title: Data model
parent: Extension template
layout: default
nav_order: 2
nav_exclude: true
---

# Extended data model

This extension template extends the [SKG-IF Ontology](https://w3id.org/skg-if/ontology/) in two ways:
- It introduces a *new entity Comment*, which captures a textual comment possibly relevant to a research product;
- It introduces a *new property* for [Research products](../../interoperability-framework/docs/research-product) in order to point to the relative Comment(s).

## Expected outcomes
In this modelling phase, two outcomes are expected
- A **OWL/RDF ontology** in the format of choice, e.g., `.ttl`, `.nt`, `.xml`, `.json` (potentially all of them, provided they are aligned);
- An `.html` **documentation page** of the developed ontology.

These files need to be placed as indicated [here](../structure). In this way, everything will be automatically wired-up in order to deliver your assets behind W3IDs. For example:
- This extension ontology, [https://w3id.org/skg-if/extension/tmpl/ontology.ttl](https://w3id.org/skg-if/extension/tmpl/ontology.ttl)
- This extension documentation, [https://w3id.org/skg-if/extension/tmpl/ontology](https://w3id.org/skg-if/extension/tmpl/ontology)

## Methodological considerations
A good Relation Database always start with requirements analysis and ER diagrams, rather than getting hands dirty with table schemas in the DBMS of reference.

Similarly, here we start with the **development of a formal ontology** that is plugged on top of the one defined by the core SKG-IF data model. As a refresher, or to getting started with ontology development, a good reading list could be the following:
- [Noy, N. F., & McGuinness, D. L. (2001). *Ontology development 101: A guide to creating your first ontology.*](https://protege.stanford.edu/publications/ontology_development/ontology101.pdf)
- [Parlar, S. (2019). *Ontologies: In Detail. How to develop an ontology?*](https://medium.com/analytics-vidhya/ontologies-in-detail-2916f9226133)

More in-depth, advanced methodologies are available here:
- [Suárez-Figueroa, M. C., & others. (2012). *NeOn Methodology for Building Ontology Networks: Specification, Scheduling and Reuse*. IOS Press.](https://oa.upm.es/3879/2/MARIA_DEL-_CARMEN_SUAREZ_DE_FIGUEROA_BAONZA.pdf)
- [Peroni, S. (2015). *SAMOD: an agile methodology for the development of ontologies*. In Formal Ontology in Information Systems (FOIS) (pp. 37-50). IOS Press.](https://essepuntato.it/samod/)
- [Gómez-Pérez, A., Fernández-López, M., & Corcho, O. (2004). *Ontological Engineering: With Examples from the Areas of Knowledge Management, E-commerce and the Semantic Web*. Springer.](https://link.springer.com/book/10.1007/b97353)

In order to avoid reinventing the wheel, you are encouraged to reuse ontologies and vocabularies already present in the literature, such as:
- [Schema.org](https://schema.org)
- [SPAR Ontologies](http://www.sparontologies.net)
- [Linked Open Vocabularies (LOV)](https://lov.linkeddata.es/dataset/lov/)

### Developing the ontology
For sizeable and reasonably small ontologies, editing the required files (e.g., `.ttl`) is a viable way to proceed, while for more complex models an ontology editor could come handy. 
In this regards, [**Protégé**](https://protege.stanford.edu) is suggested for its live and broad community of adopters, and because it is an open source, free software.

Recommendations **(TODO expand)**:
- "light import" of external properties without redefining domain and range (co-domain);
-  usage of annotations to be parsed automatically for SHACL definition (see [SHACL development phase](./shacl)).

### Producing the documentation
In order to produce the `.html` documentation of the developed ontology, no specific tool or format is required. 
In principle, the documentation can adhere to any format of choice and be developed with the preferred method.

However, we can suggest that can potentially streamline the workflow:
- [**WIDOCO**](https://github.com/dgarijo/Widoco)
