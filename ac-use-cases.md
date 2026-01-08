---

copyright:
  years: 2026
lastupdated: "2026-01-08"

keywords: app-configuration, app configuration, about app configuration, use cases

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# App Configuration Use Cases
{: #ac-use-cases}

IBM Cloud App Configuration is a centralized feature-management and configuration service on IBM Cloud. App Configuration helps developers progressively deliver features in order to ship the code faster and reduce risk of potential failures. App Configuration also offers SDKs for programming languages like Go, Node.js, Java, Python and Kotlin that can be integrated with the applications.
{: shortdesc}

## Examples of IBM Cloud App Configuration use cases
{: #ac-examples-use-cases}

IBM Cloud App Configuration supports various use-cases for feature management and configuration management.

### Progressive Delivery of features
{: #ac-progressive-delivery-features}

Progressive delivery is to rollout new features gradually to limit the potential negative impact. Progressive delivery combines software development and release practices to deliver with control. App Configuration helps rollout features in a regulated way by controlling the application behavior via toggling on-off the features. See [Enabling feature flag](/docs/app-configuration?topic=app-configuration-ac-feature-flags#enabling-feature-flag) for details.

### Dark Launch and Beta testing
{: #ac-dark-launch-beta-testing}

Dark launch releases features to a subset of users. Deploy the code to production and dark launch your features to a subset of users using Segmentation in App Configuration.
Test in your production systems by allowing the feature to be available only to the quality engineers. once feedback on usability and functionality is satisfactory, release it to all your customers. See [Targeting a segment with a feature flag](/docs/app-configuration?topic=app-configuration-ac-feature-flags#targeting-segment-with-feature-flag) for details.

### Kill Switches
{: #ac-kill-switches}

Kill Switch is a mechanism to stop something in an event of failure to avoid wider negative impact. In the context of feature flags, the kill switch is used to disable a feature because of critical bugs raised by customers (or any other type of feedback received). Instead of having to rollback the code deployment, just disable the feature using the toggle functionality in App Configuration.  See [Enabling feature flag](/docs/app-configuration?topic=app-configuration-ac-feature-flags#enabling-feature-flag) for details.

### Canary / Ring Deployments
{: #ac-canary-ring-deployments}

Canary or ring deployments are a strategy to release features incrementally to a subset of users. App Configuration supports phased rollout to enable incremental release of features to a subset of users or devices. See [Configure feature rollout percentage](/docs/app-configuration?topic=app-configuration-ac-feature-flags#configure-rollout-percentage) for details.

### Offline Support
{: #ac-offline-support}

Enabling offline mode lets you evaluate feature flags or properties when the application is running in an air-gapped environment. App Configuration SDK supports Bootstrap file for use in highly secure environments like FedRAMP compliant systems. See [Offline Support](/docs/app-configuration?topic=app-configuration-ac-offline) for details.

### Centralized Configuration Control
{: #ac-centralized-config-control}

Configuration management represents a single source for configuration items. Configuration management needs an effective way of managing changes, access control, and auditability. Create and manage properties in App Configuration to use it in your infrastructure or in your code, and access them using CLI. See [Targeting properties to segments](/docs/app-configuration?topic=app-configuration-ac-properties) for details.

### Configuration as Code
{: #ac-configuration-as-code}

Configuration as Code (CaC) separates the configuration from the code and maintains the configuration in files in a repository. App Configuration helps to export the configuration and store it into configuration files.

### Faster Incident Management
{: #ac-faster-incident-management}

Feature flags help prevent issues using kill switches and also helps to reduce the Mean Time to Respond (MTTR). Dynamically enable diagnostic traces across your applications or microservices using a feature flag to quickly debug any customer incident.

### Toolchain Integration
{: #ac-toolchain-integration}

Integrate App Configuration to your pipelines to apply specific feature flags or properties to the environment or trigger properties of the pipeline. See [Configuring App Configuration](/docs/ContinuousDelivery?topic=ContinuousDelivery-app-configuration&interface=ui) for details.

### Release features across clusters in multi-cloud deployments
{: #ac-multi-cloud-deployments}

Keeping the features and properties up-to-date across all clusters at real-time is key to  multi-cloud management. App Configuration supports templatize and control the deployment of Kubernetes clusters across clusters.

### Automate feature flag deployments
{: #ac-automate-feature-flag-deployments}

[Terraform](https://developer.hashicorp.com/terraform) is an open source project that lets you specify your cloud infrastructure resources and services by using the high-level scripting HashiCorp Configuration Language (HCL). App Configuration helps automate your feature flags in a multi cloud deployment. See [App Config Terraform Features](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/app_config_feature) for details.

### Infrastructure as Code
{: #ac-iaac}

Infrastructure as Code (IaC) is the process of managing and provisioning computer data centres through machine readable definition files. IaC tools have conditional logic to turn on/off parts of the infrastructure. Using feature flags in IaC allows you to configure and build infrastructure dynamically based on environments. See [here](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/app_config_feature) for details.
