.. _otel-components:

******************************************
Collector components
******************************************

.. meta::
    :description: Learn about the components that make up the Splunk Observability Cloud OpenTelemetry Collector.

.. toctree::
    :titlesonly:
    :hidden:


    Receivers <components/a-components-receivers.rst>
    Processors <components/a-components-processors.rst>
    Exporters <components/a-components-exporters.rst>
    Extensions <components/a-components-extensions.rst>  
    Connectors <components/a-components-connectors.rst>            


The OpenTelemetry Collector includes the following component types:

* :ref:`Receivers <collector-components-receivers>`: Get data into the Collector from multiple sources.
* :ref:`Processors <collector-components-processors>`: Perform operations on data before it's exported. For example, filtering.
* :ref:`Exporters <collector-components-exporters>`: Send data to one or more backends or destinations. 
* :ref:`Extensions <collector-components-extensions>`: Extend the capabilities of the Collector.
* :ref:`Connectors <collector-components-connectors>`: Send telemetry data between different collector pipelines.

You can activate components by configuring :ref:`service pipelines <otel-data-processing>` in the Collector configuration. See :ref:`otel-configuration` to learn how to define multiple instances of components as well as their pipelines.

The Splunk Distribution of the OpenTelemetry Collector includes and supports the components listed on this doc.

.. note:: The following lists might not contain all the latest additions. For a complete list of Collector components, including components that aren't included in the Splunk Distribution of OpenTelemetry Collector, see the ``opentelemetry-contrib`` repository in GitHub.

.. _collector-components-receivers:

.. raw:: html

  <embed>
    <h2>Receivers<a name="collector-components-receivers" class="headerlink" href="#collector-components-receivers" title="Permalink to this headline">¶</a></h2>
  </embed>

.. list-table::
   :widths: 25 55 20
   :header-rows: 1
   :width: 100%

   * - Name
     - Description
     - Pipeline types
   * - :ref:`apache-receiver` (``apache``) 
     - Fetches stats from a Apache Web Server.
     - Metrics
   * - :ref:`azureeventhub-receiver` (``azureeventhub``) 
     - Pulls logs from an Azure event hub.
     - Logs
   * - :ref:`carbon-receiver` (``carbon``)
     - Receives metrics in Carbon plaintext protocol.
     - Metrics
   * - :ref:`cloudfoundry-receiver` (``cloudfoundry``)
     - Connects to the Reverse Log Proxy (RLP) gateway of Cloud Foundry to extract metrics.
     - Metrics
   * - :ref:`collectd-receiver` (``collectd``)
     - Receives data exported through the CollectD ``write_http`` plugin. Only supports the JSON format.
     - Metrics
   * - :ref:`discovery-receiver` (``discovery``) elasticsearch-receiver
     - Wraps the receiver creator to facilitate the discovery of metric collection targets. See :ref:`discovery_mode`.
     - Logs
   * - :ref:`elasticsearch-receiver` (``elasticsearch``) 
     - Queries the Elasticsearch node stats, cluster health and index stats endpoints to scrape metrics from a running Elasticsearch cluster.
     - Metrics      
   * - :ref:`filelog-receiver` (``filelog``)
     - Tails and parses logs from files.
     - Logs
   * - :ref:`fluentd-receiver` (``fluentforward``)
     - Runs a TCP server that accepts events through the Fluentd Forward protocol.
     - Logs
   * - :ref:`haproxy-receiver` (``haproxy``)
     - Generates metrics by polling periodically the HAProxy process through a dedicated socket or HTTP URL. 
     - Metrics
   * - :ref:`host-metrics-receiver` (``hostmetrics``)
     - Generates system metrics from various sources. Use this receiver when deploying the Collector as an agent. 
     - Metrics
   * - :ref:`http-check-receiver` (``httpcheck``)
     - Performs synthethic checks against HTTP endpoints.  
     - Metrics
   * - :ref:`jaeger-receiver` (``jaeger``)
     - Receives trace data in Jaeger format.
     - Traces
   * - :ref:`jmx-receiver` (``jmx``)
     - Works in conjunction with the :new-page:`OpenTelemetry JMX Metric Gatherer <https://github.com/open-telemetry/opentelemetry-java-contrib/blob/main/jmx-metrics/README.md>` to report metrics from an MBean server.
     - Metrics
   * - :ref:`journald-receiver` (``journald``)
     - Parses Journald events from the systemd journal. The ``journalctl`` binary must be in the same ``$PATH`` of the agent.
     - Logs
   * - :ref:`kafka-receiver` (``kafka``)
     - Receives metrics, logs, and traces from Kafka. Metrics and logs only support the OTLP format.
     - Metrics, logs, traces
   * - :ref:`kafkametrics-receiver` (``kafkametrics``)
     - Collects Kafka metrics such as brokers, topics, partitions, and consumer groups from Kafka server, and converts them to OTLP format.
     - Metrics
   * - :ref:`kubernetes-cluster-receiver` (``k8s_cluster``)
     - Collects cluster-level metrics from the Kubernetes API server. It uses the Kubernetes API to listen for updates. You can use a single instance of this receiver to monitor a cluster.
     - Metrics
   * - :ref:`kubernetes-events-receiver` (``k8s_events``)
     - Collects all new and updated events from the Kubernetes API server. Supports authentication through service accounts only.
     - Logs
   * - :ref:`kubernetes-objects-receiver` (``k8sobjects``)
     - Collects objects from the Kubernetes API server. Supports authentication through service accounts only.
     - Logs
   * - :ref:`kubelet-stats-receiver` (``kubeletstats``)
     - Pulls pod metrics from the API server on a kubelet.
     - Metrics
   * - :ref:`mongodb-receiver` (``mongodb``)
     - Fetches stats from a MongoDB instance using the Golang ``mongo`` driver. 
     - Metrics
   * - :ref:`mongodb-atlas-receiver` (``mongodbatlas``)
     - Retrieves metrics from MongoDB Atlas using their monitoring APIs.
     - Metrics
   * - :ref:`mssql-server-receiver` (``sqlserver``)
     - Grabs metrics from a Microsoft SQL Server instance. 
     - Metrics    
   * - :ref:`mysql-receiver` (``mysql``)
     - Queries and retrieves metrics about MySQL's global status and InnoDB tables.
     - Metrics      
   * - :ref:`nginx-receiver` (``nginx``)
     - Fetches stats from a NGINX instance using the ``ngx_http_stub_status_module`` module's status endpoint.
     - Metrics    
   * - :ref:`oracledb` (``oracledb``) |br|
     - Connects to an Oracle Database instance and obtains metrics such as physical reads, CPU, time, and others.
     - Metrics
   * - :ref:`otlp-receiver` (``otlp``)
     - Receives data through gRPC or HTTP using OTLP format.
     - Metrics, logs, traces
   * - :ref:`postgresql-receiver` (``postgresql``)
     - Queries the PostgreSQL statistics collector. Supports PostgreSQL version 9.6 and higher.
     - Metrics
   * - :ref:`prometheus-receiver` (``prometheus``)
     - Provides a simple configuration interface to scrape metrics from a single target.
     - Metrics
   * - :ref:`simple-prometheus-receiver` (``prometheus_simple``)
     - Wraps the ``prometheus`` receiver to provide simplified settings for single targets.
     - Metrics
   * - :ref:`rabbitmq-receiver` (``rabbitmq``)
     - Fetches stats from a RabbitMQ node using the RabbitMQ Management Plugin.
     - Metrics
   * - :ref:`receiver-creator-receiver` (``receiver_creator``)
     - Instantiates other receivers at runtime based on whether observed endpoints match a configured rule. To use the receiver creator, configure one or more observer extensions to discover networked endpoints.
     - N/A
   * - :ref:`redis-receiver` (``redis``)
     - Retrieves Redis ``INFO`` data from a specific Redis instance and builds metrics from it.
     - Metrics
   * - :ref:`sapm-receiver` (``sapm``)
     - Receives traces from other collectors or from the SignalFx Smart Agent.
     - Traces
   * - :ref:`signalfx-gateway-prometheus-remote-write-receiver` (``signalfxgatewayprometheusremotewritereceiver``)
     - OTel native version of the SignalFx Prometheus remote write gateway.
     - Metrics
   * - :ref:`signalfx-receiver` (``signalfx``)
     - Accepts metrics and logs in the proto format.
     - Metrics, logs
   * - :ref:`smartagent-receiver` (``smartagent``)
     - Uses the existing Smart Agent monitors as Collector metric receivers. Learn more in :ref:`migration-monitors`.
     - Metrics
   * - :ref:`splunk-enterprise-receiver` (``splunkenterprise``)
     - Enables the ingestion of performance metrics describing the operational status of a user's Splunk Enterprise deployment.
     - Metrics
   * - :ref:`splunk-hec-receiver` (``splunk_hec``)
     - Accepts telemetry in the Splunk HEC format.
     - Metrics, logs, traces
   * - :ref:`sqlquery-receiver` (``sqlquery``)
     - Runs custom SQL queries to generate metrics from a database connection.
     - Metrics
   * - :ref:`sshcheck-receiver` (``sshcheck``)
     - Creates stats by connecting to an SSH server, might be an SFTP server.
     - Metrics
   * - :ref:`statsd-receiver` (``statsd``)
     - Collects StatsD messages to generate metrics.
     - Metrics
   * - :ref:`syslog-receiver` (``syslog``)
     - Parses syslog messages received over TCP or UDP.
     - Logs
   * - :ref:`tcp-logs-receiver` (``tcplog``)
     - Receives logs over TCP.
     - Logs
   * - :ref:`udp-logs-receiver` (``udplog``) 
     - Receives logs over UDP.
     - Logs
   * - :ref:`vcenter-receiver` (``vcenter``) 
     - Supports ESXi and vCenter.
     - Metrics
   * - :ref:`wavefront-receiver` (``wavefront``) 
     - Accepts metrics and depends on the ``carbon`` receiver proto and transport.
     - Metrics      
   * - :ref:`windowseventlog-receiver` (``windowseventlog``)
     - Tails and parses logs from the Windows Event log API.
     - Logs
   * - :ref:`windowsperfcounters-receiver` (``windowsperfcounters``) (Windows only)
     - Collects the configured system, application, or custom performance counter data from the Windows Registry.
     - Metrics
   * - :ref:`zipkin-receiver` (``zipkin``)
     - Receives spans from Zipkin versions 1 and 2.
     - Traces


.. _collector-components-processors:

.. raw:: html

  <embed>
    <h2>Processors<a name="collector-components-processors" class="headerlink" href="#collector-components-processors" title="Permalink to this headline">¶</a></h2>
  </embed>

.. list-table::
   :widths: 25 55 20
   :header-rows: 1
   :width: 100%

   * - Name
     - Description
     - Pipeline types
   * - :ref:`attributes-processor` (``attributes``)
     - Modifies attributes of a span or log record.
     - Logs, traces
   * - :ref:`batch-processor` (``batch``)
     - Accepts spans, metrics, or logs and places them into batches. Batching helps better compress the data and reduce the number of outgoing connections required to transmit the data. This processor supports both size-based and time-based batching.
     - Metrics, logs, traces
   * - :ref:`cumulative-to-delta-processor` (``cumulativetodelta``)
     - Convert cumulative monotonic metrics to delta aggretation temporality. This enhances the usage of cumulative metrics in Splunk Observability Cloud.
     - Metrics
   * - :ref:`filter-processor` (``filter``)
     - Can be configured to include or exclude metrics based on metric name in the case of the ``strict`` or ``regexp`` match types, or based on other metric attributes in the case of the ``expr`` match type.
     - Metrics
   * - :ref:`groupbyattrs-processor` (``groupbyattrs``)
     - Reassociates spans, log records, and metric data points to a resource that matches with the specified attributes. As a result, all spans, log records, or metric data points with the same values for the specified attributes are grouped under the same resource.
     - Metrics, logs, traces
   * - :ref:`kubernetes-attributes-processor` (``k8sattributes``)
     - Allows automatic tagging of spans, metrics, and logs with Kubernetes metadata. Formerly known as ``k8s_tagger``.
     - Metrics, logs, traces
   * - :ref:`memory-limiter-processor` (``memory_limiter``) 
     - Prevents out of memory situations on the Splunk Distribution of OpenTelemetry Collector.
     - Metrics, logs, traces
   * - :ref:`metrics-transform-processor` (``metricstransform``) 
     - Renames metrics, and adds, renames, or deletes label keys and values.
     - Metrics
   * - :ref:`probabilistic-sampler-processor` (``probabilisticsampler``) 
     - Supports several modes of sampling for spans and log records.
     - Traces, logs
   * - :ref:`redaction-processor` (``redaction``)
     - Deletes span attributes that don't match a list of allowed attributes. It also masks span attribute values that match a blocked value list.
     - Traces
   * - :ref:`resource-processor` (``resource``)
     - Applies changes to resource attributes. Attributes represent actions that can be applied on resources.
     - Metrics, logs, traces
   * - :ref:`resourcedetection-processor` (``resourcedetection``)
     - Detects resource information from the host, in a format that conforms to the OpenTelemetry resource semantic conventions, and appends or overrides the resource value in telemetry data with this information.
     - Metrics, logs, traces
   * - :ref:`routing-processor` (``routing``) 
     - Reads a header from the incoming HTTP request or reads a resource attribute, and then directs the trace information to specific exporters based on the value.
     - Metrics, logs, traces
   * - :ref:`span-processor` (``span``)
     - Modifies either the span name or attributes of a span based on the span name.
     - Traces
   * - :ref:`tail-sampling-processor` (``tail_sampling``) 
     - Samples traces based on a set of defined policies. All spans for a given trace must be received by the same Collector instance for effective sampling decisions.
     - Traces
   * - :ref:`transform-processor` (``transform``)
     - Modifies telemetry based on OpenTelemetry Transformation Language functions.
     - Metrics, logs, traces


.. _collector-components-exporters:
.. _otel-exporters:

.. raw:: html

  <embed>
    <h2>Exporters<a name="collector-components-exporters" class="headerlink" href="#collector-components-exporters" title="Permalink to this headline">¶</a></h2>
  </embed>

.. list-table::
   :widths: 25 55 20
   :header-rows: 1
   :width: 100%

   * - Name
     - Description
     - Pipeline types
   * - :ref:`awss3-exporter` (``awss3``) 
     - This exporter targets to support proto/json format. 
     - Metrics, logs, traces
   * - :ref:`file-exporter` (``file``)
     - Writes pipeline data to a JSON file in Protobuf JSON encoding using the OpenTelemetry protocol. 
     - Metrics, logs, traces
   * - :ref:`kafka-exporter` (``kafka``)
     - Exports metrics, logs, and traces to Kafka using a synchronous producer. 
     - Metrics, logs, traces
   * - :ref:`loadbalancing-exporter` (``loadbalancing``)
     - Exports metrics, logs, and traces to different back-ends.
     - Metrics, logs, traces
   * - :ref:`logging-exporter` (``logging``)
     - Exports data to the console. By default, ``logging`` doesn't send its output to Windows Event Viewer. Run the Splunk Distribution of OpenTelemetry Collector directly from the PowerShell terminal to send output to the Windows Event Viewer.
     - Metrics, logs, traces
   * - :ref:`otlp-exporter` (``otlp``)
     - Exports data through gRPC using the OTLP format. By default, this exporter requires TLS and provides queued retry capabilities. 
     - Metrics, logs, traces
   * - :ref:`otlphttp-exporter` (``otlphttp``)
     - Exports data in OTLP format over the HTTP protocol. 
     - Metrics, logs, traces
   * - :ref:`pulsar-exporter` (``pulsar``)
     - Exports logs, metrics, and traces to Pulsar. 
     - Metrics, logs, traces     - 
   * - :ref:`signalfx-exporter` (``signalfx``)
     - Sends metrics, events, and trace correlation to Splunk Observability Cloud. 
     - Logs (events), metrics, traces (trace to metric correlation only)
   * - :ref:`splunk-apm-exporter` (``sapm``)
     - Exports traces from multiple nodes or services in a single batch.
     - Traces
   * - :ref:`splunk-hec-exporter` (``splunk_hec``)
     - Sends telemetry to a Splunk HEC endpoint. 
     - Metrics, logs, traces

.. _collector-components-extensions:

.. raw:: html

  <embed>
    <h2>Extensions<a name="collector-components-extensions" class="headerlink" href="#collector-components-extensions" title="Permalink to this headline">¶</a></h2>
  </embed>

.. list-table::
   :widths: 25 75
   :header-rows: 1
   :width: 100%

   * - Name
     - Description
   * - :ref:`basic-auth-extension` (``basicauth``)
     - Implements both ``configauth.ServerAuthenticator`` and ``configauth.ClientAuthenticator`` to authenticate clients and servers using basic authentication. The authenticator type has to be set to ``basicauth``.      
   * - :ref:`docker-observer-extension` (``docker_observer``)
     - Detects and reports container endpoints discovered through the Docker API. Only containers that are in the state of ``Running`` and not ``Paused`` emit endpoints.
   * - :ref:`ecs-observer-extension` (``ecs_observer``)
     - Uses the ECS and EC2 API to discover Prometheus scrape targets from all running tasks and filter them based on service names, task definitions, and container labels. Only compatible with the Prometheus receiver.
   * - :ref:`ecstask-observer-extension` (``ecs_task_observer``)
     - Detects and reports container endpoints for the running ECS task of which your Collector instance is a member.
   * - :ref:`file-storage-extension` (``file_storage``)
     - Persists state to the local file system. Requires read and write access to a diectory.
   * - :ref:`health-check-extension` (``health_check``)
     - Activates an HTTP URL that can be probed to check the status of the OpenTelemetry Collector. You can also use this extension as a liveness or readiness probe on Kubernetes.
   * - :ref:`http-forwarder-extension` (``http_forwarder``)
     - Accepts HTTP requests and optionally adds headers and forwards them. The RequestURIs of the original requests are preserved by the extension. 
   * - :ref:`host-observer-extension` (``host_observer``) 
     - Looks at the current host for listening network endpoints. Uses the /proc file system and requires the ``SYS_PTRACE`` and ``DAC_READ_SEARCH`` capabilities so that it can determine what processes own the listening sockets. See :ref:`receiver-creator-receiver` for more information.
   * - :ref:`kubernetes-observer-extension` (``k8s_observer``)
     - Uses the Kubernetes API to discover pods running on the local node. See :ref:`receiver-creator-receiver` for more information.
   * - :ref:`memory-ballast-extension` (``memory_ballast``)
     - ``memory_ballast`` is deprecated. If you're using this extension, see :ref:`how to update your configuration <collector-upgrade-memory-ballast>`.
   * - :ref:`oauth2client-extension` (``oauth2client``)
     - Provides OAuth2 Client Credentials flow authenticator for HTTP and gRPC based exporters. 
   * - :ref:`pprof-extension` (``pprof``)
     - Activates the golang ``net/http/pprof`` endpoint, which is used to collect performance profiles and investigate issues with a service.
   * - :ref:`smartagent-extension` (``smartagent``) 
     - Provides a mechanism to set configuration options that are applicable to all instances of the Smart Agent receiver. Allows to migrate your existing Smart Agent configuration to the Splunk Distribution of OpenTelemetry Collector. 
   * - :ref:`zpages-extension` (``zpages``) 
     - Activates an extension that serves zPages, an HTTP endpoint that provides live data for debugging different components.

.. _collector-components-connectors:

.. raw:: html

  <embed>
    <h2>Connectors<a name="collector-components-connectors" class="headerlink" href="#collector-components-connectors" title="Permalink to this headline">¶</a></h2>
  </embed>

A connector connects different pipelines and helps you send telemetry data between them. A connector acts as an exporter to one pipeline and a receiver to another. 

Each pipeline in the OpenTelemetry Collector acts on one type of telemetry data. If you need to process one form of telemetry data into another one, route the data accordingly to its proper collector pipeline.

.. list-table::
   :widths: 25 55 20
   :header-rows: 1
   :width: 100%

   * - Name
     - Description
     - Pipeline types
   * - :ref:`span-metrics-connector` (``spanmetrics``)
     - Aggregates Request, Error and Duration (R.E.D) OpenTelemetry metrics from span data.
     - Traces, metrics

.. raw:: html

  <embed>
    <h2>Next steps<a name="next-steps" class="headerlink" href="#next-steps" title="Permalink to this headline">¶</a></h2>
  </embed>

See the following docs:

* :ref:`otel-install-platform`
* :ref:`collector-how-to`