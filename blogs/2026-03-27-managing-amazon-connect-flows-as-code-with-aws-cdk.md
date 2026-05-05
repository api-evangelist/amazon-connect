---
title: "Managing Amazon Connect flows as Code with AWS CDK"
url: "https://aws.amazon.com/blogs/contact-center/managing-amazon-connect-flows-as-code-with-aws-cdk/"
date: "Fri, 27 Mar 2026 13:34:33 +0000"
author: "Manish Tulzapur"
feed_url: "https://aws.amazon.com/blogs/contact-center/feed/"
---
<p>Every day, Amazon Customer Service handles millions of customer contacts across Amazon and its subsidiaries, spanning multiple regions including North America, Europe, South Africa, and Asia Pacific. Managing contact flows at this scale across multiple Amazon Connect instances to accommodate Retail and Amazon subsidiaries required a scalable, programmatic approach. The team set out to maintain consistency and support rapid innovation while maintaining high-quality customer experiences.</p> 
<p>Amazon Connect provides <a href="https://docs.aws.amazon.com/prescriptive-guidance/latest/aws-cdk-layers/layer-1.html">L1 (low-level) AWS CloudFormation constructs</a> for programmatic flow deployment. While these constructs support infrastructure as code (IaC) practices, developers work directly with JSON structures that mirror the <a href="https://docs.aws.amazon.com/connect/latest/APIReference/flow-language.html">Amazon Connect Flow language specification</a>. For enterprise contact centers managing hundreds of flows across multiple instances, Amazon Customer Service built higher-level abstractions that bring software engineering best practices, including type safety, build-time testing, version control, and CI/CD, to contact flow management.</p> 
<p>This post covers how the team built <a href="https://docs.aws.amazon.com/prescriptive-guidance/latest/aws-cdk-layers/layer-2.html">L2 AWS Cloud Development Kit (AWS CDK)</a> constructs to manage contact flows as code at scale, migrating hundreds of flows and modules while reducing deployment and maintenance time from days to minutes.</p> 
<h2>The opportunity with L1 constructs</h2> 
<p>Amazon Connect’s L1 AWS CloudFormation constructs provide programmatic access to flow deployment, which is essential for IaC practices. The following example shows a basic flow deployment using L1 constructs:</p> 
<pre><code class="lang-ts">import * as connect from 'aws-cdk-lib/aws-connect';
new connect.CfnContactFlow(this, 'MyFlow', {
  instanceArn: 'arn:aws:connect:us-east-1:123456789012:instance/abc-123',
  name: 'CustomerServiceFlow',
  type: 'CONTACT_FLOW',
  content: JSON.stringify({
    "Version": "2019-10-30",
    "StartAction": "12345678-1234-1234-1234-123456789012",
    "Actions": [
      {
        "Identifier": "87654321-1234-1234-1234-123456789012",
        "Parameters": {
          "Text": "Hello, welcome to Customer Service"
        },
        "Transitions": {
          "NextAction": "12345678-1234-1234-1234-123456789012"
        },
        "Type": "MessageParticipant"
      }
    ]
  })
});</code></pre> 
<p>At enterprise scale with hundreds of flows across all Connect instances, the team identified opportunities to build further on this foundation:</p> 
<ul> 
 <li>Type safety: Raw JSON strings don’t provide compile-time validation or IDE support.</li> 
 <li>Maintainability: Flows with dozens of actions become difficult to read and modify in JSON.</li> 
 <li>Consistency: Deploying the same flow across multiple instances requires careful manual duplication.</li> 
 <li>Testing: While Amazon Connect now offers <a href="https://aws.amazon.com/blogs/contact-center/reduce-testing-time-by-up-to-90-introducing-native-testing-and-simulation-for-amazon-connect/">native testing and simulation</a>, the team needed additional compile-time structural validation, resource dependency checks, and organizational rule enforcement that go beyond runtime testing.</li> 
 <li>Standards enforcement: No mechanism to verify organizational best practices are followed across flows.</li> 
</ul> 
<p>These observations led to building L2 constructs that provide higher-level abstractions while maintaining full compatibility with Amazon Connect’s capabilities.</p> 
<h2>Solution overview: L2 constructs for contact flows</h2> 
<p>The solution introduces a TypeScript library that provides L2 AWS CDK constructs for defining Amazon Connect flows programmatically. The architecture consists of four key components:</p> 
<ul> 
 <li>TypeScript library: High-level, type-safe builders for flow action blocks, flows, modules, and transitions.</li> 
 <li>Validation framework: Build-time checks for flow structure, resource dependencies, and organizational rules.</li> 
 <li>Transformation engine: Bidirectional conversion between TypeScript code and Amazon Connect Flow JSON.</li> 
 <li>AWS CDK integration: Automated deployment to multiple Amazon Connect instances through CI/CD pipelines.</li> 
</ul> 
<p>The library allows developers to write flows using intuitive builder patterns instead of manipulating raw JSON. The following example shows the same flow from earlier, reimagined with L2 constructs:</p> 
<pre><code class="lang-ts">import { FlowBuilder, MessageParticipantActionBuilder, DisconnectActionBuilder }
  from '@amzn/connect-flows-typescript';
const disconnectAction = new DisconnectActionBuilder().build();
const messageAction = new MessageParticipantActionBuilder()
  .withText('Hello, welcome to Customer Service')
  .nextAction(disconnectAction)
  .build();
const flow = new FlowBuilder('CustomerServiceFlow')
  .startingWith(messageAction)
  .build();
new ConnectFlowConstruct(this, 'MyFlow', {
  instanceArn: connectInstance.instanceArn,
  flowDefinition: flow
});</code></pre> 
<p>This approach provides immediate benefits: type safety catches errors at compile time, the code is self-documenting and easier to review, and the same flow definition can be deployed consistently across instances.</p> 
<h2>Building flows with L2 constructs</h2> 
<p>Consider a flow that checks if a queue is within operating hours and routes customers accordingly, a common pattern in high-volume contact centers. This pattern directly impacts the customer journey by directing contacts to the right destination at the right time, whether that’s a live agent, self-service automation, or an after-hours message.</p> 
<p>Using L2 constructs (TypeScript):</p> 
<pre><code class="lang-ts">const checkHoursOfOperation = new CheckHoursOfOperationActionBuilder()
  .withHoursOfOperation(hoursOfOperationId)
  .whenInHours(transferToQueueAction)
  .whenOutOfHours(disconnectAction)
  .build();

const flow = new FlowBuilder('QueueRoutingFlow')
  .startingWith(checkHoursOfOperation)
  .build();</code></pre> 
<p>Equivalent L1 approach (raw JSON):</p> 
<pre><code class="lang-json">{
  "Version": "2019-10-30",
  "StartAction": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "Actions": [
    {
      "Parameters": {},
      "Identifier": "verifyQueueOperatingHours",
      "Type": "CheckHoursOfOperation",
      "Transitions": {
        "NextAction": "b2c3d4e5-f678-90ab-cdef-123456789012",
        "Conditions": [
          {
            "NextAction": "b2c3d4e5-f678-90ab-cdef-123456789012",
            "Condition": {
              "Operator": "Equals",
              "Operands": [
                "True"
              ]
            }
          }
        ],
        "Errors": [
          {
            "NextAction": "c3d4e5f6-7890-abcd-ef12-34567890abcd",
            "ErrorType": "NoMatchingError"
          }
        ]
      }
    },
    {
      "Identifier": "b2c3d4e5-f678-90ab-cdef-123456789012",
      "Type": "SetWorkingQueue",
      "Parameters": {
        "QueueArn": "arn:aws:connect:us-east-1:123456789012:instance/abc-123/queue/primary-queue"
      }
    },
    {
      "Parameters": {},
      "Identifier": "c3d4e5f6-7890-abcd-ef12-34567890abcd",
      "Type": "DisconnectParticipant",
      "Transitions": {}
    }
  ]
}</code></pre> 
<p>The difference is clear: 10 lines of readable, type-safe TypeScript versus 30+ lines of manually managed JSON with hardcoded UUIDs and nested transition mappings.</p> 
<p>With the L2 construct approach, you can build safer flows with compile-time type mismatch detection, automatic reference updates during refactoring, extractable common patterns for reuse, and clear intent without needing to understand JSON structure details.</p> 
<h3>Composite action blocks</h3> 
<p>One of the most powerful capabilities of L2 constructs is creating composite action blocks, reusable components that encapsulate common patterns of actions frequently used together. These composites help maintain consistent customer journey experiences by standardizing how common scenarios are handled across flows.</p> 
<p><img alt="Snippet showing a potential repeating pattern of action blocks which can be designed to be a composite action block for implementation to increase reusable patterns." class="alignnone wp-image-14506 size-full" height="372" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/03/24/Blog1.png" width="936" /></p> 
<p>As shown in the image above, instead of repeating a “transfer to queue and tell customer if there’s no capacity before disconnecting” pattern throughout flows, you can create a composite action. These blocks create a library of reusable patterns that reduce code duplication, encapsulate proven patterns, simplify flow authoring, and provide building blocks for rapid development.</p> 
<h2>L2 construct architecture</h2> 
<p>The library prioritizes type safety, bidirectional transformation, and stable IDs for analytics.</p> 
<p>The public API consists of three main components: ActionDeclaration (base interface for all flow actions), FlowBuilder (orchestrates flow construction and validation), and action-specific builders, such as SetWorkingQueue, CheckHoursOfOperation, and MessageParticipant. Each builder follows a consistent pattern with fluent APIs:</p> 
<pre><code class="lang-ts">export class SetWorkingQueueActionBuilder {
  private queueArn?: string;
  private id?: string;

  withQueueArn(arn: string): this {
    this.queueArn = arn;
    return this;
  }

  withId(id: string): this {
    this.id = id;
    return this;
  }

  build(): ActionDeclaration {
    if (!this.queueArn) {
      throw new Error('Queue ARN is required');
    }
    return {
      id: this.id ?? generateStableId(),
      type: 'SetWorkingQueue',
      parameters: { QueueArn: this.queueArn }
    };
  }
}</code></pre> 
<p>The transformation engine handles three critical conversions: JSON to in-memory model, in-memory model to TypeScript code, and TypeScript code back to JSON. This bidirectional capability is essential for migration. Existing flows authored in the Amazon Connect UI can be exported as JSON, transformed into TypeScript code, and then maintained as code going forward. The transformation maintains high fidelity with the original flow definition, supporting behavioral consistency during migration.</p> 
<h3>Validation and rule engine</h3> 
<p>Build-time validation is a key differentiator of the L2 construct approach. The validation framework operates at three levels:</p> 
<p>Type-level validation: TypeScript’s type system enforces correct parameter types at compile time:</p> 
<pre><code class="lang-ts">// Compile error: wrong parameter type
const action = new CheckContactAttributesActionBuilder()
  .whenNumberGreaterThan("not a number", nextAction); // Type error

// Correct usage
const action = new CheckContactAttributesActionBuilder()
  .whenNumberGreaterThan(5, nextAction); // Type-safe</code></pre> 
<p>Structural validation: The FlowBuilder validates flow structure before generating JSON:</p> 
<pre><code class="lang-ts">const flow = new FlowBuilder('MyFlow')
  .build(); // Error: No start action defined

const validFlow = new FlowBuilder('MyFlow')
  .startingWith(action1)
  .build(); // Valid structure</code></pre> 
<p>Custom rule engine: Organizational standards are enforced through a pluggable rule engine:</p> 
<pre><code class="lang-ts">class EnableLoggingRule implements ValidationRule {
  validate(flow: FlowDefinition): ValidationResult {
    const firstAction = flow.actions[0];
    if (firstAction.type !== 'enableLogging') {
      return { valid: false, message: 'First action must enable cloudwatch logging' };
    }
    return { valid: true };
  }
}
</code></pre> 
<p>Before deployment, the validation framework also verifies that referenced AWS resources exist in the target account. Since each contact flow and module is deployed as an AWS CloudFormation template following the CRUD pattern, CloudFormation validates resource dependencies during stack operations, preventing runtime failures caused by missing dependencies.</p> 
<h2>Deployment pipeline at scale</h2> 
<p>Deploying flows to all Amazon Connect instances across multiple regions, subsidiaries, and deployment stages requires multi-stage automated orchestration.</p> 
<p>The AWS CDK construct handles deploying identical flow logic across instances while managing environment-specific configurations. In line with how Amazon performs <a href="https://aws.amazon.com/builders-library/automating-safe-hands-off-deployments/">safe, hands-off deployments</a>, Amazon Connect flows progress through four stages with automated testing gates: Beta (limited test traffic with monitoring), Gamma (significant test traffic with monitoring and approval gate), and Production (production traffic with real-time monitoring and automated rollback).</p> 
<p><img alt="Architecture diagram showing TypeScript flow definitions passing through the L2 construct library for validation, then deploying via AWS CDK and CloudFormation through Beta, Gamma, and Production " class="alignnone wp-image-14524 size-large" height="764" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/03/24/Blog2Finale1-1024x764.jpg" width="1024" /></p> 
<p>Different environments require different resource ARNs (AWS Lambda functions, queues, prompts). The library supports environment-specific configuration through a centralized mapping system:</p> 
<pre><code class="lang-ts">function getLambdaArnForEnvironment(stage: string): string {
  return stage === 'Prod'
  ? 'arn:aws:lambda:us-east-1:123456789012:function:prod-handler'
  : 'arn:aws:lambda:us-east-1:123456789012:function:dev-handler';
}</code></pre> 
<p>Deployments include automated rollback on failure with service level indicator (SLI) based monitoring:</p> 
<pre><code class="lang-ts">class FlowDeploymentMonitor {
&nbsp; async monitorDeployment(flowId: string): Promise&lt;void&gt; {
&nbsp;&nbsp;&nbsp; const metrics = await this.getFlowMetrics(flowId);
&nbsp;&nbsp;&nbsp; if (metrics.errorRate &gt; THRESHOLD) {
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; await this.rollbackDeployment(flowId);
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; throw new Error('Deployment rolled back due to high error rate');
&nbsp;&nbsp;&nbsp; }
&nbsp; }
}</code></pre> 
<p>What previously required careful coordination across instances now completes in minutes through automated CI/CD pipelines.</p> 
<h2>Best practices and lessons learned</h2> 
<p>Through implementing and operating this system at scale, the team identified several best practices. For L2 construct design: use single-parameter methods for clarity, validate parameters in builder methods (fail fast), and provide sensible defaults.</p> 
<p>When refactoring flows, preserve action IDs to maintain analytics continuity. For testing: validate individual action builders with unit tests, verify resource dependencies with integration tests, and deploy to Beta for basic functionality verification.</p> 
<p>When to use each approach: L2 constructs for complex flows, multi-instance deployments, and frequently updated flows. L1 constructs for simple flows and one-off deployments. The Amazon Connect UI for rapid prototyping, visual flow design, and training new team members. Consider prototyping new flows in the Amazon Connect UI first, then using the transformation engine to convert them to TypeScript for ongoing maintenance.</p> 
<p>For scaling: extract common patterns into shared libraries, use semantic versioning, maintain examples and migration guides, establish code review processes, and assign clear ownership to development teams.</p> 
<h2>Conclusion</h2> 
<p>Building L2 AWS CDK constructs for Amazon Connect flows has changed how Amazon Customer Service manages contact flows. The results include:</p> 
<ul> 
 <li>Type safety with compile-time validation, eliminating classes of runtime errors that previously caused customer-impacting incidents.</li> 
 <li>Deployment and maintenance time reduced from days to minutes across all instances.</li> 
 <li>Hundreds of contact flows and modules migrated; handling contact volume across subsidiaries and stages.</li> 
 <li>Zero configuration drift with consistent flow logic deployed across subsidiaries, monitored by AWS CloudFormation’s drift detection feature on templates.</li> 
 <li>Significant reduction in production incidents, as manual deployment errors that previously caused high-impact incidents are now caught before deployment.</li> 
 <li>Full audit history with every flow change tracked in Git with code review, approval, and rollback capability.</li> 
</ul> 
<p>By treating contact flows as IaC, Amazon Customer Service created a foundation that supports rapid experimentation and continuous improvement of customer journeys. Flows get tested before deployment, deploy consistently across touchpoints, and are monitored in production.</p> 
<p>This approach is applicable to enterprise Amazon Connect customers managing multiple instances. Whether you’re managing flows across subsidiaries, regions, or stages, the patterns described here can help scale your contact flow operations while maintaining quality and consistency.</p> 
<h2>Next steps</h2> 
<p>Ready to implement Contact Flows as Code? Start by auditing your current flows to identify migration candidates, then pick your most complex flow as a proof of concept. Set up a test environment and try implementing your first L2 construct.</p> 
<p>Resources to get started:</p> 
<ul> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/APIReference/flow-language.html">Amazon Connect Flow language API documentation</a></li> 
 <li><a href="https://docs.aws.amazon.com/cdk/v2/guide/constructs.html">AWS CDK construct design patterns</a></li> 
 <li><a href="https://docs.aws.amazon.com/cdk/v2/guide/best-practices.html">AWS CDK best practices</a></li> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/adminguide/what-is-amazon-connect.html">Amazon Connect developer guide</a></li> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html">Amazon Connect API reference</a></li> 
</ul> 
<p>We’re exploring making the L2 construct library available as an open-source repository. If you’re interested in using or contributing to the library, or ready to transform your customer service experience with Amazon Connect, <a href="https://pages.awscloud.com/GLOBAL-field-SP-Amazon-Connect-Contact-Us-reg-archived.html?trk=1a309559-e1e0-46f2-b6e9-10ea4a5c52b1&amp;sc_channel=el">contact us</a>.</p> 
<h3>About the Authors</h3> 
<table style="width: 100%; border-collapse: collapse;"> 
 <tbody> 
  <tr> 
   <td style="width: 220px; vertical-align: top; padding-bottom: 30px;"><img alt="Manish Tulzapur" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/03/24/Blog3-2.jpg" style="width: 201px; height: 300px;" /></td> 
   <td style="vertical-align: middle; padding-bottom: 30px;">Manish Tulzapur (he/him) is a Senior Software Development Engineer at Amazon based in Seattle, WA. He is passionate about building developer-friendly tooling that empowers teams to deliver consistent, high-quality customer experiences at scale, making it easier for builders to do the right thing. When he’s not writing code, you’ll find Manish competing on the ultimate frisbee field or logging miles on Seattle’s trail networks as he trains for his next ultramarathon.</td> 
  </tr> 
  <tr> 
   <td style="width: 220px; vertical-align: top;"><img alt="Lindsey Pogue" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/03/24/Blog4-2-201x300.jpg" style="width: 201px; height: 300px;" /></td> 
   <td style="vertical-align: middle;">Lindsey Pogue (she/her) is a Software Development Manager at Amazon based in Seattle, WA. With a background as a Software Development Engineer, she leads a team of engineers working on Amazon Customer Service technology. Outside of work, you’ll find Lindsey outside, whether it’s backpacking or boating in the summer, or snowboarding in the winter.</td> 
  </tr> 
 </tbody> 
</table> 
<p></p>
