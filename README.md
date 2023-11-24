

# README

## Two Propositions

- **Proposition 01:** 
    * `Application CRD` that contains several components in the same YAML file. (Similar to the `llorechestrator` with minor modifications).
    * Adding status (Running, Pending, Failed).
    * Removing cluster field from app, and adding `internalCommunications` to describe the communications between the deffirent components. 
    * Adding `is_exposing_metrics` to automatically create a `ServiceMonitor` and allow prometheus scrape the metrics.
    * Adding `Replicas field` instead of hardcoding it to "1" in the deployment template.
 
- **Proposition 02:**
    * `Application CRD` and `Component CRD` separated.
    - The App CRD must be applied     first, and then the components of the app. If the Component CRD is applied before the App CRD, an exception will be fired.

    - If the App CRD is applied and the one of the its components is not yet created, the status of the app will be pending.

## Communication between two applications CRD
- The `communicationBetweenTwoApps` CRD allows communication between two components of different apps. [Check this video](https://www.youtube.com/watch?v=TikEgvwhdJ8)

## Templates

- `Prometheus_template` and `ServiceMonitor_template` are used to create a Prometheus instance that scrapes the metrics exposed by a component if `is_exposing_metrics` is set to true.
- `ExternalNameService_template` is used to allow a pod communicate with another pod which exist in a deffirent namespace. 

## Operator: 
* Based on the chosen proposition, some modifications for the current operator will be required (namespace offloading, exposing metrics).
* An operator for the `communicationBetweenTwoApps` CRD must be implemented  (configure the ExternalNameService_template and apply it and establish communication between the necessary clusters).
* Adding a `Daemon or timer` handler to watch and update the status of the CRD instance.


## What can also be done: 
* Adding support for statefullSet and volumes. 

