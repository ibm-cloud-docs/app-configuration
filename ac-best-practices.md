---

copyright:
  years: 2025
lastupdated: "2025-10-24"

keywords: app-configuration, app configuration, about app configuration, best practices

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud App Configuration Best Practices 
{: #best-practices}

IBM Cloud App Configuration is a centralized feature-management and configuration service on IBM Cloud. App Configuration helps developers progressively deliver features in order to ship the code faster and reduce risk of potential failures.  App Configuration also offers SDKs for programming languages like Go, Node.js, Java, Python, JavaScript, React and Kotlin that can be integrated with the applications.  


## Best Practices
{: #ac-best-practices}
 
### Boundary protection
{: #ac-boundary-protection}

Based on the compliance requirements, you may have a boundary requirement for your prod / non-prod instances.  You can have separate non-prod & prod instances of App Configuration. Further, create App Configuration environments based on the deployment environments.  You can also choose to extend this architecture to have multiple instances for each prod regions. 

![Boundary protection](/images/ac-boundary-protection.png "Boundary Protection"){: caption="Boundary Protection" caption-side="bottom"}

### Access control
{: #ac-access-control}

You may like to control access to feature flags based on policies. For instance, only administrators should be allowed to toggle a feature flag on a production related environment in App Configuration. To restrict access to your feature flags in an Environment, manage using [environment level access](/docs/app-configuration?topic=app-configuration-ac-assign-access-to-environments) in App Configuration.

Naming Convention – Following a naming convention can help in many ways:
1.	Name can help identify the purpose of the flag.
2.	Role of the flag, like if it’s used internal or external usage.

Having a naming convention helps developer to understand the feature flag and this avoids ambiguity.

Like naming conventions on feature flag, define specific tags to categorize the feature flags / properties. Description of the flags can be used to detail the purpose of the application the flag is being used.

### Operational Flags / Properties
{: #ac-operational-flags}

App Configuration can be used to manage your operational flags / properties and not just the release flags.  Operational flags prepare the system to respond to any production failures.  It works like a circuit breaker which can help in graceful degradation of a system under peak load or customer impacting incidents.
It can also help dynamically enable trace for a specific feature failure or for a specific customer incident which in turn drastically reduces MTTR.

### Targeted feature roll-out
{: #ac-targeted-feature-rollout}

Use App Configuration to perform A/B testing, [canary testing](/docs/app-configuration?topic=app-configuration-ac-feature-flags#configure-rollout-percentage), experimentation in production, or [selectively enabling features](/docs/app-configuration?topic=app-configuration-ac-segments) for a set of groups of users or a geography. This helps to test in production with live data, to receive feedback from your business users or customers with very minimal or no impact. 

### Avoid dependencies between flags
{: #ac-avoid-dependencies}

Each flag should serve a specific purpose.  And flags should be independent of each other.  If multiple flags are needed to be enabled for a single release or switching the state of a flag conflicts with another flag, can become confusing and difficult to maintain.  This also will impact on the user experience negatively. 

### Use App Configuration to manage your secrets
{: #ac-manage-secrets}

App Configuration integrates with [IBM Cloud Secrets Manager](/docs/app-configuration?topic=app-configuration-ac-properties) which helps manage your secrets as if they are configuration properties. This can help in maintaining properties and secrets together as part of the Configuration as Code (CaC).


### Cleanup of obsolete flags
{: #ac-cleanup-obsolete-flags}

Release flags and roll-out flags are only temporarily needed. Operational flags are required until the application exist. Not removing the flags and the corresponding code, can lead to technical debt. When a flag is fully released, and no more required, it can be tagged with specific tag, and once in a specific time frame like once in 6 months, all such tagged feature code and the features can be removed from the system. The same process can be applied to properties, segments and collections.

### Version usage of SDK
{: #ac-version-usage-sdk}

Always use the latest version of the SDKs. Latest version contains the bug fixes, vulnerability fixes and new feature support.

### Listen to the feature or property changes
{: #ac-property-feature-changes}

Listen to the [event-based notifications](/docs/app-configuration?topic=app-configuration-ac-integrate-sdks#ac-integrate-ff-feature-prop-change) for real-time updates in the App Configuration instance using the SDK. This helps to keep you application up to date with the updates.

### Bootstrap your application with App Configuration snapshots
{: #ac-bootstrap-snapshots}

Capture the current configuration using [snapshots](/docs/app-configuration?topic=app-configuration-ac-snapshots) into your git repositories. This can help in maintaining the versions of your configuration, Configuration as Code, bootstrap your application even when there is no connectivity to App Configuration service. 

### Use of Feature flags / Properties in CI/CD pipelines
{: #ac-feature-flags-cicd}

Use App Configuration feature flags or properties in your CI/CD pipelines to avoid hard coding of configurations in the pipeline. 
Also using App Configuration in the pipeline helps manage secrets for your dependencies. For e.g., if a dependency is not used in a specific region or a dependency is applicable only to a specific region, control the creation of Kubernetes secrets or environmental variables in your regional infrastructure according to the applicable dependencies using the [CI/CD pipelines integrated with App Configuration](/docs/app-configuration?topic=app-configuration-ac-toolchain-integration).

### Automate using Infrastructure as Code (IaC)
{: #ac-iaac-automate}

Automate your feature flag deployments using [Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/app_config_feature) supported by App Configuration to easily onboard to a new region. 

### Follow a Governance process
{: #ac-governance-process}

Feature flag hell can be avoided by using a Governance process. This Governance process helps in ensuring the best practices are enforced. This process also helps in identifying the lifecycle of the feature flag, including how to define the feature flag, and when to remove it. App Configuration helps in auditing events using [IBM Cloud Logs](/docs/app-configuration?topic=app-configuration-at_events). Use this feature to track how users and applications are using the feature flags / properties.
