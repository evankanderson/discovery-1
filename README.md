# Knative Discovery API

**[This component is ALPHA](https://github.com/knative/community/tree/main/mechanics/MATURITY-LEVELS.md)**

[![go.dev reference](https://img.shields.io/badge/go.dev-reference-007d9c?logo=go&logoColor=white)](https://pkg.go.dev/knative.dev/discovery)
[![Go Report Card](https://goreportcard.com/badge/knative.dev/discovery)](https://goreportcard.com/report/knative.dev/discovery)
[![Releases](https://img.shields.io/github/release-pre/knative-sandbox/discovery.svg)](https://github.com/knative-sandbox/discovery/releases)
[![LICENSE](https://img.shields.io/github/license/knative-sandbox/discovery.svg)](https://github.com/knative-sandbox/discovery/blob/master/LICENSE)
[![TestGrid](https://img.shields.io/badge/testgrid-discovery-informational?logo=data:image/x-icon;base64,AAABAAEAICAAAAEACACoCAAAFgAAACgAAAAgAAAAQAAAAAEACAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALAAAAFQAAACoAAw0AAAAAVQAGGgAAAABgAAAAgAAKJgAAAACqAA0zAAATTAAAGmYAAB1zAAAmmQAAM8wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACgoKCgoKCAsQEBAQEBANDRAQEBAQEAsPEBAQEBAQAAAKCgoKCgoICxAQEBAQEA0NEBAQEBAQCw8QEBAQEBAAAAoKCgoKCggLEBAQEBAQDQ0QEBAQEBALDxAQEBAQEAAACgoKCgoKCAsQEBAQEBANDRAQEBAQEAsPEBAQEBAQAAAKCgoKCgoICxAQEBAQEA0NEBAQEBAQCw8QEBAQEBAAAAoKCgoKCggLEBAQEBAQDQ0QEBAQEBALDxAQEBAQEAAACAgICAgIBwkPDw8PDw8MDA8PDw8PDwkODw8PDw8PAAALCwsLCwsJBAsLCwsLCwYCAwMDAwMDAQkLCwsLCwsAABAQEBAQEA8LEBAQEBAQDQUKCgoKCgoDDxAQEBAQEAAAEBAQEBAQDwsQEBAQEBANBQoKCgoKCgMPEBAQEBAQAAAQEBAQEBAPCxAQEBAQEA0FCgoKCgoKAw8QEBAQEBAAABAQEBAQEA8LEBAQEBAQDQUKCgoKCgoDDxAQEBAQEAAAEBAQEBAQDwsQEBAQEBANBQoKCgoKCgMPEBAQEBAQAAAQEBAQEBAPCxAQEBAQEA0FCgoKCgoKAw8QEBAQEBAAAA0NDQ0NDQwGDQ0NDQ0NCwMFBQUFBQUCDA0NDQ0NDQAADQ0NDQ0NDAIFBQUFBQUDCw0NDQ0NDQYMDQ0NDQ0NAAAQEBAQEBAPAwoKCgoKCgUNEBAQEBAQCw8QEBAQEBAAABAQEBAQEA8DCgoKCgoKBQ0QEBAQEBALDxAQEBAQEAAAEBAQEBAQDwMKCgoKCgoFDRAQEBAQEAsPEBAQEBAQAAAQEBAQEBAPAwoKCgoKCgUNEBAQEBAQCw8QEBAQEBAAABAQEBAQEA8DCgoKCgoKBQ0QEBAQEBALDxAQEBAQEAAAEBAQEBAQDwMKCgoKCgoFDRAQEBAQEAsPEBAQEBAQAAALCwsLCwsJAQMDAwMDAwIGCwsLCwsLBAkLCwsLCwsAAA8PDw8PDw4JDw8PDw8PDAwPDw8PDw8JBwgICAgICAAAEBAQEBAQDwsQEBAQEBANDRAQEBAQEAsICgoKCgoKAAAQEBAQEBAPCxAQEBAQEA0NEBAQEBAQCwgKCgoKCgoAABAQEBAQEA8LEBAQEBAQDQ0QEBAQEBALCAoKCgoKCgAAEBAQEBAQDwsQEBAQEBANDRAQEBAQEAsICgoKCgoKAAAQEBAQEBAPCxAQEBAQEA0NEBAQEBAQCwgKCgoKCgoAABAQEBAQEA8LEBAQEBAQDQ0QEBAQEBALCAoKCgoKCgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA)](https://testgrid.knative.dev/discovery)
[![Slack Status](https://img.shields.io/badge/slack-join_chat-white.svg?logo=slack&style=social)](https://knative.slack.com)

This is Work in Progress. It is based on the [Discovery API](./docs/proposal.md)
design doc.

## Install

TODO: instructions on installing nightly and a release.

## Development

Install,

```shell script
ko apply -f ./config
```

If you modify the ClusterDuckType definition, you may have to update the ClusterDuckType's OpenAPI Schema. Refer to [hack/schema](https://github.com/knative/hack/tree/main/schema) to help generate the schema definition.

## ClusterDuckType:discovery.knative.dev/v1alpha1

The goal is to have a custom type that is user installable to help a developer,
cluster admin, or tooling to better understand the duck types that are installed
in the cluster. This information could be used to understand which Kinds could
fulfill a role for another resource.

### demos.example.com.yaml

```yaml
apiVersion: discovery.knative.dev/v1alpha1
kind: ClusterDuckType
metadata:
  name: demos.example.com
spec:
  # selectors is a list of CRD label selectors to find CRDs that have been
  # labeled as the given duck type.
  selectors:
    - labelSelector: "example.com/demo=true"

  # Names allows us to give a short name to the duck type.
  names:
    name: "Demo"
    plural: "demos"
    singular: "demo"

  # Versions are to allow the definition of a single duck type with multiple
  # versions, useful if the duck type API shape changes.
  versions:
    - name: "v1"
      # refs allows for adding native types, or crds directly as the ducks via
      # Group/Version/Kind/Resource
      refs:
        - group: "demo.example.com"
          version: "v1"
          kind: "Demo"
      # additionalPrinterColumns is intended to understand what printer columns
      # should be used for the custom objects.
      additionalPrinterColumns:
        - name: Ready
          type: string
          jsonPath: ".status.conditions[?(@.type=='Ready')].status"
        - name: Reason
          type: string
          jsonPath: ".status.conditions[?(@.type=='Ready')].reason"
        - name: Demo
          type: string
          jsonPath: .status.demo
      # schema is the partial schema of the duck type.
      schema:
        openAPIV3Schema:
          properties:
            status:
              type: object
              properties:
                address:
                  type: object
                  properties:
                    demo:
                      type: string

  # Role holds an Aggregating Role used by the duck type to manage the ducks.
	# If not specified, the Selectors are used to find a Role with an aggregation rule that matches a selector
  role:
    roleRef:
      kind: ClusterRole
      name: view
      apiGroup: rbac.authorization.k8s.io
  group: example.com
```

### Demo

Using
[`addressables.duck.knative.dev.yaml`](./config/knative/addressables.duck.knative.dev.yaml),
we will apply it,

```shell
kubectl apply -f ./config/knative/addressables.duck.knative.dev.yaml
```

```text
clusterducktype.discovery.knative.dev/addressables.duck.knative.dev created
```

After applying this, you can fetch it:

```shell
kubectl get cducks addressables.duck.knative.dev
```

```text
NAME                            SHORT NAME    DUCKS   READY   REASON
addressables.duck.knative.dev   addressable   6       True
```

And get the full DuckType `addressables.duck.knative.dev` resource:

```shell
kubectl get clusterducktypes addressables.duck.knative.dev -oyaml
```

```yaml
apiVersion: discovery.knative.dev/v1alpha1
kind: ClusterDuckType
metadata:
  generation: 1
  name: addressables.duck.knative.dev
spec: ...
status:
  conditions:
    - lastTransitionTime: "2021-04-06T01:19:42Z"
      status: "True"
      type: Ready
  clusterRoleAggregationRule:
    clusterRoleSelectors:
      - matchLabels:
          duck.knative.dev/addressable: "true"
  duckCount: 7
  ducks:
    v1:
      - accessibleByClusterRole: true
        apiVersion: eventing.knative.dev/v1
        kind: Broker
        scope: Namespaced
      - accessibleByClusterRole: true
        apiVersion: eventing.knative.dev/v1beta1
        kind: Broker
        scope: Namespaced
      - accessibleByClusterRole: true
        apiVersion: flows.knative.dev/v1
        kind: Parallel
        scope: Namespaced
      - accessibleByClusterRole: true
        apiVersion: flows.knative.dev/v1
        kind: Sequence
        scope: Namespaced
      - accessibleByClusterRole: true
        apiVersion: flows.knative.dev/v1beta1
        kind: Parallel
        scope: Namespaced
      - accessibleByClusterRole: true
        apiVersion: flows.knative.dev/v1beta1
        kind: Sequence
        scope: Namespaced
      - accessibleByClusterRole: true
        apiVersion: messaging.knative.dev/v1
        kind: Channel
        scope: Namespaced
      - accessibleByClusterRole: true
        apiVersion: messaging.knative.dev/v1
        kind: InMemoryChannel
        scope: Namespaced
      - accessibleByClusterRole: true
        apiVersion: messaging.knative.dev/v1beta1
        kind: Channel
        scope: Namespaced
      - accessibleByClusterRole: true
        apiVersion: messaging.knative.dev/v1beta1
        kind: InMemoryChannel
        scope: Namespaced
      - accessibleByClusterRole: true
        apiVersion: serving.knative.dev/v1
        kind: Route
        scope: Namespaced
      - accessibleByClusterRole: true
        apiVersion: serving.knative.dev/v1
        kind: Service
        scope: Namespaced
  observedGeneration: 1
```

## Knative Duck Types

If the `./config/knative` directory is applied (via
`kubectl apply -f config/knative`), a quick view of the duck types used by
Knative in this cluster becomes easier to find:

```shell
kubectl get clusterducktypes
```

```text
NAME                            SHORT NAME    DUCKS   READY   REASON
addressables.duck.knative.dev   Addressable   6       True
bindings.duck.knative.dev       Binding       1       True
channelables.duck.knative.dev   Channelable   0       True
podspecables.duck.knative.dev   PodSpecable   7       True
sources.duck.knative.dev        Source        4       True
```

_Note_: there is also a short name: `cducks`

```shell
kubectl get cducks
```
