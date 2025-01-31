# *Percona Distribution for MySQL Operator* 1.10.0


* **Date**

    November 24, 2021



* **Installation**

    For installation please refer to [the documentation page](https://www.percona.com/doc/kubernetes-operator-for-pxc/index.html#quickstart-guides)


## Release Highlights


* [Custom sidecar containers](../sidecar.md#operator-sidecar) allow users to customize Percona XtraDB Cluster and other Operator components without changing the container images. In this release, we enable even more customization, by allowing users to mount volumes into the sidecar containers.


* In this release, we put a lot of effort into fixing bugs that were reported by the community. We appreciate everyone who helped us with discovering these issues and contributed to the fixes.

## New Features


* [K8SPXC-856](https://jira.percona.com/browse/K8SPXC-856): Mount volumes into sidecar containers to enable customization (Thanks to Sridhar L for contributing)

## Improvements


* [K8SPXC-771](https://jira.percona.com/browse/K8SPXC-771): `spec.Backup.serviceAccount` and `spec.automountServiceAccountToken` Custom Resource options can now be used in the Helm chart (Thanks to Gerwin van de Steeg for reporting this issue)


* [K8SPXC-794](https://jira.percona.com/browse/K8SPXC-794): The `logrotate` command now doesn’t use verbose mode to avoid flooding the log with rotate information


* [K8SPXC-793](https://jira.percona.com/browse/K8SPXC-793): Logs are now strictly following JSON specification to simplify parsing


* [K8SPXC-789](https://jira.percona.com/browse/K8SPXC-789): New [source_retry_count](../operator.md#pxc-replicationchannels-configuration-sourceretrycount) and [source_connect_retry](../operator.md#pxc-replicationchannels-configuration-sourceconnectretry) options were added to tune source retries for replication between two clusters


* [K8SPXC-588](https://jira.percona.com/browse/K8SPXC-588): New [replicasServiceEnabled](../operator.md#haproxy-replicasserviceenabled) option was added to allow disabling the Kubernetes Service for `haproxy-replicas`, which may be useful to avoid the unwanted forwarding of the application write requests to all Percona XtraDB Cluster instances


* [K8SPXC-822](https://jira.percona.com/browse/K8SPXC-822): Logrotate now doesn’t rotate GRA logs (binlog events in ROW format representing the failed transaction) as ordinary log files, storing them for 7 days instead which gives additional time to debug the problem

## Bugs Fixed


* [K8SPXC-761](https://jira.percona.com/browse/K8SPXC-761): Fixed a bug where HAProxy container was not setting explicit USER id, being incompatible with the runAsNonRoot security policy (Thanks to Henno Schooljan for reporting this issue)


* [K8SPXC-894](https://jira.percona.com/browse/K8SPXC-894): Fixed a bug where trailing white spaces in the `pmm-admin add` command caused reconcile loop on OpenShift


* [K8SPXC-831](https://jira.percona.com/browse/K8SPXC-831): Fixed a bug that made it possible to have a split-brain situation, when two nodes were starting their own cluster in case of a DNS failure


* [K8SPXC-796](https://jira.percona.com/browse/K8SPXC-796): Fixed a bug due to which S3 backup deletion didn’t delete Pods attached to the backup job if the S3 finalizer was set (Thanks to Ben Langfeld for reporting this issue)


* [K8SPXC-876](https://jira.percona.com/browse/K8SPXC-876): Stopped using the `service.alpha.kubernetes.io/tolerate-unready-endpoints` deprecated Kubernetes option in the `${clustername}-pxc-unready` service annotation (Thanks to Antoine Habran for reporting this issue)


* [K8SPXC-842](https://jira.percona.com/browse/K8SPXC-842): Fixed a bug where backup finalizer didn’t delete data from S3 if the backup path contained a folder inside of the S3 bucket (Thanks to 申祥瑞 for reporting this issue)


* [K8SPXC-812](https://jira.percona.com/browse/K8SPXC-812): Fix a bug due to which the Operator didn’t support cert-manager versions since v0.14.0 (Thanks to Ben Langfeld for reporting this issue)


* [K8SPXC-762](https://jira.percona.com/browse/K8SPXC-762): Fix a bug due to which the validating webhook was not accepting scale operation in the Operator cluster-wide mode (Thanks to Henno Schooljan for reporting this issue)


* [K8SPXC-893](https://jira.percona.com/browse/K8SPXC-893): Fix a bug where HAProxy service failed during the config validation check if there was a resolution fail with one of the PXC addresses


* [K8SPXC-871](https://jira.percona.com/browse/K8SPXC-871): Fix a bug that prevented removing a Percona XtraDB Cluster manual backup for PVC storage


* [K8SPXC-851](https://jira.percona.com/browse/K8SPXC-851): Fixed a bug where changing replication user password didn’t work


* [K8SPXC-850](https://jira.percona.com/browse/K8SPXC-850): Fixed a bug where the default weight value wasn’t set for a host in a replication channel


* [K8SPXC-845](https://jira.percona.com/browse/K8SPXC-845): Fixed a bug where using malformed cr.yaml caused stuck cases in cluster deletion


* [K8SPXC-838](https://jira.percona.com/browse/K8SPXC-838): Fixed a bug due to which the Log Collector and PMM containers with unspecified memory and CPU requests were inheriting them from the PXC container


* [K8SPXC-824](https://jira.percona.com/browse/K8SPXC-824): Cluster may get into an unrecoverable state with incomplete full crash


* [K8SPXC-818](https://jira.percona.com/browse/K8SPXC-818): Fixed a bug which made Pods with a custom config inside a Secret or a ConfigMap not restarting at config update


* [K8SPXC-783](https://jira.percona.com/browse/K8SPXC-783): Fixed a bug where the root user was able to modify the monitor and clustercheck system users, making the possibility of cluster failure or misbehavior

## Supported Platforms

The following platforms were tested and are officially supported by the Operator 1.10.0:


* OpenShift 4.7 - 4.9


* Google Kubernetes Engine (GKE) 1.19 - 1.22


* Amazon Elastic Kubernetes Service (EKS) 1.17 - 1.21


* Minikube 1.22

This list only includes the platforms that the Percona Operators are specifically tested on as part of the release process. Other Kubernetes flavors and versions depend on the backward compatibility offered by Kubernetes itself.
