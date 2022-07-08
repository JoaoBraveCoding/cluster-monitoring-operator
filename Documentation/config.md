# Cluster Monitoring Configuration Reference

Parts of Cluster Monitoring are configurable. Depending on which part of
the stack users want to configure, they should edit the following:

-   Configuration of OpenShift Container Platform monitoring components
    lies in a ConfigMap called
    `` cluster-monitoring-config`in the `openshif ``-monitoring\`namespace.

-   Configuration of components that monitor user-defined projects lies
    in a ConfigMap called `user-workload-monitoring-config` in the
    `openshift-user-workload-monitoring` namespace.

The configuration file itself is always defined under the `config.yaml`
key within the ConfigMap’s data.

Monitoring a platform such as OpenShift requires a coordination of
multiple components that must work well between themselves. However,
users should be able to customize the monitoring stack in such a way
that they end up with a resilient and highly available monitoring
solution. Despite this, to avoid users from misconfiguring the
monitoring stack of their clusters not all configuration parameters are
exposed.

Configuring Cluster Monitoring is optional. If the config does not exist
or is empty or malformed, then defaults will be used.

# ClusterMonitoringConfiguration

<table>
<caption>AlertmanagerMainConfig [AlertmanagerMainConfig defines
configuration related with the main Alertmanager instance.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>enabled</p></td>
<td style="text-align: left;"><p>Enabled a boolean flag to enable or
disable the main Alertmanager instance under openshift-monitoring
default: true</p></td>
<td style="text-align: left;"><p>*bool</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>enableUserAlertmanagerConfig</p></td>
<td style="text-align: left;"><p>EnableUserAlertManagerConfig boolean
flag to enable or disable user-defined namespaces to be selected for
AlertmanagerConfig lookup, by default Alertmanager only looks for
configuration in the namespace where it was deployed to. This will only
work if the UWM Alertmanager instance is not enabled. default:
false</p></td>
<td style="text-align: left;"><p>bool</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>logLevel</p></td>
<td style="text-align: left;"><p>LogLevel defines the log level for
Alertmanager. Possible values are: error, warn, info, debug. default:
info</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>nodeSelector</p></td>
<td style="text-align: left;"><p>NodeSelector defines which Nodes the
Pods are scheduled on.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>resources</p></td>
<td style="text-align: left;"><p>Resources define resources requests and
limits for single Pods.</p></td>
<td style="text-align: left;"><p>*v1.ResourceRequirements</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>tolerations</p></td>
<td style="text-align: left;"><p>Tolerations defines the Pods
tolerations.</p></td>
<td style="text-align: left;"><p>[]v1.Toleration</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>volumeClaimTemplate</p></td>
<td style="text-align: left;"><p>VolumeClaimTemplate defines persistent
storage for Alertmanager. It’s possible to configure storageClass and
size of volume.</p></td>
<td
style="text-align: left;"><p>*monv1.EmbeddedPersistentVolumeClaim</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

AlertmanagerMainConfig \[AlertmanagerMainConfig defines configuration
related with the main Alertmanager instance.\]

<table>
<caption>K8sPrometheusAdapter [K8sPrometheusAdapter defines
configuration related with Prometheus Adapater]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>audit</p></td>
<td style="text-align: left;"><p>Audit defines the audit configuration
to be used by the prometheus adapter instance. Possible profile values
are: "metadata, request, requestresponse, none". default:
metadata</p></td>
<td style="text-align: left;"><p>*Audit</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>nodeSelector</p></td>
<td style="text-align: left;"><p>NodeSelector defines which Nodes the
Pods are scheduled on.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>tolerations</p></td>
<td style="text-align: left;"><p>Tolerations defines the Pods
tolerations.</p></td>
<td style="text-align: left;"><p>[]v1.Toleration</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

K8sPrometheusAdapter \[K8sPrometheusAdapter defines configuration
related with Prometheus Adapater\]

<table>
<caption>KubeStateMetricsConfig [KubeStateMetricsConfig defines
configuration related with the kube-state-metrics agent.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>nodeSelector</p></td>
<td style="text-align: left;"><p>NodeSelector defines which Nodes the
Pods are scheduled on.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>tolerations</p></td>
<td style="text-align: left;"><p>Tolerations defines the Pods
tolerations.</p></td>
<td style="text-align: left;"><p>[]v1.Toleration</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

KubeStateMetricsConfig \[KubeStateMetricsConfig defines configuration
related with the kube-state-metrics agent.\]

<table>
<caption>PrometheusK8sConfig [PrometheusK8sConfig holds configuration
related to the Prometheus component.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>additionalAlertmanagerConfigs</p></td>
<td style="text-align: left;"><p>AlertmanagerConfigs holds configuration
about how the Prometheus component should communicate with aditional
Alertmanager instances. default: nil</p></td>
<td style="text-align: left;"><p>[]AdditionalAlertmanagerConfig</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>enforcedBodySizeLimit</p></td>
<td style="text-align: left;"><p>EnforcedBodySizeLimit enforces body
size limit of Prometheus scrapes, if a scrape is bigger than the limit
it will fail. 3 kinds of values are accepted: 1. empty value: no limit
2. a value in Prometheus size format, e.g. "64MB" 3. string "automatic",
which means the limit will be automatically calculated based on cluster
capacity. default: 64MB</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>externalLabels</p></td>
<td style="text-align: left;"><p>ExternalLabels defines labels to be
added to any time series or alerts when communicating with external
systems (federation, remote storage, Alertmanager). default:
nil</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>logLevel</p></td>
<td style="text-align: left;"><p>LogLevel defines the log level for
Prometheus. Possible values are: error, warn, info, debug. default:
info</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>nodeSelector</p></td>
<td style="text-align: left;"><p>NodeSelector defines which Nodes the
Pods are scheduled on.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>queryLogFile</p></td>
<td style="text-align: left;"><p>QueryLogFile specifies the file to
which PromQL queries are logged. Suports both just a filename in which
case they will be saved to an emptyDir volume at /var/log/prometheus, if
a full path is given an emptyDir volume will be mounted at that
location. Relative paths not supported, also not supported writing to
linux std streams. default: ""</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>remoteWrite</p></td>
<td style="text-align: left;"><p>RemoteWrite Holds the remote write
configuration, everything from url, authorization to relabeling</p></td>
<td style="text-align: left;"><p>[]RemoteWriteSpec</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>resources</p></td>
<td style="text-align: left;"><p>Resources define resources requests and
limits for single Pods.</p></td>
<td style="text-align: left;"><p>*v1.ResourceRequirements</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>retention</p></td>
<td style="text-align: left;"><p>Retention defines the Time duration
Prometheus shall retain data for. Must match the regular expression
[0-9]+(ms|s|m|h|d|w|y) (milliseconds seconds minutes hours days weeks
years). default: 15d</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>retentionSize</p></td>
<td style="text-align: left;"><p>RetentionSize defines the maximum
amount of disk space used by blocks + WAL. default: nil</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>tolerations</p></td>
<td style="text-align: left;"><p>Tolerations defines the Pods
tolerations.</p></td>
<td style="text-align: left;"><p>[]v1.Toleration</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>volumeClaimTemplate</p></td>
<td style="text-align: left;"><p>VolumeClaimTemplate defines persistent
storage for Prometheus. It’s possible to configure storageClass and size
of volume.</p></td>
<td
style="text-align: left;"><p>*monv1.EmbeddedPersistentVolumeClaim</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

PrometheusK8sConfig \[PrometheusK8sConfig holds configuration related to
the Prometheus component.\]

<table>
<caption>PrometheusOperatorConfig [PrometheusOperatorConfig holds
configuration related to Prometheus Operator.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>logLevel</p></td>
<td style="text-align: left;"><p>LogLevel defines the log level for
Prometheus Operator. Possible values are: error, warn, info, debug.
default: info</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>nodeSelector</p></td>
<td style="text-align: left;"><p>NodeSelector defines which Nodes the
Pods are scheduled on.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>tolerations</p></td>
<td style="text-align: left;"><p>Tolerations defines the Pods
tolerations.</p></td>
<td style="text-align: left;"><p>[]v1.Toleration</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

PrometheusOperatorConfig \[PrometheusOperatorConfig holds configuration
related to Prometheus Operator.\]

<table>
<caption>OpenShiftStateMetricsConfig [OpenShiftStateMetricsConfig holds
configuration related to openshift-state-metrics agent.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>nodeSelector</p></td>
<td style="text-align: left;"><p>NodeSelector defines which Nodes the
Pods are scheduled on.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>tolerations</p></td>
<td style="text-align: left;"><p>Tolerations defines the Pods
tolerations.</p></td>
<td style="text-align: left;"><p>[]v1.Toleration</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

OpenShiftStateMetricsConfig \[OpenShiftStateMetricsConfig holds
configuration related to openshift-state-metrics agent.\]

<table>
<caption>ThanosQuerierConfig [ThanosQuerierConfig holds configuration
related to Thanos Querier component.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>enableRequestLogging</p></td>
<td style="text-align: left;"><p>EnableRequestLogging boolean flag to
enable or disable request logging default: false</p></td>
<td style="text-align: left;"><p>bool</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>logLevel</p></td>
<td style="text-align: left;"><p>LogLevel defines the log level for
Thanos Querier. Possible values are: error, warn, info, debug. default:
info</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>nodeSelector</p></td>
<td style="text-align: left;"><p>NodeSelector defines which Nodes the
Pods are scheduled on.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>resources</p></td>
<td style="text-align: left;"><p>Resources define resources requests and
limits for single Pods.</p></td>
<td style="text-align: left;"><p>*v1.ResourceRequirements</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>tolerations</p></td>
<td style="text-align: left;"><p>Tolerations defines the Pods
tolerations.</p></td>
<td style="text-align: left;"><p>[]v1.Toleration</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

ThanosQuerierConfig \[ThanosQuerierConfig holds configuration related to
Thanos Querier component.\]

<table>
<caption>AdditionalAlertmanagerConfig [AdditionalAlertmanagerConfig
defines configuration on how a component should communicate with
aditional Alertmanager instances.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>apiVersion</p></td>
<td style="text-align: left;"><p>APIVersion defines the api version of
Alertmanager.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>bearerToken</p></td>
<td style="text-align: left;"><p>BearerToken defines the bearer token to
use when authenticating to Alertmanager.</p></td>
<td style="text-align: left;"><p>*v1.SecretKeySelector</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>pathPrefix</p></td>
<td style="text-align: left;"><p>PathPrefix defines the path prefix to
add in front of the push endpoint path.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>scheme</p></td>
<td style="text-align: left;"><p>Scheme the URL scheme to use when
talking to Alertmanagers.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>staticConfigs</p></td>
<td style="text-align: left;"><p>StaticConfigs a list of statically
configured Alertmanagers.</p></td>
<td style="text-align: left;"><p>[]string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>timeout</p></td>
<td style="text-align: left;"><p>Timeout defines the timeout used when
sending alerts.</p></td>
<td style="text-align: left;"><p>*string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>tlsConfig</p></td>
<td style="text-align: left;"><p>TLSConfig defines the TLS Config to use
for alertmanager connection.</p></td>
<td style="text-align: left;"><p>TLSConfig</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

AdditionalAlertmanagerConfig \[AdditionalAlertmanagerConfig defines
configuration on how a component should communicate with aditional
Alertmanager instances.\]

<table>
<caption>RemoteWriteSpec [RemoteWriteSpec is almost a 1to1 copy of
monv1.RemoteWriteSpec but with the BearerToken field removed. In the
future other fields might be added here.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>authorization</p></td>
<td style="text-align: left;"><p>Authorization defines the authorization
section for remote write</p></td>
<td style="text-align: left;"><p>*monv1.SafeAuthorization</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>basicAuth</p></td>
<td style="text-align: left;"><p>BasicAuth defines configuration for
basic authentication for the URL.</p></td>
<td style="text-align: left;"><p>*monv1.BasicAuth</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>bearerTokenFile</p></td>
<td style="text-align: left;"><p>BearerTokenFile defines the file where
the bearer token for remote write resides.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>headers</p></td>
<td style="text-align: left;"><p>Headers custom HTTP headers to be sent
along with each remote write request. Be aware that headers that are set
by Prometheus itself can’t be overwritten.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>metadataConfig</p></td>
<td style="text-align: left;"><p>MetadataConfig configures the sending
of series metadata to remote storage.</p></td>
<td style="text-align: left;"><p>*monv1.MetadataConfig</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>name</p></td>
<td style="text-align: left;"><p>Name defines the name of the remote
write queue, must be unique if specified. The name is used in metrics
and logging in order to differentiate queues.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>oauth2</p></td>
<td style="text-align: left;"><p>OAuth2 configures OAuth2 authentication
for remote write.</p></td>
<td style="text-align: left;"><p>*monv1.OAuth2</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>proxyUrl</p></td>
<td style="text-align: left;"><p>ProxyURL defines an optional proxy
URL</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>queueConfig</p></td>
<td style="text-align: left;"><p>QueueConfig allows tuning of the remote
write queue parameters.</p></td>
<td style="text-align: left;"><p>*monv1.QueueConfig</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>remoteTimeout</p></td>
<td style="text-align: left;"><p>RemoteTimeout defines the timeout for
requests to the remote write endpoint.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>sigv4</p></td>
<td style="text-align: left;"><p>Sigv4 allows to configures AWS’s
Signature Verification 4</p></td>
<td style="text-align: left;"><p>*monv1.Sigv4</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>tlsConfig</p></td>
<td style="text-align: left;"><p>TLSConfig defines the TLS configuration
to use for remote write.</p></td>
<td style="text-align: left;"><p>*monv1.SafeTLSConfig</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>url</p></td>
<td style="text-align: left;"><p>URL defines the URL of the endpoint to
send samples to.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>writeRelabelConfigs</p></td>
<td style="text-align: left;"><p>WriteRelabelConfigs defines the list of
remote write relabel configurations.</p></td>
<td style="text-align: left;"><p>[]monv1.RelabelConfig</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

RemoteWriteSpec \[RemoteWriteSpec is almost a 1to1 copy of
monv1.RemoteWriteSpec but with the BearerToken field removed. In the
future other fields might be added here.\]

<table>
<caption>TLSConfig [TLSConfig configures the options for TLS
connections.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>ca</p></td>
<td style="text-align: left;"><p>CA defines the CA cert in the
Prometheus container to use for the targets.</p></td>
<td style="text-align: left;"><p>*v1.SecretKeySelector</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>cert</p></td>
<td style="text-align: left;"><p>Cert defines the client cert in the
Prometheus container to use for the targets.</p></td>
<td style="text-align: left;"><p>*v1.SecretKeySelector</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>key</p></td>
<td style="text-align: left;"><p>Key defines the client key in the
Prometheus container to use for the targets.</p></td>
<td style="text-align: left;"><p>*v1.SecretKeySelector</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>serverName</p></td>
<td style="text-align: left;"><p>ServerName used to verify the hostname
for the targets.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>insecureSkipVerify</p></td>
<td style="text-align: left;"><p>InsecureSkipVerify disable target
certificate validation.</p></td>
<td style="text-align: left;"><p>bool</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

TLSConfig \[TLSConfig configures the options for TLS connections.\]

# UserWorkloadConfiguration

<table>
<caption>AlertmanagerUserWorkloadConfig [AlertmanagerUserWorkloadConfig
defines configuration for the Alertmanager instance for user-defined
projects.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>enabled</p></td>
<td style="text-align: left;"><p>Enabled a boolean flag to enable or
disable a dedicated instance of Alertmanager for user-defined projects
under openshift-user-workload-monitoring default: false</p></td>
<td style="text-align: left;"><p>bool</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>enableAlertmanagerConfig</p></td>
<td style="text-align: left;"><p>EnableAlertmanagerConfig a boolean flag
to enable or disable user-defined namespaces to be selected for
AlertmanagerConfig lookup, by default Alertmanager only looks for
configuration in the namespace where it was deployed to default:
false</p></td>
<td style="text-align: left;"><p>bool</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>logLevel</p></td>
<td style="text-align: left;"><p>LogLevel defines the log level for
Alertmanager. Possible values are: error, warn, info, debug. default:
info</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>resources</p></td>
<td style="text-align: left;"><p>Resources define resources requests and
limits for single Pods.</p></td>
<td style="text-align: left;"><p>*v1.ResourceRequirements</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>nodeSelector</p></td>
<td style="text-align: left;"><p>NodeSelector defines which Nodes the
Pods are scheduled on.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>tolerations</p></td>
<td style="text-align: left;"><p>Tolerations defines the Pods
tolerations.</p></td>
<td style="text-align: left;"><p>[]v1.Toleration</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>volumeClaimTemplate</p></td>
<td style="text-align: left;"><p>VolumeClaimTemplate defines persistent
storage for Alertmanager. It’s possible to configure storageClass and
size of volume.</p></td>
<td
style="text-align: left;"><p>*monv1.EmbeddedPersistentVolumeClaim</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

AlertmanagerUserWorkloadConfig \[AlertmanagerUserWorkloadConfig defines
configuration for the Alertmanager instance for user-defined projects.\]

<table>
<caption>PrometheusRestrictedConfig [PrometheusRestrictedConfig defines
configuration related to the Prometheus component that will monitor
user-defined projects.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>additionalAlertmanagerConfigs</p></td>
<td style="text-align: left;"><p>AlertmanagerConfigs holds configuration
about how the Prometheus component should communicate with aditional
Alertmanager instances. default: nil</p></td>
<td style="text-align: left;"><p>[]AdditionalAlertmanagerConfig</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>enforcedLabelLimit</p></td>
<td style="text-align: left;"><p>EnforcedLabelLimit per-scrape limit on
the number of labels accepted for a sample. If more than this number of
labels are present post metric-relabeling, the entire scrape will be
treated as failed. 0 means no limit. default: 0</p></td>
<td style="text-align: left;"><p>*uint64</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>enforcedLabelNameLengthLimit</p></td>
<td style="text-align: left;"><p>EnforcedLabelNameLengthLimit per-scrape
limit on the length of labels name that will be accepted for a sample.
If a label name is longer than this number post metric-relabeling, the
entire scrape will be treated as failed. 0 means no limit. default:
0</p></td>
<td style="text-align: left;"><p>*uint64</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>enforcedLabelValueLengthLimit</p></td>
<td style="text-align: left;"><p>EnforcedLabelValueLengthLimit
per-scrape limit on the length of labels value that will be accepted for
a sample. If a label value is longer than this number post
metric-relabeling, the entire scrape will be treated as failed. 0 means
no limit. default: 0</p></td>
<td style="text-align: left;"><p>*uint64</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>enforcedSampleLimit</p></td>
<td style="text-align: left;"><p>EnforcedSampleLimit defines a global
limit on the number of scraped samples that will be accepted. This
overrides any SampleLimit set per ServiceMonitor or/and PodMonitor. It
is meant to be used by admins to enforce the SampleLimit to keep the
overall number of samples/series under the desired limit. Note that if
SampleLimit is lower that value will be taken instead. default:
0</p></td>
<td style="text-align: left;"><p>*uint64</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>enforcedTargetLimit</p></td>
<td style="text-align: left;"><p>EnforcedTargetLimit defines a global
limit on the number of scraped targets. This overrides any TargetLimit
set per ServiceMonitor or/and PodMonitor. It is meant to be used by
admins to enforce the TargetLimit to keep the overall number of targets
under the desired limit. Note that if TargetLimit is lower, that value
will be taken instead, except if either value is zero, in which case the
non-zero value will be used. If both values are zero, no limit is
enforced. default: 0</p></td>
<td style="text-align: left;"><p>*uint64</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>externalLabels</p></td>
<td style="text-align: left;"><p>ExternalLabels defines labels to be
added to any time series or alerts when communicating with external
systems (federation, remote storage, Alertmanager). default:
nil</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>logLevel</p></td>
<td style="text-align: left;"><p>LogLevel defines the log level for
Prometheus. Possible values are: error, warn, info, debug. default:
info</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>nodeSelector</p></td>
<td style="text-align: left;"><p>NodeSelector defines which Nodes the
Pods are scheduled on.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>queryLogFile</p></td>
<td style="text-align: left;"><p>QueryLogFile specifies the file to
which PromQL queries are logged. Suports both just a filename in which
case they will be saved to an emptyDir volume at /var/log/prometheus, if
a full path is given an emptyDir volume will be mounted at that
location. Relative paths not supported, also not supported writing to
linux std streams. default: ""</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>remoteWrite</p></td>
<td style="text-align: left;"><p>RemoteWrite Holds the remote write
configuration, everything from url, authorization to relabeling</p></td>
<td style="text-align: left;"><p>[]RemoteWriteSpec</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>resources</p></td>
<td style="text-align: left;"><p>Resources define resources requests and
limits for single Pods.</p></td>
<td style="text-align: left;"><p>*v1.ResourceRequirements</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>retention</p></td>
<td style="text-align: left;"><p>Retention defines the Time duration
Prometheus shall retain data for. Must match the regular expression
[0-9]+(ms|s|m|h|d|w|y) (milliseconds seconds minutes hours days weeks
years). default: 15d</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>retentionSize</p></td>
<td style="text-align: left;"><p>RetentionSize defines the maximum
amount of disk space used by blocks + WAL. default: nil</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>tolerations</p></td>
<td style="text-align: left;"><p>Tolerations defines the Pods
tolerations.</p></td>
<td style="text-align: left;"><p>[]v1.Toleration</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>volumeClaimTemplate</p></td>
<td style="text-align: left;"><p>VolumeClaimTemplate defines persistent
storage for Prometheus. It’s possible to configure storageClass and size
of volume.</p></td>
<td
style="text-align: left;"><p>*monv1.EmbeddedPersistentVolumeClaim</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

PrometheusRestrictedConfig \[PrometheusRestrictedConfig defines
configuration related to the Prometheus component that will monitor
user-defined projects.\]

<table>
<caption>PrometheusOperatorConfig [PrometheusOperatorConfig holds
configuration related to Prometheus Operator.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>logLevel</p></td>
<td style="text-align: left;"><p>LogLevel defines the log level for
Prometheus Operator. Possible values are: error, warn, info, debug.
default: info</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>nodeSelector</p></td>
<td style="text-align: left;"><p>NodeSelector defines which Nodes the
Pods are scheduled on.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>tolerations</p></td>
<td style="text-align: left;"><p>Tolerations defines the Pods
tolerations.</p></td>
<td style="text-align: left;"><p>[]v1.Toleration</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

PrometheusOperatorConfig \[PrometheusOperatorConfig holds configuration
related to Prometheus Operator.\]

<table>
<caption>ThanosRulerConfig [ThanosRulerConfig defines configuration for
the Thanos Ruler instance for user-defined projects.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>additionalAlertmanagerConfigs</p></td>
<td style="text-align: left;"><p>AlertmanagerConfigs holds configuration
about how the Thanos Ruler component should communicate with aditional
Alertmanager instances. default: nil</p></td>
<td style="text-align: left;"><p>[]AdditionalAlertmanagerConfig</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>logLevel</p></td>
<td style="text-align: left;"><p>LogLevel defines the log level for
Thanos Ruler. Possible values are: error, warn, info, debug. default:
info</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>nodeSelector</p></td>
<td style="text-align: left;"><p>NodeSelector defines which Nodes the
Pods are scheduled on.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>resources</p></td>
<td style="text-align: left;"><p>Resources define resources requests and
limits for single Pods.</p></td>
<td style="text-align: left;"><p>*v1.ResourceRequirements</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>retention</p></td>
<td style="text-align: left;"><p>Retention defines the time duration
Thanos Ruler shall retain data for. Must match the regular expression
[0-9]+(ms|s|m|h|d|w|y) (milliseconds seconds minutes hours days weeks
years). default: 15d</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>tolerations</p></td>
<td style="text-align: left;"><p>Tolerations defines the Pods
tolerations.</p></td>
<td style="text-align: left;"><p>[]v1.Toleration</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>volumeClaimTemplate</p></td>
<td style="text-align: left;"><p>VolumeClaimTemplate defines persistent
storage for Thanos Ruler. It’s possible to configure storageClass and
size of volume.</p></td>
<td
style="text-align: left;"><p>*monv1.EmbeddedPersistentVolumeClaim</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

ThanosRulerConfig \[ThanosRulerConfig defines configuration for the
Thanos Ruler instance for user-defined projects.\]

<table>
<caption>AdditionalAlertmanagerConfig [AdditionalAlertmanagerConfig
defines configuration on how a component should communicate with
aditional Alertmanager instances.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>apiVersion</p></td>
<td style="text-align: left;"><p>APIVersion defines the api version of
Alertmanager.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>bearerToken</p></td>
<td style="text-align: left;"><p>BearerToken defines the bearer token to
use when authenticating to Alertmanager.</p></td>
<td style="text-align: left;"><p>*v1.SecretKeySelector</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>pathPrefix</p></td>
<td style="text-align: left;"><p>PathPrefix defines the path prefix to
add in front of the push endpoint path.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>scheme</p></td>
<td style="text-align: left;"><p>Scheme the URL scheme to use when
talking to Alertmanagers.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>staticConfigs</p></td>
<td style="text-align: left;"><p>StaticConfigs a list of statically
configured Alertmanagers.</p></td>
<td style="text-align: left;"><p>[]string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>timeout</p></td>
<td style="text-align: left;"><p>Timeout defines the timeout used when
sending alerts.</p></td>
<td style="text-align: left;"><p>*string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>tlsConfig</p></td>
<td style="text-align: left;"><p>TLSConfig defines the TLS Config to use
for alertmanager connection.</p></td>
<td style="text-align: left;"><p>TLSConfig</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

AdditionalAlertmanagerConfig \[AdditionalAlertmanagerConfig defines
configuration on how a component should communicate with aditional
Alertmanager instances.\]

<table>
<caption>RemoteWriteSpec [RemoteWriteSpec is almost a 1to1 copy of
monv1.RemoteWriteSpec but with the BearerToken field removed. In the
future other fields might be added here.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>authorization</p></td>
<td style="text-align: left;"><p>Authorization defines the authorization
section for remote write</p></td>
<td style="text-align: left;"><p>*monv1.SafeAuthorization</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>basicAuth</p></td>
<td style="text-align: left;"><p>BasicAuth defines configuration for
basic authentication for the URL.</p></td>
<td style="text-align: left;"><p>*monv1.BasicAuth</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>bearerTokenFile</p></td>
<td style="text-align: left;"><p>BearerTokenFile defines the file where
the bearer token for remote write resides.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>headers</p></td>
<td style="text-align: left;"><p>Headers custom HTTP headers to be sent
along with each remote write request. Be aware that headers that are set
by Prometheus itself can’t be overwritten.</p></td>
<td style="text-align: left;"><p>map[string]string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>metadataConfig</p></td>
<td style="text-align: left;"><p>MetadataConfig configures the sending
of series metadata to remote storage.</p></td>
<td style="text-align: left;"><p>*monv1.MetadataConfig</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>name</p></td>
<td style="text-align: left;"><p>Name defines the name of the remote
write queue, must be unique if specified. The name is used in metrics
and logging in order to differentiate queues.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>oauth2</p></td>
<td style="text-align: left;"><p>OAuth2 configures OAuth2 authentication
for remote write.</p></td>
<td style="text-align: left;"><p>*monv1.OAuth2</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>proxyUrl</p></td>
<td style="text-align: left;"><p>ProxyURL defines an optional proxy
URL</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>queueConfig</p></td>
<td style="text-align: left;"><p>QueueConfig allows tuning of the remote
write queue parameters.</p></td>
<td style="text-align: left;"><p>*monv1.QueueConfig</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>remoteTimeout</p></td>
<td style="text-align: left;"><p>RemoteTimeout defines the timeout for
requests to the remote write endpoint.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>sigv4</p></td>
<td style="text-align: left;"><p>Sigv4 allows to configures AWS’s
Signature Verification 4</p></td>
<td style="text-align: left;"><p>*monv1.Sigv4</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>tlsConfig</p></td>
<td style="text-align: left;"><p>TLSConfig defines the TLS configuration
to use for remote write.</p></td>
<td style="text-align: left;"><p>*monv1.SafeTLSConfig</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>url</p></td>
<td style="text-align: left;"><p>URL defines the URL of the endpoint to
send samples to.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>writeRelabelConfigs</p></td>
<td style="text-align: left;"><p>WriteRelabelConfigs defines the list of
remote write relabel configurations.</p></td>
<td style="text-align: left;"><p>[]monv1.RelabelConfig</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

RemoteWriteSpec \[RemoteWriteSpec is almost a 1to1 copy of
monv1.RemoteWriteSpec but with the BearerToken field removed. In the
future other fields might be added here.\]

<table>
<caption>TLSConfig [TLSConfig configures the options for TLS
connections.]</caption>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Field</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Scheme</th>
<th style="text-align: left;">Required</th>
<th style="text-align: left;">Status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p>ca</p></td>
<td style="text-align: left;"><p>CA defines the CA cert in the
Prometheus container to use for the targets.</p></td>
<td style="text-align: left;"><p>*v1.SecretKeySelector</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>cert</p></td>
<td style="text-align: left;"><p>Cert defines the client cert in the
Prometheus container to use for the targets.</p></td>
<td style="text-align: left;"><p>*v1.SecretKeySelector</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>key</p></td>
<td style="text-align: left;"><p>Key defines the client key in the
Prometheus container to use for the targets.</p></td>
<td style="text-align: left;"><p>*v1.SecretKeySelector</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>serverName</p></td>
<td style="text-align: left;"><p>ServerName used to verify the hostname
for the targets.</p></td>
<td style="text-align: left;"><p>string</p></td>
<td style="text-align: left;"><p>false</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>insecureSkipVerify</p></td>
<td style="text-align: left;"><p>InsecureSkipVerify disable target
certificate validation.</p></td>
<td style="text-align: left;"><p>bool</p></td>
<td style="text-align: left;"><p>true</p></td>
<td style="text-align: left;"><p>GA</p></td>
</tr>
</tbody>
</table>

TLSConfig \[TLSConfig configures the options for TLS connections.\]
