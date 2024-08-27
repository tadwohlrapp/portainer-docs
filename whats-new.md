# What's new in version 2.21

Portainer version 2.21 includes a number of new features, fixes, and updates. It is also our first LTS release. For a full list of changes, please refer to our [release notes](release-notes.md).

## Long Term Support (LTS)

2.21 is our first Long Term Support, or "LTS", release of Portainer. LTS releases are meant to be production-ready versions that you can safely run on your mission-critical infrastructure. Generally, LTS releases won't have any new features as compared to the Short Term Support, or "STS", releases that came before - in this case 2.20 - but will be focused on making sure those features are rock solid.

You can read more about our new release principles in our CEO Neil's [blog post](https://www.portainer.io/blog/2024-release-principle).

## New Features

### New menu structure ![](.gitbook/assets/button\_be.png) ![](.gitbook/assets/button\_ce.png)

The first change you're likely to notice in 2.21 is an update to the menu structure within Portainer. In order to streamline the user experience for people that are new to containerization, as well as those more experienced, we've updated the names of some menu items, moved others into new subsections, and generally made it easier to understand where to find the functionality you're after. This is particularly evident for Kubernetes environments, but applies to Portainer as a whole as well.

### More performance improvements ![](.gitbook/assets/button\_be.png) ![](.gitbook/assets/button\_ce.png)

Our ongoing efforts to improve the performance of Portainer continue in this release. Along with the updated menu structure we have implemented additional caching to improve page load times as well as moved more of our pages and page components to the React framework. We've also added more background population of page contents so that rendering the crucial information comes first with additional longer to retrieve information being loaded asynchronously.

For Kubernetes users, we've added a per-user toggle to [enable front-end data caching for Kubernetes environments](user/account-settings.md#application-settings) that can also help with page load times. This is configurable through the [My account](user/account-settings.md) page.

### Support for streaming Portainer activity and authentication logs to external systems ![](.gitbook/assets/button\_be.png)

When deploying Portainer within your organization you may have the desire or perhaps compliancy need to ship your log files to an external log aggregator. In 2.21 BE we've added the ability to push Portainer's activity and authentication logs in syslog format to an external Security Information and Event Management (SIEM) system without having to write a custom wrapper around the Portainer API.

At present this feature is considered experimental and is [configurable via CLI options](advanced/siem.md), but we're intending to expand this feature further in the future based on customer feedback.

### Buttons to reload image up to date indicators ![](.gitbook/assets/button\_be.png)

Our new image indicator feature has been quite popular since we released it way back in 2.14, and we've made a few adjustments to it in subsequent versions. In 2.21 we've added in buttons on the Containers, Stacks, and Services list pages, as well as the details page for each, that will perform an on-demand reload of the image status for the page you're on.

<figure><img src=".gitbook/assets/2.20-whatsnew-imageindicatorbutton.png" alt=""><figcaption></figcaption></figure>

Image indicators are cached for 24 hours after they are loaded for performance reasons, but with these buttons you can force a check at any time you need one.

### List and manage more Kubernetes object types ![](.gitbook/assets/button\_be.png)

We've expanded the types of Kubernetes objects you can list and manage through Portainer in 2.21. In this version, admins will see new pages for [Service Accounts](user/kubernetes/more-resources/service-accounts.md), [Cluster Roles and Cluster Role Bindings](user/kubernetes/more-resources/cluster-roles.md), and [Roles and Role Bindings](user/kubernetes/more-resources/namespace-roles.md) under the new **More Resources** menu item.

<figure><img src=".gitbook/assets/2.20-whatsnew-moreresources.png" alt=""><figcaption></figcaption></figure>

### Enforce admin-only Kubernetes secret viewing in the UI ![](.gitbook/assets/button\_be.png)&#x20;

As a cluster administrator you may want to restrict the viewing and editing of secrets within the cluster to administrator users. In 2.21 [we've added a toggle](user/kubernetes/cluster/setup.md#security) that allows you to do just that.

<figure><img src=".gitbook/assets/2.20-whatsnew-adminsecrets.png" alt=""><figcaption></figcaption></figure>

Note that due to limitations within Kubernetes itself, this feature does not hide secrets from viewing through other tools outside of Portainer.

### Templates for Edge ![](.gitbook/assets/button\_be.png)&#x20;

Template functionality has existed in Portainer for non-Edge environments for some time, and in 2.21 we're bringing that functionality to Edge Stacks. With Edge Compute enabled, you'll find a new [Edge Templates](user/edge/templates/) option in the left-hand menu. Here you can deploy an Edge Stack from our pre-provided templates, or create and manage your own custom Edge Stack templates for your applications.

<figure><img src=".gitbook/assets/2.20-whatsnew-edgetemplates.png" alt=""><figcaption></figcaption></figure>

Edge Templates support the same functionality as our non-Edge templates, including variables and Git repository deployments, and can also be deployed from the [Create Edge stack](user/edge/stacks/add.md) page.

### New Edge Administrator role ![](.gitbook/assets/button\_be.png)

2.21 also introduces a new [Edge administrator role](admin/settings/edge.md#edge-compute-access) for Edge Compute users. This role lets you give users full control over resources in Edge environments without giving them full administrative access to all of Portainer.

<figure><img src=".gitbook/assets/2.20-whatsnew-edgeadmin.png" alt=""><figcaption></figcaption></figure>

## Enhancements and Fixes

### Updated third-party binaries and libraries ![](.gitbook/assets/button\_be.png) ![](.gitbook/assets/button\_ce.png)

As we do with every release, we've updated the versions of the third-party binaries and libraries that we use within Portainer to newer versions. This resolves a number of reported CVEs as well as providing improved performance and functionality in some cases.

### Support for new Kubernetes versions ![](.gitbook/assets/button\_be.png) ![](.gitbook/assets/button\_ce.png)

Along with updated binaries and libraries, we've also updated our Kubernetes version support in 2.21. We now support deploying to Kubernetes 1.30 environments in all cases, including through our supported cloud providers in our Kubernetes as a Service feature as well as our Kubernetes cluster creation tools for on-premise infrastructure.

### Consolidate Helm functionality into Applications ![](.gitbook/assets/button\_be.png) ![](.gitbook/assets/button\_ce.png)

As part of our menu restructuring and general usability improvements, in 2.21 we moved the Helm functionality for Kubernetes environments into the Applications system proper, rather than the separate system we had before.

<figure><img src=".gitbook/assets/2.20-whatsnew-helm.png" alt=""><figcaption></figcaption></figure>

You can now provision applications from Helm charts via the standard [Create from manifest](user/kubernetes/applications/manifest.md) option under [Applications](user/kubernetes/applications/), and Helm deployments will appear in the Applications list alongside other non-Helm deployments. We've also made some improvements to how you can configure and manage your Helm chart repositories within Portainer.

### Allow stopping a Kubernetes app by scaling to 0 ![](.gitbook/assets/button\_be.png) ![](.gitbook/assets/button\_ce.png)

Docker Swarm users have for a long time been able to scale their services to 0, but this wasn't possible in Portainer for Kubernetes deployments. With 2.21, now it is. Scaling a deployment to 0 replicas will result in the application being stopped, and you can then scale it back up at a later date to start it again.

### Added option to disable stacks for Kubernetes ![](.gitbook/assets/button\_be.png) ![](.gitbook/assets/button\_ce.png)

When deploying an application on Kubernetes, we provide the ability to define a “stack” that your deployment belongs to, which can be useful for grouping deployments. However, this functionality may not always be ideal for everyone’s workflow, so in 2.21 we’ve added the [option to disable stack functionality](admin/settings/general.md#kubernetes-settings) for Kubernetes environments.
