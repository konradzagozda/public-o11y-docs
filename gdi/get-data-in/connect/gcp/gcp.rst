.. _get-started-gcp:

********************************************************
Connect to Google Cloud Platform 
********************************************************

.. meta::
   :description: Connect your Google Cloud Platform / GCP account to Splunk Observability Cloud.

.. toctree::
   :hidden:

   Supported GCP services <https://docs.splunk.com/observability/en/gdi/integrations/cloud-gcp.html>
   gcp-metrics
   Send GCP logs to Splunk Platform <gcp-logs>   

With a Google Cloud Platform (GCP) integration in Splunk Observability Cloud, you can track your Google Cloud Monitoring metrics and monitor your GCP services in one place. To configure a GCP integration with Splunk Infrastructure Monitoring, check the prerequisites and follow the instructions on this document. You can also :ref:`use the API <gcp-api>` to connect to GCP. 

For the list of the GCP services available in Splunk Observability Cloud by default, see the list of :ref:`supported integrations <gcp-integrations>`. 

.. _gcp-prerequisites:

.. raw:: html

   <embed>
      <h2>Prerequisites<a name="gcp-prerequisites" class="headerlink" href="#gcp-prerequisites" title="Permalink to this headline">¶</a></h2>
   </embed>

The following pre-requisites apply:

* You must be an administrator of your Splunk Observability Cloud organization to create a GCP connection.
* Splunk Observability Cloud supports all GCP regions. 

.. raw:: html

   <embed>
      <h3>Account permissions<a name="gcp-permissions" class="headerlink" href="#gcp-permissions" title="Permalink to this headline">¶</a></h3>
   </embed>

Starting in March 2024, GCP disables service account key creation by setting ``iam.disableServiceAccountKeyCreation`` to ``false`` by default. When this constraint is set, you cannot create user-managed credentials for service accounts in projects affected by the constraint. Check the restrictions on your organization's account keys before connecting to Splunk Observability Cloud.

For more information, refer to Google's official announcement :new-page:`Introducing stronger default Org Policies for our customers <https://cloud.google.com/blog/products/identity-security/introducing-stronger-default-org-policies-for-our-customers/>`.

.. raw:: html

   <embed>
      <h2>Connect to GCP using the guided setup<a name="gcp-guided" class="headerlink" href="#gcp-guided" title="Permalink to this headline">¶</a></h2>
   </embed>

.. _gcp-one:

.. raw:: html

   <embed>
      <h3>Select a role for your GCP service account<a name="gcp-one" class="headerlink" href="#gcp-one" title="Permalink to this headline">¶</a></h3>
   </embed>

If you use GCP's :strong:`Project Viewer` role, you won't require any changes to your GCP setup to use Splunk Observability Cloud, and any update will be applied automatically. 

If you want to use a more restrictive role than Project Viewer, make sure your selected role has sufficient permissions to connect to Splunk Observability Cloud, otherwise you'll get an error message when trying to connect. Review and activate any missing permissions, or change the role to Project Viewer.

The following table specifies the permissions required for GCP integrations:

.. list-table::
   :header-rows: 1
   :widths: 40 60

   *  - :strong:`Permission`
      - :strong:`Required?`

   *  - ``compute.instances.list``
      - Yes, if the Compute Engine service is activated

   *  - ``compute.machineTypes.list``
      - Yes, if the Compute Engine service is activated

   *  - ``container.clusters.list``
      - Yes, if the Kubernetes (GKE) service is activated

   *  - ``container.nodes.list``
      - Yes, if the Kubernetes (GKE) service is activated

   *  - ``container.pods.list``
      - Yes, if the Kubernetes (GKE) service is activated

   *  - ``monitoring.metricDescriptors.get``
      - Yes

   *  - ``monitoring.metricDescriptors.list``
      - Yes

   *  - ``monitoring.timeSeries.list``
      - Yes

   *  - ``resourcemanager.projects.get``
      - Yes, if you want to sync project metadata (such as labels)

   *  - ``serviceusage.services.use``
      - Yes, if you want to activate the use of a quota from the project where metrics are stored

   *  - ``spanner.instances.list``
      - Yes, if the Spanner service is activated

   *  - ``storage.buckets.list``
      - Yes, if the Spanner service is activated

.. _gcp-two:

.. raw:: html

   <embed>
      <h3>Configure GCP<a name="gcp-two" class="headerlink" href="#gcp-two" title="Permalink to this headline">¶</a></h3>
   </embed>

To configure your GCP service, follow these steps:

#. In a new window or tab, go to the Google Cloud Platform website, and log into your GCP account.
#. Open the GCP web console, and select a project you want to monitor.
#. From the sidebar, select :menuselection:`IAM & admin`, then :menuselection:`Service Accounts`.
#. Go to :guilabel:`Create Service Account` at the top of the screen, and complete the following fields:

   .. list-table::
      :header-rows: 1
      :widths: 40 60

      *  - :strong:`Field`
         - :strong:`Description`

      *  - Service account name
         - Enter ``Splunk``.

      *  - Service account ID
         - This field autofills after you enter ``Splunk`` for Service account name.

      *  - Service account description
         - Enter the description for your service account.

#. Select :guilabel:`CREATE`.
#. (Optional) Select a role to grant this Service account access to the selected project, then select :guilabel:`CONTINUE`.
#. Activate Key type :guilabel:`JSON`, and select :guilabel:`CREATE`. A new service account key JSON file is then downloaded to your computer.
#. In a new window or tab, go to :new-page:`Cloud Resource Manager API <https://console.cloud.google.com/apis/library/cloudresourcemanager.googleapis.com?pli=1>`, and activate the Cloud Resource Manager API. You need to activate this API so Splunk Infrastructure Monitoring can use it to validate permissions on the service account keys.

.. _gcp-projects:

.. note:: To monitor multiple GCP projects, repeat the steps described in this section for each one of the projects.

.. _gcp-three:

.. raw:: html

   <embed>
      <h3>Start the integration<a name="gcp-three" class="headerlink" href="#gcp-three" title="Permalink to this headline">¶</a></h3>
   </embed>

By default, all supported services are monitored, and any new services added later are also monitored. When you set integration parameters, you can choose to import metrics from a subset of the available services.

#. Log in to Splunk Observability Cloud. 
#. Open the :new-page:`Google Cloud Platform guided setup <https://login.signalfx.com/#/integrations/gcp>`. Optionally, you can navigate to the guided setup on your own:

   #. In the navigation menu, select :menuselection:`Data Management`.
   
   #. Go to the :guilabel:`Available integrations` tab, or select :guilabel:`Add Integration` in the :guilabel:`Deployed integrations` tab.

   #. In the integration filter menu, select :guilabel:`By Use Case`, and select the :guilabel:`Monitor Infrastructure` use case.

   #. In the :guilabel:`Cloud Integrations` section, select the :guilabel:`Google Cloud Platform` tile to open the Google Cloud Platform guided setup.

   #. Go to :guilabel:`New Integration`.

#. Enter a name for the new GCP integration, then :guilabel:`Add Project`. 
#. Next, select :guilabel:`Import Service Account Key`, and select one or more of the JSON key files that you downloaded from GCP in :ref:`Configure GCP <gcp-two>`.
#. Select :guilabel:`Open`. You can then see the project IDs corresponding to the service account keys you selected.
#. To import :ref:`metrics <gcp-metrics>` from only some of the available services, follow these steps:

   - Go to :guilabel:`All Services` to display a list of the services you can monitor.
   - Select the services you want to monitor, and then :guilabel:`Apply`.

#.  Select the rate (in seconds) at which you want Splunk Observability Cloud to poll GCP for metric data, with 1 minute as the minimum unit, and 10 minutes as the maximum unit. For example, a value of 300 polls metrics once every 5 minutes. 
#. Optional: 

   - List any additional GCP service domain names that you want to monitor, using commas to separate domain names in the :strong:`Custom Metric Type Domains` field. 
      
      - For example, to obtain Apigee metrics, add ``apigee.googleapis.com``.
      - To learn about custom metric type domain syntax, see :new-page:`Custom metric type domain examples <https://dev.splunk.com/observability/docs/integrations/gcp_integration_overview#Custom-metric-type-domain-examples>` in the Splunk developer documentation.

   - If you select Compute Engine as one of the services to monitor, you can enter a comma-separated list of Compute Engine Instance metadata keys to send as properties. These metadata keys are sent as properties named ``gcp_metadata_<metadata-key>``.

   - Select :strong:`Use quota from the project where metrics are stored` to use a quota from the project where metrics are stored. The service account provided for the project needs either the ``serviceusage.services.use`` permission, or the `Service Usage Consumer` role.

Your GCP integration is now complete.

.. note:: Splunk is not responsible for data availability, and it can take up to several minutes (or longer, depending on your configuration) from the time you connect until you start seeing valid data from your account. 

.. raw:: html

   <embed>
      <h2>Alternatives to connect to GCP<a name="connect-gcp-other" class="headerlink" href="#connect-gcp-other" title="Permalink to this headline">¶</a></h2>
   </embed>

.. _gcp-api:

.. raw:: html

   <embed>
      <h3>Integrate GCP using the API <a name="gcp-api" class="headerlink" href="#gcp-api" title="Permalink to this headline">¶</a></h3>
   </embed>

You can also integrate GCP with Splunk Observability Cloud using the GCP API. See :new-page:`Integrate Google Cloud Platform Monitoring with Splunk Observability Cloud <https://dev.splunk.com/observability/docs/integrations/gcp_integration_overview#Specifying-custom-metric-type-domains>` in our developer portal for details.

.. raw:: html

   <embed>
      <h3>Connect to GCP using Terraform<a name="connect-gcp-terraform" class="headerlink" href="#connect-gcp-terraform" title="Permalink to this headline">¶</a></h3>
   </embed>

To connect using Terraform, see :ref:`terraform-config`.

.. raw:: html

   <embed>
      <h2>Install the Splunk Distribution of OpenTelemetry Collector<a name="install-splunk-otel-collector" class="headerlink" href="#install-splunk-otel-collector" title="Permalink to this headline">¶</a></h2>
   </embed>

To take advantage of the full benefits of the Splunk Observability Cloud platform, install the :ref:`OpenTelemetry Collector <otel-intro>`. 

.. raw:: html

  <embed>
    <h3>Track your OpenTelemetry enablement<a name="install-splunk-otel-collector-enablement" class="headerlink" href="#install-splunk-otel-collector-enablement" title="Permalink to this headline">¶</a></h3>
  </embed>

To track the degree of OpenTelemetry enablement in your GCP integrations: 

1. From Splunk Observability Cloud, go to :guilabel:`Data Management > Deployed integrations > Google Cloud Platform`.

2. Select :guilabel:`OpenTelemetry Enabled` to see whether the OTel Collector is installed on each GCE instance or GKE cluster. This helps you identify the instances that still need to be instrumented. 

..  image:: /_images/gdi/gcp-collector-insights.png
  :width: 80%
  :alt: Amount of GCP entities with the Collector installed.  

3. For OTel Collector instances that are successfully instrumented, you can see which version of the Collector is deployed.  

.. _next-gcp-steps:

.. raw:: html

   <embed>
      <h2>Next steps<a name="next-gcp-steps" class="headerlink" href="#next-gcp-steps" title="Permalink to this headline">¶</a></h2>
   </embed>

To validate your setup, examine the details of your GCP integration as displayed in the list at the end of the setup page.

* For details about the metrics provided by an GCP integration, see :ref:`gcp-metrics`.
* To send logs from GCP to Splunk Observability Cloud, follow the instructions in :ref:`gcp-logs`.
* Learn about Splunk Observability Cloud's :ref:`GCP Infrastructure Monitoring options <infrastructure-gcp>`. 
* To learn more about Splunk Observability Cloud's data model, refer to :ref:`data-model`.
