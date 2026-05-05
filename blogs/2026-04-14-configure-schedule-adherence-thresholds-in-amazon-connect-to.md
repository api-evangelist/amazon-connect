---
title: "Configure Schedule Adherence Thresholds in Amazon Connect to Account for Operational Variances"
url: "https://aws.amazon.com/blogs/contact-center/configure-schedule-adherence-thresholds-in-amazon-connect-to-account-for-operational-variances/"
date: "Tue, 14 Apr 2026 13:43:34 +0000"
author: "Vikas Prasad"
feed_url: "https://aws.amazon.com/blogs/contact-center/feed/"
---
<h2><strong>1. Introduction</strong></h2> 
<h3><strong>1.1. What are adherence thresholds and why do they matter</strong></h3> 
<p>Schedule adherence is a Workforce Management (WFM) metric that measures how closely agents follow their assigned work schedules. Every contact center, however, operates with a degree of expected operational variance — agents finishing calls before transitioning to breaks, or handoffs running slightly long. When adherence measurement treats every deviation from the schedule as non-compliance, regardless of duration or context, it inflates non-adherence metrics and generates alert fatigue for supervisors — making it harder to identify the deviations that actually require attention.</p> 
<p>Configurable adherence thresholds solve this problem. They define an accepted tolerance window — in minutes — for each shift activity. Agents operating within the configured window are counted as adherent. Only deviations that genuinely exceed the threshold are flagged as non-adherent, ensuring that adherence data reflects meaningful variances rather than routine timing differences.</p> 
<p>Contact centers monitor adherence at multiple levels. Real-time analysts use dashboards to get an at-a-glance view of how sites and locations are performing. When adherence falls below acceptable levels, analysts alert supervisors who can intervene — coaching agents, adjusting assignments, or escalating as needed. Supervisors monitor adherence both in real time and historically to identify patterns, address root causes, and take corrective action.</p> 
<p>Small improvements in adherence translate directly into staffing capacity. Consider this example: in an 8-hour shift, an agent adheres to their schedule 80% of the time — meaning, out of 480 minutes, they were adherent for 384 minutes, and out of adherence for 96 minutes. Improving this agent’s adherence by 5% would mean this agent is now adherent for 408 minutes, and hence available to take contacts for 24 additional minutes. When this is scaled across a hypothetical 1,000 agents contact center, that represents 24,000 more minutes in a single day — equivalent to roughly 2,000 additional contacts at an average handle time of 12 minutes — without requiring additional staffing.</p> 
<h3><strong>1.2. Schedule Adherence in Amazon Connect</strong></h3> 
<p>Amazon Connect provides a robust set of schedule adherence capabilities that supervisors and workforce management teams rely on daily:</p> 
<ul> 
 <li><strong>Real-time adherence monitoring:</strong> The<a href="https://docs.aws.amazon.com/connect/latest/adminguide/queue-performance-dashboard.html"> Queue and agent performance dashboard</a> includes an Agent Adherence widget that shows each agent’s current adherence status, scheduled activity versus actual activity, and how long they have been in their current state. Supervisors can see at a glance which agents are on-schedule and which are not.</li> 
 <li><strong>Scheduled versus actual activity view:</strong> When viewing <a href="https://docs.aws.amazon.com/connect/latest/adminguide/definition-real-time-schedule-adherence.html">real-time schedule adherence</a>, supervisors can compare what an agent is scheduled to be doing against what they are actually doing, making it easy to identify the nature of each deviation.</li> 
 <li><strong>Historical adherence reporting:</strong> <a href="https://docs.aws.amazon.com/connect/latest/adminguide/historical-metrics.html">Historical metrics reports</a> include adherence percentage, adherent time, non-adherent time, and scheduled time — allowing workforce management teams to analyze adherence trends over days, weeks, and months.</li> 
 <li><strong>Adherence toggle on the published schedule:</strong> The <a href="https://docs.aws.amazon.com/connect/latest/adminguide/scheduling-view-schedule-supervisors.html">published calendar view</a> includes an adherence toggle that overlays adherence data directly on top of agent schedules, providing a visual representation of adherence breaches by agent and day for up to 30 days in the past.</li> 
</ul> 
<p>These capabilities give workforce management teams visibility into adherence across their organization. However, they provided no mechanism to account for predictable operational variance — the known timing tolerances built into every contact center’s daily operations. Without this, adherence metrics flagged routine variances as non-compliance, reducing the accuracy and usefulness of adherence data. Configurable adherence thresholds address this by allowing workforce management teams to define an accepted tolerance window for each shift activity.</p> 
<h3><strong>1.3. The challenge — accounting for operational variances</strong></h3> 
<p>Without a mechanism to account for expected variance, Amazon Connect treats every deviation from the schedule — regardless of duration or operational context — as non-adherent time. Consider a common scenario: an agent is handling a customer call when their scheduled break begins at 10:00 AM. The agent resolves the customer’s issue at 10:03 AM and then starts their break. Under strict adherence measurement, those three minutes are counted as non-adherent time, even though completing the customer interaction was the operationally correct decision.</p> 
<p>This creates two problems for workforce management teams:</p> 
<ol> 
 <li><strong>Inaccurate data:</strong> Minor variances caused by routine operational realities — call wrap-up, system transitions, handoffs — inflate non-adherence metrics, making it harder to identify genuine adherence issues that require action.</li> 
 <li><strong>Alert fatigue:</strong> Supervisors receive notifications for predictable, acceptable timing differences. Over time, this reduces the signal value of adherence dashboards, and supervisors begin to discount real alerts alongside the noise.</li> 
</ol> 
<h3><strong>1.4. The solution — configurable adherence thresholds</strong></h3> 
<p>Amazon Connect addresses this with configurable adherence thresholds in Forecasting, Capacity Planning, and Scheduling (FCS). Thresholds define the allowed variance, in minutes, between an agent’s scheduled activity and their actual activity before they are flagged as non-adherent. With this feature, organizations can account for expected operational variances so that adherence metrics and alerts reflect meaningful deviations.</p> 
<p>With configurable adherence thresholds, the scenario from the previous section plays out differently. Workforce management teams define an accepted tolerance window for each shift activity — for example, allowing agents to start their break, up to 5 minutes late. The agent who finishes their call at 10:03 AM and starts their break at 10:03 AM is now considered adherent. Only variances that exceed the configured threshold — the ones that genuinely warrant a supervisor’s attention — are flagged as non-adherent.</p> 
<p>In this post, we walk through how adherence thresholds work, how to configure them at multiple levels with practical examples, and how supervisors can monitor adherence using threshold-aware dashboards and reports.</p> 
<p>Watch the step-by-step video walkthrough:</p> 
<p></p> 
<h3><strong>1.5. Who benefits and how</strong></h3> 
<p><strong>For agents:</strong> Agents who complete a customer interaction a few minutes past a scheduled activity transition remain adherent when the variance falls within the configured threshold. This aligns adherence measurement with expected operational behavior.</p> 
<p><strong>For supervisors:</strong> Real-time and historical dashboards distinguish between agents operating within configured thresholds and those who have exceeded them. This helps supervisors at every level (regional, divisional, team) prioritize their attention on agents with meaningful adherence deviations.</p> 
<p><strong>For workforce management teams:</strong> When adherence metrics account for expected operational variances, the resulting historical data more accurately reflects agent behavior. This improves the reliability of inputs used for forecasting and capacity planning.</p> 
<h2><strong>2. Adherence thresholds in action: a walkthrough example</strong></h2> 
<p>To illustrate the impact of adherence thresholds, consider an agent with a shift from 9:00 AM to 2:00 PM, with work, break, and lunch activities scheduled throughout the day.</p> 
<table style="width: 100%; border-collapse: collapse;"> 
 <tbody> 
  <tr style="background-color: #000000; color: #ffffff;"> 
   <td style="border: 1px solid #000000; padding: 8px;">Scenario</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Description</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Original schedule</td> 
   <td style="border: 1px solid #000000; padding: 8px;">The shift as assigned: work → break → work → lunch → work</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Fully adherent</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Agent follows every activity transition at the scheduled time</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Without thresholds</td> 
   <td style="border: 1px solid #000000; padding: 8px;"> <p>Without thresholds, every deviation is counted as non-adherent — regardless of cause or context. Assume the following three variances occur: (1) Work starts 15 minutes late because the agent was caught in traffic — flagged as 15 minutes non-adherent. (2) Break runs 10 minutes over because the agent was finishing a customer call before stepping away — flagged as 10 minutes non-adherent. (3) Lunch starts 20 minutes late because the agent was handling a complex customer issue — flagged as 20 minutes non-adherent.</p> <p>Total non-adherent time: 45 minutes — all counted as non-compliance, even though two of the three variances were the direct result of doing the right thing for the customer.</p></td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">With thresholds applied</td> 
   <td style="border: 1px solid #000000; padding: 8px;">With configurable adherence thresholds, the same three variances are measured differently. (1) Work starts 15 minutes late — a 10-minute start-late threshold covers the first 10 minutes, leaving only 5 minutes marked non-adherent. (2) Break runs 10 minutes over — a 5-minute end-late threshold covers the first 5 minutes, leaving only 5 minutes marked non-adherent. (3) Lunch starts 20 minutes late — a 15-minute start-late threshold covers the first 15 minutes, leaving only 5 minutes marked non-adherent.Total non-adherent time: 15 minutes — only the variances that genuinely exceeded the configured thresholds are flagged, protecting adherence data from routine operational noise.</td> 
  </tr> 
 </tbody> 
</table> 
<p><img alt="" class="aligncenter wp-image-14648 size-full" height="710" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/04/13/Picture1-6.png" width="1068" /></p> 
<p style="text-align: center;"><strong>Figure 1:</strong> Comparison of adherence calculations with and without thresholds.</p> 
<p>With thresholds applied, non-adherent time is reduced by 67%. The 15 minutes of remaining non-adherent time represent variances that exceeded the configured thresholds — these are the deviations that warrant supervisor review.</p> 
<h2>3. Understanding adherence thresholds</h2> 
<p>An adherence threshold defines the allowed variance, in minutes, between an agent’s scheduled activity and their actual activity, before they are flagged as non-adherent. Each threshold can be configured with values from 1 to 10 minutes.</p> 
<p>Every threshold has four configurable options:</p> 
<table style="width: 100%; border-collapse: collapse;"> 
 <tbody> 
  <tr style="background-color: #000000; color: #ffffff; font-weight: bold;"> 
   <td style="border: 1px solid #000000; padding: 8px;">Threshold</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Abbreviation</td> 
   <td style="border: 1px solid #000000; padding: 8px;">What it controls</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Example</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Start Early</td> 
   <td style="border: 1px solid #000000; padding: 8px;">SE</td> 
   <td style="border: 1px solid #000000; padding: 8px;">How many minutes before the scheduled start an agent can begin and still be adherent</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Agent can start their break up to 3 minutes early</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Start Late</td> 
   <td style="border: 1px solid #000000; padding: 8px;">SL</td> 
   <td style="border: 1px solid #000000; padding: 8px;">How many minutes after the scheduled start an agent can begin and still be adherent</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Agent can start lunch up to 10 minutes late if finishing a call</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">End Early</td> 
   <td style="border: 1px solid #000000; padding: 8px;">EE</td> 
   <td style="border: 1px solid #000000; padding: 8px;">How many minutes before the scheduled end an agent can finish and still be adherent</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Agent can return from break up to 2 minutes early</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">End Late</td> 
   <td style="border: 1px solid #000000; padding: 8px;">EL</td> 
   <td style="border: 1px solid #000000; padding: 8px;">How many minutes after the scheduled end an agent can finish and still be adherent</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Agent can end their break up to 5 minutes late</td> 
  </tr> 
 </tbody> 
</table> 
<p><img alt="" class="aligncenter wp-image-14651 size-full" height="312" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/04/13/Picture2-2.png" width="426" /></p> 
<p style="text-align: center;"><strong>Figure 2:</strong> Threshold configuration options — SE, SL, EE, and EL — available at both shift and activity levels.</p> 
<p>The 4 options can be applied in 2 levels</p> 
<h3>3.1. Shift-level thresholds</h3> 
<p>Shift-level thresholds apply to the overall shift start and end times. For example, if you configure a 5-minute Start Early and 5-minute Start Late threshold at the shift level, an agent whose shift starts at 9:00 AM can log in anytime between 8:55 AM and 9:05 AM and still be considered adherent.</p> 
<p>This is useful because agents commonly log in a few minutes before or after their scheduled start. Without shift-level thresholds, an agent who logs in at 8:57 AM for a 9:00 AM shift would be marked as non-adherent.</p> 
<h3>3.2. Activity-level thresholds</h3> 
<p>Activity-level thresholds apply to each specific activity within the shift. Each activity — work, break, lunch, training — can have its own set of thresholds. This provides granular control over adherence measurement for different activity types.</p> 
<p><strong>Example:</strong> A contact center has a 15-minute break scheduled at 10:00 AM. Operationally, agents frequently complete customer calls 3-5 minutes past the break start time. You configure:</p> 
<ul> 
 <li>Can start late: 5 minutes</li> 
 <li>Can end late: 5 minutes</li> 
</ul> 
<p>Now an agent who starts their break at 10:04 AM (because they were completing a call) and returns at 10:19 AM (4 minutes late) is still considered adherent. The threshold accounts for this expected operational variance.</p> 
<h2>4. Configuring adherence thresholds — step by step</h2> 
<p>Amazon Connect provides four levels of threshold configuration across two main areas: the Shift Activities page and the Staffing Groups page. These levels form a precedence hierarchy, giving you both broad defaults and team-specific overrides.</p> 
<h3>4.1. Level 4 — Shift activity defaults (broadest scope)</h3> 
<p>This is the starting point. Thresholds configured here apply across all staffing groups unless explicitly overridden at a higher level.</p> 
<ol> 
 <li>In the Amazon Connect admin website, navigate to Scheduling &gt; Shift Activities.</li> 
 <li>Select an activity (for example, a 15-minute break).</li> 
 <li>Scroll down to the Adherence Threshold section.</li> 
 <li>Configure the threshold options: 
  <ol> 
   <li>Can start early: 3 minutes</li> 
   <li>Can start late: 5 minutes</li> 
   <li>Can end early: 2 minutes</li> 
   <li>Can end late: 5 minutes</li> 
  </ol> </li> 
 <li>Click Save.</li> 
</ol> 
<p><img alt="" class="aligncenter wp-image-14652 size-full" height="663" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/04/13/Picture3-2.png" width="825" /></p> 
<p style="text-align: center;"><strong>Figure 3:</strong> Level 4 — Shift activity defaults</p> 
<p><strong>What this means in practice:</strong> If an agent’s break is scheduled from <strong>11:00 AM to 11:15 AM</strong>, they can start their break anytime between<strong> 10:57 AM and 11:05 AM</strong>, and end it between <strong>11:13 AM and 11:20 AM</strong>, and still be considered adherent. This applies to every agent in every staffing group — unless a staffing group override exists.</p> 
<h3>4.2. Levels 1–3 — Staffing group overrides (team-specific)</h3> 
<p>Different teams have different operational realities. A team handling complex technical support calls may need more generous thresholds than a team handling quick billing inquiries. Staffing group configuration lets you tailor thresholds per team.</p> 
<ol> 
 <li>Navigate to <strong>Scheduling</strong> &gt; <strong>Staffing Groups</strong>.</li> 
 <li>Select a staffing group.</li> 
 <li>Scroll to the <strong>Adherence Threshold</strong> section. You will see two tabs: <strong>For Shifts</strong> and <strong>For Activities</strong>.</li> 
</ol> 
<h4 style="padding-left: 40px;"><strong>For Shifts tab (Level 1 — highest precedence):</strong></h4> 
<p style="padding-left: 40px;">Configure thresholds that apply to the overall shift start and end. For example:</p> 
<ul> 
 <li> 
  <ul> 
   <li>Shift can start <strong>5 minutes early</strong> or <strong>5 minutes late</strong></li> 
   <li>Shift can end <strong>5 minutes early</strong> or <strong>5 minutes late</strong></li> 
  </ul> </li> 
</ul> 
<p style="padding-left: 40px;">This gives agents a 10-minute window to start and end their shifts. Level 1 has the highest precedence — it overrides all other threshold configurations for the first and last activities in the shift.</p> 
<h4 style="padding-left: 40px;"><strong>For Activities tab — Individual activities (Level 2):</strong></h4> 
<p style="padding-left: 40px;">Set thresholds for specific activities. For example, for your technical support team:</p> 
<ul> 
 <li> 
  <ul> 
   <li><strong>Lunch</strong> can start <strong>10 minutes late</strong> and end<strong> 5 minutes late</strong> — accommodating agents who need to finish complex customer interactions before taking lunch.</li> 
   <li><strong>Break</strong> can start <strong>5 minutes late</strong> — because short calls often run a few minutes over.</li> 
  </ul> </li> 
</ul> 
<h4 style="padding-left: 40px;">For Activities tab — All activities (Level 3):</h4> 
<p style="padding-left: 40px;">Apply the same threshold uniformly across all activities on the shift. For example, set all activities to allow starting <strong>5 minutes early</strong>. This is a convenient way to set a baseline without configuring each activity individually.</p> 
<p style="padding-left: 40px;">4. Click <strong>Save</strong> to apply.</p> 
<p><img alt="" class="aligncenter wp-image-14653 size-large" height="408" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/04/13/Picture4-2-1024x408.png" width="1024" /></p> 
<p style="text-align: center;"><strong>Figure 4:</strong> Levels 1–3 — Staffing group overrides</p> 
<p style="text-align: left;"><strong>Important:</strong> Staffing group thresholds override the shift activity defaults (Level 4) for agents assigned to that specific group. Changes to thresholds apply to future adherence calculations only.</p> 
<h2>5. Threshold precedence — how the system decides which threshold to apply</h2> 
<p>When you have thresholds configured at multiple levels, the system follows a clear decision flow from highest to lowest priority. For each activity, it checks:</p> 
<ul> 
 <li><strong>Level 1 — Shift-level threshold (staffing group):</strong> Does a shift-level threshold exist for this staffing group, and is this activity at the start or end of the shift? If yes, apply it.</li> 
 <li><strong>Level 2 — Activity-specific threshold (staffing group):</strong> Does an activity-specific threshold exist for this activity type in this staffing group? If yes, apply it.</li> 
 <li><strong>Level 3 — All-activities threshold (staffing group):</strong> Does a general all-activities threshold exist for this staffing group? If yes, apply it.</li> 
 <li><strong>Level 4 — Shift activity default:</strong> Fall back to the default threshold configured on the Shift Activities page.</li> 
</ul> 
<p><img alt="" class="aligncenter wp-image-14656 size-full" height="463" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/04/13/Picture5-1.png" width="432" /></p> 
<p style="text-align: center;"><strong>Figure 5:</strong> The four configuration levels for adherence thresholds — three at the staffing group level and one at the shift activity level.</p> 
<h3>5.1. Precedence example</h3> 
<p>Let’s see how this works with a Work activity scheduled from 10:00 AM to 11:00 AM, where thresholds are configured at all four levels:</p> 
<table style="width: 100%; border-collapse: collapse;"> 
 <tbody> 
  <tr style="background-color: #000000; color: #ffffff; font-weight: bold;"> 
   <td style="border: 1px solid #000000; padding: 8px;">Level</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Start Threshold</td> 
   <td style="border: 1px solid #000000; padding: 8px;">End Threshold</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Level 1 (Shift)</td> 
   <td style="border: 1px solid #000000; padding: 8px;">2 min early</td> 
   <td style="border: 1px solid #000000; padding: 8px;">—</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Level 2 (Activity-specific)</td> 
   <td style="border: 1px solid #000000; padding: 8px;">3 min early</td> 
   <td style="border: 1px solid #000000; padding: 8px;">—</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Level 3 (All activities)</td> 
   <td style="border: 1px solid #000000; padding: 8px;">—</td> 
   <td style="border: 1px solid #000000; padding: 8px;">1 min late</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Level 4 (Shift activity default)</td> 
   <td style="border: 1px solid #000000; padding: 8px;">4 min early</td> 
   <td style="border: 1px solid #000000; padding: 8px;">6 min late</td> 
  </tr> 
 </tbody> 
</table> 
<p>The system resolves the effective threshold as follows:</p> 
<ul> 
 <li><strong>Start time:</strong> Level 1 has a threshold (2 minutes early), so it wins. The agent can start work at 9:58 AM and still be adherent.</li> 
 <li><strong>End time:</strong> Level 1 has no end threshold. Level 2 has no end threshold. Level 3 has an end threshold (1 minute late), so it wins. The agent can end work at 11:01 AM and still be adherent.</li> 
</ul> 
<p>The Level 4 defaults (4 minutes early start, 6 minutes late end) are not used because higher-precedence thresholds exist. This hierarchy ensures the most specific threshold always wins, giving you flexible control while maintaining clear priority rules.</p> 
<h2>6. Boundary threshold intervals — handling activity transitions</h2> 
<p>One of the most practical aspects of this feature is how it handles the transition between consecutive activities. When your work period ends and your break begins at the same time, the system creates what are called boundary threshold intervals — shared time windows where you can be adherent to either activity.</p> 
<h3>6.1. Why does this matter</h3> 
<p>Without boundary handling, an agent could be marked non-adherent during the transition between activities. For example, if work ends at 10:30 AM and break starts at 10:30 AM, an agent who is completing a call at 10:32 AM could be marked non-adherent for both work (ending late) and break (starting late) — counted twice for a single variance.</p> 
<h3>6.2. How it works — a practical example</h3> 
<p>Consider the following schedule and thresholds:</p> 
<ul> 
 <li><strong>Work activity</strong> ends at 10:30 AM with a threshold of ±5 minutes (can end between 10:25 AM and 10:35 AM)</li> 
 <li><strong>Break activity</strong> starts at 10:30 AM with a threshold of ±3 minutes (can start between 10:27 AM and 10:33 AM)</li> 
</ul> 
<p>These two windows overlap, creating a <strong>shared window from 10:25 AM to 10:35 AM</strong>. During this 10-minute shared window, whether the agent is finishing work or starting their break, they are considered adherent to the schedule. The system recognizes that either activity is acceptable during the transition period.</p> 
<p><img alt="" class="aligncenter wp-image-14659 size-full" height="194" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/04/13/Picture7.png" width="1121" /></p> 
<p style="text-align: center;"><strong>Figure 6:</strong> Boundary threshold intervals showing the shared window where either activity is considered adherent.</p> 
<p>This merging of threshold windows provides consistent adherence tracking at activity boundaries, accounting for the natural flow of transitions between activities.</p> 
<h2>7. Monitoring adherence with thresholds</h2> 
<p>Adherence thresholds are surfaced across three monitoring views in Amazon Connect, giving supervisors real-time and historical visibility.</p> 
<h3>7.1. Real-time dashboard — Queue and agent performance</h3> 
<p>The Agent Adherence widget on the Queue and agent performance dashboard now shows three adherence states instead of two:</p> 
<table style="width: 100%; border-collapse: collapse;"> 
 <tbody> 
  <tr style="background-color: #000000; color: #ffffff; font-weight: bold;"> 
   <td style="border: 1px solid #000000; padding: 8px;">Status</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Indicator</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Meaning</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Adherent</td> 
   <td style="border: 1px solid #000000; padding: 8px; color: #2e7d32; font-weight: bold;">Green</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Agent is following their schedule</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Using thresholds</td> 
   <td style="border: 1px solid #000000; padding: 8px; color: #f9a825; font-weight: bold;">Yellow warning</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Agent is within the configured threshold window — technically deviating but within acceptable bounds</td> 
  </tr> 
  <tr> 
   <td style="border: 1px solid #000000; padding: 8px;">Non-adherent</td> 
   <td style="border: 1px solid #000000; padding: 8px; color: #c62828; font-weight: bold;">Red</td> 
   <td style="border: 1px solid #000000; padding: 8px;">Agent has exceeded the threshold and is genuinely off-schedule</td> 
  </tr> 
 </tbody> 
</table> 
<p><strong>Why this matters for supervisors:</strong> Previously, the dashboard showed only green (adherent) and red (non-adherent). With the yellow “Using thresholds” state, supervisors can distinguish between agents who have exceeded thresholds and those operating within configured variance windows. This helps supervisors prioritize which agents to follow up with.</p> 
<p>Hovering over the yellow indicator shows details about which threshold is being used and how much threshold time remains.</p> 
<h3>7.2. Published calendar view</h3> 
<p>The published calendar view now displays adherence data with two types of visual indicators:</p> 
<ul> 
 <li><strong>Red bars</strong> — out of adherence (exceeds threshold)</li> 
 <li><strong>Yellow bars</strong> — within adherence threshold</li> 
</ul> 
<p>To view this, turn on the <strong>Adherence toggle</strong> in the top-right corner of the published calendar.</p> 
<h3>7.3. Historical metrics</h3> 
<p>Historical metrics now account for thresholds in the adherence calculation. The formula has changed:</p> 
<ul> 
 <li><strong>Previously:</strong> Adherence % = Adherent Time ÷ Scheduled Time</li> 
 <li><strong>Now:</strong> Adherence % = min(Adherent Time, Scheduled Time) ÷ Scheduled Time</li> 
</ul> 
<p>This ensures that adherence percentage stays meaningful and doesn’t exceed 100%, even when agents work beyond their scheduled hours while remaining adherent. Time spent within configured thresholds counts as adherent time.</p> 
<p>Historical reports can display:</p> 
<ul> 
 <li>Adherence percentage with and without thresholds</li> 
 <li>Time spent within configured thresholds</li> 
 <li>Threshold utilization patterns across teams</li> 
</ul> 
<h2>8. Prerequisites</h2> 
<p>Before configuring adherence thresholds, make sure you have:</p> 
<ul> 
 <li>An Amazon Connect instance with Forecasting, Capacity Planning, and Scheduling enabled</li> 
 <li>Published schedules with shift activities where Adherence = Yes</li> 
 <li>Appropriate IAM permissions to access scheduling and metrics configuration</li> 
 <li>Familiarity with your contact center’s operational patterns to set meaningful threshold values</li> 
</ul> 
<h2>9. Conclusion and next steps</h2> 
<p>Adherence thresholds in Amazon Connect FCS provide organizations with the ability to account for expected operational variances in schedule adherence measurement. By configuring thresholds at up to four levels of granularity, you can:</p> 
<ul> 
 <li><strong>Account for operational variances</strong> so that minor timing differences are not counted as non-adherent time</li> 
 <li><strong>Help supervisors prioritize</strong> by distinguishing between agents within thresholds and those who have exceeded them</li> 
 <li><strong>Improve adherence data accuracy</strong> for use in forecasting and capacity planning</li> 
 <li><strong>Handle activity transitions consistently</strong> with boundary threshold intervals</li> 
 <li><strong>Monitor with greater precision</strong> through real-time dashboards, calendar views, and historical reports</li> 
</ul> 
<p>To get started, review the common timing variances in your contact center operations. Configure thresholds that align with your operational expectations, beginning with the shift activity defaults (Level 4) and then adding staffing group overrides where teams have different requirements.</p> 
<p>For a detailed step-by-step walkthrough of every configuration screen, watch the <a href="https://www.youtube.com/watch?v=-sP126Xr8Zc">video demonstration on YouTube</a>.</p> 
<h2>10. Related resources</h2> 
<ul> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/adminguide/schedule-adherence.html">Schedule Adherence for agent productivity in Amazon Connect</a></li> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/adminguide/schedule-adherence-examples.html">Examples of adherence thresholds for agent shifts</a></li> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/adminguide/calculating-agents-productivity-time.html">Examples of Agent Adherence calculations</a></li> 
 <li><a href="https://docs.aws.amazon.com/connect/latest/adminguide/scheduling-metrics.html">Schedule Adherence metrics</a></li> 
 <li><a href="https://aws.amazon.com/about-aws/whats-new/2025/10/amazon-connect-configurable-thresholds-schedule-adherence/">Amazon Connect now provides configurable thresholds for schedule adherence</a></li> 
</ul> 
<h2>About the author</h2> 
<p><strong><img alt="" class="size-full wp-image-14662 alignleft" height="180" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/04/13/Vikas.png" width="137" /></strong></p> 
<p><strong>Vikas Prasad</strong> is a Senior Specialist Solutions Architect at AWS, focused on Amazon Connect Forecasting, Capacity Planning, and Scheduling. He enables customers to achieve business outcomes through Customer Experience solutions and digital transformation. In his leisure time, he enjoys outdoor activities such as traveling, cycling, and trekking.</p> 
<p><br class="blank" /><br class="blank" /><br class="blank" /><br class="blank" /><br class="blank" /></p> 
<p><strong><img alt="" class="size-full wp-image-14663 alignleft" height="175" src="https://d2908q01vomqb2.cloudfront.net/af3e133428b9e25c55bc59fe534248e6a0c0f17b/2026/04/13/Naveen.png" width="132" /></strong></p> 
<p><strong>Naveen Narayan</strong> is a Solutions Architect at AWS based in Tacoma, specializing in Amazon Connect and contact center solutions. He partners with customers to transform their contact center operations, leveraging Amazon Connect’s capabilities to drive exceptional customer experiences and operational efficiency.</p>
