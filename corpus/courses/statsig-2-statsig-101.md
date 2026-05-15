# Statsig 2 - Statsig 101

_Estimated time: ~2h_

## Module 1 - Introduction to Statsig

_Estimated time: ~10m_

### Welcome to Statsig 101!

[StatsigUni_Statsig101_Intro_700x400_031125_1ec751.png](https://drive.google.com/file/d/19eIwmHIpR-AwOR-ZgEYn3HI4_TmoNXbx/view)

Welcome to Statsig University!

We're excited to have you here as you explore how Statsig can help you build, test, and scale with confidence. This course is designed to give you a clear understanding of what Statsig offers and how to get started.

This course is designed to take about 2 hours, so grab a snack and let's dive in! Oh, and feel free to exit and re-enter the course at any time - your progress will be saved!

[Julie export.mp4](https://drive.google.com/file/d/1s5WjBvsALM0OAQbs9rBG9fKWO_XmjTTA/view) | [https://amplitude.wistia.com/medias/4o8x2ejyse](https://amplitude.wistia.com/medias/4o8x2ejyse)

### Statsig Product Overview

Statsig's Core Product Offerings

Statsig is built to power data-driven decision-making, helping teams move fast while staying confident in their product changes. At its core, Statsig offers four major product SKUs that seamlessly integrate to support the entire product development lifecycle.

[Slide1 4_761428.jpg](https://drive.google.com/file/d/1tv8EnIDdDrt_-h6Xt8PdDa2qKZBkt0RT/view)

---

##### Feature Flagging: Controlled, Confident Releases

Feature flags empower teams to roll out new features gradually, control access dynamically, and reduce the risks of deployments. With Statsig's feature flagging, you can:

- Target features to specific user segments.
- Instantly toggle features on or off without redeploying code.
- Implement kill switches to quickly disable problematic features.

---

##### Experimentation: Test, Learn, and Iterate

Experimentation is at the heart of data-driven product development. Statsig's experimentation platform makes it easy to run A/B tests, multivariate tests, and feature rollouts with statistically rigorous analysis. Teams can:

- Measure the impact of changes with real-time metrics.
- Use Statsig's proprietary stats engine to detect meaningful insights.
- Run experiments at scale without the manual work of analysis.

---

##### Product Analytics: Insights That Drive Action

Product Analytics brings all your event data together, giving you a complete view of user behavior. With built-in dashboards and flexible analytics, you can:

- Track key user interactions across your product.
- Analyze retention, funnels, and user journeys.
- Make data-driven decisions without waiting on custom reports.

---

##### Session Replay: See User Behavior in Action

Session Replay allows teams to record and replay user interactions, providing visual insights into how users navigate and experience your product. With Statsig's Session Replay, you can:

- Identify friction points in onboarding and workflows
- Pinpoint UI issues and debug faster with real session data
- Analyze user behavior to optimize conversions and engagement

### Quiz

**[MATCHING QUESTION]** Which explanation best describes each of Statsig's products?

| Product | Description |
|---|---|
| Experiments | Run randomized controlled trials (A/B or A/B/n tests) with minimal effort, allowing you to measure the impact of product changes on key metrics |
| Feature Flags | A mechanism for teams to configure what system behavior is visible to users without changing application code |
| Product Analytics | Metrics Explorer and dashboards that help you understand how your users experience and interact with your product |
| Session Replay | Record users using your website or product, and play back those recorded sessions |

### Intro to Statsig: What's Next?

Now, you have a fundamental understanding of Statsig and how it helps teams build better products with data. You've learned about Statsig's core product lines including Feature Flags, Experimentation, Product Analytics, and Session Replay.

When you're ready to take the next step, continue to the next module to get Statsig set up!

## Module 2 - Setting up Statsig

_Estimated time: ~30m_

### Introduction to Statsig's SDKs

[StatsigUni_Statsig101_SettingUp_700x400_031125_94e3c1.png](https://drive.google.com/file/d/1paMzOJ0XtA-mIXJ3GjPmmYt0QatGq2Ce/view)

Getting started is easy - our SDKs help you integrate experimentation, feature flagging, and logging into your apps.

With support for 30+ platforms, Statsig's SDKs let you roll out features and run experiments seamlessly across web, mobile, and server-side environments.

In this section, we will cover:

- For everyone using Statsig - core concepts and how to use Statsig's SDKs
- For those setting up Statsig for the first time - design decisions and SDK and workspace setup

### Setting Up Statsig's SDKs

The first step in using Statsig is to set up SDKs so you can use Statsig's products in your application. Hear from our Product Manager, Brock Lumbard, as he shares best practices for getting started and explains how Statsig works under the hood.

[Brock SDK final.mp4](https://drive.google.com/file/d/1YqL98MkRu-cZybApTBWl3vspNgWecc-5/view) | [https://amplitude.wistia.com/medias/g8s2ribmnb](https://amplitude.wistia.com/medias/g8s2ribmnb)

[Getting Started with Statsig's SDKs](https://docs.google.com/presentation/d/1B5WEr9gupt7akiRaPnatPLHDHtlRYNs7mH9IxL4BYV4/edit)

### Quiz

**[MULTIPLE CHOICE]** What is a key difference between Statsig's client-side and server-side SDKs?

- A. Client-side SDKs run within backend environments, while server-side SDKs run in browsers and mobile apps.
- B. ✓ A Statsig Server SDK is used on the backend to manage feature gates, configurations, and experiments, while a Statsig Client SDK is used on the frontend (web, mobile, or other client-facing parts) to communicate with Statsig servers and make runtime decisions.
- C. Server-side SDKs do not support feature flagging, while client-side SDKs do.
- D. There is no difference; both work the same way across all environments.

### Setting up Statsig: What's Next?

That's a wrap on Setting up Statsig!

In this module we've covered:

- How Statsig's SDKs download values and evaluate users
- How to use the SDK
- How to debug your SDK
- Design decisions: deployment model, SDKs, and metrics
- SDK and workspace setup

When you're ready to dive deeper, check out our Docs for step-by-step guides on setting up your SDKs.

## Module 3 - Feature Management

_Estimated time: ~20m_

### Introduction to Feature Flags

[StatsigUni_Statsig101_FeatureManagement_700x400_031125_50f82f.png](https://drive.google.com/file/d/1SsgsR6B7IfjR07JuDx87K3q1RN3SNzOF/view)

Welcome to Feature Management!

Releasing and managing features shouldn't be risky or complex. With Statsig's Feature Management Suite, you can easily roll out changes, personalize experiences, and adapt dynamically - without redeploying code.

What to expect in this module:

- Introduction to Statsig's Feature Management Suite
- A guide to building your first Feature Flag
- A guide to building your first Dynamic Config

Let's dive in!

### Feature Flags Overview

Join our Head of Product, Margaret-Ann for an overview of Statsig's Feature Management Suite. Learn how to control rollouts, test features, and optimize user experiences.

[New Final Feature Flag Demo_5fb378.mp4](https://drive.google.com/file/d/1MMOLTujJfw1Rk5AMiD7E8F9keD4up-m3/view) | [https://amplitude.wistia.com/medias/o1setqayr7](https://amplitude.wistia.com/medias/o1setqayr7)

### Building Your First Feature Flag

Time to dive in! Open up the Statsig Console and follow along as we set up our first Feature Flag.

[Getting started with your first feature flag](https://docs.google.com/presentation/d/1rV2Ev1tabq_bR66CfLlprjatW3906JqiemcKm1ZR9ng/edit)

### Building Your First Dynamic Config

With Statsig's Dynamic Configs, you can replace hard-coded values with JSON defined on the server so you can make changes dynamically without redeploying code. Lets hop back into the Statsig Console and learn how to set up your first Dynamic Config.

[Getting started with your first dynamic config](https://docs.google.com/presentation/d/1qmE1f-MxI77KNjPtRRp3U5TKk1YT80I_OaTAb5MVuLM/edit)

### Quiz

**[MATCHING]** Match the correct definitions for Statsig Feature Flags and Dynamic Configs

| Term | Definition |
|------|-----------|
| Feature Flags | Mechanisms that allow teams to control which system behaviors are visible to users without modifying the application code |
| Dynamic Configs | Mechanisms that enable the replacement of hard-coded values in applications with server-defined JSON, allowing real-time updates and targeted user experiences |

### Feature Management: What's Next?

That's a wrap on the Feature Management Suite! In this module, we've learned about:

- **Feature Flags** - How to turn features on or off, roll out changes gradually, and target specific users.
- **Dynamic Configs** - How to update configurations in real time without redeploying code.

When you're ready to take the next step and implement Feature Management in your own product, check out our Docs for in-depth guides and best practices.

## Module 4 - Experiments

_Estimated time: ~15m_

### Introduction to Experiments

[StatsigUni_Statsig101_Experiments_700x400_031125_d6e1b4.png](https://drive.google.com/file/d/1bZMDiS9GB0AldDnpPi0gDjIVW7l9EiUh/view)

Welcome to Experimentation!

It's time to dive into Statsig's Experimentation suite and learn how to run effective experiments on your product.

In this module, you can look forward to:

- Introduction to Statsig's Experimentation Product
- Building Your First Experiment: Step-by-step guidance on setting up and running your very first experiment

Let's get started!

### Experimentation Overview

Join our Head of Product, Margaret-Ann for an overview of Statsig's Experimentation product. Learn how to test multiple variants of a product feature, run mutually exclusive experiments in parallel, and measure the direct impact of changes in product and business metrics.

[new final Experimentation Demo 3_6ebba0.mp4](https://drive.google.com/file/d/1kwo6X0-0Dlq2c5yZDYRpNHOVPptU8P66/view) | [https://amplitude.wistia.com/medias/w0e8b957ef](https://amplitude.wistia.com/medias/w0e8b957ef)

### Creating Your First Experiment

Time to dive in! Open up the Statsig Console and follow along as we set up our first experiment.

[Getting started with your first experiment](https://docs.google.com/presentation/d/1tYTvxicyTg5MhJbWjVgQTBXAeCENaU4Rz0K2moZXBH4/edit)

### Quiz

**[MULTIPLE CHOICE]** Which of the following is NOT a use case of Statsig's experimentation product?

- A. Test multiple variants (A/B or A/B/n) of a product feature
- B. ✓ Instantly adjust app properties like UI elements or service thresholds without changing code
- C. Run mutually exclusive experiments in parallel
- D. Measure the direct impact of changes on product and business metrics

### Experimentation: What's Next?

That's a wrap on Statsig's Experimentation Suite! In this module, you've learned about how to create, manage, and analyze experiments, ensuring you ship features that deliver value to your users and business.

When you're ready to take the next step and implement Experiments for yourself, check out our Docs for in-depth guides and best practices.

## Module 5 - Product Analytics

_Estimated time: ~15m_

### Introduction to Product Analytics

[StatsigUni_Statsig101_ProductAnalytics_700x400_031125_ac0ab0.png](https://drive.google.com/file/d/1lMJUonPGHvxSNQ9G1Piki7sx6J3EpGAF/view)

Welcome to Product Analytics!

Understanding your users and how they interact with your product is key to making smarter decisions. Statsig's Product Analytics suite helps you track, analyze, and optimize your product performance with powerful metrics, dashboards, and drill-down capabilities - all without complex setup.

In this module, you'll learn:

- An introduction to Statsig Product Analytics, including Metrics Explorer and dashboards
- Using Statsig Product Analytics to analyze key trends, segment users, and uncover insights with different chart types
- Best practices for setting up dashboards to monitor product performance effectively

Let's get started!

### Product Analytics Overview

Join our Product Analytics PM, Akin Olugbade, for an overview of Statsig's Product Analytics tools. Learn how to explore key metrics, uncover trends, and build insightful dashboards to better understand user behavior and make data-informed decisions.

[Product Analytics Overview_f4ab9d.mp4](https://drive.google.com/file/d/11ek9er-z3cBwM1R7XUwl0gizPfZnTsbj/view) | [https://amplitude.wistia.com/medias/g359xcnsxw](https://amplitude.wistia.com/medias/g359xcnsxw)

### Getting Started with Product Analytics

Explore more ways to use Product Analytics - from metric drilldowns to conversion funnels to user journeys - to better understand your users and uncover actionable insights.

[Getting started with Product Analytics](https://docs.google.com/presentation/d/10wdx1DFcp5orQQ7MlMqR6nCL53_jD2kvApxV5vnxYPk/edit)

### Quiz

**[MULTIPLE CHOICE]** Which of the following is NOT a common chart type for Statsig Product Analytics?

- A. Funnels
- B. Retention
- C. Distribution
- D. ✓ Heatmaps
- E. User Journeys

### Product Analytics: What's Next?

That's a wrap on Statsig Product Analytics! In this module, we've covered:

- **Metric Drilldowns** - Analyze trends over time, segment users, and compare key metrics.
- **Funnels** - Visualize user drop-off and optimize conversion flows.
- **Retention** - Measure how well users return to your product over time.
- **Distributions** - Understand how metrics are distributed across your user base.
- **User Journeys** - Map out paths users take through your product to uncover common behaviors.
- **Dashboards** - Build custom views to monitor product health and key performance indicators.

Whether you're tracking feature adoption, diagnosing drop-offs, or refining user experiences, Statsig's Product Analytics gives you the tools to make data-driven decisions with confidence. When you're ready to dive into your own metrics, check out our Docs for in-depth guides and best practices.

## Module 6 - Powering Product Development Lifecycle

_Estimated time: ~30m_

### Introduction to the Product Development Lifecycle

[StatsigUni_Statsig101_PoweringLifecycle_700x400_031125_7282e8.png](https://drive.google.com/file/d/1lBO1ZashWV_Au4GMjmlWBWSU8WI_3aQE/view)

Powering Your Product Development Lifecycle

Now that you understand how to set up and use Statsig, let's explore how to get the most out of the platform.

Statsig's feature flagging, experimentation, and analytics tools can be used together to power your Build-Ship-Measure-Learn product loop. In this module, you will learn how to best use these products together to quickly and confidently create products that your users love.

What to expect in this module:

- How to use Statsig's products together to maximize insights and efficiency
- The Build -> Ship -> Measure -> Learn framework and why it matters
- How to build an experimentation culture that enables data-driven decisions at scale

Let's get started!

### Build → Ship → Measure → Learn Loop

Bringing It All Together: Build. Ship. Measure. Learn. Repeat.

The Build -> Ship -> Measure -> Learn loop is the foundation of modern product development. Each stage benefits from using Statsig's tools as key inputs:

- **Build** smarter by making informed product decisions backed by data
- **Ship** confidently behind Feature Gates and Dynamic Configs, giving you full control over rollouts.
- **Measure** impact on key metrics using Experiments and Gate Pulse, ensuring every change delivers value.
- **Learn** by drilling into results with Product Analytics and Session Replay, uncovering actionable insights to refine and improve.

By using Statsig's products together, you create a continuous learning loop - where every feature launch isn't just a release, but a step toward better products, deeper insights, and a stronger experimentation culture.

[Slide1 5_a1e0f5.jpg](https://drive.google.com/file/d/15u7vM2WOMbS-j-ROtAP0b2LV1cBjtACK/view)

### How to Build an Experimentation Culture for Data-Driven Product Development

Building a Culture of Data-driven Product Development

Experimentation is often seen as an aspirational practice, especially at smaller, fast-moving companies who are strapped for time and resources. But the most successful companies prove that making data-driven decisions at scale isn't just possible - it's essential.

So, how can you get your team making decisions in a more data-driven way while continuing to remain lean and maintaining ship velocity? To truly unlock their value, teams need to embrace experimentation as a core part of their culture. In this section, we'll cover:

- How to start building metrics understanding & empathy on your team
- Crawl -> Walk -> Run framework for kickstarting your experimentation journey
- What "good" actually looks like at scale

[How to build an experimentation culture for data-driven product development.mp4](https://drive.google.com/file/d/1sPmr2VF-81mefqmbly6HNxhEbi-hYH3P/view) | [https://amplitude.wistia.com/medias/4tik79zcxh](https://amplitude.wistia.com/medias/4tik79zcxh)

### Quiz

**[MULTIPLE CHOICE]** True or false: building a culture for data-driven product development helps make decisions more centralized, and less distributed

- A. True
- B. ✓ False

---

**[MULTIPLE CHOICE]** At which time horizon should you measure the impact of a new feature or product?

- A. Short-term
- B. Long-term
- C. ✓ Both

### Wrapping Up: Powering Your Product Development Lifecycle

That's a wrap on learning how to use Statsig's Feature Flags, Experiments, and Analytics together to power your entire product development lifecycle. In this module, we've covered:

- **The Build -> Ship -> Measure -> Learn framework** - How to connect feature management, experimentation, and analytics to make smarter product decisions.
- **Building a culture for data-driven product development** - How to foster a data-driven mindset and scale decision-making across your team.

Thank you for taking the Statsig 101 course! We hope you found it valuable and now have a stronger foundation for using Statsig to build faster and make smarter decisions.

If you want to dive deeper, check out these resources:

- Statsig Docs - Comprehensive guides and documentation
- Resource Library - Case studies, best practices, and more
- Slack Community - Connect with other users and Statsig experts

We're excited to see what you build with Statsig!
