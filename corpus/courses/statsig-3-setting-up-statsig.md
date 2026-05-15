# Statsig 3 - Setting up Statsig

_Estimated time: ~1h 45m_

## Module 1 - Setting up Statsig Overview

_Estimated time: ~1m_

### Course Overview

[StatsigU_SUS_MetaImage_800x400_100125 (1)_82e203.jpeg](https://drive.google.com/file/d/1wa8WYgPHkIET--X6h713uzTpqevElBNj/view)

If you're in charge of setting up Statsig for your team, congrats! Experimentation programs can transform a company. We'll do our best to make setup easy.

In this course, you'll learn how to configure Statsig's SDKs, connect your data and metrics, set up permissions and organization policies, and explore the key resources available to support your team as you scale with Statsig.

## Module 2 - Install and Initialize the Statsig SDK

_Estimated time: ~30m_

### Section overview

[Setting up Statsig_787a70.png](https://drive.google.com/file/d/1welMRM6D8Ev1iz5iw5ZYpfPSloTseSVe/view)

First, we'll walk through how to configure Feature Gate and Experiment Assignment.

This includes installing and initializing the Statsig SDK, setting up the SDK user object and targeting, and running a quick test to make sure assignment is working correctly. Let's dive in!

### Introduction to client and server SDKs

Statsig offers client and server SDKs to enable experimentation and feature management across different parts of your application. In this video, we will dive into when you should use each!

[StatsigU1.1a.mp4](https://drive.google.com/file/d/1GDrw3SJze7GKOKh-KrgVWMvMYaGrZkXL/view) | [https://amplitude.wistia.com/medias/lh3c9mzfar](https://amplitude.wistia.com/medias/lh3c9mzfar)

Visit our docs to learn more about choosing the right SDK Client vs Server.

### Install and initialize the Statsig client SDK

If you've determined you will use Statsig's Client SDK, watch the video below to learn how to install and initialize. Skip this video if you will use Statsig's Server SDK.

[https://www.youtube.com/watch?v=QDPu7EvaLf0](https://www.youtube.com/watch?v=QDPu7EvaLf0) | [https://amplitude.wistia.com/medias/jakavyfdpn](https://amplitude.wistia.com/medias/jakavyfdpn)

Visit our docs to learn more about installing and initializing the Statsig Client SDK.

### SDK user object and targeting

Once your SDK is initialized, the next step is defining your user object - the foundation for targeting and evaluation in Statsig. In this video, we'll walk through how to pass user attributes to the SDK, use them for feature gates and experiments, and verify that targeting and assignment are working correctly in your app.

[https://www.youtube.com/watch?v=_mZVuBzgtEE](https://www.youtube.com/watch?v=_mZVuBzgtEE) | [https://amplitude.wistia.com/medias/ff3u93zvow](https://amplitude.wistia.com/medias/ff3u93zvow)

Visit our docs to learn more about SDK User Object and Targeting.

### Install and initialize the Statsig server SDK

If you've determined you will use Statsig's Server SDK, watch the video below to learn how to install and initialize. Skip this video if you will use Statsig's Client SDK.

[https://youtu.be/r4-4Hed_1Sk?si=IeAk1R4PynDinj9r](https://youtu.be/r4-4Hed_1Sk?si=IeAk1R4PynDinj9r) | [https://amplitude.wistia.com/medias/izms0f5f4l](https://amplitude.wistia.com/medias/izms0f5f4l)

Visit our docs to learn more about installing and initializing the Statsig Server SDK.

### Optional advanced setup

There are a number of advanced setup options that will help you get more out of Statsig's SDKs. In this video, we'll cover advanced configurations like bootstrapping, data adapters, and forward proxies—as well as guidance for handling PII and setting up environment tiers.

These setups aren't required, but they can help improve performance, add resilience, and give you greater control over how Statsig runs in your infrastructure.

[StatsigU1.1b.mp4](https://drive.google.com/file/d/1yop09eRv7O1ReLiQVC8GHMYPRObLxHuu/view) | [https://amplitude.wistia.com/medias/59xvlurt0b](https://amplitude.wistia.com/medias/59xvlurt0b)

### Testing and diagnostics

Once your SDK is configured, it's time to validate that everything is working correctly. In this video, we'll walk through how to test your feature gates and experiments using overrides, set up rollouts in lower environments, and use Diagnostics to monitor gate and experiment health.

[https://www.youtube.com/watch?v=9XR-gVI2g1I](https://www.youtube.com/watch?v=9XR-gVI2g1I) | [https://amplitude.wistia.com/medias/s9zytg1k7s](https://amplitude.wistia.com/medias/s9zytg1k7s)

#### _Referenced Resources_

##### SDK Basics, Install & Initialize

**Type:** How-To Video

[https://www.youtube.com/watch?v=QDPu7EvaLf0](https://www.youtube.com/watch?v=QDPu7EvaLf0) | [https://amplitude.wistia.com/medias/jakavyfdpn](https://amplitude.wistia.com/medias/jakavyfdpn)

Deep Dive 101: SDK Basics, Install and Initialize

##### SDK Logging Events & Exposures

**Type:** How-To Video

[https://youtu.be/rkjq5eCOY9w?si=9uzWEzAX_QFJKysX](https://youtu.be/rkjq5eCOY9w?si=9uzWEzAX_QFJKysX) | [https://amplitude.wistia.com/medias/07xfhbsn1i](https://amplitude.wistia.com/medias/07xfhbsn1i)

Deep Dive 101: SDK Logging Events and Exposures

##### SDK Server-Side Concepts & Differences

**Type:** How-To Video

[https://youtu.be/r4-4Hed_1Sk?si=IeAk1R4PynDinj9r](https://youtu.be/r4-4Hed_1Sk?si=IeAk1R4PynDinj9r) | [https://amplitude.wistia.com/medias/izms0f5f4l](https://amplitude.wistia.com/medias/izms0f5f4l)

Deep Dive 101: SDK Server-Side Concepts and Differences

##### SDK User Object & Targeting

**Type:** How-To Video

[https://www.youtube.com/watch?v=_mZVuBzgtEE](https://www.youtube.com/watch?v=_mZVuBzgtEE) | [https://amplitude.wistia.com/medias/ff3u93zvow](https://amplitude.wistia.com/medias/ff3u93zvow)

Deep Dive 101: SDK User Object and Targeting

## Module 3 - Connect your Events and Metrics

_Estimated time: ~30m_

### Section overview

[StatsigU_SUS_CardImage_1.2_100125_bdabea.jpeg](https://drive.google.com/file/d/1P0jjQij7YIfMObaEIQD0EbplNqRRYW2i/view)

Next, we'll walk through how to connect your events and metrics in Statsig.

This includes linking your data sources, whether through your data warehouse or cloud setup, defining key metrics, and verifying that your feature gates and experiments are reporting results correctly. Let's dive in!

### Connect your warehouse

For teams using a warehouse-native setup, this video walks through how to connect your data to Statsig. You'll learn how to create a new metric source, connect your warehouse tables or queries, and configure fields like timestamp and unit ID so Statsig can analyze your experiments accurately.

[StatsigU1.2afinalfinal.mp4](https://drive.google.com/file/d/1k83q70gx1Lx5ChD5OgW3TDJgOHMNo-kL/view) | [https://amplitude.wistia.com/medias/x4ounfqp50](https://amplitude.wistia.com/medias/x4ounfqp50)

Visit our docs to learn more about how to connect your warehouse to Statsig.

### Define and create your metric catalog

In this video, you'll learn how to build metrics in your Metric Catalog, whether you're using Statsig Cloud or a warehouse-native setup. We'll cover how to pick your metric source, select from different metric types, add filters and breakdowns, and use advanced settings like CUPED and baking windows to make your analysis more powerful.

[StatsigU1.2dfinal.mp4](https://drive.google.com/file/d/1F2E_v5jDMhX7WBTD7d1QP0Y4ehq0WbN9/view) | [https://amplitude.wistia.com/medias/d2bp2bniod](https://amplitude.wistia.com/medias/d2bp2bniod)

Visit our docs to learn more about how to define and create your metric catalog.

### Analyze existing experiment data

If you're using a warehouse-native setup, this optional video shows how to analyze experiments directly within Statsig once your metrics are connected. You'll learn how to interpret the experiment results page, read cumulative exposure and scorecard charts, and dive deeper into insights like variance reduction, impact analysis, and experiment health checks.

[StatsigU1.2f.mp4](https://drive.google.com/file/d/1__LZa1Uvx4EJTwnjEwyW49Q37_28318e/view) | [https://amplitude.wistia.com/medias/5zwzgf22fs](https://amplitude.wistia.com/medias/5zwzgf22fs)

### Connect events

If you're using Statsig Cloud, this video walks through how to connect your events and metrics to Statsig. You'll learn how to either send events through the Statsig SDK, connect existing CDP tools like Segment or Rudderstack, or ingest data directly from your warehouse. By the end, you'll know how to stream the right events into Statsig to power your metrics and experiment analysis.

[StatsigU1.2c.mp4](https://drive.google.com/file/d/10-ZUj5E97n0b6PyVC3DSueZBBq000qMb/view) | [https://amplitude.wistia.com/medias/o4yrx101ir](https://amplitude.wistia.com/medias/o4yrx101ir)

Visit our docs to learn more about how to connect your events to Statsig.

### Test: analyze feature gates and experiments

Once your gates and experiments are live, it's time to make sure everything is working and performing as expected. In this video, you'll learn how to use Diagnostics to verify setup health and debug assignments, and explore the Results page to measure the real impact of your experiments and feature gates on key metrics.

[StatsigU1.2e.mp4](https://drive.google.com/file/d/1BjB46A8EXz8OKz6qW77af0ajkvlQFRza/view) | [https://amplitude.wistia.com/medias/y01v52rlc7](https://amplitude.wistia.com/medias/y01v52rlc7)

## Module 4 - Organization and Project Settings

_Estimated time: ~30m_

### Section overview

[StatsigU_SUS_CardImage_1.3_100125_264664.jpeg](https://drive.google.com/file/d/1COjnIQQiK14ItPMTZGwq9dU3GfUducZf/view)

In this module, we'll walk through the key configurations needed to set up your organization and projects in Statsig Enterprise.

You'll learn how to manage access, configure roles and permissions, and define organization-wide policies to keep your environment secure and consistent. This module is designed for organization admins who are setting up the initial environment and putting guardrails in place for their teams.

It also includes best practices to help you operate efficiently and set your organization up for long-term success. While you don't need to complete each step in order, the sequence follows the setup flow that works best for most enterprise customers.

### Overview of the workspace structure

[statsig workspace structure_357471.png](https://drive.google.com/file/d/1TSzRwvw5qo3WPqpPUV25jLIc7_tRFv60/view)

In Statsig, we have three constructs to help you organize your workspace and scale it out more broadly within your organization.

**Organization** is an enterprise-level environment that allows companies to create project(s) and bring members to work inside the project.

**Project** is a workspace within the organization where the configs (e.g., feature gates and experiments), metrics, and SDK keys you and your team created lives.

**Team** is a group of members at the project level that can help your organization manage the permissions and ownership of resources.

In Statsig, each project within the organization is isolated from one another. This means that none of the resources or data is shared among different projects, even if they are part of the same organization.

For example, if you anticipate any of the metrics between two experiments to be shared today or in the future, you should manage them in the same project. On the flip side, you could consider creating a new project when you're managing separate products or subsidiaries where each has a unique definition of metrics and users.

Visit our docs to learn more about Statsig's organization and project settings.

### Workspace structure that we recommend

[workspace structure that we would recommend_0a4f4e.png](https://drive.google.com/file/d/1WMT2x1jlj8ZmTD9iI317GV-CRci5ZyO_/view)

Statsig team believes that the sensible default structure for most customers is having an organization with a single project where multiple teams contribute and collaborate. So, a single organization, a single project, and multiple teams within the project.

We believe that different teams and functions across your organization can stay well-organized within a single project by leveraging features such as teams, roles, tags, and templates. This also removes the risk of costly migrations if some projects ever need to be consolidated in the future for cross-functional collaborations.

Note that Statsig has rich support for environments within our resources. We consider it an anti-pattern to create multiple projects just to manage lower environment separately from production.

### Configure SSO

[setting up the SSO_382140.png](https://drive.google.com/file/d/1OfwWK6glTCT-TUx-9l-da90xmDrYjBsR/view)

SSO (Single Sign-On) can be configured for your Statsig organization to simplify the user experience and onboarding while improving your security. Given that your organization already have an OIDC provider up and running, we highly recommend configuring SSO on Statsig.

Statsig supports any Identity Provider that implements the OIDC protocol for SSO, such as Okta, Microsoft Entra ID, Google, and more.

Also, if you are using Okta as your Identity Provider, consider integrating SCIM (System for Cross-domain Identity Management) to efficiently manage the user creation/deactivation process as well as user roles for Statsig within Okta.

Visit our docs to learn more about configuring SSO.

### Setting up the organization

[Setting up the organization_ec92a3.png](https://drive.google.com/file/d/1gDGrgChbWb6JLL9rD0qz5Op-RtNlB3L0/view)

When you sign an enterprise contract with Statsig, we will provision your existing Statsig account into an enterprise account. Once provisioned, your account will have access to all the features available for the enterprise plan.

In the settings page from console, you will see that the tab for Organization is now added for your account along with some additional security and governance settings

### Member access

[Setting up the roles_2b1e8f.png](https://drive.google.com/file/d/1fFTduaUUQZ_fD9ciL3r3leWza4kWWST6/view)

Each person is assigned a role that defines their level of access, one at the project level and the other at the organization level. Review the permissions set for each predefined roles so you can assign the appropriate roles to each member. Additionally, you may want to create and assign custom roles in order to align with your organization's needs.

Common examples of custom roles include a **Metrics Admin** (responsible for managing metrics) and a **Data Warehouse Admin** (in Warehouse Native projects, responsible for managing warehouse connections).

Visit our docs to learn more about access management.

### Creating your first project

[Creating your first project_279800.png](https://drive.google.com/file/d/1AeGHywtRZPxezLqknatWdbHqa-QrRntw/view)

As mentioned, a project in Statsig serves as a workspace that contains everything you and your team will create. This includes configs (e.g., feature gates, experiments, dynamic configs, layers) you create, metrics you define, and integrations you set up.

When creating a project, you can set its type to **Open** which would allow anyone in the organization to join freely, or to **Closed** which would allow people to join only by invitation or request.

### Invite your team to the organization

[invite your team to the organization_c023dc.png](https://drive.google.com/file/d/1efgHzhWxKxTNRpHk7grzeAcOPvYa_41D/view)

If you've successfully configured SSO, your teams can now join the Statsig organization by signing in with your identity provider. By default, users who are provisioned through SSO will be assigned a 'Member' role.

If you haven't set up the SSO yet, you can send an invitation email to join the organization to your team members using the 'Invite to Organization' button.

Visit our docs to learn more about inviting your team to the organization.

##### Best practices for your team

Those were the essential first steps for you to get started on Statsig! Now, your teams can join the organization we've just set up and start playing around within the Statsig console and SDK. But this is not the end!

The following pages cover several features that we consider as "best practices" for most enterprise customers using Statsig. While every organization is different and there's no one-size-fits-all, we believe these features will empower you and your team to use Statsig more efficiently and securely.

That being said, there's no need to implement all the following features at once in the beginning. Instead, we'd encourage you to keep them in the back of your mind as these features do come in handy as you scale the adoption of Statsig to your broader organization.

### Creating a team inside your project

[creating a team inside your project_2b63e0.png](https://drive.google.com/file/d/1k8_pvbcxoUqzoTxkNnTD0yLc_vVLFZEY/view)

**Team** is a workspace structure that sits at the **project level** to help with organization and ownership.

Once the teams are configured inside a project and a user is added to the team, any configs (e.g., feature gates, experiments, metrics) created by a user will be **associated** with the team that the user belongs to. And these configs by the user will **automatically inherit** all the default settings and templates from that team.

This feature becomes extremely useful as multiple teams begin to use Statsig, and it also helps the onboarding of new users as it provides a set of defaults from the start.

Visit our docs to learn more about teams within Statsig.

[Configuring the default settings for the team_2ef2b3.png](https://drive.google.com/file/d/1wNfiJB0rtQt0wB8xhl2Eio_jig8N0js2/view)
*Configuring the default settings for team*

[filtering the experiments by associated team_77b6a7.png](https://drive.google.com/file/d/1RXqPFQRweZJk71_BoQxjzp9iVUArnPJc/view)
*Filtering the experiments by associated team*

### Setting review policies

[setting review policies_895b56.png](https://drive.google.com/file/d/1goEkCd8pAygHRoGt25RYI0rKzDjKgzdG/view)

Within Statsig, you can enable reviews for all Statsig configs such as feature gates, dynamic configs, segments, and experiments, requiring a second pair of eyes to review the changes before they get deployed to production.

If desired, you can customize your review policies to align with your organization's needs. For example, you can set up a team of reviewers by giving their roles a permission to approve the reviews. Or, you can give certain roles (e.g., oncalls) the ability to self-approve their changes to allow for agility when needed. Note that you can set the review policies at both project and team level.

Visit our docs to learn more about setting up reviews for team workflows.

### Setting up target apps

[setting up target apps_be1210.png](https://drive.google.com/file/d/1Z9ANWl1G-EZUK0pRnDR0Bhok5aaG_uX2/view)

Target apps is one of the attributes you can associate to your SDK keys and configs. Through target apps, you can precisely set the scope of configs that will be accessed from each SDK key and reduce the size of your payloads.

We highly recommend setting up target apps as you scale the usage of Statsig. It can improve the performance of your application by making the initialization of SDKs faster and keeping the volume of local cache light. It can also enhance your security as the SDKs will send only the necessary configs to each of your client.

Visit our docs to learn more about target apps.

### Setting up notifications

[setting up notifications_c4717e.png](https://drive.google.com/file/d/12Nd6tX6215wHCmEamMAlMwDQccc0mW4L/view)

Statsig has an integration with **Slack**, so you can receive real-time notifications about the activities, status changes, and other useful alerts directly from your Slack workspace.

There are various filters to the notifications, so you can tailor it to focus on the information that matters most for you and your team.

Additionally, you can choose to receive notifications in your email as well for any alerts, reviews, reports, and more.

Visit our docs to learn more about setting up notifications.

### Define experiment policy

##### Experiment Policy grants organization admins the ability to:

- **Set defaults for new experiments:** While Statsig aims to provide an intuitive platform for all users, we understand the unique requirements of every organization. Now, data scientists and experts can decide on experiment best practices for their business, such as default experiment duration and use of sequential testing.
- **Enforce these defaults:** This ensures consistency across all experiments, and that best practices are enforced for experimenters.
- **Tailor Statsig for the business:** Safeguard against unintended misuse by limiting the set of experimentation practices to ones effective to the organization.

Visit our docs to learn more about Experiment Policy.

##### Where can these be configured?

Organization Experiment Policies can be managed by visiting **Product Configuration > Experimentation > Organization** tab. Only organization admins have the ability to modify these settings.

[experiment policy_e1377f.png](https://drive.google.com/file/d/1CkKtuLOfLMVXy9CjxvBMZHx5QUJOKD7D/view)

### Define feature gates policy

##### Feature Gates Policy grants organization admins the ability to:

**Configure the Custom Fields leveraged in Feature Gate targeting:** With this setting, admins can pre-define allowed Custom Fields by ID type, add a description to provide more context on the Custom Field to end users, and pre-define the allowed values. Defining allowed values is optional.

Visit our docs to learn more about Feature Gate policy.

[FG1_a7f707.png](https://drive.google.com/file/d/1fAG8WxnqLbSCgUCuGzA5_79ZYW03WBMJ/view)

**Configure allowed Targeting Criteria for Feature Gates:** With this setting, admins can select which targeting criteria will surface as options during gate creation for end users. These allowed targeting criteria are defined at the ID type as well, enabling you to, for example, create one set of targeting criteria for logged-in (UserID) vs. logged-out (stableID) feature rollouts.

[FG2_613ea3.png](https://drive.google.com/file/d/18V0Ww_MZLF6nsvUlUZEfcNmBB3nqMhiT/view)

**Require Templates for Gate or Dynamic Config Creation:** Enables admins to enforce that all gate or dynamic config creations are from a template. Restrictions on who can create/edit templates (as well as which templates are allowed per-team) can be managed under People -> Teams and Roles.

[FG3_6a4eaf.png](https://drive.google.com/file/d/1e3o-qn5BjqGpH-6rhI2iklrtUeTx6yxI/view)

##### Where can these be configured?

Organization Gate Policy can be managed in settings by visiting **Product Configuration > Feature Management > Organization** tab. Only organization admins have the ability to modify these settings.

[FG4_3272f9.png](https://drive.google.com/file/d/120qb5bgF0eezJX4i2ibuWjs6d3HahMKw/view)

### Create feature gates / experiment templates

Templates enable you to create a blueprint for gates/dynamic configs/experiments to enable standardization and reusability across your Project. Templates can help enforce a rollout sequence, or make it easy for new experimenters to get up & running with your standard team settings for experimentation.

Templates can be enforced at the Org (via Organization Settings and Role-based Access Controls) or at the Team-level. We will detail the various levels of controls and permissions you can enable for templates below.

##### Creating Templates

There are two primary ways to create a new template:

- From the Templates page under Product Configuration
- From a gate/experiment you want to turn into a new template

##### 1. Creating Templates from Project Settings

To create a new template from Project Settings, navigate to **Settings -> Project Configuration -> Templates** and click the **+Create New** CTA, then select whether you want to create a gate, experiment, or dynamic config template.

[templates 2_1189ee.png](https://drive.google.com/file/d/1SxnuE0qJJXdiGXdQP1rKMi4XOPdWLUBH/view)

##### 2. Converting an Existing Config into a Template

If you create a new config that you think would be useful to more folks on the team as a template, you can convert an existing (or currently being created) config into a template. To do this, in the config you wish to convert to a template, tap the "..." menu and select **Save as Template**. This will prompt you to name your template and add a description before saving.

Visit our docs to learn more about templates for Feature Gates and Experiments.

[templates 3_27bc55.png](https://drive.google.com/file/d/1smgaGuV9F4LGHZ7BTFen_a4Y0nAHRoc-/view)

## Module 5 - Next Steps and Support Resources

_Estimated time: ~15m_

### Section overview

[statsigu_sus_cardimage_2.0_101425_480_acba28.png](https://drive.google.com/file/d/11MV_cpTfruIBEU_ogfm54iE7RscQp01o/view)

In this module, we'll share the best ways to stay connected, get help, and keep learning with Statsig. From documentation and community support to webinars and events, you'll find everything you need to keep growing your data-driven development practice. Let's dive in!

### Internal Statsig channel

As new team members start using Statsig, having a central place for questions and learnings can speed up adoption. We recommend creating a dedicated Slack or Teams channel (for example, `#statsig-help`) where users can:

- Ask quick setup or experiment questions
- Share tips and lessons learned
- Tag internal "Statsig champions" or admins for support

This helps your organization build shared knowledge and maintain momentum as usage grows.

### Lean on Statsig Support

Need additional help? Our support team and online resources are here for you.

If your organization has **Premium Support**, you can reach out directly through your **dedicated Statsig Slack channel** for personalized assistance from our team.

If you're on a **Free, Pro, or Self-Serve plan**, you can get help by joining the [Statsig Community Slack](https://statsig.com/slack) — a space where product builders, data scientists, and engineers share questions, tips, and best practices.

You can also:

- **Leverage Statsig's Statbot** to get instant personalized answers to your questions via your in-product Help menu
- Explore the **Statsig Docs** for detailed guides, SDK references, and troubleshooting tips
- Review additional setup guides and product deep dives in the **Statsig Resource Library**

**Pro tip:** Bookmark these links — they'll be invaluable as your team scales and new members onboard.

### See how other teams use Statsig

Curious how other leading companies use Statsig?

Visit [statsig.com/customers](https://statsig.com/customers) to explore real stories and examples from companies using Statsig for experimentation, feature management, and analytics.

Each case study highlights how product, data, and engineering teams scale their culture of data-driven development and measure impact.

### Statsig events

Stay connected with the broader Statsig community by joining our events and webinars.

We regularly host live sessions featuring product deep dives, customer stories, and best practices from teams building and experimenting at scale. You'll also get early looks at new features and insights from the Statsig team.

You can:

- Explore upcoming and past **Statsig Events** to learn from and connect with the Statsig community
- **Follow us on LinkedIn** to keep an eye out for **Statsig Webinars** on product deep dives, conversations with industry leaders, etc.
- Keep an eye out for regional **meetups and community gatherings** throughout the year

**Pro tip:** Bookmark the Events page to stay in the loop on what's coming next — from product updates to advanced experimentation talks.

### Explore the Statsig resource library

Continue your learning journey through **Statsig University** and our additional resources:

- **Statsig University** - self-paced courses like this one and a resource library featuring a collection of learning videos
- **Docs** - in-depth technical reference and implementation examples
- **Blog** - product updates, best practices, and industry insights
- **Webinars** - live sessions and recordings on experimentation, analytics, and AI

🎓 Stay curious — we're always adding new educational content and deep dives to help you and your team get the most out of Statsig.
