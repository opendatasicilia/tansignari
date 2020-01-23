# Messaggio Read the Docs di “build fails”: [cannot import name “PackageFinder” from “pip._internal.index”]

Può capitare che durante la procedura di compilazione del progetto su ReadtheDocs appaia un messaggio: *“cannot import name “PackageFinder” from “pip._internal.index”*.

## La causa

*Currently all builds are failing because the automatic upgrade (since #4823) to pip 20.0 was buggy (see pypa/pip#7620). There’s now a 20.0.1 release which seems to have fixed the problem for others … but how can I force my readthedocs to also upgrade to the .1 version?*

[Dall'issue del 20 gennaio 2020](https://github.com/readthedocs/readthedocs.org/issues/6554)

