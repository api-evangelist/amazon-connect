---
title: "How NatWest Simplified Contact Center Analytics with Amazon Connect analytics data lake"
url: "https://aws.amazon.com/blogs/contact-center/how-natwest-simplified-contact-center-analytics-with-amazon-connect-analytics-data-lake/"
date: "Wed, 07 Jan 2026 15:33:14 +0000"
author: "Prabhakar Rajasekar"
feed_url: "https://aws.amazon.com/blogs/contact-center/feed/"
---
<h2>Introduction</h2> 
<p>As one of the UK’s leading financial institutions, <a href="https://www.natwestgroup.com/">NatWest Group</a> delivers a wide range of banking services across retail, commercial, and private banking sectors. The bank enhanced its customer service capabilities in 2019 by deploying Amazon Connect across its contact centers. This implementation provided NatWest with comprehensive analytics and detailed insights into customer interactions. To further understand <a href="https://www.youtube.com/watch?v=zbrLI6ktTcg&amp;t=1952s">customer sentiments</a> and gather valuable insights, NatWest utilized <a href="https://aws.amazon.com/connect/conversational-analytics/">Amazon Connect Conversational Analytics</a> to analyze their complete call volume, while also <a href="https://aws.amazon.com/blogs/contact-center/insights-and-learning-of-amazon-q-in-connect-at-natwest/">testing the Amazon Connect AI agents.</a> Additionally, the bank implemented a <a href="https://aws.amazon.com/blogs/contact-center/implementation-of-devsecops-ecosystem-for-amazon-connect-at-natwest/">DevSecOps Ecosystem</a> to accelerate the deployment of their innovative solutions.</p> 
<p>Initially, NatWest used custom ETL pipelines to process this data for analysis. While this method worked, it required significant maintenance and regular updates to meet business needs.</p> 
<p>In 2024, they adopted <a href="https://docs.aws.amazon.com/connect/latest/adminguide/data-lake.html">Amazon Connect data lake</a> with Zero ETL architecture, simplifying data access and analysis. This solution reduced complexity in data management and improved the speed of generating insights for customer service operations. This blog explores NatWest’s transition to Amazon Connect data lake and shows how this technology helps deliver better customer service.</p> 
<h2>Complex ETL operations</h2> 
<p>Prior to implementing the Amazon Connect data lake solution, NatWest faced significant challenges in data management. The organization struggled with complex data ingestion from Amazon Connect, involving diverse data types and sources such as Contact Records, conversation analytics, and agent performance metrics across multiple database systems. Manual Extract, Transform, Load (ETL) processes were required to standardize and prepare data for structured database storage. These efforts resulted in resource-intensive infrastructure that demanded continuous updates and modifications to accommodate evolving data formats and shifting organizational needs, ultimately leading to increased operational complexity and higher maintenance expenses.</p> 
<p><img alt="" class="alignnone wp-image-14278 size-full" height="428" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/06/Screenshot-2026-01-06-at-12.33.58.png" width="1108" /></p> 
<h3>Key metrics</h3> 
<p>To enhance Interactive Voice Response (IVR) performance and elevate customer experience, NatWest implemented a comprehensive monitoring approach that captured key performance indicators. The organization meticulously tracked an extensive range of call-related metrics, encompassing detailed volumes across multiple categories including total calls, handled interactions, incoming and outgoing communications, callback scenarios, and additional granular classifications. By leveraging advanced analytics tools like conversational analytics through Contact Lens, NatWest gained deep insights into customer interactions. The organization’s robust tracking strategy also included detailed contact statistics, precise containment rate measurements, and comprehensive agent performance metrics, enabling data-driven decision-making and continuous service improvement.</p> 
<h2>The solution: Amazon Connect Analytics data lake</h2> 
<h3>Zero-ETL approach</h3> 
<p>To overcome the constraints of traditional data processing methods, NatWest implemented the Amazon Connect data lake—an innovative and simplified solution designed to streamline data ingestion and analysis by eliminating manual transformation complexities. This strategic approach unlocked several key capabilities:</p> 
<ul> 
 <li>Optimized data structuring: Amazon Connect data is now stored in a readily analyzable format, enabling immediate and direct insights extraction.</li> 
 <li>Rapid data accessibility: Customer interaction data becomes available within an hour of call completion, empowering teams with timely, actionable information.</li> 
 <li>Flexible dataset management: The data lake facilitates efficient dataset updates, simplifying data maintenance while acknowledging current limitations in large-scale query performance.</li> 
 <li>Intelligent insight generation: Pre-processed metrics like sentiment analysis and call outcomes are instantly accessible, dramatically reducing time-to-intelligence.</li> 
 <li>Selective data integration: While most datasets are seamlessly integrated, Contact Flow Logs continue to leverage traditional processing methods to ensure comprehensive IVR journey analysis.</li> 
 <li>Strategic infrastructure evolution: Dedicated Terraform pipelines were established to create a clear demarcation between legacy systems and the new data architecture, enabling independent infrastructure modifications.</li> 
 <li>Out of Box Partitioning: Close collaboration with AWS during NatWest’s data lake adoption aligned with the rollout of partitioning capabilities on the AWS Data Lake platform, supporting the delivery of faster, more efficient, and scalable data solutions.</li> 
</ul> 
<p><img alt="" class="alignnone wp-image-14285 size-full" height="329" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/06/Screenshot-2026-01-06-at-12.45.00.png" width="633" /></p> 
<p>This architecture not only simplifies complex data operations but fundamentally reshaped NatWest’s data management and analytical capabilities, driving organizational agility and insights-driven decision-making.</p> 
<h3>Key benefits</h3> 
<ul> 
 <li>Streamlined data management: By removing complex ETL processes, NatWest significantly minimized operational complexities and administrative burden.</li> 
 <li>Accelerated operational intelligence: The new architecture enables rapid insights generation, empowering teams to make data-driven decisions with unprecedented speed and transforming customer service responsiveness.</li> 
 <li>Flexible architectural framework: The data lake solution provides a robust, adaptable infrastructure that seamlessly accommodates future technological expansions, emerging data sources, and evolving business requirements.</li> 
 <li>Improved Accuracy &amp; Reduced Manual Effort: Key datapoints will be readily available out of the box, eliminating the need for manual derivation and reducing the risk of human error. Additionally, any future updates to the underlying data will be automatically absorbed by Amazon Connect Analytics data lake, requiring no changes or maintenance from NatWest.</li> 
</ul> 
<h3>Use cases</h3> 
<h4>IVR performance dashboard (X-Ray dashboards):</h4> 
<p>NatWest developed a comprehensive IVR performance dashboard designed to offer deep, actionable insights into customer interaction dynamics. The dashboard delivers sophisticated analytics across multiple critical dimensions:</p> 
<ul> 
 <li>Containment efficiency tracking: A sophisticated metric that quantifies the IVR’s capability to resolve customer queries autonomously without requiring agent intervention.</li> 
 <li>Agent transition analysis: A detailed examination of call flow patterns, systematically identifying the precise triggers and circumstances causing customer interactions to escalate from automated systems to live agent support.</li> 
 <li>Call abandonment diagnostics: A robust mechanism for monitoring and investigating call drop-off rates, enabling proactive identification of potential friction points in the customer journey.</li> 
 <li>Failure mode categorization: A structured approach to documenting and visualizing IVR interaction breakdowns, providing clear insights into systemic challenges and improvement opportunities.</li> 
 <li>Call intent classification: Customer call intents are classified at a granular level and linked to the broader motivations and communication goals behind each interaction. i.e., The intents are contextualized within key banking journeys—such as account servicing, payments, or fraud resolution etc., thereby offering a holistic view of customer behavior and enabling more targeted experience improvements.</li> 
 <li>Granular data exploration: Access to comprehensive call interaction raw-data (call identifiers), facilitating deep-dive analytical investigations and supporting advanced performance optimization strategies.</li> 
</ul> 
<p><strong>Disclaimer:</strong> The screenshots shown is from a sandbox Proof of Concept (PoC) environment. It is intended solely for illustrative and indicative purposes and should not be considered a live or production representation.</p> 
<p><img alt="" class="alignnone wp-image-14276 size-full" height="808" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/06/image003.png" width="1535" /></p> 
<h3><img alt="" class="alignnone wp-image-14280 size-full" height="625" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/06/NLCS2.png" width="1536" /></h3> 
<h3>Conversation insights:</h3> 
<p>NatWest developed an advanced conversation quality analytics dashboard designed to provide a comprehensive, multi-dimensional view of customer-agent interactions. The dashboard offers sophisticated insights into communication dynamics:</p> 
<ul> 
 <li>Interaction temporal analysis: A precise measurement of total conversation duration, revealing the efficiency and depth of customer service engagements.</li> 
 <li>Conversational rhythm evaluation: An intricate assessment of speech patterns, tracking the pace, cadence, and natural flow of dialogue between agents and customers.</li> 
 <li>Silence interval mapping: Strategic identification and visualization of non-verbal periods during interactions, highlighting potential communication gaps or moments of deliberation.</li> 
 <li>Dialogue interruption monitoring: A detailed tracking mechanism that captures instances of speech overlap, agent interventions, and communication disruptions, providing insights into conversational dynamics.</li> 
 <li>Emotional intelligence tracking: An advanced sentiment analysis framework that transforms raw communication data into nuanced emotional insights, correlating customer satisfaction levels with conversational characteristics such as pace and interaction patterns.</li> 
</ul> 
<p>This innovative dashboard transforms raw communication data into actionable intelligence, enabling NatWest to continuously refine and optimize customer service strategies.</p> 
<p><strong>Disclaimer:</strong> The screenshots shown is from a sandbox Proof of Concept (PoC) environment. It is intended solely for illustrative and indicative purposes and should not be considered a live or production representation.</p> 
<p><img alt="" class="alignnone wp-image-14281 size-full" height="822" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/06/CA1Analytics.png" width="1286" /></p> 
<p><img alt="" class="alignnone wp-image-14282 size-full" height="874" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/06/CA2Analytics.png" width="1092" /></p> 
<h2>Results and impact</h2> 
<h3>Operational Improvements</h3> 
<p>NatWest’s innovative data strategy revolutionized its operational approach by dramatically accelerating insight generation, delivering near-instantaneous analytical capabilities that enable proactive decision-making. By transforming raw data into actionable intelligence, the organization empowered teams to develop precision-targeted strategies for enhancing customer experience and operational effectiveness. The streamlined approach significantly reduced infrastructure complexity and manual intervention, liberating valuable human resources to focus on strategic innovation and high-impact initiatives, thereby creating a more agile and responsive organizational framework. The original CTR pipeline took 2 months to build, whereas the CTR on data lake simplified the consumption and pipelines were adopted and delivered within just 1 week, drastically accelerating development timelines. With the new ETL approach, additional data elements (like call quality metrics) are integrated instantly, eliminating the need for 1–2 weeks of bespoke ETL effort.</p> 
<h3>Future implications</h3> 
<p>NatWest’s innovative data platform establishes a highly adaptive infrastructure capable of seamlessly accommodating expanding data volumes and emerging interaction modalities. By enabling sophisticated predictive analytics and personalized customer insights, the solution transforms raw data into strategic organizational capabilities. The enhanced metric accessibility creates a dynamic ecosystem that systematically drives iterative improvements, encouraging continuous data-driven experimentation and organizational learning.</p> 
<h2>Conclusion</h2> 
<p>NatWest’s migration to <a href="https://docs.aws.amazon.com/connect/latest/adminguide/data-lake.html">Amazon Connect analytics data lake</a> represents a transformative approach to data management that fundamentally reimagines the organization’s analytical capabilities. By streamlining complex infrastructure and eliminating traditional data movement barriers, the bank has established a robust, simplified, forward-looking framework for intelligent customer service. This architecture directly integrates critical interaction metrics and supports near real-time data availability, enabling unprecedented operational agility and data-driven insights. While some data processing such as existing dashboards and contact flow logs still relies on traditional pipelines, our strategic evolution builds flexible and a simplified foundation that balances current capabilities with future technological potential, positioning NatWest to respond more adaptively to evolving customer expectations.</p> 
<p>Amazon Connect data lake is available today in <a href="https://docs.aws.amazon.com/connect/latest/adminguide/regions.html#analytics_datalake_region">multiple AWS regions</a>. You can get started by <a href="https://docs.aws.amazon.com/connect/latest/adminguide/access-datalake.html">enabling Amazon Connect analytics data lake</a> in your Amazon Connect instance or reach out to your AWS account team for more information.</p> 
<h2>Authors bio</h2> 
<table style="height: 231px;" width="837"> 
 <tbody> 
  <tr> 
   <td><img alt="" class="alignnone size-thumbnail wp-image-13678" height="150" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2025/10/30/Kousik-Suresh-e1761812728779-150x150.jpg" width="150" /></td> 
   <td><b>Kousik Suresh </b>is a Principal Engineer at NatWest, specialised in Amazon Connect solutions. He designs secure, scalable platforms focused on enhancing customer experience, driving innovation, and delivering automation through cutting-edge AI-powered services.</td> 
  </tr> 
  <tr> 
   <td><img alt="" class="alignnone size-thumbnail wp-image-13676" height="150" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2025/10/30/Krishanu-Bhar-150x150.jpg" width="150" /></td> 
   <td><strong>Krishanu Bhar</strong> is a Director and Lead Enterprise Architect for the Remote Contact Platform at NatWest Group. He drives the modernization of bank’s contact center ecosystem through cloud-first and AI-powered transformation, leveraging AWS to build resilient, scalable, and future ready platforms.</td> 
  </tr> 
  <tr> 
   <td><img alt="" class="alignnone wp-image-14267 size-thumbnail" height="150" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/05/Thilaga-Kannappan-150x150.png" width="150" /></td> 
   <td><strong>Thilaga Kannappan </strong>is a Data Analyst at NatWest who transforms data into actionable insights while focusing on Generative AI and cloud-native solutions. She specializes in AWS analytics and AI services, helping organizations modernize data workflows and unlock business value.</td> 
  </tr> 
  <tr> 
   <td><img alt="" class="alignnone wp-image-14268 size-thumbnail" height="150" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/05/Vishesh-Goel-150x150.jpeg" width="150" /></td> 
   <td><strong> Vishesh Goel</strong> is a Senior Software Engineer at NatWest, specializing in Python development and AWS cloud solutions. He designs and implements scalable backend systems and cloud architectures that drive efficiency and performance.</td> 
  </tr> 
  <tr> 
   <td><img alt="" class="alignnone size-full wp-image-10503" height="186" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2024/03/17/Pavan.png" width="186" /></td> 
   <td><strong>Pavan Dusanapudi</strong> is a Worldwide Solutions Architect Lead for Amazon Connect Forecasting, Capacity Planning, and Scheduling (FCS), based in Manchester, UK. He leads cross-functional teams to deliver customer and agent experience solutions that drive business outcomes through digital transformation. Outside of work, he enjoys hiking with his family in the Peak District, CrossFit, and finding inner peace.</td> 
  </tr> 
  <tr> 
   <td><img alt="" class="alignnone size-full wp-image-13687" height="216" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2025/10/30/Prabha.png" width="165" /></td> 
   <td><strong>Prabhakar Rajasekar </strong>is a Specialist Customer Experience Solution Architect at Amazon Web Services for WWSO in Aachen, Germany. Besides helping customers in their digital transformation, you will see him spending time with his kids in the garden or in the woods.</td> 
  </tr> 
 </tbody> 
</table> 
<p></p>
