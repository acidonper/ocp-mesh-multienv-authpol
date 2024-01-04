# Openshift Service Mesh - Multi-environments based on Authorization Policies

This repository collects information and a real example to manage multiple logical environments in Openshift Service Mesh based on AuthorizationPolicies.

## Prerequisites

* Openshift 4.14+
* Openshift Service Mesh 2.4.5+

## Setting Up

* Deploy OSSM Operator, control plane and SMMR

```
$ oc apply -f files/istio.yaml
$ sleep 60  (*Waiting for operators installation)
$ oc apply -f files/istio-controlplane.yaml
$ oc apply -f files/istio-smmr.yaml
```


* Create the environments (namespaces, deployments, services and authorizationpolicies) to test the different use cases:

```
$ helm template . | oc apply -f -
```

## Testing

* Go to a specific project (E.g. pro01)

```
$ oc project pro01support-tool
```

* Connect to the specific support-tool-deployment-xx pod (E.g. pro01)

```
$ oc rsh support-tool-deployment-5fbdb87455-6rj5x
```

* Perform a set of curl to check connections

```
$ curl support-tool.pro03.svc.cluster.local:8080
RBAC: access denied

$ curl support-tool.pro02.svc.cluster.local:8080
...
        </div>
        </body>
</html>

$ curl support-tool.pro01.svc.cluster.local:8080
...
        </div>
        </body>
</html>

```

## Author

Asier Cidon @RedHat
