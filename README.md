# OpenShift workshops content

Workshop content designed to be used by the [Workshopper tool](https://github.com/osevg/workshopper).

## Using this content

Either use the content directly by pointing at this repository

```
https://raw.githubusercontent.com/appuio/workshopper-content/master/
```

or host locally as static content, e.g. on OpenShift using the PHP S2I builder

```
$ oc new-app php~https://github.com/appuio/workshopper-content.git
```

and use that url to feed Workshopper with content.


## Create a full workshop

You can follow this instructions to create a full workshop site:

```
$ oc new-project appuio-techlab
$ oc new-app osevg/workshopper -e WORKSHOPS_URLS="https://raw.githubusercontent.com/appuio/workshopper-content/master/_workshops/training.yml" -e CONSOLE_ADDRESS=ose3-lab-master.puzzle.ch:8443 -e ROUTER_ADDRESS=ose3-lab.puzzle.ch -e DOCS_URL=docs.openshift.org --name appuio-techlab -n appuio-techlab
$ oc expose service appuio-techlab --hostname techlab.ose3-lab.puzzle.ch -n appuio-techlab
```

NOTE: You will need the following ENV values:

* *WORKSHOPS_URLS*: Raw URL for a training. There's some trainings [here](https://github.com/appuio/workshopper-content/tree/master/_workshops)

Depending on the workshop, you might need additional ENV. These are defined per workshop. In the sample use, we define:
* *CONSOLE_ADDRESS*: Address to the master server's console
* *ROUTER_ADDRESS*: Wildcard DNS used for deployed apps
* *DOCS_URL*: Link to the OpenShift documentation
