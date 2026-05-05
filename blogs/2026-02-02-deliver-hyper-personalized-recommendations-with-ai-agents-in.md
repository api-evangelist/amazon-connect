---
title: "Deliver hyper-personalized recommendations with AI agents in Amazon Connect"
url: "https://aws.amazon.com/blogs/contact-center/deliver-hyper-personalized-recommendations-with-ai-agents-in-amazon-connect/"
date: "Mon, 02 Feb 2026 20:18:46 +0000"
author: "Abhishek Pandey"
feed_url: "https://aws.amazon.com/blogs/contact-center/feed/"
---
<h2><strong>Introduction</strong></h2> 
<p>Every customer interaction leaves digital traces that reveal preferences and needs. While businesses collect vast amounts of customer data, most struggle to move beyond basic personalization to understand the ‘why’ behind customer behavior. The key challenge isn’t gathering data—it’s converting these signals into real-time, actionable insights. Whether in retail, airlines, telecom, or entertainment, companies seek to provide value beyond just responding to immediate customer requests. Now, <a href="https://aws.amazon.com/connect/">Amazon Connect</a> can turn that data into real-time product recommendations</p> 
<p>Amazon Connect customers can use enriched customer profiles with AI powered recommendations for common use cases such as:</p> 
<ul> 
 <li><strong>Recommended for you</strong> – Suggests items based on user’s past behavior and interactions</li> 
 <li><strong>Similar items</strong> – Uses AI to find thematically related products commonly bought together for cross-selling</li> 
 <li><strong>Frequently paired items</strong> – Identifies products commonly bought together for cross-selling</li> 
 <li><strong>Popular items</strong> – Shows most-interacted products across all users</li> 
 <li><strong>Trending now</strong> – Highlights products gaining rapid popularity</li> 
</ul> 
<p>Each use case uses a proven AI algorithm that learns from customer behavior and catalog data. Businesses can quickly implement this thought pre-configured AI sales agents that access real-time customer data and provide tailored recommendations. Businesses can then customize these AI agents’ responses through configurable guardrails and purpose-built prompts, ensuring consistent and brand-aligned messaging.</p> 
<p>In this blog, we will demonstrate how a&nbsp;fictitious company, AnyCompany, can use AI-based recommendations&nbsp;to enhance proactive self-service and human agent-assisted customer interactions.</p> 
<h3><strong>Solution overview</strong></h3> 
<p>Here’s a quick overview of all the steps to be followed</p> 
<ol> 
 <li>Enable Data Store in Customer Profiles</li> 
 <li>Add interaction data into Customer Profiles</li> 
 <li>Create Predictive Insights</li> 
 <li>Using Customer Profiles Recommendation in Amazon Connect Flows</li> 
 <li>Create AI Agent</li> 
 <li>Exploring Recommendations via API</li> 
</ol> 
<h3><strong>Prerequisites</strong></h3> 
<p>For this walk through, it is assumed you have the following prerequisites:</p> 
<ul> 
 <li>An <a href="https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fportal.aws.amazon.com%2Fbilling%2Fsignup%2Fresume&amp;client_id=signup">AWS account</a></li> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-instances.html">Amazon Connect instance</a></li> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/adminguide/enable-customer-profiles.html">Amazon Connect Customer Profiles is enabled</a></li> 
</ul> 
<h3><strong>Deployment steps</strong></h3> 
<p><strong>Step 1: &nbsp;Enable Data Store in Amazon Connect Customer Profiles</strong></p> 
<ol> 
 <li>Sign in to the <a href="https://aws.amazon.com/console/">AWS Management Console</a>.</li> 
 <li>Search for Amazon Connect on the services search bar and click on <strong>Amazon Connect</strong>.</li> 
 <li>Click on <strong>Access URL</strong> and log in to your Amazon Connect instance.</li> 
 <li>On the Amazon Connect Instances page, click on <strong>Customer Profiles</strong> in the left side navigation menu.</li> 
 <li>Enable <strong>Introducing Data Store</strong></li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14359" height="311" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure1_2.png" width="777" /></p> 
<p style="padding-left: 40px;"></p> 
<p style="padding-left: 40px;"></p> 
<p style="padding-left: 40px;"><strong>Figure 1:</strong> Enable Data Store</p> 
<p><strong>Step 2: &nbsp;Add Interaction data into Amazon Connect Customer Profiles</strong></p> 
<p><strong>Web analytics ingestion</strong></p> 
<p>Amazon Connect Customer Profiles now supports real-time ingestion of click-stream events data based on users’ activity on a website/mobile application. Customers can store data across the&nbsp;<a href="https://docs.aws.amazon.com/connect/latest/adminguide/object-type-mapping-definition-details.html">existing</a> and newly launched Web Analytics object. This data can&nbsp;then be used for personalizing the user experience in real-time through web notifications (<a href="https://docs.aws.amazon.com/connect/latest/adminguide/object-type-mapping-definition-details.html">Outbound campaigns</a>) or during inbound customer queries to a contact center powered by Amazon Connect.</p> 
<ol> 
 <li>Using the <a href="https://docs.aws.amazon.com/connect/latest/APIReference/API_connect-customer-profiles_PutProfileObjectType.html">PutProfileObjectType API</a> create a data mapping to map your clickstream data to the Web Analytics object. For more information, see <a href="https://docs.aws.amazon.com/connect/latest/adminguide/standard-loyalty-promotion-object-mapping-web-analytics.html">Object type mapping for Web Analytics Object</a>. 
  <ol> 
   <li>Refer to sample API payload: <a href="https://aws-contact-center-blog.s3.us-west-2.amazonaws.com/deliver-hyper-personalized-recommendations-with-ai-agents-in-amazon-connect/PutProfileObjectTypeSamplePayload.json">PutProfileObjectTypeSamplePayload.json</a>. Update DomainName in the script.</li> 
   <li>aws cli command: aws customer-profiles put-profile-object-type –region us-east-1 –cli-input-json file://PutProfileObjectTypeSamplePayload.json</li> 
  </ol> </li> 
 <li>After creating the profile object type, the data can be ingested using <a href="https://docs.aws.amazon.com/connect/latest/adminguide/customer-profiles-object-type-mappings.html">Amazon S3</a>, <a href="https://docs.aws.amazon.com/connect/latest/adminguide/customer-profiles-kinesis-integration.html">Amazon Kinesis integration</a> or <a href="https://docs.aws.amazon.com/connect/latest/APIReference/API_connect-customer-profiles_PutProfileObject.html">PutProfileObject API</a>. 
  <ol> 
   <li>Refer to <a href="https://aws-contact-center-blog.s3.us-west-2.amazonaws.com/deliver-hyper-personalized-recommendations-with-ai-agents-in-amazon-connect/PersonalizationWebAnalytics.json">PersonalizationWebAnalytics.json</a> for sample data and <a href="https://aws-contact-center-blog.s3.us-west-2.amazonaws.com/deliver-hyper-personalized-recommendations-with-ai-agents-in-amazon-connect/PutProfileObjectScript.py">PutProfileObjectScript.py</a> script to ingest this sample data into your CustomerProfiles domain using PutProfileObject API. Update DomainName and region_name in the script. Execute the script using the command: python PutProfileObjectScript.py</li> 
  </ol> </li> 
</ol> 
<p><strong>Step 3: Create predictive&nbsp;insights (Public Preview)</strong></p> 
<ol> 
 <li>Sign in to the <a href="https://aws.amazon.com/console/">AWS Management Console</a>.</li> 
 <li>Upload your Item Catalog data to Amazon S3 bucket and update S3 bucket permission as shown below. Refer to <a href="https://aws-contact-center-blog.s3.us-west-2.amazonaws.com/deliver-hyper-personalized-recommendations-with-ai-agents-in-amazon-connect/PersonalizationItemCatalog.csv">PersonalizationItemCatalog.csv</a> for sample Item Catalog.</li> 
</ol> 
<p><strong>Note:</strong> Update the S3 bucket permission to grant Amazon Flow read access permission. Sample permission below for reference.</p> 
<div class="hide-language"> 
 <pre class="unlimited-height-code"><code class="lang-json">{
&nbsp;&nbsp;&nbsp; "Version": "2012-10-17",
&nbsp;&nbsp;&nbsp; "Statement": [
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "Effect": "Allow",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "Principal": {
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "Service": "appflow.amazonaws.com"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; },
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "Action": [
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "s3:ListBucket",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "s3:GetObject"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ],
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "Resource": [
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "arn:aws:s3:::[Your S3 Bucket Name] ",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "arn:aws:s3:::[Your S3 Bucket Name]/*"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }
&nbsp;&nbsp;&nbsp; ]
} </code></pre> 
</div> 
<ol start="3"> 
 <li>Search for Amazon Connect on the services search bar and click on <strong>Amazon Connect</strong>.</li> 
 <li>Click on <strong>Access URL</strong> and log in to your Amazon Connect instance.</li> 
 <li>On the Amazon Connect Instances page, click on <strong>Customer Profiles</strong> in the left side navigation menu.</li> 
 <li>Under Predictive Insights section, click on <strong>Add item catalog</strong>.</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14313" height="462" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure2-2.png" width="1315" /></p> 
<p style="padding-left: 40px;"><strong>Figure 2:</strong> Add item catalog</p> 
<ol start="7"> 
 <li>Select the <strong>AWS S3 Bucket</strong> and add the <strong>S3 prefix</strong> for the item catalog data. You can also download the template to format your data properly. Click <strong>Add item catalog</strong>.</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14318" height="764" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure3-1.png" width="1323" /></p> 
<p style="padding-left: 40px;"><strong>Figure 3:</strong> Select AWS S3 Bucket and add S3 Prefix</p> 
<ol start="8"> 
 <li>A green banner will appear at the top confirming S3 integration to Customer Profiles domain</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14319" height="74" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure4-1.png" width="1304" /></p> 
<p style="padding-left: 40px;"><strong>Figure 4:</strong> S3 integration confirmation</p> 
<ol start="9"> 
 <li>Under Predictive Insights section, click on <strong>Manage recommendations,</strong> click on <strong>Create recommendations.</strong></li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14321" height="477" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure5-1.png" width="1317" /></p> 
<p style="padding-left: 40px;"><strong>Figure 5:</strong> Create recommender under Predictive insights</p> 
<ol start="10"> 
 <li>Navigate to Users -&gt; Security Profiles and Configure Security Profiles to support View (list and view predictive insights), Create (create recommendations), Delete (delete recommendations), and Edit (update recommendations) permissions with Predictive insights enabled.</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14322" height="341" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure6-2.png" width="1340" /></p> 
<p style="padding-left: 40px;"><strong>Figure 6:</strong> Update Security profiles for Predictive Insights</p> 
<ol start="11"> 
 <li>Navigate to Customer Profiles -&gt; Predictive Insights and then click on <strong>Create Recommendation</strong>.</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14323" height="659" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure7-1.png" width="1312" /></p> 
<p style="padding-left: 40px;"><strong>Figure 7:</strong> Create recommendation</p> 
<ol start="12"> 
 <li>Enter the Name, Description, choose a Recommendation Type to generate the recommendations you want to deliver, including Recommended for you, Similar items, Frequently paired items, Popular items and Trending now. Add the optional Event Type, Event value threshold. Click on <strong>Add event</strong>. Click on <strong>Create</strong> for Create Recommendation</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14325" height="820" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure8-1.png" width="1311" /></p> 
<p style="padding-left: 40px;"><strong>Figure 8:</strong> Create recommendation for product recommendation</p> 
<ol start="13"> 
 <li>You will see a green banner on the top with successfully created recommendations.</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14326" height="85" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure9-1.png" width="1110" /></p> 
<p style="padding-left: 40px;"><strong>Figure 9:</strong> Green banner showing successful creation of the recommendation</p> 
<ol start="14"> 
 <li>The status of the recommendation will be shown as <strong>In Progress</strong>. Click on the <strong>product_recommendation</strong>, click <strong>View details</strong> under Actions.</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14327" height="418" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure10-1.png" width="1117" /></p> 
<p style="padding-left: 40px;"><strong>Figure 10:</strong> View details of recommendation</p> 
<ol start="15"> 
 <li>Under Prediction Quality, filter by <strong>training date</strong>. Please wait for status to become <strong>Active</strong>.</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14328" height="719" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure11-1.png" width="1112" /></p> 
<p style="padding-left: 40px;"><strong>Figure 11:</strong> Filter recommendation by training date</p> 
<ol start="16"> 
 <li>Select <strong>Next Actions</strong>, <strong>Add to flow</strong> or add to <strong>Add to Q in Connect</strong>.</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14329" height="684" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure12.png" width="1108" /></p> 
<p style="padding-left: 40px;"><strong>Figure 12:</strong> Select Next actions for the recommendation</p> 
<p><strong>Step 4: Using Customer Profile recommendations in Amazon Connect Flows</strong></p> 
<p>This section describes how we can use the Customer Profiles <strong>Get profile recommendations</strong> flow block to enrich user experience during a contact by generating AI-powered recommendations for a profile in real-time.</p> 
<p>The following sections cover detailed explanations of the <strong>Get profile recommendations</strong> block’s properties, branches, and how to use its response within the rest of the flow definition.</p> 
<p><strong>Flow Block Properties</strong></p> 
<p>The <strong>Get profile recommendations</strong> flow block has the following properties to configure:</p> 
<ol> 
 <li><strong>Profile ID (required):</strong> A Profile ID is required for this block to function. The <strong>Get profile recommendations</strong> flow block generates recommendations for the Profile ID provided here. You have the option to manually input the Profile ID or use a pre-defined value stored in an attribute. If using a pre-defined value, ensure you provide the Profile ID by using a preceding <a href="https://docs.aws.amazon.com/connect/latest/adminguide/customer-profiles-block.html#customer-profiles-block-properties-get-profile">Get profile block</a>, as illustrated in the following image. Use the <strong>Get profile</strong> block to pinpoint the specific profile before moving forward to generate recommendations in the subsequent block.</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14331" height="417" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure13.png" width="1109" /></p> 
<p style="padding-left: 40px;"><strong>Figure 13:</strong> Get profile recommendation in the flow</p> 
<ol start="2"> 
 <li><strong>Recommender name (required)</strong>: A recommender name is required for this block to function. This is the name of the recommender you want to use to generate recommendations for the given Profile ID. You can only use recommenders that are active to generate recommendations.</li> 
 <li><strong>Max results (required)</strong>: The maximum number of recommendations to generate for the given Profile ID. This can range between 1 to 3 recommendations.</li> 
 <li><strong>Recommendation attributes (required)</strong>: Define which attributes of the recommendations response to persist in contact attribute.</li> 
 <li><strong>Item ID</strong>: This is the Item ID provided as additional context to generate recommendations for the given Profile ID. Item ID is only required when using a “Similar items” or “Frequently paired items” recommender type. You have the option to manually input the Profile ID or use a pre-defined value stored in an attribute. If using a pre-defined value, ensure you provide the Item ID by using a preceding <a href="https://docs.aws.amazon.com/connect/latest/adminguide/customer-profiles-block.html#customer-profiles-block-properties-get-calculated-attributes">Get calculated attributes block</a>, as illustrated in the following image. Use the <strong>Get calculated attributes</strong> block to pinpoint the specific Item ID before moving forward to generate recommendations in the subsequent block.</li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14332" height="530" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure14.png" width="1082" /></p> 
<p style="padding-left: 40px;"><strong>Figure 14:</strong> Get calculated attributes with get profile recommendations</p> 
<p>The following image illustrates how the block properties may be configured:</p> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14333" height="981" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure15.png" width="437" /></p> 
<p style="padding-left: 40px;"><strong>Figure 15:</strong> Get profile recommendations under customer profiles block</p> 
<p><strong>Flow Block Branches</strong></p> 
<p>The <strong>Get profile recommendations</strong> flow block can route contacts down the following branches:</p> 
<ol> 
 <li><strong>Success:</strong> Recommendations were successfully generated for the provided Profile ID. Selected recommendation attributes were persisted to contact attribute $.Customer.Recommendations.</li> 
 <li><strong>Error:</strong> An error was encountered while trying to generate recommendations. This may be due to a system error or how Get profile recommendations block is configured.</li> 
 <li><strong>None Found:</strong> No recommendations could be generated.</li> 
</ol> 
<p><strong>Using Recommendations from the block</strong><br /> Now let’s look at how to use the recommendations generated by the <strong>Get profile</strong> <strong>recommendations</strong> block within the rest of your flow definition.</p> 
<p><img alt="" class="alignnone size-full wp-image-14334" height="231" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure16.png" width="1114" /></p> 
<p><strong>Figure 16:</strong> Sample flow</p> 
<p>The recommendations response is persisted to the $.Customer.Recommendations contact attribute JSONPath as a JSON list of recommendation objects. Each recommendation object will contain the selected <strong>Recommendation attributes</strong></p> 
<pre class="unlimited-height-code"><code class="lang-json">[ &nbsp;&nbsp; &nbsp; &nbsp;{&nbsp;&nbsp;// Recommendation object &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; "Score": number, &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; "CatalogItem": { &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"Id": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"Name": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"Code": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"Type": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"Category": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"Description": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"Ad<code class="lang-json">ditionalInformation": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"ImageLink": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"Link": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"CreatedAt": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"UpdatedAt": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"Price": "string", &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;"Attributes": { &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; "string": "string" &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;} &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; } &nbsp;&nbsp; &nbsp; &nbsp;}, &nbsp; &nbsp; &nbsp; ...&nbsp;// upto 3 recommendations ]</code></code></pre> 
<p>Amazon Connect Flows currently cannot directly access list elements using index notation (e.g. $.Customer.Recommendations[0]), so we use a <a href="https://docs.aws.amazon.com/connect/latest/adminguide/invoke-lambda-function-block.html">AWS Lambda function</a> to transform the recommendations list, as illustrated in the following image.</p> 
<p><img alt="" class="alignnone size-full wp-image-14336" height="575" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure17.png" width="1118" /></p> 
<p><strong>Figure 17:</strong> Invoke AWS Lambda function</p> 
<p><img alt="" class="alignnone size-full wp-image-14337" height="469" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure18.png" width="414" /></p> 
<p><strong>Figure 18:</strong> Add function input parameters</p> 
<p>Here is the <a href="https://docs.aws.amazon.com/connect/latest/adminguide/predictive-insights-get-started.html">link</a> to sample Python code snippet from a Lambda function shows how it can be used to transform recommendations from the <strong>Get profile recommendations</strong> block and persist into other contact attributes such that the recommendations can be used in subsequent blocks:</p> 
<p>After persisting transformed recommendations into contact attributes, here’s an example showing its usage in a <a href="https://docs.aws.amazon.com/connect/latest/adminguide/play.html">Play Prompt block</a>.</p> 
<p><img alt="" class="alignnone size-full wp-image-14339" height="952" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure19.png" width="609" /></p> 
<p><strong>Figure 19:</strong> Sample play prompt</p> 
<p>Once you have setup your flow with the <strong>Get profile recommendations</strong> block, you can start using it to generate recommendations for your customers during their contacts.</p> 
<p><img alt="" class="alignnone size-full wp-image-14340" height="755" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure20.png" width="407" /></p> 
<p><strong>Figure 20:</strong> Sample chat</p> 
<p><strong>Step 5: Create AI agent</strong></p> 
<p>AI agents provide agentic capability by providing a new agent type <strong>Orchestration</strong> which will be able to orchestrate between different tools that the agent has.</p> 
<p>We will leverage this new feature of AI Agent to provide a Recommender AI agent which can provide item recommendation in response to user’s/agent’s input. This can be used both in self-service and agent-assist use case. One of the use cases of this agent can be to act as an upsell agent.</p> 
<ol> 
 <li>Sign in to the <a href="https://aws.amazon.com/console/">AWS Management Console</a>.</li> 
 <li>Search for Amazon Connect on the services search bar and click on <strong>Amazon Connect</strong>.</li> 
 <li>Click on <strong>Access URL</strong> and log in to your Amazon Connect instance.</li> 
 <li>On the Amazon Connect console, on the left side menu, please click on the option <strong>AI Agent Designer</strong> and select <strong>AI agents</strong>. Click on <strong>Create AI Agent</strong></li> 
</ol> 
<p>An AI Agent of type <strong>Orchestration – System</strong> in <strong>Saved as draft</strong> status will be provided under AI Agents. This will act as template providing customers all the configuration required to use all the 1P tools to get recommendations and example prompts.</p> 
<ol> 
 <li>You will create a new AI agent of Orchestration Type and select <strong>Copy from existing Agent</strong> select <strong>SalesAgent</strong> from the drop down. Add Description and click <strong>Create.</strong></li> 
</ol> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14341" height="824" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure21.png" width="807" /></p> 
<p style="padding-left: 40px;"><strong>Figure 21:</strong> Create AI Agent</p> 
<ol start="2"> 
 <li>This will create the AI-Sales-Agent with all the tools pre-configured. Update the Security Profile as <strong>Admin</strong>. For AI Agent, you can create your own security profiles based on the tools access. <strong>SalesAgent</strong> prompt has already been added. Click <strong>Save</strong> and <strong>Publish</strong>.</li> 
</ol> 
<p><strong>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Note:</strong> For updating AI Prompts and AI Guardrails, refer <a href="https://docs.aws.amazon.com/connect/latest/adminguide/customize-connect-ai-agents.html">here</a>.</p> 
<p style="padding-left: 40px;"><img alt="" class="alignnone size-full wp-image-14342" height="1120" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Figure22.png" width="1040" /></p> 
<p style="padding-left: 40px;"><strong>Figure 22:</strong> Save and Publish AI Agent</p> 
<ol start="2"> 
 <li>Now, you can update the flow which has the Amazon lex bot by selecting this new agent.</li> 
 <li>You need to add the <a href="https://docs.aws.amazon.com/connect/latest/adminguide/customer-profiles-block.html">Customer Profile flow block</a> to get profile Id.</li> 
 <li>This flow can be used with either the chat widget contacts or the voice call and customer input will be passed to the AI agent on Amazon lex bot.</li> 
</ol> 
<p><strong>Step 6: Exploring recommendations via the API</strong></p> 
<p>Once the recommender is active, it is ready to provide recommendations. In this section we will explore how to use Customer Profiles APIs to retrieve profile recommendations and predictive insights. These APIs can be used to surface recommendations directly with web and mobile pages as well as in any other custom integration.</p> 
<p>Using the GetProfileRecommendations API, recommendations can be obtained for a specific profile from the recommender in a domain. The following example illustrates the API request to retrieve recommendations from the “SimilarItems” recommender for the profile “26b43ae9a2ad4f9c9c01-3455bf91eff1” within the “my-domain” domain. Since this recommender type recommends similar items to an existing item in the catalog, the existing item’s catalog ID is provided in the “Context” of the request. The request also indicates that a maximum of 20 similar items should be returned.</p> 
<pre><code class="lang-json">POST /domains/my-domain/profiles/26b43ae9a2ad4f9c9c01-3455bf91eff1/recommendations  { &nbsp;&nbsp; "RecommenderName": "SimilarItems", &nbsp;&nbsp; "Context": { &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "_catalogItem.Id": "PROD-001-XYZ" &nbsp;&nbsp; }, &nbsp;&nbsp; "MaxResults": 20 }</code></pre> 
<p>The API response includes the catalog information for each recommended item along with a score that represents the relative certainty that the recommended item is relevant or similar to the input item. For brevity, only one catalog item is shown below.</p> 
<pre><code class="lang-json">{ &nbsp;&nbsp; "Recommendations": [
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; { &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "Score": 0.8, &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "CatalogItem": { &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "Id": "PROD-001-XYZ", &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "Name": "Ergonomic Office Chair", &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "Description": "A high-back ergonomic office chair with adjustable lumbar support, breathable mesh material, and a five-star wheeled base for enhanced mobility and comfort during long working hours.", &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "Category": "Office Furniture", &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "Price": "249.99" &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; } &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }
&nbsp;&nbsp; ] }</code></pre> 
<p>The GetProfileRecommendations API provides programmatic access to the predictive insights and item recommendations in a Customer Profile domain. These APIs can be used to surface recommendations directly within applications or custom integrations.</p> 
<h2><strong>Conclusion</strong></h2> 
<p>These new AI-powered capabilities in Amazon Connect transform customer experiences from reactive to proactive. By combining AI powered recommendations with Amazon Connect Customer Profiles and AI agents, businesses can deliver personalized experiences that anticipate customer needs.</p> 
<p>Providing personalized, omnichannel experiences at scale is a critical competitive differentiator for businesses. The walkthrough presented in this blog demonstrates how businesses can create meaningful interactions that drive both customer satisfaction and business growth using Amazon Connect. By implementing these capabilities, organizations can transform every customer touchpoint into an opportunity for deeper engagement, ultimately building stronger relationships and fostering long-term customer loyalty.</p> 
<h2>Author Bio</h2> 
<table> 
 <tbody> 
  <tr> 
   <td><img alt="" class="alignnone wp-image-14368" height="285" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/01/29/Picture1-12.png" width="285" /></td> 
   <td><strong>Nimish Amlathe</strong> is a Product Lead at Amazon Web Services based in Seattle, WA. At AWS, he works with teams at the intersection of customer data, Agentic AI capabilities, and proactive customer engagement. Outside of work, you are likely to see him at a local comedy club.</td> 
  </tr> 
  <tr> 
   <td><img alt="" class="alignnone size-full wp-image-13146" height="772" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2025/08/25/Abhishek-Pandey.png" width="738" /></td> 
   <td><strong>Abhishek Pandey</strong> is a Principal Solutions Architect with Amazon Web Services based in Houston, TX. Abhishek is passionate about architecting creative solutions that&nbsp; support business innovation across different industries. Abhishek is specialized in helping customers design and implement AI contact center solutions using Amazon Connect and the broader AWS ecosystem. Outside of work, he loves to hang out with family and friends.</td> 
  </tr> 
 </tbody> 
</table> 
<p>&nbsp;</p>
