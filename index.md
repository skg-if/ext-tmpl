---
title: Extension template
layout: default
parent: Extensions
# nav_exclude: true
# search_exclude: true
---

# Extension template documentation

{: .highlight }
This page serves to kickstart the development of your extension and provide guidance in the process. Once confident with the whole process, please delete the content of this page and replace it with an introductory description of the extension, comprehending its context, scope and objectives.

## Documentation checklist
In order to document the specification introduced by your extension, please use the suggested folder structure.
In particular, the document you have to produce has to cover these fundamental aspects:
- description of the [data model](/extension-template/data-model/) and formal implementation in OWL;
- production and documentation of an extended [JSON-LD context](/extension-template/context/);
- description of [extensions to core entities]({% link extension-template/interoperability-framework/core-extensions/ext-research-product.md %}) (properties and relations);
- description of [new entities]({% link extension-template/interoperability-framework/extension-entities/ext-entity.md %}) (properties and relations);
- [extension](/extension-template/api) to the core APIs; i.e., customisations of core API resolvers (if any) and/or introduction of custom API methods (if any);
- production of [JSON-LD examples](/extension-template/examples/).

{: .important }
The documentation must be written in [Markdown](https://www.markdownguide.org) and will be compiled automatically using [Jekyll](https://jekyllrb.com) against the [Just the Docs](https://just-the-docs.com) theme. Each time you `git push`, a GitHub action will wake up and take care of it. Once compiled successfully, your documentation will be deployed on GitHub Pages on the SKG-IF website, despite being initially hidden in the left-hand-side menu. Please follow the indications and the examples provided and feel free to customise it as long as it complies with the overall workflow.


## Repository structure
The repository for your extension comes with a folder structure that should guide you in the extension development process.
While most of the structure is in general non-prescriptive, some parts (e.g., versioning) are binding.
Please review the following to learn how to structure information in your repository.

{: .highlight }
Provided that your extension acronym of choice is `abc`, your repository will be named `ext-abc` to conveniently locate extension repositories under the SKG-IF organisation on GitHub. For example, the repository [`ext-ra-skg`](https://github.com/skg-if/ext-ra-skg) is the repository name of the extension `RA-SKG`.


### The `data-model` folder
This folder contains material necessary to implement the data model for SKG-IF extension. 

It contains:
* The directory `ontology`, which includes all the versions of the OWL ontology developed for implementing the data model. In particular, this directory:
  * must contain a directory for each version of the ontology developed, named using the [semantic versioning system](https://semver.org/) of the version of the ontology (e.g., `1.0.0`, `1.1.3`, `2.5.1`, etc.); 
  * must contain the directory `current` that contains the last available version of the ontology;
  * all OWL files defining the ontology (despite the version considered) must be named using the acronym of the extension as defined in the related SKG-IF GitHub repository assigned with the extension, without considering the prefix `ext-`, plus a `.` and the format used to linearised the ontology - N-Triples (`.nt`), Turtle (`.ttl`), RDF/XML (`.xml`), JSON-LD (`.json`), and HTML (`.html`). For instance, the file name for the ontology defined for implementing the [RA-SKG extension](https://github.com/skg-if/ext-ra-skg) data model in Turtle format is `ra-skg.ttl`.
* The directory `shacl` contains all the versions of the SHACL document developed, to track the evolution of the semantic validation document in time. This directory:
  * must contain a directory for each version of the SHACL document developed, named using the [semantic versioning system](https://semver.org/) of the version of the context (e.g., `1.0.0`, `1.1.3`, `2.5.1`, etc.); 
  * must contain the directory `current` that contains the last available version of the SHACL document;
  * all SHACL document files defining the validation document (despite the version considered) must be named `shacl.ttl`.

An exemplar structure has been provided in the current template, containing the directory for version `1.0.0`, the directory `current` (which is a static copy of directory `1.0.0`), and empty files in each directory, for both the `ontology` directory and `shacl` directory. If this structure is followed, permanent w3id.org URLs are generated automatically for accessing all the files. In particular:
* the current (i.e., last) version of the OWL ontology implementing the data model for an extension is available at the following URL pattern: 

  ```
  https://w3id.org/skg-if/extension/<extension acronym>/ontology/<extension acronym>/
  ```
* the particular version of the ontology of implementing the data model of an extension, instead, can be accessed using a version number at the end of the the `w3id.org` URL, following this pattern:
  
  ```
  https://w3id.org/skg-if/extension/<extension acronym>/ontology/<extension acronym>/<X.Y.Z>/
  ```
* the current (i.e., last) version of the SHACL document for validating the data model for an extension is available at the following URL pattern: 

  ```
  https://w3id.org/skg-if/extension/<extension acronym>/validation/shacl/
  ```
* the particular version of the ontology of the SHACL document for validating the data model of an extension, instead, can be accessed using a version number at the end of the the `w3id.org` URL, following this pattern:
  
  ```
  https://w3id.org/skg-if/extension/<extension acronym>/validation/shacl/<X.Y.Z>/
  ```

The `<extension acronym>` in the URLs above is the acronym of the extension as defined in the related SKG-IF GitHub repository assigned with the extension, without considering the prefix `ext-`. For instance, the current ontology for the [RA-SKG extension](https://github.com/skg-if/ext-ra-skg) is accessible at the URL [https://w3id.org/skg-if/extension/ra-skg/ontology/ra-skg/](https://w3id.org/skg-if/extension/ra-skg/ontology/ra-skg/).

Instead, `<X.Y.Z>` in the URLs above identifies the version number of the particular context developed for the extension. For instance, the ontology having version `1.0.0` for the [RA-SKG extension](https://github.com/skg-if/ext-ra-skg) is accessible at the URL [https://w3id.org/skg-if/extension/ra-skg/ontology/ra-skg/1.0.0/](https://w3id.org/skg-if/extension/ra-skg/ontology/ra-skg/1.0.0/).


### The `context` folder
This folder contains the JSON-LD context for SKG-IF extension. 

The directory `ver` contains all the versions of the JSON-LD context developed, to track the evolution of the context in time. This directory:
* must contain a directory for each version of the context developed, named using the [semantic versioning system](https://semver.org/) of the version of the context (`1.0.0`, `1.1.3`, `2.5.1`, etc.); 
* must contain the directory `current` that contains the last available version of the context;
* all JSON-LD files defining the context (despite the version considered) must be named `skg-if.json`.

An exemplar structure has been provided in the current template, containing the directory for version `1.0.0`, the directory `current` (which is a static copy of directory `1.0.0`), and empty JSON-LD context files in each directory. If this structure is followed, permanent w3id.org URLs are generated automatically for accessing the context files. In particular:
* the current (i.e., last) version of the JSON-LD context for an extension is available at the following URL pattern: 

  ```
  https://w3id.org/skg-if/extension/<extension acronym>/context/skg-if.json
  ```
* the particular version of a context of the extension, instead, can be accessed using a version number in the `w3id.org` URL, before the name of the JSON file, following this pattern:
  ```
  https://w3id.org/skg-if/extension/<extension acronym>/context/<X.Y.Z>/skg-if.json
  ```

The `<extension acronym>` in the URLs above is the acronym of the extension as defined in the related SKG-IF GitHub repository assigned with the extension, without considering the prefix `ext-`. For instance, the current context for the [RA-SKG extension](https://github.com/skg-if/ext-ra-skg) is accessible at the URL [https://w3id.org/skg-if/extension/ra-skg/context/skg-if.json](https://w3id.org/skg-if/extension/ra-skg/context/skg-if.json).

Instead, `<X.Y.Z>` in the URLs above identifies the version number of the particular context developed for the extension. For instance, the context having version `1.0.0` for the [RA-SKG extension](https://github.com/skg-if/ext-ra-skg) is accessible at the URL [https://w3id.org/skg-if/extension/ra-skg/context/1.0.0/skg-if.json](https://w3id.org/skg-if/extension/ra-skg/context/1.0.0/skg-if.json).


### The `interoperability-framework` folder
This folder contains most of the documentation pages describing how your extension effectively extends core entities (i.e., their properties and relations) and the new entities (and their properties and relations) it introduces.
To provide some structure, the repository contains two subfolders for the aforementioned purposes.


### The `examples` folder
This folder contains JSON-LD examples of real or mock data compliant to the specification of your extension.


### The `api` folder
This folder contains the documentation pages relative to the api customisation that your extension intends to introduce.
For the starter, one file is provided, but nothing prevents you from structuring the pages in a more articulated manner.