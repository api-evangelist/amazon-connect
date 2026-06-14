# Amazon Connect GraphQL Schema

This directory contains a conceptual GraphQL schema for the Amazon Connect cloud contact center platform, derived from the [Amazon Connect API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/).

## Overview

Amazon Connect is AWS's cloud-based contact center service providing omnichannel routing (voice, chat, email, tasks), AI-powered agent assistance via Amazon Q, real-time and historical analytics via Contact Lens, outbound campaigns, cases management, and deep integrations with the AWS ecosystem.

The GraphQL schema (`amazon-connect-schema.graphql`) models the core resources and operations exposed by the Amazon Connect Service API and its companion APIs.

## Schema File

- [`amazon-connect-schema.graphql`](amazon-connect-schema.graphql)

## Type Coverage

The schema defines **70+ named types** across the following categories:

### Scalars
Custom AWS scalars: `AWSDateTime`, `AWSJSON`, `AWSPhone`, `AWSARN`

### Enums (12)
| Enum | Description |
|------|-------------|
| `InstanceStatus` | CREATION_IN_PROGRESS, ACTIVE, CREATION_FAILED |
| `QueueType` | STANDARD, AGENT |
| `QueueStatus` | ENABLED, DISABLED |
| `ContactFlowType` | CONTACT_FLOW, CUSTOMER_QUEUE, OUTBOUND_WHISPER, and more |
| `ContactFlowStatus` | PUBLISHED, SAVED |
| `ContactState` | INCOMING, PENDING, CONNECTING, CONNECTED, ENDED, and more |
| `ContactInitiationMethod` | INBOUND, OUTBOUND, TRANSFER, API, CALLBACK, and more |
| `Channel` | VOICE, CHAT, TASK, EMAIL |
| `PhoneNumberType` | TOLL_FREE, DID, UIFN, SHARED, and more |
| `PhoneNumberStatus` | CLAIMED, IN_PROGRESS, FAILED |
| `AgentStatusType` | ROUTABLE, CUSTOM, OFFLINE |
| `StorageType` | S3, KINESIS_VIDEO_STREAM, KINESIS_STREAM, KINESIS_FIREHOSE |

### Core Resource Types
| Type | Description |
|------|-------------|
| `ContactCenter` | Top-level resource aggregating all instance resources |
| `Instance` | An Amazon Connect instance with status and configuration |
| `Queue` | Contact queue with routing, hours, and capacity settings |
| `RoutingProfile` | Agent routing profile with media concurrencies and queue priorities |
| `ContactFlow` | IVR/routing flow with content and lifecycle state |
| `ContactFlowModule` | Reusable contact flow module |
| `Contact` | A customer interaction across voice, chat, or task channels |
| `Agent` | Contact center agent (user) with identity, phone config, hierarchy |
| `AgentStatus` | Named agent state (Available, Offline, custom states) |
| `HoursOfOperation` | Operating schedule with timezone and per-day time ranges |
| `SecurityProfile` | Permission set for agents and supervisors |
| `PhoneNumber` | Claimed DID or toll-free number associated with an instance |
| `PromptConfig` | Audio prompt stored in S3 for use in contact flows |
| `HierarchyGroup` | Organizational unit within a 5-level agent hierarchy |
| `HierarchyLevel` | Named level (L1-L5) in the agent hierarchy structure |
| `IntegrationAssociation` | Third-party or AWS service integration record |

### Channel-Specific Types
| Type | Description |
|------|-------------|
| `Voice` | Voice contact properties including phone number and auto-accept |
| `Chat` | Chat contact with participant tokens and persistent session support |
| `Task` | Task contact with name, references, and scheduled time |
| `ChatTranscript` | Full transcript with pagination |
| `TranscriptEvent` | Individual message or event within a chat session |

### Metrics Types
| Type | Description |
|------|-------------|
| `RealTimeMetric` | Live metric definition (contacts in queue, agents available, etc.) |
| `HistoricalMetric` | Historical metric with statistic, unit, and threshold |
| `MetricResult` | Metric value with dimensional breakdown |
| `MetricDataV2` | V2 metric result with filters |
| `MetricInterval` | Time window and interval period for metric queries |
| `MetricThreshold` | Comparison and threshold value for SLA metrics |
| `MetricDimensions` | Queue, channel, routing profile, agent, and contact dimensions |

### Supporting Types
`StorageConfig`, `StorageLocation`, `EncryptionConfig`, `KinesisVideoStreamConfig`, `KinesisStreamConfig`, `KinesisFirehoseConfig`, `RoutingProfileQueue`, `QueueReference`, `DefaultContactFlow`, `RoutingProfileAssociation`, `MediaConcurrency`, `OutboundCallerConfig`, `Priority`, `Endpoint`, `ContactAttribute`, `ContactTimestamp`, `Tag`, `TimeRange`, `UserData`, `CurrentUserData`, `UserIdentityInfo`, `UserPhoneConfig`, `AgentHierarchy`, `HierarchyGroupSummary`, `LexBot`, `Lambda`, `APIKey`, `Token`, `VoiceRecording`, `AttachmentItem`, `MessageMetadata`, `QueueMetric`, `QueueName`, `ContactFlowSummary`, `AgentSummary`

## Operations

### Queries (40+)
- Instance and contact center overview
- Queue listing, search, and detail
- Routing profile and queue association queries
- Contact flow and module retrieval
- Contact search with time range filters
- Agent/user listing, search, and current state
- Agent status and hierarchy traversal
- Security profile and phone number queries
- Hours of operation detail
- Real-time and historical metrics (V2)
- Prompt, storage config, and integration listing
- Chat transcript retrieval

### Mutations (55+)
- Full CRUD for instances, queues, routing profiles, contact flows, agents, security profiles, hours of operation, and prompts
- Contact lifecycle: start (voice/chat/task), stop, suspend, resume, transfer, tag
- Queue and routing profile queue association management
- Phone number claim, update, and release
- Storage config association and update
- Lambda and Lex bot association
- Integration association create and delete
- Tag/untag any resource by ARN

### Subscriptions (3)
- `onContactStateChanged` — real-time contact state updates
- `onAgentStatusChanged` — agent availability changes
- `onQueueMetricUpdated` — live queue metric updates

## Source

- API Reference: https://docs.aws.amazon.com/connect/latest/APIReference/
- Service docs: https://docs.aws.amazon.com/connect/latest/adminguide/
- Base URL: `https://connect.amazonaws.com`
