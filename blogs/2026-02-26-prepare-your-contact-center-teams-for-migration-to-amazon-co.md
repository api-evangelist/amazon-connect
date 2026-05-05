---
title: "Prepare Your Contact Center Teams for Migration to Amazon Connect"
url: "https://aws.amazon.com/blogs/contact-center/prepare-your-contact-center-teams-for-migration-to-amazon-connect/"
date: "Thu, 26 Feb 2026 23:07:15 +0000"
author: "Parind Poi"
feed_url: "https://aws.amazon.com/blogs/contact-center/feed/"
---
<h3><strong>Introduction</strong></h3> 
<p>When organizations embark on a contact center transformation journey, technology gets much of the focus. At the same time, it’s the people who determine whether a migration succeeds or falls short. Your agents, supervisors, and support staff are the heartbeat of your contact center, and their readiness to embrace change is as critical as any technical deployment plan. As you prepare to migrate to <a href="https://aws.amazon.com/connect/">Amazon Connect</a>, investing in your team’s confidence, skills, and understanding of the new platform will lay the foundation for a smoother transition and a stronger customer experience on the other side. Amazon Connect is an omnichannel cloud contact center that transforms how teams work. AI analyzes conversations. Dashboards show what’s happening now. Infrastructure scales on demand. These capabilities deliver value when your people know how to use them.</p> 
<p>When you invest in people transformation, you achieve faster time-to-value and higher adoption rates. This post shows you how roles evolve and how to prepare your teams for success.</p> 
<h3><strong>Understanding Role Transitions</strong></h3> 
<p>Your team has questions. Agents wonder if their customer service skills still matter. Supervisors want to know if they’ll lose visibility into their teams. Developers worry about learning entirely new technologies. Infrastructure engineers question whether their expertise becomes obsolete.</p> 
<p>These concerns are valid. Contact center migration changes how people work every day. Team members who feel uncertain resist change. Key contributors who lack clarity disengage. Experienced staff who don’t see their value leave.</p> 
<p>When you address these questions early with clear role mapping and training paths, you build confidence and momentum.</p> 
<h3><strong>Operations Teams: Enhanced Tools and Intelligence</strong></h3> 
<p><strong>Agents</strong> toggle between multiple applications during a single customer interaction. Customer Relationship Management (CRM) for customer history. Ticketing system for case details. Knowledge base for responses. Separate tools for voice and chat. Amazon Connect changes this.</p> 
<p>One <a href="https://aws.amazon.com/connect/agent-workspace/">omnichannel Workspace</a> handles voice, chat, and tasks. Customer history, case details, and AI suggestions appear together. Step-by-step guidance walks agents through complex processes. While the application changes, customer service skills remain essential.</p> 
<p><strong>Supervisors</strong> monitor team performance and coach agents across all channels. Real-time visibility changes how they work. Metrics update continuously. Threshold alerts flag for service level changes. Amazon Connect <a href="https://docs.aws.amazon.com/connect/latest/adminguide/contact-lens.html">Contact Lens</a> analyzes conversations and surfaces coaching opportunities that supervisors would otherwise miss.</p> 
<p>Dashboard navigation and analytics configuration are new skills to develop. Leadership instincts, coaching acumen, and service level expertise remain the foundation.</p> 
<p><strong>Quality Analysts</strong> review samples of customer interactions across voice and chat today. Manual sampling implies reviewing a small percentage of interactions. Important patterns hide in the conversations they never hear.</p> 
<p>With Amazon Connect, they configure rules that analyze the conversations that matter most. Amazon Connect Contact Lens detects sentiment, identifies compliance risks, and supports automated evaluations across all channels. Learning Contact Lens and setting up automated evaluations are the new skills.</p> 
<p><strong>Workforce Managers</strong> forecast contact volume and build agent schedules. Amazon Connect provides native <a href="https://docs.aws.amazon.com/connect/latest/adminguide/forecasting-capacity-planning-scheduling.html">forecasting, capacity planning and scheduling</a> powered by machine learning. It analyzes your historical contact data and generates forecasts that update automatically. No data exports. No integrations. No manual data reconciliation.</p> 
<h3><strong>Infrastructure Teams: From Hardware to Cloud Operations</strong></h3> 
<p><strong>Telephony Engineers</strong> manage telco circuits, carrier relationships, and hardware capacity. With Amazon Connect, AWS manages carrier connections and redundancy on global infrastructure. Engineers focus on claiming and porting numbers, selecting number types (DID, toll-free, UIFN), and preparing documentation for international requirements. No circuits to manage. Single consolidated billing.</p> 
<p><strong>ACD Administrators</strong> own routing logic and system configuration. Amazon Connect provides a visual interface for configuring queues, routing profiles, and hours of operation. Changes deploy immediately. Version control tracks every update with rollback capability. Administrators configure queue priorities, manage routing profiles, and set up agent assignments. Learning the admin interface and configuration options comes next. Adapting to system-managed routing with prebuilt instructions and moving away from intraday manual changes needs some unlearning and relearning.</p> 
<p><strong>Network Specialists</strong> ensure connectivity, security, and performance. With Amazon Connect, the focus shifts to cloud connectivity. Specialists plan <a href="https://aws.amazon.com/directconnect/">AWS Direct Connect</a> or <a href="https://aws.amazon.com/vpn/">AWS VPN</a> for data center access, configure <a href="https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html">Amazon Virtual Private Cloud</a> (VPC) for Lambda integrations, and design transit gateway for multi-account setups. Network architecture principles guide these decisions. The new skills are AWS networking services.</p> 
<p><strong>Security and Compliance Leads</strong> protect customer data and meet regulatory requirements. Amazon Connect provides encryption at rest and in transit, <a href="https://aws.amazon.com/iam/">AWS IAM</a> for granular permissions, and <a href="https://aws.amazon.com/cloudtrail/">AWS CloudTrail</a> for audit logging. They define security policies, configure access controls, and generate compliance reports. Same mission, new tools. Learning AWS security services and policy-as-code comes next.</p> 
<p><strong>Help Desk Support</strong> resolves agent and system issues quickly. Amazon Connect provides centralized logging through <a href="https://aws.amazon.com/cloudwatch/">Amazon CloudWatch</a> and detailed contact flow logs. Support teams diagnose issues through log analysis and metrics dashboards. Troubleshooting instincts remain essential. The shift is to CloudWatch and flow log analysis.</p> 
<p><strong>Platform Operations Support</strong> provides production support and coordinates incident response. With Amazon Connect, this function evolves toward Site Reliability Engineering (SRE). CloudWatch provides metrics, alarms, and dashboards in one platform. Teams define service-level objectives, configure automated alerts, and build runbooks. Keeping systems running remains the core job. Learning SRE practices and CloudWatch comes next.</p> 
<h3><strong>Applications Teams: From Proprietary to Cloud-Native Development</strong></h3> 
<p>Legacy platforms require separate specialists for Interactive Voice Response (IVR) development, routing logic, and agent desktop customization, each with proprietary skill sets tied to specific vendors. Amazon Connect consolidates these into a unified cloud-native developer role focused on building seamless, end-to-end customer and agent experiences using standard web technologies and AWS services.</p> 
<p><strong>Customer Experience </strong>Developers design self-service journeys and conversational interfaces using natural language. Developers create and deploy <a href="https://aws.amazon.com/connect/ai-agents/">Connect AI agents</a> with controlled access to customer profiles, knowledge bases, and business systems. They build upon their understanding of user personas, messaging, experience design, and customer journeys. Learning to configure Connect AI agents, engineer prompts, and set up guardrails comes next.</p> 
<p><strong>Agent Desktop </strong>Developers build and customize agent-facing applications. Most organizations use the Amazon Connect agent workspace with its native features. Web development skills transfer. They learn to build guided <a href="https://docs.aws.amazon.com/connect/latest/adminguide/step-by-step-guided-experiences.html">step by step</a> workflows with dynamic UI panels that walk agents through decisions and actions during live contacts. For additional integrations, developers use the <a href="https://docs.aws.amazon.com/agentworkspace/latest/devguide/getting-started-install-sdk.html">Amazon Connect SDK</a> to extend the workspace. For deeper customization, the <a href="https://github.com/amazon-connect/amazon-connect-streams">Streams API</a> enables embedding the Contact Control Panel (CCP) or building fully custom agent interfaces.</p> 
<p><strong>Routing </strong>Developers build contact flow logic and dynamic routing rules. Amazon Connect provides a visual flow designer with drag-and-drop blocks and <a href="https://aws.amazon.com/lambda/">AWS Lambda</a> integration. Developers create contact flows and Lambda functions for real-time omnichannel routing decisions across voice, chat, email, and tasks . Logic design and problem-solving drive the work. The new skills are flow designer and Lambda patterns.</p> 
<p><strong>Analytics </strong>Developers turn interaction data into business insights using <a href="https://docs.aws.amazon.com/connect/latest/adminguide/data-lake.html">Amazon Connect data lake</a>. They build dashboards in <a href="https://aws.amazon.com/quick/quicksight/">Amazon Quick</a> and query data with <a href="https://aws.amazon.com/athena/">Amazon Athena</a>. Data modeling and visualization skills apply directly. The shift is to AWS analytics services.</p> 
<p><strong>DevOps </strong>Engineers manage deployment pipelines and environments. Amazon Connect supports infrastructure as code through <a href="https://aws.amazon.com/cloudformation/">AWS CloudFormation</a> and <a href="https://aws.amazon.com/cdk/">AWS Cloud Development Kit</a> (CDK). Engineers build CI/CD pipelines that deploy contact flows, Lambda functions, and Amazon Lex bots with version control and automated testing. Automation thinking remains the foundation. Learning AWS CloudFormation and CDK syntax comes next.</p> 
<h3><strong>Detailed Role Mapping with Training Paths</strong></h3> 
<p>Mapping roles is step one. Getting teams ready is step two. Here are the specific training paths.</p> 
<p><strong>Foundational Training (All Roles)</strong></p> 
<p>All team members should complete the <a href="https://skillbuilder.aws/learning-plan/1EJ6WNS6XY/amazon-connect-fundamentals--knowledge-badge-readiness-path/D7Z2GEDGEY">Amazon Connect Fundamentals Badge</a> and the <a href="https://skillbuilder.aws/learn/F3TUU2BTRD/amazon-connect-communications-specialist-assessment/VZK9NYXEQ4">Communications Specialist Assessment</a> as a baseline. Access all badge training at <a href="https://skillbuilder.aws/search?searchText=amazon%20connect%20badge">AWS Skill Builder</a>. The Training column in the following tables lists additional courses available on <a href="https://skillbuilder.aws/">AWS Skill Builder</a> to build role-specific skills.</p> 
<p><strong>Operations Team </strong></p> 
<p>Agents should complete <a href="https://skillbuilder.aws/learn/3H4HKJ1D7M/amazon-connect-agent-applications-fundamentals/27Y6GMR9MV">Agent Applications Fundamentals</a> to understand how to navigate the agent workspace and handle omnichannel customer interactions.</p> 
<p>Operations leaders should complete <a href="https://skillbuilder.aws/learning-plan/8P99XA72ZK/amazon-connect-reporting--analytics--knowledge-badge-readiness-path/KGFNQVYY37">Reporting &amp; Analytics Badge</a> to monitor contact center performance with dashboards, metrics, and data-driven insights. The following table covers additional role specific training for operations team leaders.</p> 
<table bgcolor="#dde0df" border="0"> 
 <tbody> 
  <tr align="center" bgcolor="#dde0df"> 
   <td><strong>Legacy Role</strong></td> 
   <td><strong>Amazon Connect Role</strong></td> 
   <td><strong>Training</strong></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>Supervisor</td> 
   <td>Supervisor</td> 
   <td><a href="https://skillbuilder.aws/learn/QD3NY9MG19/amazon-connect-operations/5RV776AM3X">Operations</a>, <a href="https://skillbuilder.aws/learn/HQT989RN4Q/amazon-connect-agent-performance-evaluations/S7XRZT99B7">Agent Performance Evaluations</a>, <a href="https://skillbuilder.aws/learn/SQD71CTJ93/amazon-connect-ai-supervisor-capabilities/YQG983QNCT">AI Supervisor Capabilities</a></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>QA Analyst</td> 
   <td>QA Analyst</td> 
   <td><a href="https://skillbuilder.aws/learn/HQT989RN4Q/amazon-connect-agent-performance-evaluations/S7XRZT99B7">Agent Performance Evaluations</a>, <a href="https://skillbuilder.aws/learn/UNYS5GBG1S/amazon-connect-conversational-analytics-essentials/UV2ADB8A7S">Conversational Analytics</a></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>Workforce Manager</td> 
   <td>Workforce Manager</td> 
   <td><a href="https://skillbuilder.aws/learn/DZEETEHBSW/amazon-connect-ai-workforce-optimization/BHKCYW6AS8">AI Workforce Optimization</a></td> 
  </tr> 
 </tbody> 
</table> 
<p><strong>Infrastructure Team</strong></p> 
<table bgcolor="#dde0df" border="0"> 
 <tbody> 
  <tr align="center" bgcolor="#dde0df"> 
   <td><strong>Legacy Role</strong></td> 
   <td><strong>Amazon Connect Role</strong></td> 
   <td><strong>AWS Certification</strong></td> 
   <td><strong>Amazon Connect Badge</strong></td> 
   <td><strong>Training</strong></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>Telephony Engineer</td> 
   <td>Cloud Contact Center Architect</td> 
   <td><a href="https://aws.amazon.com/certification/certified-solutions-architect-associate/">Solutions Architect</a></td> 
   <td><a href="https://skillbuilder.aws/learning-plan/6YW2QYUBKS/amazon-connect-developer-learning--badge-plan/NEWQZB4HAQ">Developer</a></td> 
   <td><a href="https://skillbuilder.aws/learn/EBZVGES8XB/amazon-connect-foundations/DENMS3UWD8">Foundations</a>, <a href="https://skillbuilder.aws/learn/TJD69CUE97/amazon-connect-voice-intermediate/GV3M4DU54Y">Voice</a></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>ACD Administrator</td> 
   <td>Administrator</td> 
   <td><a href="https://aws.amazon.com/certification/certified-cloud-practitioner/">Cloud Practitioner</a></td> 
   <td><a href="https://skillbuilder.aws/learning-plan/6YW2QYUBKS/amazon-connect-developer-learning--badge-plan/NEWQZB4HAQ">Developer</a></td> 
   <td><a href="https://skillbuilder.aws/learn/K8JX1GK6CE/amazon-connect-flows-fundamentals/JN9CJHF551">Flows Fundamentals</a>, <a href="https://skillbuilder.aws/learn/EXACSYQJXC/amazon-connect-optimizing-routing-solutions/KD7MM9WPKB">Optimizing Routing</a></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>Network Specialist</td> 
   <td>Cloud Network Engineer</td> 
   <td><a href="https://aws.amazon.com/certification/certified-advanced-networking-specialty/">Advanced Networking</a></td> 
   <td>–</td> 
   <td><a href="https://skillbuilder.aws/learn/EBZVGES8XB/amazon-connect-foundations/DENMS3UWD8">Foundations</a>, <a href="https://skillbuilder.aws/learn/TJD69CUE97/amazon-connect-voice-intermediate/GV3M4DU54Y">Voice</a></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>Security and Compliance Lead</td> 
   <td>Cloud Security Architect</td> 
   <td><a href="https://aws.amazon.com/certification/certified-security-specialty/">Security Specialty</a></td> 
   <td>–</td> 
   <td><a href="https://explore.skillbuilder.aws/learn/course/external/view/elearning/19002/amazon-connect-instance-fundamentals">Instance Fundamentals</a></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>Help Desk Support</td> 
   <td>Cloud Operations Support</td> 
   <td><a href="https://aws.amazon.com/certification/certified-cloud-practitioner/">Cloud Practitioner</a></td> 
   <td>–</td> 
   <td><a href="https://explore.skillbuilder.aws/learn/course/external/view/elearning/424/amazon-connect-troubleshooting-with-amazon-cloudwatch">Troubleshooting with CloudWatch</a></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>Platform Operations</td> 
   <td>Site Reliability Engineer</td> 
   <td><a href="https://aws.amazon.com/certification/certified-solutions-architect-associate/">Solutions Architect</a></td> 
   <td><a href="https://skillbuilder.aws/learning-plan/8P99XA72ZK/amazon-connect-reporting--analytics--knowledge-badge-readiness-path/KGFNQVYY37">Reporting &amp; Analytics</a></td> 
   <td><a href="https://explore.skillbuilder.aws/learn/course/external/view/elearning/424/amazon-connect-troubleshooting-with-amazon-cloudwatch">Troubleshooting with CloudWatch</a></td> 
  </tr> 
 </tbody> 
</table> 
<p><strong>Applications Team</strong></p> 
<table bgcolor="#dde0df" border="0"> 
 <tbody> 
  <tr align="center" bgcolor="#dde0df"> 
   <td><strong>Legacy Role</strong></td> 
   <td><strong>Amazon Connect Role</strong></td> 
   <td><strong>AWS Certification</strong></td> 
   <td><strong>Amazon Connect Badge</strong></td> 
   <td><strong>Training</strong></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>Customer Experience Developer</td> 
   <td>Serverless Developer</td> 
   <td><a href="https://aws.amazon.com/certification/certified-developer-associate/">Developer Associate</a></td> 
   <td><a href="https://skillbuilder.aws/learning-plan/C75KRNZ9N7/amazon-connect-ai-fundamentals--knowledge-badge-readiness-path/D56C11BKKD">AI Fundamentals</a></td> 
   <td><a href="https://skillbuilder.aws/learn/U1FFNCZ2HE/amazon-connect-conversational-interfaces-fundamentals/6F38AWECGY">Conversational Interfaces</a>, <a href="https://skillbuilder.aws/learn/P997VWCMGQ/amazon-connect-ai-agent-capabilities/9YMJBMPGK1">AI Agents</a>, <a href="https://explore.skillbuilder.aws/learn/course/external/view/elearning/14504/amazon-connect-implementing-chat-in-connect">Chat</a></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>Agent Desktop Developer</td> 
   <td>Full-Stack Cloud Developer</td> 
   <td><a href="https://aws.amazon.com/certification/certified-developer-associate/">Developer Associate</a></td> 
   <td><a href="https://skillbuilder.aws/learning-plan/6YW2QYUBKS/amazon-connect-developer-learning--badge-plan/NEWQZB4HAQ">Developer</a></td> 
   <td><a href="https://explore.skillbuilder.aws/learn/course/external/view/elearning/20582/amazon-connect-custom-contact-control-panel-fundamentals">Custom CCP Fundamentals</a></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>Routing Developer</td> 
   <td>Cloud-Native Engineer</td> 
   <td><a href="https://aws.amazon.com/certification/certified-developer-associate/">Developer Associate</a></td> 
   <td><a href="https://skillbuilder.aws/learning-plan/6YW2QYUBKS/amazon-connect-developer-learning--badge-plan/NEWQZB4HAQ">Developer</a></td> 
   <td><a href="https://skillbuilder.aws/learn/K8JX1GK6CE/amazon-connect-flows-fundamentals/JN9CJHF551">Flows Fundamentals</a>, <a href="https://skillbuilder.aws/learn/CWEG5J84E5/amazon-connect-apis-intermediate/YUVW8UK33B">Integrations &amp; API operations</a></td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>Analytics Developer</td> 
   <td>Cloud Analytics Engineer</td> 
   <td><a href="https://aws.amazon.com/certification/certified-data-engineer-associate/">Data Engineer</a> (optional)</td> 
   <td><a href="https://skillbuilder.aws/learning-plan/8P99XA72ZK/amazon-connect-reporting--analytics--knowledge-badge-readiness-path/KGFNQVYY37">Reporting &amp; Analytics</a></td> 
   <td>–</td> 
  </tr> 
  <tr align="center" bgcolor="#ffffff"> 
   <td>DevOps Engineer</td> 
   <td>DevOps Engineer</td> 
   <td><a href="https://aws.amazon.com/certification/certified-devops-engineer-professional/">DevOps Professional</a></td> 
   <td><a href="https://skillbuilder.aws/learning-plan/6YW2QYUBKS/amazon-connect-developer-learning--badge-plan/NEWQZB4HAQ">Developer</a></td> 
   <td><a href="https://skillbuilder.aws/learn/4B7F8FF3UW/amazon-connect--infrastructure-as-code-fundamentals/T8HT6F22JX">Infrastructure as Code</a></td> 
  </tr> 
 </tbody> 
</table> 
<h3><strong>Getting There: Training and Organizational Strategies</strong></h3> 
<p>Role transitions and training paths set the direction. Execution determines success.</p> 
<p><strong>Assess First</strong>: Leverage your existing organizational change management teams. Understand each team’s starting point, current skills, cloud experience, and comfort with change. This shapes training intensity and timeline.</p> 
<p><strong>Professional Support</strong>: Consider seeking help from AWS Professional Services or a certified Amazon Connect partner if you are new to organizational change management and cloud migrations. The experts can provide train-the-trainer programs for business roles (agents, supervisors, quality analysts, workforce managers). Internal trainers learn first, then deliver customized training using proven content. Infrastructure and application development teams can work side by side with these experts for on-the-job upskilling on Amazon Connect and AWS best practices through hands-on workshops and architecture reviews.</p> 
<p><strong>Train Smart</strong>: Use train-the-trainer for high-volume roles. Select strong performers to learn first, then train their peers close to go-live when knowledge retention is highest.</p> 
<p><strong>Roll Out in Phases</strong>: Start with a pilot group. Validate the approach, identify gaps, and build internal champions. Expand to early adopters with pilot participants as mentors. Then complete the rollout with proven processes.</p> 
<p><strong>Build Support Networks</strong>: Create a superuser program from early adopters who want to help others succeed. Establish tiered support with peers helping first, then helpdesk and SRE handling technical issues, and finally AWS Support addressing platform questions.</p> 
<p><strong>Communicate the “Why”</strong>: Open feedback channels. Coach individuals who need extra support. Focus on growth opportunities in addition to new requirements.</p> 
<h3><strong>Measuring Success</strong></h3> 
<p>With training complete and support structures in place, measure success using specific indicators from day one.</p> 
<p><strong>Cutover Support</strong>: Plan support during the first week. Floor walkers who respond to questions in real time make a difference. Reduce support as confidence builds.</p> 
<p><strong>Week 1 Indicators</strong>: Most team members handle core tasks independently. Supervisors actively use dashboards. Watch for patterns that signal training gaps.</p> 
<p><strong>Month 1 Indicators</strong>: Productivity returns to baseline. Coaching frequency increases. Technical teams resolve routine issues without escalation.</p> 
<p><strong>Month 3 Indicators</strong>: Look for optimization signs: teams finding new ways to use capabilities, quality coverage expanding, operations building automation.</p> 
<h3><strong>Conclusion</strong></h3> 
<p>Your investment in people transformation pays off through faster adoption, higher productivity, and better customer outcomes. When you prioritize people alongside technology, you unlock the full value of your transformation.</p> 
<p>With Amazon Connect, you pay for what you use. There are no upfront payments, long-term commitments, or minimum monthly fees. Should you need help with setting this up, you can get assistance from <a href="https://aws.amazon.com/professional-services/">AWS Professional Services</a> and use proven offerings like <a href="https://aws.amazon.com/marketplace/pp/prodview-len66pa5fg6x4">AI Powered Contact Centers</a> in AWS Marketplace. You can also seek assistance from <a href="https://aws.amazon.com/connect/partners/">Amazon Connect partners</a> available worldwide.</p> 
<p>Ready to transform your customer service experience with Amazon Connect? <a href="https://aws.amazon.com/contact-us/">Contact us</a>.</p> 
<h3><strong>Meet the authors</strong></h3> 
<table> 
 <tbody> 
  <tr> 
   <td><a href="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2024/07/10/parinpo.jpg"><img alt="" class="alignleft size-thumbnail wp-image-11312" height="150" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2024/07/10/parinpo-150x150.jpg" width="150" /></a></td> 
   <td>Parind Poi is a Senior Practice Leader at AWS Professional Services. He leads a specialized practice with deep expertise in customer experience (CX) on AWS. Parind is passionate about helping customers modernize their customer engagement workloads on cloud.</td> 
  </tr> 
  <tr> 
   <td><img alt="" class="alignnone wp-image-8826" height="100" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2023/03/02/2023-03-02_05-15-36.jpg" width="100" /></td> 
   <td>Prashant Desai is a Principal Consultant at AWS Professional Services, specializing in contact center migrations to the cloud. Prashant brings expertise across legacy and cloud platforms, focusing on innovative ways to modernize customer workloads and simplify the customer experience.</td> 
  </tr> 
 </tbody> 
</table> 
<p></p>
