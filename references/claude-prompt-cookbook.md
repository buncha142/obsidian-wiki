---
title: Appendix ก — Prompt Cookbook (90+ Templates)
tags: [claude, prompts, templates, business, content, coding, writing, productivity]
category: references
created: 2026-06-15
updated: 2026-06-15
sources: [claude-complete-guide-2026]
summary: "90 prompt templates พร้อมใช้ แบ่งเป็น 6 หมวด: Business/Content/Analysis/Coding/Writing/Productivity — copy & customize ทันที"
provenance:
  extracted: 0.98
  inferred: 0.02
  ambiguous: 0.00
---

# Appendix ก — Prompt Cookbook (90+ Templates)

> 90+ Prompts พร้อมใช้ · Test แล้ว · แบ่งตาม Category · Copy & Customize
>
> วิธีใช้ Prompt Cookbook: แต่ละ prompt ออกแบบให้ใช้ได้ทันทีโดยแทนที่ [วงเล็บ] ด้วยข้อมูลของคุณ ทุก prompt ผ่านการทดสอบกับ Claude Sonnet เครื่องหมาย แสดงตัวอย่าง output ที่ได้

| หมวด | จำนวน |
|---|---|
| ก.1 Business & Communication | 15 prompts |
| ก.2 Content Creation | 15 prompts |
| ก.3 Analysis & Research | 15 prompts |
| ก.4 Coding & Technical | 15 prompts |
| ก.5 Writing & Editing | 15 prompts |
| ก.6 Productivity & Operations | 15 prompts |
| **รวม** | **90 prompts** |

---

## ก.1 Business & Communication

*Email · Meeting · Negotiation · Client Communication · Internal Comms*

### #01 Email Reply — ตอบอีเมลให้กระชับและมืออาชีพ
*ได้รับ email ยาวที่ต้องตอบอย่างสุภาพแต่กระชับ*

```
Reply to this email professionally and concisely.
Email: <email>[paste email here]</email>
My role: [your position]
Key points I want to make: [list 2-3 points]
Tone: [formal/friendly/firm]
Length: max 150 words
```
*ได้ email reply ที่กระชับ ครบคลุม ไม่เยิ่นเย้อ*

---

### #02 Meeting Agenda — สร้าง agenda ก่อน meeting
*ต้องการ agenda ที่ทำให้ meeting มีประสิทธิภาพ*

```
Create a meeting agenda for:
Meeting purpose: [describe]
Duration: [X minutes]
Attendees: [roles]
Key decisions needed: [list]
Format: Time-boxed items with owner
```
*Agenda พร้อม time allocation และ owner ทุก item*

---

### #03 Meeting Summary — สรุป meeting หลังจบ
*มี transcript หรือ notes และต้องสรุปให้ทีม*

```
Summarize this meeting. Extract: decisions made,
action items (person + task + deadline),
open questions, next meeting needed?
<notes>[paste meeting notes]</notes>
```
*Summary กระชับพร้อม action items ชัดเจน*

---

### #04 Negotiation Brief — เตรียมก่อนเจรจา
*ต้องเจรจาราคาหรือ terms กับ client/vendor*

```
Prepare a negotiation brief.
My goal: [what I want to achieve]
Their likely position: [what they want]
My BATNA (best alternative): [describe]
Concessions I can make: [list]
Red lines: [what I cannot accept]
Provide: opening position, key arguments, concession sequence
```
*Brief 1 หน้าพร้อม strategy และ talking points*

---

### #05 Client Proposal — เขียน proposal ให้ลูกค้า
*ต้องส่ง proposal หลัง discovery call*

```
Write a client proposal.
Client: [name + industry]
Problem they have: [describe]
Our solution: [describe]
Price: [range or exact]
Timeline: [duration]
Our credentials: [relevant past work]
Include: exec summary, approach, timeline, investment, next steps
```
*Proposal ที่ convert ได้จริง*

---

### #06 Difficult Conversation — คุยเรื่องยากกับ colleague
*ต้องพูดเรื่อง performance, conflict หรือ boundary*

```
Help me prepare for a difficult conversation.
Issue: [describe the situation]
My role: [manager/peer/report]
What I need them to understand: [key message]
Their likely reaction: [how they might respond]
Goal: [desired outcome]
Provide: opening line, key points, how to handle pushback
```
*Script ที่ respectful และ direct พร้อม contingencies*

---

### #07 Status Report — รายงาน progress ให้ management
*ต้องส่ง weekly/monthly status ที่ executive อ่านเร็วได้*

```
Write a status report.
Project: [name]
Period: [dates]
Accomplishments: [list]
On track items: [list]
At risk: [describe issues]
Next period focus: [list]
Format: RAG status per workstream, max 1 page
```
*Status report ที่ executive อ่านใน 2 นาที*

---

### #08 Stakeholder Update — update ผู้เกี่ยวข้อง
*ต้องแจ้งข้อมูลสำคัญให้ stakeholders หลาย group*

```
Write a stakeholder update email.
Audience: [describe their background and concerns]
News to share: [describe update]
Positive aspects: [list]
Challenges/concerns: [list]
What you need from them: [ask]
Tone: transparent but reassuring
```
*Email ที่ address concerns ล่วงหน้า*

---

### #09 Job Description — เขียน JD ที่ดึงดูด candidate
*ต้องหาคนเข้าร่วมทีมและต้องการ JD ที่ดี*

```
Write a job description for: [role title]
Company context: [1-2 sentences]
Core responsibilities: [list 5-7]
Must-have qualifications: [list]
Nice-to-have: [list]
Culture/benefits highlights: [list]
Include: role overview, responsibilities, qualifications,
what makes this role unique, application instructions
```
*JD ที่ authentic และ attract ผู้สมัครที่ใช่*

---

### #10 Performance Review — เขียน review ที่ constructive
*ต้องเขียน performance review สำหรับ team member*

```
Write a performance review.
Employee: [role] | Period: [dates]
Strengths demonstrated: [list with examples]
Areas for development: [list]
Goals achieved: [list outcomes]
Goals missed + context: [explain]
Next period goals: [3 SMART goals]
Overall assessment: [1-5] | Tone: constructive
```
*Review ที่ specific, fair และ forward-looking*

---

### #11 Objection Handling — ตอบ objections ลูกค้า
*ลูกค้ามี objections ต่อ product/service ที่เสนอ*

```
Create objection handling responses for my product.
Product/service: [describe]
Objection 1: [paste objection]
Objection 2: [paste objection]
Objection 3: [paste objection]
For each: acknowledge + reframe + evidence + close
```
*Responses ที่ confident ไม่ defensive*

---

### #12 Cold Outreach — ส่งข้อความหา prospect ใหม่
*ต้องการ reach out หา leads ที่ไม่เคยติดต่อมาก่อน*

```
Write a cold outreach message.
Platform: [LinkedIn/email/other]
Recipient: [role + company + context]
My offering: [what I provide]
Specific reason for reaching out: [personalized hook]
Ask: [1 specific CTA, small ask]
Length: max 80 words. No buzzwords. No 'I hope this finds you well.'
```
*Cold message ที่ open rate สูงกว่า generic*

---

### #13 Executive Summary — สรุปรายงานสำหรับ C-suite
*มีรายงานยาวและต้องสรุปให้ผู้บริหารอ่านได้เร็ว*

```
Create an executive summary from this report.
<report>[paste report or key sections]</report>
Audience: C-suite with limited time
Format: Situation (1 sentence) | Findings (3 bullets)
       | Implications (2 bullets) | Recommendation (1 sentence)
Length: max 250 words
```
*Summary ที่ executive อ่านได้ใน 60 วินาที*

---

### #14 Change Communication — แจ้งการเปลี่ยนแปลงองค์กร
*ต้องสื่อสาร organizational change ให้ทีมรับได้*

```
Write a change communication message.
What is changing: [describe]
Why it's changing: [honest reasons]
Timeline: [when + milestones]
Impact on audience: [what changes for them]
What stays the same: [reassurance]
What support is available: [resources]
Tone: transparent, empathetic, forward-looking
```
*Communication ที่ลด resistance และ build trust*

---

### #15 Vendor Evaluation — เปรียบเทียบ vendors
*ต้องเลือก vendor และต้องการ structured comparison*

```
Create a vendor evaluation framework.
What we're buying: [describe]
Vendors to compare: [list]
Our top criteria: [list 5-7 with relative importance]
Budget constraint: [range]
Create: scoring matrix, key questions to ask each vendor,
red flags to watch for, recommendation framework
```
*Framework ที่ defensible สำหรับ decision makers*

---

## ก.2 Content Creation

*Social Media · Blog · Video · Newsletter · Ad Copy*

### #16 LinkedIn Post — เขียน post ที่ reach สูง
*ต้องการ LinkedIn post ที่ engage professionals*

```
Write a LinkedIn post about: [topic]
My professional angle: [your unique perspective]
Target audience: [job title/industry]
Format: Story + Insight + Practical takeaway
Length: 200-300 words
End with: 1 question to drive comments
No hashtag spam. No emojis every line.
```
*Post ที่ sounds human ไม่ใช่ AI-generated*

---

### #17 Twitter/X Thread — สร้าง thread ที่คนอยากอ่านต่อ
*ต้องการ thread ที่ educate และ entertain*

```
Write a Twitter thread about: [topic]
My unique take: [what makes this perspective different]
Target audience: [describe]
Thread length: [8-12 tweets]
Format: Tweet 1 = hook (bold claim/question)
Tweets 2-10 = teaching content
Last tweet = summary + CTA
Max 240 chars per tweet
```
*Thread ที่ share ได้และ grow following*

---

### #18 YouTube Script — เขียน script วิดีโอ
*ต้องการ script ที่ keep viewers watching ตลอด*

```
Write a YouTube video script about: [topic]
Video length: [X minutes]
Audience: [describe]
My style: [educational/entertaining/both]
Structure: Hook (30s) | Intro (1m) | Main content |
Midpoint hook | Conclusion + CTA
Include: B-roll suggestions, screen share moments
```
*Script พร้อม production cues*

---

### #19 TikTok Hook — เขียน hook 3 วินาที
*ต้องการ opening ที่หยุดคนเลื่อนได้*

```
Write 10 TikTok hook variations for video about: [topic]
Target: [age group, interest]
Hooks to try: curiosity gap, controversial statement,
relatable problem, surprising stat, direct address
Each hook: max 10 words
Mark top 3 with reasoning
```
*10 hooks หลากสไตล์ เลือกที่ fit กับ brand*

---

### #20 Blog Post — เขียน article ที่ rank บน Google
*ต้องการ SEO blog post ที่ helpful จริงๆ*

```
Write a blog post about: [topic]
Primary keyword: [keyword]
Target reader: [description + search intent]
Word count: [800-1500]
Structure: Hook + H2 sections + FAQ + Conclusion
Include: 1 internal link suggestion, 1 stat citation,
5 related keywords to include naturally
```
*Article ที่ rank และ read*

---

### #21 Newsletter Issue — สร้าง newsletter รายสัปดาห์
*ต้องส่ง newsletter ที่คนอยากเปิดทุกอาทิตย์*

```
Write a newsletter issue for: [newsletter name]
Topic this week: [describe]
My unique insight: [what I know that others don't]
Format: Hook (2 lines) | Main insight (200w) |
Quick win (3-5 sentences) | Resource of week | Question
Tone: Smart friend sharing what they learned
```
*Newsletter ที่ open rate สูงกว่า 30%*

---

### #22 Ad Copy — เขียน ad ที่ convert
*ต้องการ ad copy สำหรับ Meta, Google หรือ TikTok*

```
Write ad copy for: [product/service]
Platform: [Meta/Google/TikTok/Line]
Target audience: [description + pain point]
CTA: [desired action]
Budget: [premium/mid/budget positioning]
Provide: 3 variations
Variation A: Problem-aware | B: Solution-aware | C: Social proof
```
*3 variations ready to A/B test*

---

### #23 Product Description — เขียน description ที่ขายได้
*ต้องการ product description สำหรับ e-commerce*

```
Write a product description for: [product name]
Category: [type]
Target buyer: [description]
Key features: [list 3-5]
Price point: [range]
Platform: [Shopee/Lazada/Website]
Include: benefit headline, 3 feature bullets, story paragraph,
SEO-friendly title (60 chars)
```
*Description ที่ both discover-able และ convert*

---

### #24 Instagram Caption — เขียน caption กับ call to action
*ต้องการ caption ที่ match กับ visual content*

```
Write an Instagram caption.
Photo/video describes: [describe the visual]
Brand tone: [adjectives describing your style]
Target audience: [describe]
Goal: [awareness/engagement/click to bio]
Length: [short<50w / medium 50-150w / long 150-300w]
Include: 1 question, relevant hashtag strategy (5-10 tags)
```
*Caption ที่ complements visual ไม่ซ้ำกัน*

---

### #25 Press Release — เขียน press release มาตรฐาน
*มีข่าว announcement ที่ต้องส่งให้สื่อ*

```
Write a press release.
News: [describe announcement]
Company: [name + 1-line description]
Key spokesperson quote: [provide or ask Claude to draft]
Supporting data: [any numbers or proof points]
Standard format: Headline, Dateline, Lead paragraph,
Body (3-4 paragraphs), Quote, Boilerplate, Contact
```
*Press release ตาม AP style*

---

### #26 FAQ Section — สร้าง FAQ ที่ตอบจริง
*ต้องการ FAQ ที่ address concerns ก่อนที่ user จะถาม*

```
Create a FAQ section for: [product/service/topic]
Target audience: [description]
Their top concerns: [list what they worry about]
Tone: [conversational/formal]
Write 10 Q&A pairs. Each answer: 2-4 sentences.
Include: practical, pricing, and trust questions
```
*FAQ ที่ลด support tickets และเพิ่ม conversion*

---

### #27 Case Study — เขียน customer success story
*มี client result ที่อยากใช้เป็น social proof*

```
Write a case study.
Client: [industry, size — no name if confidential]
Challenge they faced: [describe problem]
Solution we provided: [describe]
Results: [specific numbers]
Timeline: [how long]
Structure: Challenge | Solution | Results | Quote | Learnings
Length: 400-600 words
```
*Case study ที่ conversion-ready*

---

### #28 Podcast Show Notes — เขียน show notes + SEO
*มี podcast episode และต้องการ show notes ที่ดี*

```
Write show notes for this podcast episode.
Episode title: [title]
Guest: [name + credentials]
Key topics discussed: [list]
Timestamps: [provide or estimate]
Include: 3-sentence summary, key takeaways (5 bullets),
guest bio, episode links, SEO description (155 chars)
```
*Show notes ที่ rank บน Google Podcast search*

---

### #29 Email Subject Line — เพิ่ม open rate
*ต้องการ subject line ที่คนอยากเปิด*

```
Write 10 email subject lines for email about: [topic]
Audience: [describe]
Goal: [what you want them to do after opening]
Mix of: curiosity / benefit / urgency / personal / number
Max 50 chars each. Mark top 3 for A/B test.
```
*10 options ready to test*

---

### #30 Webinar Description — ดึงดูดให้คน register
*จัด webinar และต้องการ landing page copy*

```
Write a webinar description.
Topic: [title]
Host: [name + credentials]
Date/time: [details]
Key takeaways: [3-5 bullets]
Who should attend: [description]
Include: headline, subheadline, 3 problem statements,
3 learning outcomes, speaker bio, FAQ (3 questions)
```
*Landing page copy ที่ conversion rate ดี*

---

## ก.3 Analysis & Research

*Data Analysis · Market Research · Competitive Intel · Decision Making*

### #31 Data Pattern Analysis — วิเคราะห์ข้อมูลหา insights
*มี data และต้องการ insights ที่ actionable*

```
Analyze this data and find actionable insights.
<data>[paste data or describe dataset]</data>
Context: [what this data represents]
Key questions: [what you want to understand]
Provide: top 3 patterns, 1 anomaly, 3 recommendations
Format: finding + evidence + so-what per insight
```
*Insights ที่ business team เข้าใจและใช้งานได้*

---

### #32 Competitive Analysis — วิเคราะห์คู่แข่ง
*ต้องการเข้าใจ competitive landscape ก่อนตัดสินใจ*

```
Analyze competitors for: [product/service/market]
Competitors: [list 3-5]
My company: [brief description]
Analyze each on: positioning, pricing, strengths,
weaknesses, target customer, key messages
Conclude: gaps in market, our best opportunity,
3 strategic moves to differentiate
```
*Competitive map ที่ strategic*

---

### #33 SWOT Analysis — วิเคราะห์ก่อนตัดสินใจ
*กำลังพิจารณา strategic decision ที่ต้องการ SWOT*

```
Create a SWOT analysis for: [topic/company/decision]
Context: [describe situation]
Internal info: [what you know about strengths/weaknesses]
External info: [market/industry context]
For each quadrant: 5 specific points
Conclude: top 2 strategic priorities based on this SWOT
```
*SWOT ที่ lead to action ไม่ใช่แค่ list*

---

### #34 Market Sizing — ประมาณขนาดตลาด
*ต้องการ market size estimate สำหรับ pitch หรือ planning*

```
Estimate the market size for: [product/service]
Geography: [country/region]
Target customer: [description]
Approach: Top-down (TAM/SAM/SOM) and bottom-up
Show assumptions clearly
Provide: best case, base case, conservative case
```
*Market sizing ที่มี assumptions transparent*

---

### #35 Customer Research Synthesis — สรุป customer feedback
*มี feedback จาก surveys/interviews และต้องสรุป*

```
Synthesize this customer research.
<feedback>[paste survey responses or interview notes]</feedback>
Research goal: [what you were trying to learn]
Provide: top 3 themes with evidence quotes,
key pain points ranked by frequency,
unmet needs, surprising findings,
recommended product/service changes
```
*Synthesis ที่ team นำไปใช้ตัดสินใจได้เลย*

---

### #36 Financial Analysis — วิเคราะห์ตัวเลขการเงิน
*มี financial data และต้องการ interpretation*

```
Analyze these financial figures.
<financials>[paste financial data]</financials>
Company context: [industry, size, stage]
Key metrics to analyze: revenue growth, margins, burn rate
Compare to: industry benchmarks if known
Flag: concerning trends, positive indicators,
3 questions management should answer
```
*Analysis ที่ investor หรือ board เข้าใจ*

---

### #37 Root Cause Analysis — หาต้นเหตุของปัญหา
*เกิดปัญหาซ้ำๆ และต้องการหาสาเหตุที่แท้จริง*

```
Conduct a root cause analysis for: [problem]
Symptoms observed: [describe what you see]
When it started: [timeline]
What changed recently: [context]
Use 5-Whys methodology
Provide: likely root cause(s), contributing factors,
recommended fixes ranked by impact vs effort
```
*RCA ที่ fix ปัญหาได้ permanent*

---

### #38 Survey Design — ออกแบบ survey ที่ได้ข้อมูลดี
*ต้องการ survey ที่ได้ข้อมูลที่ใช้ได้จริง*

```
Design a survey to measure: [objective]
Respondents: [who will answer]
Length: max [N] minutes
Include: screening question, Likert scales,
1-2 open-ended questions
Avoid: leading questions, double-barreled questions
Provide: 10-15 questions with response options
```
*Survey ที่ response rate ดีและ data clean*

---

### #39 Decision Matrix — เปรียบเทียบตัวเลือก
*ต้องตัดสินใจระหว่างหลายทางเลือกอย่าง objective*

```
Create a decision matrix for: [decision]
Options to evaluate: [list 3-5]
Key criteria: [list 5-7 criteria]
Weight each criterion (total = 100%)
Score each option per criterion (1-5)
Show calculation and recommendation
Include: key risks per top option
```
*Decision matrix ที่ defensible กับ stakeholders*

---

### #40 Scenario Planning — วางแผนรับมือหลาย scenarios
*ต้องการ plan ที่รับมือได้กับ future uncertainty*

```
Create scenario plans for: [situation]
Timeframe: [planning horizon]
Key uncertainties: [2-3 major unknowns]
Create 3 scenarios: Optimistic | Base | Pessimistic
For each: probability, key assumptions,
strategic response, early warning signs
```
*Scenarios ที่ trigger-based ไม่ใช่แค่ story*

---

### #41 Literature Review — สรุปงานวิจัย
*ต้องการ synthesis ของ research papers หลายชิ้น*

```
Synthesize these research findings.
<papers>[paste abstracts or key sections]</papers>
Research question: [what you're trying to answer]
Provide: consensus findings, contradictions,
methodological limitations, gaps in literature,
implications for [your context]
Format: narrative synthesis, not just summary
```
*Literature review ที่ advance ความเข้าใจ*

---

### #42 Trend Analysis — วิเคราะห์ trend ในอุตสาหกรรม
*ต้องการเข้าใจ trends ที่จะกระทบ business*

```
Analyze trends affecting: [industry/sector]
Timeframe: [next 2-5 years]
My company: [brief context]
Provide: 5 macro trends, impact assessment per trend,
opportunities created, threats to prepare for,
3 strategic recommendations
```
*Trend analysis ที่ actionable*

---

### #43 Risk Assessment — ประเมินความเสี่ยง
*ต้องการ risk assessment ก่อน launch หรือ decision*

```
Create a risk assessment for: [project/decision]
Scope: [describe what's being assessed]
Stakeholders: [who is affected]
For each risk: description, likelihood (1-5),
impact (1-5), risk score, owner, mitigation action
Identify top 5 risks to prioritize
```
*Risk register ที่ actionable*

---

### #44 Customer Journey Map — map ประสบการณ์ลูกค้า
*ต้องการเข้าใจ touchpoints ในการ journey ของ customer*

```
Create a customer journey map.
Customer persona: [description]
Journey stage: [awareness through retention]
For each stage: touchpoints, customer goal,
emotion (frustrated/neutral/delighted),
our actions, improvement opportunities
```
*Journey map ที่ highlight moments of truth*

---

### #45 A/B Test Analysis — วิเคราะห์ผล experiment
*ทำ A/B test เสร็จแล้วและต้องการ interpretation*

```
Analyze this A/B test result.
Hypothesis: [what you were testing]
Variant A: [control] | Variant B: [test]
Results: [conversion rates, sample size, duration]
Provide: statistical significance assessment,
practical significance, recommendation,
follow-up tests to consider
```
*Analysis ที่ confident กับ decision*

---

## ก.4 Coding & Technical

*Code Generation · Review · Debug · Documentation · Architecture*

### #46 Function Generator — เขียน function ที่สมบูรณ์
*ต้องการ function พร้อม type hints, docstring และ tests*

```
Write a Python function that: [describe what it should do]
Input: [describe parameters and types]
Output: [describe return value and type]
Edge cases to handle: [list]
Include: type hints, Google-style docstring,
3 unit tests (happy path, edge case, error case)
```
*Production-ready function ที่ทำงานได้*

---

### #47 Code Review — review code อย่าง systematic
*ต้องการ thorough code review ก่อน merge*

```
Review this code systematically.
<code>[paste code]</code>
Language: [language] | Context: [what it does]
Review for: bugs (must fix), security (must fix),
performance (should fix), readability (nice to fix)
For each issue: line number + problem + suggested fix
```
*Review ที่ prioritized และ actionable*

---

### #48 Bug Diagnosis — หา root cause ของ bug
*มี bug ที่ reproduce ได้และต้องการ diagnosis*

```
Help me diagnose this bug.
Code: <code>[paste relevant code]</code>
Error message: [paste error]
Expected behavior: [describe]
Actual behavior: [describe]
What I've tried: [list attempts]
Provide: likely root cause, fix, how to test the fix
```
*Diagnosis พร้อม fix ที่ verified*

---

### #49 SQL Query — เขียน query ที่ efficient
*ต้องการ SQL query สำหรับ data analysis*

```
Write a SQL query for: [describe what data you need]
Database: [PostgreSQL/MySQL/BigQuery/etc.]
Tables available: [list with key columns]
Filters needed: [describe conditions]
Output format: [columns, aggregations, sorting]
Include: comments explaining complex joins,
performance notes if relevant
```
*Query ที่ correct และ optimized*

---

### #50 API Design — ออกแบบ REST API
*ต้องการ design API สำหรับ new service*

```
Design a REST API for: [service name and purpose]
Core entities: [list main objects]
Key operations: [CRUD + special operations]
Auth requirements: [describe]
Provide: endpoint list with methods,
request/response schemas for each,
error codes and messages, versioning strategy
```
*API design ที่ follow REST best practices*

---

### #51 Regex Pattern — เขียน pattern ที่ match ถูกต้อง
*ต้องการ regex สำหรับ validation หรือ extraction*

```
Write a regex pattern for: [describe what to match]
Examples that SHOULD match: [list]
Examples that should NOT match: [list]
Language: [Python/JavaScript/PHP/etc.]
Include: the pattern, explanation of each part,
Python code snippet to use it
```
*Regex ที่ tested กับ examples*

---

### #52 Database Schema — ออกแบบ schema
*ต้องการ database design สำหรับ new application*

```
Design a database schema for: [application]
Core features: [list main features]
Expected data volume: [rough estimate]
Database: [PostgreSQL/MySQL/MongoDB/etc.]
Create: tables/collections with columns/fields,
data types, constraints, indexes,
explain normalization decisions
```
*Schema ที่ scalable และ normalized*

---

### #53 Error Handling — เพิ่ม error handling ที่ robust
*มี code ที่ยังไม่มี proper error handling*

```
Add robust error handling to this code.
<code>[paste code]</code>
Context: [what this code does, where it runs]
Expected error types: [list if known]
Add: specific exception handling, logging,
user-friendly error messages, retry logic if appropriate
Show before and after
```
*Code ที่ handle failures gracefully*

---

### #54 Refactor — ปรับ code structure ให้ดีขึ้น
*มี legacy code ที่ works แต่ maintain ยาก*

```
Refactor this code for better maintainability.
<code>[paste code]</code>
Issues to address: [God function / duplicate code / poor naming / etc.]
Constraints: [must keep backward compatible / no new dependencies]
Show: original, refactored, and what changed + why
```
*Refactored code พร้อม explanation*

---

### #55 Test Cases — เขียน test coverage
*ต้องการ test suite ที่ครอบคลุม edge cases*

```
Write comprehensive tests for this function.
<code>[paste function]</code>
Test framework: [pytest/jest/mocha/etc.]
Include: happy path, boundary values, error cases,
type mismatches if relevant
Each test: descriptive name + arrange-act-assert
```
*Test suite ที่ catch real bugs*

---

### #56 README Documentation — เขียน README ที่ชัดเจน
*มี project ที่ต้องการ documentation ที่ดี*

```
Write a README for this project.
Project: [name + 1-line description]
Tech stack: [list]
Sections: Overview, Prerequisites, Installation,
Configuration, Usage (with examples), API Reference,
Contributing, License
Tone: developer-friendly, concise
```
*README ที่ onboard developer ได้ทันที*

---

### #57 Performance Optimization — หา bottleneck
*มี code ที่ช้าและต้องการ optimize*

```
Identify performance bottlenecks in this code.
<code>[paste code]</code>
Current performance: [describe issue]
Language/runtime: [describe]
Provide: bottlenecks ranked by impact,
optimization suggestions with trade-offs,
what to benchmark to verify improvement
```
*Analysis พร้อม concrete optimizations*

---

### #58 System Design — วาง architecture สำหรับ system
*ต้องการ high-level design สำหรับ new system*

```
Design a system for: [describe the system]
Scale requirements: [users, requests/sec, data volume]
Non-functional requirements: [availability, latency, etc.]
Provide: component diagram (text format),
tech choices with rationale,
data flow, failure modes + mitigations,
what to defer to v2
```
*Design ที่ pragmatic และ scalable*

---

### #59 Code Translation — แปลง code ระหว่าง languages
*ต้องการ port code จาก language หนึ่งไปอีก language*

```
Translate this code from [source language] to [target language].
<code>[paste source code]</code>
Preserve: logic, behavior, error handling
Apply: idiomatic patterns of the target language
Note: any behaviors that differ between languages
```
*Translation ที่ idiomatic ไม่ใช่ literal*

---

### #60 Cron Job / Scheduler — เขียน scheduled task
*ต้องการ task ที่รันอัตโนมัติตามเวลา*

```
Write a scheduled task that: [describe task]
Schedule: [cron expression or description]
Language/platform: [Python/Node/etc.]
Include: error handling, logging, retry on failure,
notification on success/failure, idempotency
```
*Scheduled task ที่ production-ready*

---

## ก.5 Writing & Editing

*Copy Editing · Style · Clarity · Simplification · Translation*

### #61 Clarity Edit — ทำให้ประโยคชัดขึ้น
*มี text ที่ complex และต้องการให้อ่านง่ายขึ้น*

```
Edit this text for clarity and conciseness.
<text>[paste text]</text>
Target: cut 20%, improve clarity
Rules: shorter sentences (max 20 words avg),
active voice, concrete over abstract,
remove jargon unless necessary
Show: original → edited with change rationale
```
*Text ที่ชัดขึ้นและสั้นลง 20%*

---

### #62 Tone Adjustment — ปรับ tone ให้เหมาะกับ audience
*มี text ที่ tone ไม่ตรงกับ audience*

```
Adjust the tone of this text.
<text>[paste text]</text>
Current tone: [describe]
Target tone: [formal/casual/empathetic/authoritative]
Audience: [describe]
Preserve: the core message and all facts
Change: vocabulary, sentence structure, examples
```
*Same content, different vibe*

---

### #63 Plain Language — แปลง jargon เป็นภาษาที่เข้าใจง่าย
*มี technical text ที่ต้องทำให้คนทั่วไปอ่านได้*

```
Rewrite this in plain language.
<text>[paste technical text]</text>
Original audience: [experts]
New audience: [general public / 8th grade reading level]
Keep: accuracy and all key information
Replace: jargon with simple words
Add: analogies where helpful
```
*Text ที่ reading level ลดลงโดยไม่เสียความหมาย*

---

### #64 Grammar & Style — แก้ grammatical errors
*มี text ที่ต้องการ proofreading ครั้งสุดท้าย*

```
Proofread and correct this text.
<text>[paste text]</text>
Style guide: [AP/Chicago/Oxford/company style or none]
Fix: grammar, punctuation, spelling
Flag: style inconsistencies, awkward phrasing
Show corrections in [BRACKETS] or as tracked changes
```
*Error-free text พร้อม submit*

---

### #65 Summarization — สรุปให้สั้นและครบ
*มี document ยาวและต้องการ summary หลายระดับ*

```
Summarize this document.
<document>[paste document]</document>
Audience: [who will read the summary]
Create 3 versions: 1-sentence, 3-sentence, 1-paragraph
Each must: capture the main argument,
not add new information,
use simpler language than original
```
*3 summaries เลือกใช้ตาม context*

---

### #66 Expand — ขยาย outline เป็น full text
*มี bullet points และต้องการ full paragraphs*

```
Expand these bullet points into full prose.
<bullets>[paste bullet points]</bullets>
Target length: [X words]
Tone: [describe]
Add: smooth transitions, supporting examples,
topic sentences per paragraph
Don't: add new facts not in bullets
```
*Full text ที่ flows naturally*

---

### #67 Passive to Active — เปลี่ยน passive เป็น active
*มี text ที่ passive voice ทำให้อ่านยาก*

```
Convert passive voice to active in this text.
<text>[paste text]</text>
Identify: all passive constructions
Convert: to active where it improves clarity
Keep passive: when active would be awkward
Show: list of changes made
```
*Text ที่ direct และ vivid กว่าเดิม*

---

### #68 Thai-English Translation — แปลคุณภาพสูง
*ต้องการ translation ที่ natural ไม่ใช่ word-for-word*

```
Translate this from [Thai/English] to [English/Thai].
<source>[paste source text]</source>
Audience: [describe]
Tone: [formal/casual/technical]
Preserve: tone, cultural nuances, technical terms
Note: terms I want kept in original language: [list]
```
*Translation ที่ native speakers ยอมรับ*

---

### #69 Paraphrase — เขียนใหม่โดยไม่ lose meaning
*ต้องการ paraphrase เพื่อหลีกเลี่ยง plagiarism หรือ repetition*

```
Paraphrase this text.
<text>[paste text]</text>
Change: sentence structure, vocabulary, organization
Keep: all facts and arguments
Level: [light / medium / complete rewrite]
```
*Text ที่ different surface, same substance*

---

### #70 Headline/Title Optimization — เพิ่ม click-through
*ต้องการ title ที่คนอยากคลิก*

```
Write 10 headline variations for: [topic/article/content]
Audience: [describe]
Goal: [inform/persuade/entertain]
Mix styles: how-to, list, question, provocative, benefit
Max 60 chars each. Mark top 3 for testing.
```
*10 headlines ready for A/B test*

---

### #71 Speech Writing — เขียน speech สำหรับงาน
*ต้องกล่าว speech ในงาน event สำคัญ*

```
Write a speech for: [occasion]
Speaker: [your role]
Audience: [description]
Key message: [1 sentence]
Duration: [X minutes]
Include: opening hook, 3 main points, personal story,
memorable closing, no filler phrases
```
*Speech ที่ delivered ได้ naturally*

---

### #72 Academic Abstract — เขียน abstract งานวิจัย
*มี research paper และต้องการ abstract มาตรฐาน*

```
Write an academic abstract for this paper.
<paper>[paste introduction and conclusion]</paper>
Journal target: [describe field]
Word limit: [max words]
Structure: Background, Objective, Methods,
Results, Conclusion, Keywords (5-8 terms)
```
*Abstract ที่ follows academic conventions*

---

### #73 Cover Letter — เขียน cover letter ที่โดดเด่น
*สมัครงานและต้องการ cover letter ที่ memorable*

```
Write a cover letter.
Job: [title + company]
Key requirements from JD: [list 3 must-haves]
My relevant experience: [describe]
Why this company specifically: [personalized reason]
My unique value: [what I bring that others don't]
Tone: professional but personal, not template
```
*Cover letter ที่ get interview*

---

### #74 Executive Bio — เขียน bio สำหรับ events
*ต้องการ professional bio สำหรับ website หรือ speaker deck*

```
Write a professional bio.
Name and current role: [describe]
Career highlights: [top 3 achievements]
Areas of expertise: [list]
Unique angle: [what makes you different]
Length: [50 words / 150 words / 300 words]
POV: [first person / third person]
```
*Bio ที่ establish authority naturally*

---

### #75 Apology Communication — เขียน apology อย่างมืออาชีพ
*เกิดข้อผิดพลาดและต้องการ apologize อย่างเหมาะสม*

```
Write a professional apology.
What happened: [describe mistake/issue]
Who was affected: [customer/partner/employee]
Impact: [what it caused]
Corrective action taken: [what you've done/will do]
Tone: sincere, accountable, forward-looking
Don't: over-promise, make excuses, be defensive
```
*Apology ที่ restore trust*

---

## ก.6 Productivity & Operations

*Planning · Organization · Learning · Problem Solving · Process*

### #76 Project Planning — วาง project plan ที่ realistic
*ต้องการ project plan ก่อนเริ่มงาน*

```
Create a project plan for: [project name]
Goal: [specific outcome]
Timeline: [start to end date]
Team: [roles available]
Key constraints: [budget, resources, dependencies]
Include: milestones, tasks per milestone,
risk items, assumptions, success metrics
```
*Plan ที่ realistic และ trackable*

---

### #77 Weekly Planning — organize สัปดาห์ให้มีประสิทธิภาพ
*ต้องการ structure สัปดาห์ให้ get things done*

```
Help me plan my week.
My goals this week: [list 3 main goals]
Meetings already scheduled: [list with duration]
Tasks outstanding: [list with estimated time]
Energy pattern: [am person/pm person]
Create: daily schedule with deep work blocks,
task batching, buffer time, and end-of-day review
```
*Week plan ที่ balanced*

---

### #78 Problem Solving — สร้าง solution ด้วย structured framework
*มีปัญหาที่ยากและต้องการ systematic approach*

```
Help me solve this problem systematically.
Problem: [describe clearly]
Constraints: [what limits your options]
Resources available: [time, people, budget]
What I've already tried: [list]
Use: Define > Causes > Options > Evaluate > Plan
Output: top 3 solutions with pros/cons + recommended next step
```
*Solution ที่ addressable ทันที*

---

### #79 Learning Plan — สร้าง self-study curriculum
*ต้องการ learn topic ใหม่อย่างมีระบบ*

```
Create a learning plan for: [skill/topic]
Current level: [beginner/intermediate/advanced]
Goal: [what competency you want to achieve]
Time available: [hours per week]
Timeline: [total weeks/months]
Include: phased curriculum, resources per phase,
practice exercises, milestone checkpoints
```
*Learning roadmap ที่ follow ได้จริง*

---

### #80 Brainstorming — generate ideas อย่างรวดเร็ว
*ต้องการ ideas จำนวนมากก่อนกรอง*

```
Generate ideas for: [topic/challenge]
Context: [background information]
Constraints: [any limits]
Mode: [wild ideas / practical / combination]
Quantity: 20 ideas minimum
After listing: group by theme, mark top 5,
suggest how to combine 2-3 ideas
```
*20+ ideas with clustering*

---

### #81 Prioritization — จัด priority ด้วย impact-effort
*มีหลายงานและต้องการ decide ว่าทำอะไรก่อน*

```
Help me prioritize these tasks/initiatives.
Items: [list all tasks]
Goal: [what you're trying to achieve]
Score each on: Impact (1-5) × Ease (1-5)
Plot into: Quick Wins, Big Bets, Fill-ins, Don'ts
Recommend: top 3 to focus on this sprint
```
*Clear priority ranking พร้อม reasoning*

---

### #82 Process Documentation — เขียน process ให้คนอื่นทำได้
*มี process ที่ต้องการ document ให้ทีมใช้*

```
Document this process.
Process: [describe in your words]
Frequency: [how often it's done]
Roles involved: [list]
Tools used: [list]
Write: overview, step-by-step instructions,
decision points, common errors, shortcuts
```
*Process doc ที่ใครก็ทำได้*

---

### #83 Feedback Synthesis — รวบรวม feedback และสรุป themes
*ได้รับ feedback จากหลายคนและต้องสรุป*

```
Synthesize this feedback.
<feedback>[paste feedback from multiple sources]</feedback>
Context: [what was being evaluated]
Group into: strengths, weaknesses, opportunities
Find: top 3 themes with supporting examples
Recommend: 3 specific actions based on feedback
```
*Synthesis ที่ actionable*

---

### #84 Delegation Brief — มอบหมายงานอย่างชัดเจน
*ต้องการ delegate งานให้ทีมโดยไม่ต้อง micromanage*

```
Create a delegation brief for: [task]
Delegating to: [role]
Task description: [detailed description]
Success criteria: [what 'done' looks like]
Deadline: [date]
Resources provided: [what support you give]
Check-in points: [when to update you]
Authority level: [recommend/inform/decide independently]
```
*Brief ที่ empower ไม่ใช่ micromanage*

---

### #85 Retrospective — สรุปบทเรียนหลัง project
*จบ project หรือ sprint และต้องการ structured retro*

```
Facilitate a retrospective.
Project/sprint: [describe]
Team size: [N people]
Duration: [X months/weeks]
Input: [paste any notes, outcomes, metrics]
Structure: What went well, What to improve,
Surprises, Process improvements, Action items
Format as: team discussion guide with questions
```
*Retro guide ที่ generate real learnings*

---

### #86 OKR Writing — เขียน OKRs ที่วัดได้
*ต้องการ OKRs ที่ clear และ motivating*

```
Write OKRs for: [team/company/individual]
Quarter: [Q]
Context: [company strategy + current challenges]
Draft objective: [your rough idea]
Refine to: 1 aspirational objective (not measurable)
3-5 Key Results (measurable, numeric, ambitious)
Each KR: baseline → target
```
*OKRs ที่ motivate และ measure*

---

### #87 SLA Definition — กำหนด service levels
*ต้องการ define SLAs สำหรับ service หรือ support*

```
Define SLAs for: [service type]
Service: [describe what is being provided]
Customers: [internal/external, their expectations]
Define: response time, resolution time per priority,
measurement method, escalation path,
reporting frequency, consequences of breach
```
*SLA document ที่ clear และ fair*

---

### #88 Onboarding Plan — plan ต้อนรับพนักงานใหม่
*มีพนักงานใหม่เข้าและต้องการ onboarding ที่ดี*

```
Create an onboarding plan for a new [role].
Team: [team name] | Start date: [date]
First month goals: [what they should achieve]
Key stakeholders to meet: [list with purpose]
Systems to set up: [list]
Include: Day 1, Week 1, Month 1 structure,
buddy assignment, 30-day check-in agenda
```
*Onboarding ที่ ramp up ได้เร็ว*

---

### #89 Budget Allocation — วางงบประมาณ
*ต้องการ allocate budget อย่าง strategic*

```
Help me allocate this budget.
Total budget: [amount]
Period: [timeframe]
Business goals: [list 3-5 priorities]
Current spending by category: [if known]
Recommend: allocation by category with rationale,
ROI expectation per category,
what to cut if 20% reduction required
```
*Budget allocation ที่ strategic*

---

### #90 Post-Mortem — วิเคราะห์หลัง incident
*เกิด incident และต้องการ learn โดยไม่ blame*

```
Write a post-mortem for: [incident]
Date/time: [when]
Impact: [describe what was affected]
Timeline: [sequence of events]
Root causes: [what caused it]
Detection: [how it was found]
Format: blameless. Focus on: what happened,
why, how to prevent, action items with owners
```
*Post-mortem ที่ prevent recurrence*

---

## Related
- [[concepts/claude-safety-pitfalls]]
- [[skills/claude-mini-workflows]]
- [[concepts/prompt-engineering]]
- [[references/claude-complete-guide-2026]]
- [[concepts/claude-custom-skills]]
