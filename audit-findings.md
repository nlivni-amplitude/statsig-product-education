# Statsig Content Audit — NotebookLM Findings

_Generated 2026-05-12 from NotebookLM "Statsig Content Audit — Course Material & Captions"_
_50 sources: 3 course MDs + 41 video captions + 1 handover-gaps doc + 5 LXD design context docs_
_Notebook: https://notebooklm.google.com/notebook/55d9758a-32a7-49f7-8041-d6ab513c9989_

---

## 1. Competencies — what learners can do after all three courses

_Prompt: 

Continuing conversation 9bb603f0...
Answer:
**Implementation & Data Connections**
*   By the end, a learner can install and initialize both client-side and 
server-side Statsig SDKs across various environments [1, 2].
*   By the end, a learner can configure the Statsig user object to pass standard
and custom attributes for precise user targeting [3-5].
*   By the end, a learner can connect data sources by streaming events via 
SDKs/CDPs or by connecting and querying data warehouse tables [6-8].
*   By the end, a learner can define and build custom metrics in the Metric 
Catalog using different aggregation types, filters, and measurement windows 
[9-11].
*   By the end, a learner can configure advanced SDK infrastructure options such
as bootstrapping, data adapters, and forward proxies to improve performance and 
resilience [2, 12-14].

**Feature Management**
*   By the end, a learner can create and deploy feature gates with targeted 
rules and conditions to safely control feature rollouts [15-17].
*   By the end, a learner can build dynamic configs to replace hard-coded values
and update application configurations in real-time [18, 19].
*   By the end, a learner can utilize overrides and the "test gate" tool to 
manually force specific feature variants for QA and development testing [20-22].
*   By the end, a learner can schedule automated feature rollouts to gradually 
scale up user exposure without manual intervention [15, 23].

**Experimentation**
*   By the end, a learner can design and configure multivariate experiments with
clearly defined target units, variants, and primary/secondary metrics [24-27].
*   By the end, a learner can validate experiment health using the Diagnostics 
tab to investigate exposure streams and spot issues like Sample Ratio Mismatch 
(SRM) [28-30].
*   By the end, a learner can interpret experiment scorecards to evaluate 
confidence intervals, variance reduction, and statistical significance [31-33].

**Product Analytics**
*   By the end, a learner can build product analytics charts—including Funnels, 
Retention, and User Journeys—to analyze conversion drop-offs, feature 
stickiness, and user navigation paths [34-37].
*   By the end, a learner can construct and curate shared analytics dashboards 
to monitor trends and track Key Performance Indicators (KPIs) by product area 
[38, 39].

**Governance & Administration**
*   By the end, a learner can manage organizational governance by configuring 
Single Sign-On (SSO), role-based access control (RBAC), peer review policies, 
and configuration templates [40-43].

Resumed conversation: 9bb603f0-ffe5-4343-aa20-30d9f9552dd0

---

## 2. Instructional Design Audit

_Prompt: 

Answer:
Here is a candid instructional design assessment of the Statsig course materials
based on your internal audit criteria. 

Overall, the courses exhibit strong subject-matter expertise but rely heavily on
traditional, passive presentation methods (video lectures) rather than modern, 
active learning experience design (LXD) principles. 

**A. Presence of Explicit Learning Objectives**
*   **Assessment:** Poor. The courses lack strictly formulated, measurable 
learning objectives (e.g., using Bloom's Taxonomy action verbs). 
*   **Evidence:** Course intros generally rely on broad "what we will cover" or 
"you will learn to understand" statements. For example, Statsig 101 states, 
"you'll learn: An introduction to Statsig Product Analytics... Using Statsig 
Product Analytics to analyze key trends" [1]. Statsig 1 states, "This course 
will help you get hands-on... You'll learn how to manage feature rollouts" [2].
*   **Critique:** These statements fail to define the terminal behaviors the 
user must demonstrate. They violate the internal LXD rule to "never use 
'understand,' 'learn,' 'know,' or 'be aware of'" [3]. They describe the content 
agenda rather than learner competencies. 

**B. Practice / Application Opportunities**
*   **Assessment:** Weak. The courses are heavily reliant on passive video 
consumption and lack structured interactivity or sandbox practice.
*   **Evidence:** The primary directive for application is unstructured: "Time 
to dive in! Open up the Statsig Console and follow along as we set up our first 
Feature Flag" [4], [5]. 
*   **Critique:** There are no structured "Try It Out" prompts tied to specific 
scenarios or demo data [6], [7]. The learner is left to mimic the video clicks 
in their own console, assuming they have an environment properly configured to 
do so. This creates a high barrier to actual skill application during the 
course.

**C. Application-Style Assessment vs. Recall-Style**
*   **Assessment:** Poor. The assessments are purely recall-style and do not 
test application or interpretation.
*   **Evidence:** All visible quizzes in Statsig 101 are Level 1/2 Bloom's 
(Remember/Understand). They consist of basic matching questions for product 
definitions [8], [9], [10], true/false recall questions [11], and 
multiple-choice questions about definitions ("What is a key difference between 
Statsig's client-side and server-side SDKs?" [12]). 
*   **Critique:** This directly conflicts with the LXD principle that 
"interpretation literacy is now more important, not less... Make interpretation 
a first-class objective" [13], [14]. None of the quizzes ask the learner to look
at an experiment scorecard to identify an issue, interpret a funnel drop-off, or
decide on a feature rollout based on simulated data. 

**D. Gotcha / Common-Mistake Coverage**
*   **Assessment:** Strong. The SMEs narrating the videos do an excellent job 
anticipating and explaining common user pitfalls.
*   **Evidence:** 
    *   In the SDK module, Brock explicitly calls out common errors, such as 
accidentally evaluating a gate before initialization is complete [15], falling 
into bootstrapping data traps [16], and forgetting to refresh `updateUser` for 
long-lived client tabs [16].
    *   In the Experimentation modules, Tyler flags misinterpretations of the 
"mean observed difference" (reminding users that values are normalized per user,
not raw counts) [17], [18], [19]. He also addresses the causes of Sample Ratio 
Mismatch (SRM), such as redirect tests dropping exposures [20], and debunks the 
overblown fear of interaction effects between overlapping experiments [21].
    *   Tyler explains the logic trap of the `else if` rule execution in feature
gates, warning users that if someone fails an earlier rule, they will not pass a
later one [22], [23].
*   **Critique:** The spoken content shines here. It provides deep, authentic 
insights that will save developers and PMs real time in production.

**E. Conceptual Scaffolding**
*   **Assessment:** Good, but inconsistent. The courses provide solid mental 
models for complex topics, but sometimes devolve into feature-click tours.
*   **Evidence:**
    *   *Strong scaffolding:* The Experimentation module anchors the complex 
process of testing to middle-school science methodology (PHEOC: Problem, 
Hypothesis, Experiment, Observe, Conclusion) [24]. The strategy for building an 
experimentation culture uses a highly effective "Walk, Jog, Run, Fly" framework 
[25], [26]. The foundational differences between Client and Server SDKs are also
well-mapped before showing code [27], [28], [29].
    *   *Weak scaffolding:* The Product Analytics module lists out features 
sequentially ("Here we have dashboards... Funnel charts... Retention charts... 
User journeys" [30]) rather than using a "problem-first" approach to introduce 
them [31].
*   **Critique:** While the strategic and developer-focused content is 
well-scaffolded, the analytics sections feel like feature-tours. The 
instructional design would benefit from anchoring these analytics tools to 
specific use cases or business problems [32] rather than just explaining what 
each chart does.

Conversation: 9bb603f0-ffe5-4343-aa20-30d9f9552dd0 (turn 1)

---

## 3. Persona Reshape — three ILT tracks

_Prompt: 

Answer:
Based on the Statsig course inventory and our LXD principles, here is how the 
existing content should be mapped to a three-track Instructor-Led Training (ILT)
program, along with what should be dropped and what needs to be added. 

### 1. Content Mapping by Audience Track

**Track 1: Product Manager / Decision Maker**
*Focus: Experiment design, measuring impact, product analytics, and building a 
data-driven culture.*
*   **Building an Experimentation Culture:** The "Walk, Jog, Run, Fly" framework
[1, 2] and strategy for turning every launch into a test [3].
*   **Experiment Design & Interpretation:** Formulating hypotheses [4], setting 
primary/secondary metrics [5, 6], and reading Pulse scorecards (understanding 
confidence intervals and mean observed differences) [7, 8].
*   **Advanced Experimentation Strategy:** Managing interaction effects with 
mutually exclusive layers [9] and using meta-insights/holdouts to measure 
aggregate impact [10, 11].
*   **Product Analytics for PMs:** Using Funnels for conversion drop-off [12], 
Retention charts to measure product stickiness [13], and User Journeys to 
discover organic navigation paths [14].
*   **Feature Gates (Strategic):** Turning feature gates into A/B tests [15] and
using scheduled/canary rollouts to minimize risk [16, 17].

**Track 2: Engineer / Implementer**
*Focus: SDK integration, data pipelines, codebase implementation, and 
debugging.*
*   **SDK Initialization:** Core differences between Server and Client SDKs 
[18-20], and how SDKs evaluate rules without constant network calls [21, 22]. 
*   **User Object Configuration:** Passing standard and custom attributes to the
SDK for precise targeting [23, 24].
*   **Advanced Infrastructure:** Configuring bootstrapping to reduce latency 
[25, 26], setting up data adapters for fallback storage (e.g., Redis) [27], and 
using forward proxies [28].
*   **Testing & Diagnostics:** Using overrides and the "test gate" tool for QA 
[29, 30], evaluating the live exposure stream [31, 32], and debugging Sample 
Ratio Mismatch (SRM) caused by redirect tests or crashes [33, 34].
*   **Data Connections:** Connecting data warehouses (BigQuery, Snowflake) [35, 
36], configuring metric queries using timestamp and unit ID [36], and streaming 
events via SDKs [37, 38].

**Track 3: Admin / Owner**
*Focus: Governance, security, workspace architecture, and standardization.*
*   **Workspace Architecture:** Deciding between a single-project vs. 
multi-project setup and configuring Environments (Dev, Staging, Prod) [39-41].
*   **Access & Security:** Configuring Single Sign-On (SSO/SCIM) [42] and 
defining custom Role-Based Access Control (RBAC) [43].
*   **Policies & Safeguards:** Mandating peer review policies for feature gates 
and experiments [44], enforcing organization-wide experiment policies [45], and 
creating mandatory configuration templates for teams [46, 47].
*   **Performance Optimization:** Setting up target apps to restrict SDK payload
sizes [48].

### 2. Content to Drop for an ILT Context

*   **Passive "Click-Tour" Walkthroughs:** The existing courses rely heavily on 
"follow along as I click" videos [49, 50]. In an ILT, these must be dropped in 
favor of live, hands-on sandbox activities where learners perform the task 
themselves. 
*   **Recall-Style Quizzes:** Drop all basic matching and true/false questions 
(e.g., "What is a feature flag?") [51, 52]. ILT assessments should be 
scenario-based discussion prompts, aligning with the internal LXD rule to avoid 
low-level Bloom's taxonomy in favor of applied interpretation [53, 54].
*   **Redundant Marketing Content:** General introductory videos pitching *why* 
Statsig is great [55, 56] should be drastically reduced. ILT learners have 
already purchased the tool; their time should be spent on application.

### 3. What's Missing & Needs to be Added

**For the PM / Decision Maker Track:**
*   **Interpreting Ambiguous Results:** The current content teaches what the 
charts mean [8, 57], but lacks scenario-based interpretation labs [53]. We need 
scenarios where secondary metrics tank while primary metrics rise, or where 
confidence intervals are borderline, forcing PMs to make and defend a 
ship/no-ship decision.
*   **Stakeholder Communication:** Templates or frameworks for communicating 
experiment results and the "why" behind a rollback to non-technical 
stakeholders.

**For the Engineer / Implementer Track:**
*   **Live Coding Sandboxes:** Engineers need a "Try It Out" lab where they are 
given a broken React app and must initialize the SDK properly, handle a caching 
error, or implement a targeted feature gate in real code.
*   **Handling Network Latency:** Deeper scenarios on dealing with long-lived 
client tabs and ensuring `updateUser` is called correctly to prevent stale 
experiment variants [58].

**For the Admin / Owner Track:**
*   **Cost and Billing Management:** Guidance on how to monitor event volume, 
manage data ingestion costs, and audit inactive metrics.
*   **User Lifecycle Management:** Procedures for offboarding users, auditing 
workspace changes via audit logs, and cleaning up stale feature flags that are 
cluttering the codebase [59].

Conversation: 9bb603f0-ffe5-4343-aa20-30d9f9552dd0 (turn 1)

---

## 4. Gap Map — shallow coverage and missing application

_Prompt: 

Answer:
**List A: Topics introduced but not deeply explained**
*   **Session Replay:** Introduced in the initial product overview as one of 
Statsig's four core product SKUs used to record and replay user interactions, 
but it is never covered in a dedicated deep-dive module like Feature Flags, 
Experiments, or Product Analytics [1, 2].
*   **Multi-arm bandits:** Briefly name-dropped as an advanced experimentation 
capability Statsig offers, but the course immediately pivots to standard A/B/n 
testing without explaining how bandits work or how to configure them [3]. 
*   **CUPED (Variance Reduction):** Mentioned as a toggleable setting in the 
Metric Catalog to reach statistical significance faster using a look-back 
window, and shown on the scorecard, but the underlying mechanics of how it 
reduces variance are not deeply explained [4, 5].
*   **Advanced SDK Infrastructure (Bootstrapping, Data Adapters, Forward 
Proxies):** Introduced as ways to improve performance, reduce latency, and 
manage fallback storage [6-8]. The narrator warns about common traps (like 
changing the user object between bootstrapping and getting values), but actual 
implementation steps are deferred to the documentation [9, 10].
*   **Target Apps:** Mentioned as a tool to restrict which configs an SDK key 
can access to reduce payload sizes and improve performance, but the course does 
not walk through the actual setup process [11].
*   **AI / LLM Experimentation:** Briefly mentioned as a use case for parameters
(e.g., passing weights and ranking parameters to ML models without changing 
code), but no specific examples or workflows are provided for evaluating AI 
models [12, 13].

**List B: Topics explained well but never applied**
*   **Interpreting Experiment Scorecards (Pulse):** The courses thoroughly 
explain how to read confidence intervals, interpret the mean observed 
difference, normalize metrics per user, and look for novelty effects [14-19]. 
However, there are no scenario-based assessments where a learner must look at a 
simulated scorecard and make a "ship" or "no-ship" decision.
*   **Formulating Hypotheses and Power Analysis:** The instructional scaffolding
is strong, linking hypothesis creation to the "PHEOC" scientific method and 
explaining the importance of estimating impact magnitude and using power 
analysis to set durations [20-22]. Despite this, learners are never asked to 
draft a hypothesis or calculate a target duration for a mock scenario.
*   **Diagnosing Sample Ratio Mismatch (SRM):** The narrator explicitly explains
what causes SRM (e.g., redirect tests dropping exposures or varying crash rates)
and how the chi-square test detects it [23, 24]. Yet, there is no hands-on 
troubleshooting exercise where a learner must investigate a failing health 
check.
*   **Managing Interaction Effects with Layers:** The concept is explained 
brilliantly, debunking overblown fears of interaction effects while clearly 
explaining how to use mutually exclusive layers and cap traffic allocations at 
100% [25-28]. However, learners never configure a layer or resolve a simulated 
overlapping experiment conflict. 
*   **Building an Experimentation Culture:** The strategy for scaling 
data-driven decisions is detailed comprehensively using the "Walk, Jog, Run, 
Fly" framework, complete with real-world examples from companies like Facebook 
[29-33]. Because the course assessments rely on simple multiple-choice recall, 
learners are never prompted to assess their own company's maturity stage or 
apply the framework to a business case study [34, 35]

Conversation: 9bb603f0-ffe5-4343-aa20-30d9f9552dd0 (turn 1)

---

## 5. Briefing Doc (NotebookLM auto-generated)

# Briefing Document: Learning Experience Design and Statsig Product Integration

## Executive Summary

This document synthesizes the strategic framework for Learning Experience Design (LXD) and the comprehensive product architecture of the Statsig platform. It provides an exhaustive overview of the internal LXD workflows at Amplitude—ranging from needs assessment to data-driven tracking—and the technical foundations of Statsig’s experimentation, feature management, and analytics suites. 

Key insights include a detailed analysis of the "Rule of Thirds" in product development, the "Walk, Jog, Run, Fly" framework for building an experimentation culture, and the technical specifications for implementing the Statsig SDK across client and server environments. Additionally, the document outlines the iterated architecture for Course Inventory 2.0, designed to streamline content management and refresh cycles.

---

## Detailed Analysis of Key Themes

### 1. The LXD Workflow and Course Architecture
The LXD process at Amplitude follows a rigorous six-phase lifecycle:
*   **Needs Assessment:** Scanning for pitfalls and conducting stakeholder interviews to scope research.
*   **Course Design:** Drafting learning objectives and outlines using specialized agents (e.g., `Course-objectives-bot`).
*   **Course Development:** Building lesson structures in authoring tools like Rise, supplemented by automated knowledge check generation.
*   **Publishing:** Delivery via Skilljar/Amplitude Academy, requiring a completed Launch Sheet for metadata and SEO.
*   **Tracking & Data Analysis:** Monitoring video engagement via Wistia and course satisfaction through SurveyMonkey.
*   **Stakeholder Communication:** Weekly performance reporting and relationship tracking.

#### Course Inventory 2.0 Structure
To support this workflow, the Course Inventory is transitioning to a more robust architecture (v2), moving toward JSON or AWS/Superblocks (v3).

| Category | Key Fields |
| :--- | :--- |
| **Identity** | Name, slug, language, and english_source_id for localized content. |
| **Ownership** | SME roles (PM, PMM, Engineering, Support) and relevant Slack channels. |
| **Skilljar Metadata** | Status (live, hidden, deprecated), short/long descriptions, and search keywords. |
| **Production Assets** | Drive links for SCORM files, Rise 360 project links, and course decks. |
| **Refresh Tracking** | Audit dates, product versions at publish, and AI video flags. |

### 2. Statsig Product Pillars
Statsig offers four major product SKUs that integrate to support the full product development lifecycle:

*   **Feature Management:** Utilizes "Feature Gates" as kill switches and for targeted rollouts. It allows teams to divorce code deployment from feature release, enabling remote toggling of functionality.
*   **Experimentation:** Facilitates randomized controlled trials (A/B/n tests). It includes advanced statistical tools like CUPED (variance reduction) and sequential testing to shorten experiment durations while maintaining rigor.
*   **Product Analytics:** Provides deep-dive capabilities through Metric Drilldown, Funnels, Retention charts, and User Journeys to discover real user paths.
*   **Session Replay:** Records and replays user interactions to pinpoint UI friction and debug issues visually.

### 3. Experimentation Culture and the "Rule of Thirds"
A core tenet of the Statsig philosophy is the observation of the "Rule of Thirds":
*   **One-third of features are winners:** They move metrics in the positive direction.
*   **One-third are neutral:** They require iteration to become positive.
*   **One-third are losers:** They actively degrade top-line metrics.

Without experimentation, organizations ship the "losers" blindly, leaving money on the table. A healthy culture celebrates losses as learning opportunities, fostering a distributed, bottoms-up decision-making process.

#### The "Walk, Jog, Run, Fly" Framework
Organizations scale their experimentation maturity through four phases:
1.  **Walk:** Establishing a data baseline and identifying North Star metrics (e.g., ARR for B2B, DAU for consumer apps).
2.  **Jog:** Putting every launch behind a feature flag and starting to run experiments based on hypotheses.
3.  **Run:** 10x-ing experiment velocity and using analytics to identify new opportunities.
4.  **Fly:** Every launch is an experiment across the entire stack (Front-end, Back-end, Infra, and ML models).

### 4. Technical Infrastructure: SDKs and Data Ingestion
Statsig’s architecture is designed for high performance and minimal latency.

| SDK Type | Context | Behavior |
| :--- | :--- | :--- |
| **Client-side** | Single end-user (iOS, Android, JS) | Downloads all evaluations upon initialization; subsequent checks require **no network call**. |
| **Server-side** | Multi-user (Node, Go, Python, etc.) | Downloads rule sets to the server; evaluates logic locally to remain secure and performant. |

#### Data Ingestion Methods
*   **Statsig Cloud:** Ingests data via SDKs, auto-capture events (clicks), or CDP providers like Segment and RudderStack.
*   **Warehouse Native:** Statsig connects directly to data warehouses (BigQuery, Snowflake) to analyze experiments using existing business metrics without moving the underlying data.

---

## Important Quotes with Context

### On Experimentation Philosophy
> "If you double the number of experiments you do per year, you're going to double your inventiveness." — **Jeff Bezos (quoted in "Product Best Practices")**
*   **Context:** Used to emphasize that frequent experimentation leads to faster learning and better discovery of user preferences.

### On Statistical Rigor
> "If that entire range of outcomes does not include that there is a zero percent difference between test and control, we are saying there is a statistically significant difference... that's where the name Statsig comes from." — **Tyler (Statsig Engineer, Analyze Results)**
*   **Context:** Explaining the interpretation of confidence intervals and p-values in the Pulse results view.

### On Culture and Leadership
> "I would celebrate teams. I would applaud these teams who ran twelve experiments and all twelve failed... for him this represented that they were valuing velocity and learning." — **Chamath Palihapitiya (quoted regarding Facebook’s growth culture)**
*   **Context:** Illustrating that a successful experimentation culture values the process and learning over purely positive outcomes.

### On the "HIPPO" Effect
> "When you have data, this culture [of following the Highest Paid Person's Opinion] can't thrive. It just doesn't work." — **Margaret Ann (Statsig PM, Experimentation Culture)**
*   **Context:** Discussing how data empowers distributed decision-making and prevents decision-making based purely on seniority or confidence.

---

## Actionable Insights

*   **Implement "Kill Switches" for All Mobile Releases:** Due to the lengthy approval cycles of app stores, teams should place every new mobile feature behind a Feature Gate. This allows for an immediate rollback if a critical bug is detected without a new code push.
*   **Utilize Layers for Mutual Exclusivity:** When running multiple experiments that may clash (e.g., various changes to a "left rail" UI), use Statsig Layers. This ensures a single user is only in one experiment within that layer, preventing "interaction effect" noise.
*   **Standardize Hypothesis Setting with PHEOC:** Before running any test, teams should follow the Problem, Hypothesis, Experiment, Observation, and Conclusion framework. Hypotheses should explicitly state the "Action," "Predicted Outcome," and "Rationale" to insulate the team from false positives.
*   **Audit Handover Assets for "Gaps":** When migrating content from one LMS to another (as seen in the Statsig-to-Amplitude migration), look specifically for "inline screenshots," "trimmed video cuts," and "quiz content," as these are frequently missing from standard Drive exports.
*   **Adopt Progressive Rollouts:** Use a multiplier-based rollout strategy (e.g., 0% -> 2% -> 10% -> 50% -> 100%) to validate system health and user impact before full exposure. This is particularly critical for infrastructure or backend changes.
*   **Enforce Tag Taxonomy:** For Course Inventory management, ensure all courses are tagged by `product_tags`, `sku_tags`, and `matrix_domain_tags`. This enables the automated "Refresh" and "Audit" workflows to correctly scope changelog searches and documentation checks.