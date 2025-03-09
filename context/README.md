# SKG-IF Extension: JSON-LD context

This repository contains the JSON-LD context for SKG-IF extension. 

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