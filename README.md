# Amazon Connect (amazon-connect)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Amazon Connect is a cloud-based contact center service that makes it easy to set up and manage a customer contact center and provide reliable customer engagement at any scale, with omnichannel support for voice, chat, email, and task management. It includes AI-powered features for agent assistance, customer profiles, conversation analytics, and outbound campaign management.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/amazon-connect/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/amazon-connect/refs/heads/main/apis.yml)

## Scope

- **Type:** Index

## Tags

- AWS
- Chat
- Contact Center
- Customer Service
- Voice
- AI
- Omnichannel

## Timestamps

- **Created:** 2024-01-15
- **Modified:** 2026-05-19

## APIs

### Amazon Connect Service API

The Amazon Connect Service API provides programmatic access to manage contact center instances, users, routing profiles, contact flows, queues, hours of operation, security profiles, and real-time and historical metrics for customer engagement operations.

- **Human URL:** [https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Service.html](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Service.html)
- **Base URL:** `https://connect.amazonaws.com`

#### Tags

- Contact Center
- AWS
- Voice
- Chat

#### Properties

- [Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Service.html)
- [OpenAPI](openapi/amazon-connect-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/amazon-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/amazon-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [OpenAPI](https://api.apis.guru/v2/specs/amazonaws.com/connect/2017-08-08/openapi.yaml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [JSON Schema](json-schema/amazon-connect-instance-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/amazon-connect-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Pricing](https://aws.amazon.com/connect/pricing/)
- [Getting Started](https://aws.amazon.com/connect/getting-started/)
- [F A Q](https://aws.amazon.com/connect/faqs/)
- [API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/)
- [C L I](https://docs.aws.amazon.com/cli/latest/reference/connect/)
- [Security](https://docs.aws.amazon.com/connect/latest/adminguide/security.html)
- [JSON Schema](json-schema/user-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/queue-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/contact-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/routing-profile-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/contact-flow-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/instance-schema.json) — [JSON Schema](https://json-schema.org/specification)

### Amazon Connect Streams SDK

Amazon Connect Streams is a browser-based integration API and JavaScript SDK that enables embedding and controlling the Amazon Connect Contact Control Panel (CCP) within your web application or CRM system.

- **Human URL:** [https://github.com/amazon-connect/amazon-connect-streams](https://github.com/amazon-connect/amazon-connect-streams)
- **Base URL:** `https://github.com/amazon-connect/amazon-connect-streams`

#### Tags

- SDK
- JavaScript
- Browser
- Contact Center

#### Properties

- [SDK](https://github.com/amazon-connect/amazon-connect-streams)
- [SDK](https://www.npmjs.com/package/amazon-connect-streams)
- [Code Examples](https://github.com/amazon-connect/amazon-connect-snippets)
- [Code Examples](https://github.com/amazon-connect/amazon-connect-chat-ui-examples)
- [SDK](https://github.com/amazon-connect/amazon-connect-chatjs)
- [SDK](https://github.com/amazon-connect/amazon-connect-chat-ios)
- [SDK](https://github.com/amazon-connect/amazon-connect-chat-android)
- [SDK](https://github.com/amazon-connect/AmazonConnectSDK)
- [Tutorials](https://github.com/amazon-connect/amazon-connect-workshops)
- [Postman Collection](collections/amazon-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/amazon-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Amazon AppIntegrations API

The Amazon AppIntegrations service enables you to configure and reuse connections to external applications, powering third-party integrations in the Amazon Connect agent workspace.

- **Human URL:** [https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_AppIntegrations_Service.html](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_AppIntegrations_Service.html)
- **Base URL:** `https://app-integrations.amazonaws.com`

#### Tags

- Integrations
- AWS
- Contact Center

#### Properties

- [Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_AppIntegrations_Service.html)
- [API Reference](https://docs.aws.amazon.com/appintegrations/latest/APIReference/)
- [Postman Collection](collections/amazon-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/amazon-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Amazon Connect Contact Lens API

Amazon Connect Contact Lens enables you to analyze conversations between customers and agents using speech transcription, natural language processing, and intelligent search capabilities. It performs sentiment analysis, detects issues, and enables automatic categorization of contacts with both real-time and post-call analytics.

- **Human URL:** [https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Contact_Lens.html](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Contact_Lens.html)
- **Base URL:** `https://contact-lens.amazonaws.com`

#### Tags

- Analytics
- AI
- Contact Center
- NLP

#### Properties

- [Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Contact_Lens.html)
- [API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Contact_Lens.html)
- [Postman Collection](collections/amazon-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/amazon-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Amazon Connect Outbound Campaigns API

With the outbound campaigns feature of Amazon Connect, you can create high-volume outbound campaigns for appointment reminders, telemarketing, subscription renewals, or debt collection.

- **Human URL:** [https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Outbound_Campaigns.html](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Outbound_Campaigns.html)
- **Base URL:** `https://connect-campaigns.amazonaws.com`

#### Tags

- Outbound
- Campaigns
- Contact Center

#### Properties

- [Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Outbound_Campaigns.html)
- [API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Outbound_Campaigns.html)
- [Postman Collection](collections/amazon-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/amazon-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Amazon Connect Outbound Campaigns V2 API

The outbound campaigns V2 API provides an updated interface for creating high-volume outbound campaigns including multi-channel support and availability in all Amazon Connect regions.

- **Human URL:** [https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Outbound_Campaigns_V2.html](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Outbound_Campaigns_V2.html)
- **Base URL:** `https://connect-campaigns.amazonaws.com`

#### Tags

- Outbound
- Campaigns
- Contact Center

#### Properties

- [Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Outbound_Campaigns_V2.html)
- [API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Outbound_Campaigns_V2.html)
- [Postman Collection](collections/amazon-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/amazon-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Amazon Connect Cases API

With Amazon Connect Cases, agents can track and manage customer issues that require multiple interactions, follow-up tasks, and teams in your contact center. A case represents a customer issue including the steps and interactions taken to resolve it.

- **Human URL:** [https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Cases.html](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Cases.html)
- **Base URL:** `https://cases.amazonaws.com`

#### Tags

- Cases
- Case Management
- Contact Center

#### Properties

- [Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Cases.html)
- [API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Cases.html)
- [Postman Collection](collections/amazon-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/amazon-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Amazon Connect Participant Service API

The Amazon Connect Participant Service enables managing chat participants including agents, customers, and managers. Use it to send messages and events, manage connection state, share attachments, and retrieve chat transcripts within a chat contact.

- **Human URL:** [https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Participant_Service.html](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Participant_Service.html)
- **Base URL:** `https://participant.connect.amazonaws.com`

#### Tags

- Chat
- Participants
- Contact Center

#### Properties

- [Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Participant_Service.html)
- [API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Participant_Service.html)
- [Postman Collection](collections/amazon-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/amazon-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Amazon Connect Customer Profiles API

Amazon Connect Customer Profiles provides a unified customer profile for your contact center with pre-built connectors powered by AppFlow that make it easy to combine customer information from third-party applications such as Salesforce (CRM), ServiceNow (ITSM), and ERP systems with contact history from Amazon Connect.

- **Human URL:** [https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Customer_Profiles.html](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Customer_Profiles.html)
- **Base URL:** `https://profile.profile.amazonaws.com`

#### Tags

- Customer Profiles
- CRM
- Contact Center

#### Properties

- [Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Customer_Profiles.html)
- [API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Connect_Customer_Profiles.html)
- [Postman Collection](collections/amazon-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/amazon-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Amazon Q Connect API

Amazon Q in Connect is a generative AI customer service assistant built on Amazon Bedrock. It provides real-time recommendations to help contact center agents resolve customer issues quickly and accurately by detecting customer intent and providing immediate generative responses, suggested actions, and links to relevant documents.

- **Human URL:** [https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Q_Connect.html](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Q_Connect.html)
- **Base URL:** `https://wisdom.amazonaws.com`

#### Tags

- AI
- Generative AI
- Agent Assist
- Contact Center

#### Properties

- [Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Q_Connect.html)
- [API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Q_Connect.html)
- [Postman Collection](collections/amazon-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/amazon-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Amazon Voice ID API

Amazon Connect Voice ID provides real-time caller authentication and fraud risk detection to make voice interactions in contact centers more secure and efficient. Note - Voice ID end of support is scheduled for May 20, 2026.

- **Human URL:** [https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Voice_ID.html](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Voice_ID.html)
- **Base URL:** `https://voiceid.amazonaws.com`

#### Tags

- Voice
- Authentication
- Fraud Detection
- Contact Center

#### Properties

- [Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Voice_ID.html)
- [API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/API_Operations_Amazon_Voice_ID.html)
- [Postman Collection](collections/amazon-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/amazon-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Arazzo Workflows](arazzo/) — [Arazzo Specification](https://spec.openapis.org/arazzo/latest.html)
- [Portal](https://aws.amazon.com/)
- [Developer Portal](https://aws.amazon.com/connect/)
- [Documentation](https://docs.aws.amazon.com/connect/latest/adminguide/)
- [Terms of Service](https://aws.amazon.com/service-terms/)
- [Privacy Policy](https://aws.amazon.com/privacy/)
- [Support](https://aws.amazon.com/support/)
- [Blog](https://aws.amazon.com/blogs/contact-center/)
- [GitHub Organization](https://github.com/aws)
- [GitHub Organization](https://github.com/amazon-connect)
- [Console](https://console.aws.amazon.com/connect/)
- [Sign Up](https://portal.aws.amazon.com/billing/signup)
- [Login](https://signin.aws.amazon.com/)
- [Status Page](https://health.aws.amazon.com/health/status)
- [Knowledge Center](https://repost.aws/knowledge-center)
- [YouTube](https://www.youtube.com/user/AmazonWebServices)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/amazon-connect)
- [Contact](https://aws.amazon.com/contact-us/)
- [Security](https://aws.amazon.com/security/)
- [Compliance](https://aws.amazon.com/compliance/)
- [Pricing](https://aws.amazon.com/connect/pricing/)
- [Features](undefined)
- [Use Cases](undefined)
- [Spectral Rules](rules/amazon-connect-spectral-rules.yml)
- [Vocabulary](vocabulary/amazon-connect-vocabulary.yaml)
- [Integrations](undefined)
- [Integrations](https://aws.amazon.com/marketplace)
