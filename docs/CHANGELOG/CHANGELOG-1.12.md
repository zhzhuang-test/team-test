<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [v1.12.0-alpha.1](#v1120-alpha1)
  - [Downloads for v1.12.0-alpha.1](#downloads-for-v1120-alpha1)
  - [Changelog since v1.11.0](#changelog-since-v1110)
  - [Urgent Update Notes](#urgent-update-notes)
  - [Changes by Kind](#changes-by-kind)
    - [API Changes](#api-changes)
    - [Features & Enhancements](#features--enhancements)
    - [Deprecation](#deprecation)
    - [Bug Fixes](#bug-fixes)
    - [Security](#security)
  - [Other](#other)
    - [Dependencies](#dependencies)
    - [Helm Charts](#helm-charts)
    - [Instrumentation](#instrumentation)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# v1.12.0-alpha.1
## Downloads for v1.12.0-alpha.1

Download v1.12.0-alpha.1 in the [v1.12.0-alpha.1 release page](https://github.com/karmada-io/karmada/releases/tag/v1.12.0-alpha.1).

## Changelog since v1.11.0

## Urgent Update Notes

## Changes by Kind

### API Changes
- Introduced `extraVolumes` and `extraVolumemounts` to the `Karmada` API to optionally specify extra volumes and volume mounts for the Karmada API server component. ([#5509](https://github.com/karmada-io/karmada/pull/5509), @jabellard)
- Introduced a new condition `CompleteAPIEnablements` to represent api collection status of clusters. ([#5400](https://github.com/karmada-io/karmada/pull/5400), @whitewindmills)
- Introduced `PreserveResourcesOnDeletion` field to both PropagationPolicy and ClusterPropagationPolicy API, which provides the ability to roll back migration safely. ([#5575](https://github.com/karmada-io/karmada/pull/5575), @RainbowMango)
- API Change: Introduced `FieldOverrider` to both OverridePolicy and ClusterOverridePolicy, which provides the ability to override structured data nested in manifest like ConfigMap or Secret. ([#5581](https://github.com/karmada-io/karmada/pull/5581), @RainbowMango)

### Features & Enhancements
- implement preserveResourcesOnDeletion to support migration rollback. ([#5597](https://github.com/karmada-io/karmada/pull/5597), @a7i)
- Introduced `FieldOverrider` for overriding values in JSON and YAML. ([#5591](https://github.com/karmada-io/karmada/pull/5591), @sophiefeifeifeiya)
- standardize the naming of karmada config in local up installation method. ([#5679](https://github.com/karmada-io/karmada/pull/5679), @chaosi-zju)
- `karmadactl`: Implementing autocompletion for karmadactl to save a lot of typing. ([#5533](https://github.com/karmada-io/karmada/pull/5533), @zhzhuang-zju)
- `karmadactl`: Added shorthand letter `s` to 'operation-scope' flags across commands. ([#5483](https://github.com/karmada-io/karmada/pull/5483), @ahorine)
- `karmadactl`: `karmadactl init` support multiple label selection ability with flag `EtcdNodeSelectorLabels`. ([#5321](https://github.com/karmada-io/karmada/pull/5321), @tiansuo114)
- `karmadactl`: set `PreserveResourcesOnDeletion` by default in auto-created propagation policy during promotion process. ([#5601](https://github.com/karmada-io/karmada/pull/5601), #wulemao)
- `karmada-sheduler`: The `scheduler-estimator-service-namespace` flag is introduced, which can be used to explicitly specify the namespace that should be used to discover scheduler estimator services. For backwards compatibility, when not explicitly set, the default value of `karmada-system` is retained. ([#5478](https://github.com/karmada-io/karmada/pull/5478), @jabellard)
- `karmada-desheduler`: The `scheduler-estimator-service-namespace` flag is introduced, which can be used to explicitly specify the namespace that should be used to discover scheduler estimator services. For backwards compatibility, when not explicitly set, the default value of `karmada-system` is retained. ([#5478](https://github.com/karmada-io/karmada/pull/5478), @jabellard)
- `karmada-controller-manager`: The health status of resources without ResourceInterpreter customization will be treated as healthy by default. ([#5530](https://github.com/karmada-io/karmada/pull/5530), @a7i)
- `karmada-webhook`: validate fieldOverrider operation. ([#5671](https://github.com/karmada-io/karmada/pull/5671), @chaunceyjiang)

### Deprecation
- The following flags have been deprecated from release `v1.11.0` and now have been removed: 
    * `karmada-agent`: ([#5548](https://github.com/karmada-io/karmada/pull/5548), @whitewindmills)
      --bind-address
      --secure-port    
    * `karmada-controller-manager`: ([#5549](https://github.com/karmada-io/karmada/pull/5549), @whitewindmills)
     --bind-address
     --secure-port
    * `karmada-scheduler-estimator`: ([#5555](https://github.com/karmada-io/karmada/pull/5555), @seanlaii)
      --bind-address
      --secure-port
    * `karmada-scheduler`: ([#5551](https://github.com/karmada-io/karmada/pull/5551), @chaosi-zju)
      --bind-address
      --secure-port
    * `karmada-descheduler`: ([#5552](https://github.com/karmada-io/karmada/pull/5552), @chaosi-zju)
      --bind-address
      --secure-port

### Bug Fixes
- `karmada-operator`: Fixed the issue where the manifests for the `karmada-scheduler` and `karmada-descheduler` components were not parsed correctly. ([#5546](https://github.com/karmada-io/karmada/pull/5546), @jabellard)
- `karmada-operator`: Fixed `system:admin` can not proxy to member cluster issue. ([#5572](https://github.com/karmada-io/karmada/pull/5572), @chaosi-zju)
- `karmada-aggregate-apiserver`: limit aggregate apiserver http method to get. User can modify member cluster's object with * in aggregated apiserver url. ([#5430](https://github.com/karmada-io/karmada/pull/5430), @spiritNO1)
- `karmada-scheduler`: skip the filter if the cluster is already in the list of scheduling result even if the API is missed. ([#5216](https://github.com/karmada-io/karmada/pull/5216), @yanfeng1992)
- `karmada-controller-manager`: Ignored StatefulSet Dependencies with PVCs created via the VolumeClaimTemplates. ([#5568](https://github.com/karmada-io/karmada/pull/5568), @jklaw90)
- `karmada-controller-manager`: Clean up the residual annotations when resources are preempted by pp from cpp. ([#5563](https://github.com/karmada-io/karmada/pull/5563), @zhzhuang-zju)
- `karmada-controller-manager`: Fixed an issue that policy claim metadata might be lost during the rapid deletion and creation of PropagationPolicy(s)/ClusterPropagationPolicy(s). ([#5319](https://github.com/karmada-io/karmada/pull/5319), @zhzhuang-zju)
- `karmadactl`：Fixed the issue where commands `create`, `annotate`, `delete`, `edit`, `label`, and `patch` cannot specify the namespace flag. ([#5487](https://github.com/karmada-io/karmada/pull/5487), @zhzhuang-zju)
- `karmadactl`: Fixed the issue that karmadactl addon failed to install karmada-scheduler-estimator due to unknown flag. ([#5523](https://github.com/karmada-io/karmada/pull/5523), @chaosi-zju)

### Security

## Other
### Dependencies
- `karmada-apiserver` and `kube-controller-manager` is using v1.30.4 by default. ([#5515](https://github.com/karmada-io/karmada/pull/5515), @liangyuanpeng)
- The base image `alpine` now has been promoted from `alpine:3.20.2` to `alpine:3.20.3`.
- Karmada now using Golang v1.22.7. ([#5529](https://github.com/karmada-io/karmada/pull/5529), @yelshall)

### Helm Charts
- `Helm chart`: Added helm index for v1.10.0 and v1.11.0 release. ([#5579](https://github.com/karmada-io/karmada/pull/5579), @chaosi-zju)

### Instrumentation
