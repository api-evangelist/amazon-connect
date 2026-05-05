---
title: "Build Unified Voice, Video and Chat Communications with Amazon Connect"
url: "https://aws.amazon.com/blogs/contact-center/build-unified-voice-video-and-chat-communications-with-amazon-connect/"
date: "Thu, 26 Mar 2026 19:39:23 +0000"
author: "Ying Qian"
feed_url: "https://aws.amazon.com/blogs/contact-center/feed/"
---
<h1>1. Introduction</h1> 
<p>Amazon Connect supports voice/video and chat as separate channels, each with its own APIs. Using native or custom widgets, these channels operate independently. This works for most contact center scenarios.</p> 
<p>But what happens when a customer and an agent need more than just talking and seeing each other?</p> 
<p>For example, a customer calls to finalize a loan application. The agent confirms pre-approval. But the customer must review and sign a document, and the mailed copy hasn’t arrived. The agent could ask the customer to hang up, wait for the mail, or start a separate chat. That means multiple interactions, different agents, and potentially days of delay.</p> 
<p>What if the agent could send the document while staying on the call? The customer signs and returns it—same agent, same engagement, minutes not days.</p> 
<p>That’s what this post covers. We walk through a solution that unifies voice/video and chat into one seamless customer experience.</p> 
<h2>1.1. Why Amazon Connect makes this possible</h2> 
<p>The core challenge is simple: how does a customer text and share files with an agent during a live call?</p> 
<p>Amazon Connect provides the necessary APIs and tools. The StartWebRTCContact API initiates voice and video calls. The DescribeContact API exposes the agent ID once an agent answers. Contact flows support attributes for routing logic that targets a specific agent. The Chat Widget accepts contact attributes at initialization, so your application can pass the agent ID when the chat starts.</p> 
<p>None of these capabilities are new. What’s new is how we wire them together. A custom UI extracts the agent ID from an active call and feeds it into the chat routing logic. The customer remains connected to the same agent throughout the chat—no need to disconnect or wait in a separate queue.</p> 
<h2>1.2. Business valu<span style="font-size: 16px;">e</span></h2> 
<p>Unifying channels within a single customer-agent engagement delivers measurable impact.</p> 
<p>For customers: No callbacks, no transfers, no waiting in another queue. The loan customer walks away with an approved application in minutes, not days.</p> 
<p>For operations: The agent handles the complete customer journey end to end. No duplicate work, no handoff friction, no follow-up tasks consuming agent capacity.</p> 
<p>For compliance: Every voice and chat exchange is tied to one agent, one customer, and one case. In regulated industries, this linkage of contact records across channels simplifies auditing.</p> 
<h1>2. Solution architecture</h1> 
<p>The solution connects a custom frontend to AWS services across three layers: hosting and delivery, authentication and authorization, and real-time communication.</p> 
<h1><img alt="Unified Voice, Video, and Chat Communications" class="alignnone wp-image-14520 size-large" height="572" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/03/24/wholeSolution-1024x572.png" style="font-size: 16px;" width="1024" /></h1> 
<h2>2.1. Overview</h2> 
<p>The following steps correspond to the numbered labels in Figure 1.</p> 
<p>Step 1 — Authentication. The customer logs into the user interface. The frontend sends their credentials to an <a href="https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html">Amazon Cognito user pool</a>, which validates them and returns an ID token.</p> 
<p>Step 2 — Authorization. The frontend passes the ID token to an <a href="https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html">Amazon Cognito identity pool</a>, which calls <a href="https://docs.aws.amazon.com/STS/latest/APIReference/welcome.html">AWS STS</a> AssumeRoleWithWebIdentity. An IAM role grants least-privilege Amazon Connect permissions, and temporary credentials flow back to the frontend. This is an important design choice. The frontend never holds long-lived secrets. Every credential is scoped and short-lived.</p> 
<p>Step 3 — Voice and video call. The customer starts a call. The frontend uses the temporary credentials to invoke the <a href="https://docs.aws.amazon.com/connect/latest/APIReference/API_StartWebRTCContact.html">StartWebRTCContact</a> API, which triggers the WebRTCQueueRouting contact flow. This flow distributes the call to an available agent and returns the <a href="https://github.com/aws/amazon-chime-sdk-js">Amazon Chime SDK</a> meeting configuration. The frontend initializes the Chime SDK session and manages the real-time audio and video streams. Meanwhile, the frontend calls the <a href="https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeContact.html">DescribeContact</a> API to retrieve the agent ID from the active contact and stores it locally.</p> 
<p>Step 4 — Chat with the same agent. When the customer opens the chat, the frontend passes the stored agent ID to the <a href="https://docs.aws.amazon.com/connect/latest/adminguide/add-chat-to-website.html">Amazon Connect Chat Widget</a>, which loads from the Amazon Connect hosted endpoint. The chat contact triggers the ChatAgentRouting contact flow, which uses the agent ID to route directly to the same agent already on the call. This is the step that ties everything together: voice/video and chat converge on a single agent. When the engagement ends, the frontend calls the <a href="https://docs.aws.amazon.com/connect/latest/APIReference/API_StopContact.html">StopContact</a> and <a href="https://docs.aws.amazon.com/connect/latest/APIReference/API_connect-participant_DisconnectParticipant.html">DisconnectParticipant</a> APIs for clean session termination.</p> 
<h2>2.2. Frontend components</h2> 
<p>Five components make up the user interface, each with a distinct responsibility.</p> 
<p><img alt="" class="alignnone wp-image-14522 size-large" height="633" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/03/24/frontend-1024x633.png" width="1024" /></p> 
<p>The <strong>Authentication State Manager</strong> handles login through the Cognito user pool flow and produces the ID token.</p> 
<p>The <strong>Credential Manager</strong> exchanges that token for temporary AWS credentials scoped to Amazon Connect APIs.</p> 
<p>The <strong>Session Manager</strong> coordinates everything. It stores encrypted session context in local storage, drives call initiation, and captures the agent ID so that the Chat Widget knows where to route.</p> 
<p>The <strong>WebRTC Manager</strong> owns real-time media: calling StartWebRTCContact, initializing the Chime SDK session, and managing audio/video streams.</p> 
<p>The <strong>Chat Widget</strong> loads from the Amazon Connect hosted endpoint. It receives the agent ID from the Session Manager and routes the chat to the same agent. It handles the full chat lifecycle: contact creation, WebSocket connections, messaging, and file attachments.</p> 
<h2>2.3. Backend services</h2> 
<p>Three layers of AWS services power the backend.</p> 
<p><img alt="" class="alignnone wp-image-14523 size-large" height="580" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/03/24/backend-1024x580.png" width="1024" /></p> 
<p><strong>Hosting and Delivery:</strong> Amazon CloudFront serves the UI globally with security headers and caching. Amazon S3 stores static assets.</p> 
<p><strong>Authentication and Authorization:</strong> Amazon Cognito user pool, Amazon Cognito identity pool, AWS STS, and IAM chain together. The frontend gets exactly the permissions it needs — nothing more.</p> 
<p><strong>Communication:</strong> This is where real-time engagement happens. The StartWebRTCContact API triggers the WebRTCQueueRouting flow to assign an agent. The API returns the Amazon Chime SDK configuration, which the frontend uses to establish real-time audio and video. The DescribeContact API extracts the agent ID. The ChatAgentRouting flow routes chat to that same agent. The StopContact and DisconnectParticipant APIs clean up the session.</p> 
<h1>3. Prerequisites</h1> 
<p>Before deploying, make sure you have:</p> 
<ul> 
 <li>An <a href="https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/">AWS account</a></li> 
 <li>An <a href="https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-instances.html">Amazon Connect instance</a> with&nbsp;<a href="https://docs.aws.amazon.com/connect/latest/adminguide/enable-attachments.html">file attachments enabled</a></li> 
 <li><a href="https://docs.aws.amazon.com/cdk/v2/guide/home.html">AWS CDK</a> v2 installed and configured</li> 
 <li><a href="https://nodejs.org/">Node.js</a> v20.x or later</li> 
 <li><a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html">AWS CLI</a> configured with appropriate permissions</li> 
</ul> 
<h1>4. Deploy the solution and clean up</h1> 
<p>The complete solution is packaged as an AWS CDK application in the <a href="https://github.com/aws-samples/sample-voice-video-chat-amazon-connect">GitHub repository</a>. The stack provisions everything: CloudFront, S3, Cognito, IAM roles, and Amazon Connect contact flows.</p> 
<p>The README walks through each step: clone the repo, install dependencies, configure your Connect instance, deploy the stack, create a test user, and verify the unified experience.</p> 
<p>Follow along with the step-by-step deployment walkthrough. When you’re done testing, make sure to tear down all resources to avoid unnecessary charges.<br /> </p> 
<h1>5. Conclusion and next steps</h1> 
<p>We showed how to unify voice/video and chat with one Amazon Connect agent in a single customer-agent engagement. The solution wires together existing capabilities: StartWebRTCContact and DescribeContact APIs, contact flow routing, Amazon Chime SDK, the standard chat widget, and short-lived AWS credentials through Amazon Cognito and AWS STS.</p> 
<p>Keep in mind, this is one approach. You can also build a custom voice/video and chat widget from scratch for full flexibility. The Amazon Connect APIs, such as <a href="https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html">StartChatContact</a> to initiate chat, <a href="https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_CreateParticipantConnection.html">CreateParticipantConnection</a> to establish the WebSocket connection, <a href="https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_SendMessage.html">SendMessage</a> for messaging, and <a href="https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_StartAttachmentUpload.html">StartAttachmentUpload</a> and <a href="https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_CompleteAttachmentUpload.html">CompleteAttachmentUpload</a> for file sharing, give you granular control over every interaction, but at the cost of added implementation complexity. Where possible, leverage Amazon Connect built-in capabilities first and customize only where you need to.</p> 
<p>Now it’s your turn. Start by identifying where customers need multiple touchpoints to complete a task, such as document signing, visual troubleshooting, or form submission. Deploy the solution from the <a href="https://github.com/aws-samples/sample-voice-video-chat-amazon-connect">GitHub repository</a>, walk through the solution yourself, and see it in action. Then pilot with one team and one use case. Measure handle time, first-contact resolution, and customer effort before and after. Use that data to evaluate whether the solution fits your customer service operations.</p> 
<h1>6. Related materials</h1> 
<ul> 
 <li><a href="https://github.com/aws-samples/sample-voice-video-chat-amazon-connect">Solution GitHub repository</a></li> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/adminguide/inapp-calling.html">Amazon Connect Administrator Guide: Set up in-app, web, video calling, and screen sharing capabilities</a></li> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/APIReference/API_StartWebRTCContact.html">Amazon Connect StartWebRTCContact API</a></li> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeContact.html">Amazon Connect DescribeContact API</a></li> 
 <li><a href="https://github.com/aws/amazon-chime-sdk-js">Amazon Chime SDK for JavaScript</a></li> 
 <li><a href="https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html">Amazon Connect Cognito Developer Guide</a></li> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/adminguide/add-chat-to-website.html">Amazon Connect Administrator Guide: Add a chat user interface to your website</a></li> 
</ul> 
<h1>About the authors</h1> 
<table style="width: 100%;"> 
 <tbody> 
  <tr> 
   <td style="text-align: left; vertical-align: top;"><img alt="Ying Qian" class="alignleft wp-image-14045 size-large" height="1024" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2025/11/23/YingPass_KontrastPlus-scaled-e1763917558365-800x1024.jpg" width="800" /></td> 
   <td style="text-align: left; vertical-align: top;"><strong>Ying Qian</strong> brings over 19 years of contact center technology experience, having held roles spanning Solutions Architect, Technical Project Manager, ICT Lead Engineer, and Operations Engineer. At AWS, she works as the service-aligned Solutions Architect, leading the Amazon Connect Telephony &amp; Resiliency SME team, and helping customers unlock business value by guiding Amazon Connect implementations aligned with AWS Well-Architected Framework principles. Outside of work, she enjoys jogging, hiking the Alps with her family, and swimming in Lake Constance.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td></td> 
  </tr> 
  <tr> 
   <td></td> 
   <td></td> 
  </tr> 
  <tr> 
   <td style="text-align: left; vertical-align: top;"><img alt="Nelson Martinez" class="alignleft wp-image-14045 size-large" height="1024" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2023/03/28/Nelson-Photo-small.png" width="800" /></td> 
   <td style="text-align: left; vertical-align: top;"><strong>Nelson Martinez</strong> is an Applied AI Senior Solutions Architect based in Sydney, with over 31 years of experience spanning Contact Centre, Unified Communications, IP Telephony, and Networking across Australia and the United States. Over the past five years at AWS, he has specialized in Cloud Contact Centre and Applied AI solutions, working directly with customers to deliver industry-leading implementations at a global scale.</td> 
  </tr> 
 </tbody> 
</table> 
<p>&nbsp;</p>
