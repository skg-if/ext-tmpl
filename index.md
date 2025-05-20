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
- description of the [data model](/extension-template/data-model/) and formal implementation in OWL + SHACL;
- production and documentation of an extended [JSON-LD context](/extension-template/context/);
- description of [extensions to core entities]({% link extension-template/interoperability-framework/core-extensions/ext-research-product.md %}) (properties and relations);
- description of [new entities]({% link extension-template/interoperability-framework/extension-entities/ext-entity.md %}) (properties and relations);
- [extension](/extension-template/api) to the core APIs; i.e., customisations of core API resolvers (if any) and/or introduction of custom API methods (if any);
- production of [JSON-LD examples](/extension-template/examples/).

{: .important }
The documentation must be written in [Markdown](https://www.markdownguide.org) and will be compiled automatically using [Jekyll](https://jekyllrb.com) against the [Just the Docs](https://just-the-docs.com) theme. Each time you `git push`, a GitHub action will wake up and take care of it. Once compiled successfully, your documentation will be deployed on GitHub Pages on the SKG-IF website, despite being initially hidden in the left-hand-side menu. Please follow the indications and the examples provided and feel free to customise it as long as it complies with the overall workflow.