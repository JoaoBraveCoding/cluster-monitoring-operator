# Cluster Monitoring Configuration Reference

Parts of Cluster Monitoring are configurable. Depending on which part of
the stack users want to configure, they should edit the following:

-   Configuration of OpenShift Container Platform monitoring components
    lies in a ConfigMap called `cluster-monitoring-config` in the
    `openshif-monitoring` namespace.

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

# Table of Contents

-   \[AdditionalAlertmanagerConfig\](#additionalalertmanagerconfig)

-   \[AlertmanagerMainConfig\](#alertmanagermainconfig)

-   \[AlertmanagerUserWorkloadConfig\](#alertmanageruserworkloadconfig)

-   \[ClusterMonitoringConfiguration\](#clustermonitoringconfiguration)

-   \[K8sPrometheusAdapter\](#k8sprometheusadapter)

-   \[KubeStateMetricsConfig\](#kubestatemetricsconfig)

-   \[OpenShiftStateMetricsConfig\](#openshiftstatemetricsconfig)

-   \[PrometheusK8sConfig\](#prometheusk8sconfig)

-   \[PrometheusOperatorConfig\](#prometheusoperatorconfig)

-   \[PrometheusRestrictedConfig\](#prometheusrestrictedconfig)

-   \[RemoteWriteSpec\](#remotewritespec)

-   \[TLSConfig\](#tlsconfig)

-   \[ThanosQuerierConfig\](#thanosquerierconfig)

-   \[ThanosRulerConfig\](#thanosrulerconfig)

-   \[UserWorkloadConfiguration\](#userworkloadconfiguration)

# AdditionalAlertmanagerConfig

AdditionalAlertmanagerConfig defines configuration on how a component
should communicate with aditional Alertmanager instances.

&lt;em&gt;appears in: \[PrometheusK8sConfig\](#prometheusk8sconfig),
\[PrometheusRestrictedConfig\](#prometheusrestrictedconfig),
\[ThanosRulerConfig\](#thanosrulerconfig)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | apiVersion | APIVersion defines the api version of
Alertmanager. | string | true | | bearerToken | BearerToken defines the
bearer token to use when authenticating to Alertmanager. |
\*\[v1.SecretKeySelector\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#secretkeyselector-v1-core>)
| false | | pathPrefix | PathPrefix defines the path prefix to add in
front of the push endpoint path. | string | false | | scheme | Scheme
the URL scheme to use when talking to Alertmanagers. | string | false |
| staticConfigs | StaticConfigs a list of statically configured
Alertmanagers. | \[\]string | false | | timeout | Timeout defines the
timeout used when sending alerts. | \*string | false | | tlsConfig |
TLSConfig defines the TLS Config to use for alertmanager connection. |
\[TLSConfig\](#tlsconfig) | false |

\[Back to TOC\](#table-of-contents)

# AlertmanagerMainConfig

AlertmanagerMainConfig defines configuration related with the main
Alertmanager instance.

&lt;em&gt;appears in:
\[ClusterMonitoringConfiguration\](#clustermonitoringconfiguration)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | enabled | Enabled a boolean flag to enable or
disable the main Alertmanager instance under openshift-monitoring
default: true | \*bool | true | | enableUserAlertmanagerConfig |
EnableUserAlertManagerConfig boolean flag to enable or disable
user-defined namespaces to be selected for AlertmanagerConfig lookup, by
default Alertmanager only looks for configuration in the namespace where
it was deployed to. This will only work if the UWM Alertmanager instance
is not enabled. default: false | bool | true | | logLevel | LogLevel
defines the log level for Alertmanager. Possible values are: error,
warn, info, debug. default: info | string | true | | nodeSelector |
NodeSelector defines which Nodes the Pods are scheduled on. |
map\[string\]string | true | | resources | Resources define resources
requests and limits for single Pods. |
\*\[v1.ResourceRequirements\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#resourcerequirements-v1-core>)
| true | | tolerations | Tolerations defines the Pods tolerations. |
\[\]\[v1.Toleration\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#toleration-v1-core>)
| true | | volumeClaimTemplate | VolumeClaimTemplate defines persistent
storage for Alertmanager. It’s possible to configure storageClass and
size of volume. |
\*\[monv1.EmbeddedPersistentVolumeClaim\](<https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#embeddedpersistentvolumeclaim>)
| true |

\[Back to TOC\](#table-of-contents)

# AlertmanagerUserWorkloadConfig

AlertmanagerUserWorkloadConfig defines configuration for the
Alertmanager instance for user-defined projects.

&lt;em&gt;appears in:
\[UserWorkloadConfiguration\](#userworkloadconfiguration)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | enabled | Enabled a boolean flag to enable or
disable a dedicated instance of Alertmanager for user-defined projects
under openshift-user-workload-monitoring default: false | bool | true |
| enableAlertmanagerConfig | EnableAlertmanagerConfig a boolean flag to
enable or disable user-defined namespaces to be selected for
AlertmanagerConfig lookup, by default Alertmanager only looks for
configuration in the namespace where it was deployed to default: false |
bool | true | | logLevel | LogLevel defines the log level for
Alertmanager. Possible values are: error, warn, info, debug. default:
info | string | true | | resources | Resources define resources requests
and limits for single Pods. |
\*\[v1.ResourceRequirements\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#resourcerequirements-v1-core>)
| true | | nodeSelector | NodeSelector defines which Nodes the Pods are
scheduled on. | map\[string\]string | true | | tolerations | Tolerations
defines the Pods tolerations. |
\[\]\[v1.Toleration\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#toleration-v1-core>)
| true | | volumeClaimTemplate | VolumeClaimTemplate defines persistent
storage for Alertmanager. It’s possible to configure storageClass and
size of volume. |
\*\[monv1.EmbeddedPersistentVolumeClaim\](<https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#embeddedpersistentvolumeclaim>)
| true |

\[Back to TOC\](#table-of-contents)

# ClusterMonitoringConfiguration

ClusterMonitoringConfiguration defines configuration that allows users
to customise the platform monitoring stack through the
cluster-monitoring-config ConfigMap in the openshift-monitoring
namespace

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | alertmanagerMain | AlertmanagerMainConfig defines
configuration related with the main Alertmanager instance. |
\*\[AlertmanagerMainConfig\](#alertmanagermainconfig) | true | |
enableUserWorkload | UserWorkloadEnabled boolean flag to enable
monitoring for user-defined projects. | \*bool | true | | http | |
\*HTTPConfig | true | | k8sPrometheusAdapter | K8sPrometheusAdapter
defines configuration related with prometheus-adapter |
\*\[K8sPrometheusAdapter\](#k8sprometheusadapter) | true | |
kubeStateMetrics | KubeStateMetricsConfig defines configuration related
with kube-state-metrics agent |
\*\[KubeStateMetricsConfig\](#kubestatemetricsconfig) | true | |
prometheusK8s | PrometheusK8sConfig defines configuration related with
prometheus | \*\[PrometheusK8sConfig\](#prometheusk8sconfig) | true | |
prometheusOperator | PrometheusOperatorConfig defines configuration
related with prometheus-operator |
\*\[PrometheusOperatorConfig\](#prometheusoperatorconfig) | true | |
openshiftStateMetrics | OpenShiftMetricsConfig defines configuration
related with openshift-state-metrics agent |
\*\[OpenShiftStateMetricsConfig\](#openshiftstatemetricsconfig) | true |
| telemeterClient | | \*TelemeterClientConfig | true | | thanosQuerier |
ThanosQuerierConfig defines configuration related with the Thanos
Querier component | \*\[ThanosQuerierConfig\](#thanosquerierconfig) |
true |

\[Back to TOC\](#table-of-contents)

# K8sPrometheusAdapter

K8sPrometheusAdapter defines configuration related with Prometheus
Adapater

&lt;em&gt;appears in:
\[ClusterMonitoringConfiguration\](#clustermonitoringconfiguration)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | audit | Audit defines the audit configuration to
be used by the prometheus adapter instance. Possible profile values are:
\\"metadata, request, requestresponse, none\\". default: metadata |
\*Audit | true | | nodeSelector | NodeSelector defines which Nodes the
Pods are scheduled on. | map\[string\]string | true | | tolerations |
Tolerations defines the Pods tolerations. |
\[\]\[v1.Toleration\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#toleration-v1-core>)
| true |

\[Back to TOC\](#table-of-contents)

# KubeStateMetricsConfig

KubeStateMetricsConfig defines configuration related with the
kube-state-metrics agent.

&lt;em&gt;appears in:
\[ClusterMonitoringConfiguration\](#clustermonitoringconfiguration)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | nodeSelector | NodeSelector defines which Nodes
the Pods are scheduled on. | map\[string\]string | true | | tolerations
| Tolerations defines the Pods tolerations. |
\[\]\[v1.Toleration\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#toleration-v1-core>)
| true |

\[Back to TOC\](#table-of-contents)

# OpenShiftStateMetricsConfig

OpenShiftStateMetricsConfig holds configuration related to
openshift-state-metrics agent.

&lt;em&gt;appears in:
\[ClusterMonitoringConfiguration\](#clustermonitoringconfiguration)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | nodeSelector | NodeSelector defines which Nodes
the Pods are scheduled on. | map\[string\]string | true | | tolerations
| Tolerations defines the Pods tolerations. |
\[\]\[v1.Toleration\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#toleration-v1-core>)
| true |

\[Back to TOC\](#table-of-contents)

# PrometheusK8sConfig

PrometheusK8sConfig holds configuration related to the Prometheus
component.

&lt;em&gt;appears in:
\[ClusterMonitoringConfiguration\](#clustermonitoringconfiguration)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | additionalAlertmanagerConfigs |
AlertmanagerConfigs holds configuration about how the Prometheus
component should communicate with aditional Alertmanager instances.
default: nil |
\[\]\[AdditionalAlertmanagerConfig\](#additionalalertmanagerconfig) |
true | | enforcedBodySizeLimit | EnforcedBodySizeLimit enforces body
size limit of Prometheus scrapes, if a scrape is bigger than the limit
it will fail. 3 kinds of values are accepted:\n 1. empty value: no
limit\n 2. a value in Prometheus size format, e.g. \\"64MB\\"\n 3.
string \\"automatic\\", which means the limit will be automatically
calculated based on\n cluster capacity.\ndefault: 64MB | string | false
| | externalLabels | ExternalLabels defines labels to be added to any
time series or alerts when communicating with external systems
(federation, remote storage, Alertmanager). default: nil |
map\[string\]string | true | | logLevel | LogLevel defines the log level
for Prometheus. Possible values are: error, warn, info, debug. default:
info | string | true | | nodeSelector | NodeSelector defines which Nodes
the Pods are scheduled on. | map\[string\]string | true | | queryLogFile
| QueryLogFile specifies the file to which PromQL queries are logged.
Suports both just a filename in which case they will be saved to an
emptyDir volume at /var/log/prometheus, if a full path is given an
emptyDir volume will be mounted at that location. Relative paths not
supported, also not supported writing to linux std streams. default:
\\"\\" | string | true | | remoteWrite | RemoteWrite Holds the remote
write configuration, everything from url, authorization to relabeling |
\[\]\[RemoteWriteSpec\](#remotewritespec) | true | | resources |
Resources define resources requests and limits for single Pods. |
\*\[v1.ResourceRequirements\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#resourcerequirements-v1-core>)
| true | | retention | Retention defines the Time duration Prometheus
shall retain data for. Must match the regular expression
\[0-9\]+(ms\\|s\\|m\\|h\\|d\\|w\\|y) (milliseconds seconds minutes hours
days weeks years). default: 15d | string | true | | retentionSize |
RetentionSize defines the maximum amount of disk space used by blocks +
WAL. default: nil | string | true | | tolerations | Tolerations defines
the Pods tolerations. |
\[\]\[v1.Toleration\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#toleration-v1-core>)
| true | | volumeClaimTemplate | VolumeClaimTemplate defines persistent
storage for Prometheus. It’s possible to configure storageClass and size
of volume. |
\*\[monv1.EmbeddedPersistentVolumeClaim\](<https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#embeddedpersistentvolumeclaim>)
| true |

\[Back to TOC\](#table-of-contents)

# PrometheusOperatorConfig

PrometheusOperatorConfig holds configuration related to Prometheus
Operator.

&lt;em&gt;appears in:
\[ClusterMonitoringConfiguration\](#clustermonitoringconfiguration),
\[UserWorkloadConfiguration\](#userworkloadconfiguration)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | logLevel | LogLevel defines the log level for
Prometheus Operator. Possible values are: error, warn, info, debug.
default: info | string | true | | nodeSelector | NodeSelector defines
which Nodes the Pods are scheduled on. | map\[string\]string | true | |
tolerations | Tolerations defines the Pods tolerations. |
\[\]\[v1.Toleration\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#toleration-v1-core>)
| true |

\[Back to TOC\](#table-of-contents)

# PrometheusRestrictedConfig

PrometheusRestrictedConfig defines configuration related to the
Prometheus component that will monitor user-defined projects.

&lt;em&gt;appears in:
\[UserWorkloadConfiguration\](#userworkloadconfiguration)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | additionalAlertmanagerConfigs |
AlertmanagerConfigs holds configuration about how the Prometheus
component should communicate with aditional Alertmanager instances.
default: nil |
\[\]\[AdditionalAlertmanagerConfig\](#additionalalertmanagerconfig) |
true | | enforcedLabelLimit | EnforcedLabelLimit per-scrape limit on the
number of labels accepted for a sample. If more than this number of
labels are present post metric-relabeling, the entire scrape will be
treated as failed. 0 means no limit. default: 0 | \*uint64 | true | |
enforcedLabelNameLengthLimit | EnforcedLabelNameLengthLimit per-scrape
limit on the length of labels name that will be accepted for a sample.
If a label name is longer than this number post metric-relabeling, the
entire scrape will be treated as failed. 0 means no limit. default: 0 |
\*uint64 | true | | enforcedLabelValueLengthLimit |
EnforcedLabelValueLengthLimit per-scrape limit on the length of labels
value that will be accepted for a sample. If a label value is longer
than this number post metric-relabeling, the entire scrape will be
treated as failed. 0 means no limit. default: 0 | \*uint64 | true | |
enforcedSampleLimit | EnforcedSampleLimit defines a global limit on the
number of scraped samples that will be accepted. This overrides any
SampleLimit set per ServiceMonitor or/and PodMonitor. It is meant to be
used by admins to enforce the SampleLimit to keep the overall number of
samples/series under the desired limit. Note that if SampleLimit is
lower that value will be taken instead. default: 0 | \*uint64 | true | |
enforcedTargetLimit | EnforcedTargetLimit defines a global limit on the
number of scraped targets. This overrides any TargetLimit set per
ServiceMonitor or/and PodMonitor. It is meant to be used by admins to
enforce the TargetLimit to keep the overall number of targets under the
desired limit. Note that if TargetLimit is lower, that value will be
taken instead, except if either value is zero, in which case the
non-zero value will be used. If both values are zero, no limit is
enforced. default: 0 | \*uint64 | true | | externalLabels |
ExternalLabels defines labels to be added to any time series or alerts
when communicating with external systems (federation, remote storage,
Alertmanager). default: nil | map\[string\]string | true | | logLevel |
LogLevel defines the log level for Prometheus. Possible values are:
error, warn, info, debug. default: info | string | true | | nodeSelector
| NodeSelector defines which Nodes the Pods are scheduled on. |
map\[string\]string | true | | queryLogFile | QueryLogFile specifies the
file to which PromQL queries are logged. Suports both just a filename in
which case they will be saved to an emptyDir volume at
/var/log/prometheus, if a full path is given an emptyDir volume will be
mounted at that location. Relative paths not supported, also not
supported writing to linux std streams. default: \\"\\" | string | true
| | remoteWrite | RemoteWrite Holds the remote write configuration,
everything from url, authorization to relabeling |
\[\]\[RemoteWriteSpec\](#remotewritespec) | true | | resources |
Resources define resources requests and limits for single Pods. |
\*\[v1.ResourceRequirements\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#resourcerequirements-v1-core>)
| true | | retention | Retention defines the Time duration Prometheus
shall retain data for. Must match the regular expression
\[0-9\]+(ms\\|s\\|m\\|h\\|d\\|w\\|y) (milliseconds seconds minutes hours
days weeks years). default: 15d | string | true | | retentionSize |
RetentionSize defines the maximum amount of disk space used by blocks +
WAL. default: nil | string | true | | tolerations | Tolerations defines
the Pods tolerations. |
\[\]\[v1.Toleration\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#toleration-v1-core>)
| true | | volumeClaimTemplate | VolumeClaimTemplate defines persistent
storage for Prometheus. It’s possible to configure storageClass and size
of volume. |
\*\[monv1.EmbeddedPersistentVolumeClaim\](<https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#embeddedpersistentvolumeclaim>)
| true |

\[Back to TOC\](#table-of-contents)

# RemoteWriteSpec

RemoteWriteSpec is almost a 1to1 copy of monv1.RemoteWriteSpec but with
the BearerToken field removed. In the future other fields might be added
here.

&lt;em&gt;appears in: \[PrometheusK8sConfig\](#prometheusk8sconfig),
\[PrometheusRestrictedConfig\](#prometheusrestrictedconfig)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | authorization | Authorization defines the
authorization section for remote write | \*monv1.SafeAuthorization |
false | | basicAuth | BasicAuth defines configuration for basic
authentication for the URL. |
\*\[monv1.BasicAuth\](<https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#basicauth>)
| false | | bearerTokenFile | BearerTokenFile defines the file where the
bearer token for remote write resides. | string | false | | headers |
Headers custom HTTP headers to be sent along with each remote write
request. Be aware that headers that are set by Prometheus itself can’t
be overwritten. | map\[string\]string | false | | metadataConfig |
MetadataConfig configures the sending of series metadata to remote
storage. |
\*\[monv1.MetadataConfig\](<https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#metadataconfig>)
| false | | name | Name defines the name of the remote write queue, must
be unique if specified. The name is used in metrics and logging in order
to differentiate queues. | string | false | | oauth2 | OAuth2 configures
OAuth2 authentication for remote write. | \*monv1.OAuth2 | false | |
proxyUrl | ProxyURL defines an optional proxy URL | string | false | |
queueConfig | QueueConfig allows tuning of the remote write queue
parameters. |
\*\[monv1.QueueConfig\](<https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#queueconfig>)
| false | | remoteTimeout | RemoteTimeout defines the timeout for
requests to the remote write endpoint. | string | false | | sigv4 |
Sigv4 allows to configures AWS’s Signature Verification 4 |
\*monv1.Sigv4 | false | | tlsConfig | TLSConfig defines the TLS
configuration to use for remote write. |
\*\[monv1.SafeTLSConfig\](<https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#safetlsconfig>)
| false | | url | URL defines the URL of the endpoint to send samples
to. | string | true | | writeRelabelConfigs | WriteRelabelConfigs
defines the list of remote write relabel configurations. |
\[\]\[monv1.RelabelConfig\](<https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#relabelconfig>)
| false |

\[Back to TOC\](#table-of-contents)

# TLSConfig

TLSConfig configures the options for TLS connections.

&lt;em&gt;appears in:
\[AdditionalAlertmanagerConfig\](#additionalalertmanagerconfig)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | ca | CA defines the CA cert in the Prometheus
container to use for the targets. |
\*\[v1.SecretKeySelector\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#secretkeyselector-v1-core>)
| false | | cert | Cert defines the client cert in the Prometheus
container to use for the targets. |
\*\[v1.SecretKeySelector\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#secretkeyselector-v1-core>)
| false | | key | Key defines the client key in the Prometheus container
to use for the targets. |
\*\[v1.SecretKeySelector\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#secretkeyselector-v1-core>)
| false | | serverName | ServerName used to verify the hostname for the
targets. | string | false | | insecureSkipVerify | InsecureSkipVerify
disable target certificate validation. | bool | true |

\[Back to TOC\](#table-of-contents)

# ThanosQuerierConfig

ThanosQuerierConfig holds configuration related to Thanos Querier
component.

&lt;em&gt;appears in:
\[ClusterMonitoringConfiguration\](#clustermonitoringconfiguration)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | enableRequestLogging | EnableRequestLogging
boolean flag to enable or disable request logging default: false | bool
| true | | logLevel | LogLevel defines the log level for Thanos Querier.
Possible values are: error, warn, info, debug. default: info | string |
true | | nodeSelector | NodeSelector defines which Nodes the Pods are
scheduled on. | map\[string\]string | true | | resources | Resources
define resources requests and limits for single Pods. |
\*\[v1.ResourceRequirements\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#resourcerequirements-v1-core>)
| true | | tolerations | Tolerations defines the Pods tolerations. |
\[\]\[v1.Toleration\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#toleration-v1-core>)
| true |

\[Back to TOC\](#table-of-contents)

# ThanosRulerConfig

ThanosRulerConfig defines configuration for the Thanos Ruler instance
for user-defined projects.

&lt;em&gt;appears in:
\[UserWorkloadConfiguration\](#userworkloadconfiguration)&lt;/em&gt;

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | additionalAlertmanagerConfigs |
AlertmanagerConfigs holds configuration about how the Thanos Ruler
component should communicate with aditional Alertmanager instances.
default: nil |
\[\]\[AdditionalAlertmanagerConfig\](#additionalalertmanagerconfig) |
true | | logLevel | LogLevel defines the log level for Thanos Ruler.
Possible values are: error, warn, info, debug. default: info | string |
true | | nodeSelector | NodeSelector defines which Nodes the Pods are
scheduled on. | map\[string\]string | true | | resources | Resources
define resources requests and limits for single Pods. |
\*\[v1.ResourceRequirements\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#resourcerequirements-v1-core>)
| true | | retention | Retention defines the time duration Thanos Ruler
shall retain data for. Must match the regular expression
\[0-9\]+(ms\\|s\\|m\\|h\\|d\\|w\\|y) (milliseconds seconds minutes hours
days weeks years). default: 15d | string | true | | tolerations |
Tolerations defines the Pods tolerations. |
\[\]\[v1.Toleration\](<https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.24/#toleration-v1-core>)
| true | | volumeClaimTemplate | VolumeClaimTemplate defines persistent
storage for Thanos Ruler. It’s possible to configure storageClass and
size of volume. |
\*\[monv1.EmbeddedPersistentVolumeClaim\](<https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#embeddedpersistentvolumeclaim>)
| true |

\[Back to TOC\](#table-of-contents)

# UserWorkloadConfiguration

UserWorkloadConfiguration defines configuration that allows users to
customise the monitoring stack responsible for user-defined projects
through the user-workload-monitoring-config ConfigMap in the
openshift-user-workload-monitoring namespace

| Field | Description | Scheme | Required | | ----- | ----------- |
------ | -------- | | alertmanager | Alertmanager defines configuration
for Alertmanager component. |
\*\[AlertmanagerUserWorkloadConfig\](#alertmanageruserworkloadconfig) |
true | | prometheus | Prometheus defines configuration for Prometheus
component. |
\*\[PrometheusRestrictedConfig\](#prometheusrestrictedconfig) | true | |
prometheusOperator | PrometheusOperator defines configuration for
prometheus-operator component. |
\*\[PrometheusOperatorConfig\](#prometheusoperatorconfig) | true | |
thanosRuler | ThanosRuler defines configuration for the Thanos Ruler
component | \*\[ThanosRulerConfig\](#thanosrulerconfig) | true |

\[Back to TOC\](#table-of-contents)
