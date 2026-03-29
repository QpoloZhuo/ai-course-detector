---
name: ai-course-detector
description: Evaluates whether an AI course is worth taking or is a low-value cash-grab. Use this skill whenever a user shares a course URL, sales page text, or asks whether an AI course is worth buying. Trigger phrases include "is this course worth it", "is this a scam", "evaluate this course", "should I buy this", or any AI course URL or description being shared for review.
---

# AI Course Quality Detector Skill

## What This Skill Does

Analyzes an AI course sales page or description across two dimensions:
1. **Course quality**: Nine weighted indicators, scored out of 100
2. **Personal fit**: Whether this specific course is worth it for *this specific person*

---

## Execution Flow

### Step 1: Get Course Content

If the user provides a URL, use `web_fetch` to retrieve the sales page.
If the user pastes course content directly, proceed to Step 2.

### Step 2: Understand the User's Background

Before analyzing, ask the user these questions in a single message:

> Before I evaluate this course, I need to understand where you're coming from:
>
> 1. **What's your current AI skill level?**
>    - Beginner: Occasionally use ChatGPT to ask questions
>    - Intermediate: Use AI regularly to assist with work, have established habits
>    - Advanced: Design prompts, use APIs, or build automation workflows
>
> 2. **Do you have a real work need related to this course's topic?** (Yes/No, or brief description)
>
> 3. **Is the price within your acceptable range?**

---

### Step 3: Score on Nine Indicators (100 points total)

---

#### 🔴 W1. Integrity of Benefit Claims (10 pts)

Does the course make honest, grounded claims about learning outcomes?

| Grade | Score | Criteria |
|-------|-------|----------|
| Excellent | 10 | Benefits are tied to specific contexts with clear conditions and prerequisites stated |
| Good | 7 | Specific numbers given but no methodology explained (e.g. "save 3 hours/day" with no explanation of how) |
| Poor | 3 | Numbers exist but the math is suspicious (e.g. using $10/hr to calculate "$70,000/year saved") |
| Failing | 0 | Pure vague claims ("10x or even 100x better") or emotional manipulation ("beat 90% of people") |

---

#### 🔴 W2. Content Scarcity (12 pts)

Is the course content actually unavailable for free elsewhere?

| Grade | Score | Criteria |
|-------|-------|----------|
| Excellent | 12 | Clear proprietary perspective, original organization logic, or instructor's own battle-tested methodology |
| Good | 8 | Partially differentiated, but the backbone is still repackaged official docs or free tutorials |
| Poor | 4 | Most content is freely available on YouTube, official docs, or forums |
| Failing | 0 | Core content is essentially a translated/rephrased version of official documentation |

---

#### 🔴 W3. Audience Specificity (8 pts)

Does the course clearly define its target audience, and does the content actually serve them?

| Grade | Score | Criteria |
|-------|-------|----------|
| Excellent | 8 | Audience is clearly defined; difficulty, examples, and language all match that audience |
| Good | 5 | Audience is named, but some content drifts (e.g. claims "no coding required" but syllabus has unexplained jargon) |
| Poor | 2 | Vague audience definition ("anyone who wants to be more productive") |
| Failing | 0 | "Suitable for everyone" — no filtering whatsoever |

---

#### 🔴 W4. Instructor Credibility (15 pts)

Does the instructor have verifiable, real-world results?

| Grade | Score | Criteria |
|-------|-------|----------|
| Excellent | 15 | Publicly verifiable work (live products, client case studies, portfolio) directly related to the course topic |
| Good | 10 | Public presence and audience, but insufficient hands-on work in the specific course domain |
| Poor | 5 | Only self-reported background; no third-party verifiable evidence |
| Failing | 0 | Instructor is almost unfindable, or credibility is based solely on student testimonials from other courses |

> If verification is needed, use `web_search` with the instructor's name + relevant keywords

---

#### 🟢 V1. Tangible Deliverables (10 pts)

What can students actually take away when the course ends?

| Grade | Score | Criteria |
|-------|-------|----------|
| Excellent | 10 | Walk away with a deployable tool, template, or Skill — usable the next day |
| Good | 7 | Clear deliverable but requires additional customization before real-world use |
| Poor | 3 | Abstract deliverables ("develop a mental framework", "learn to judge") |
| Failing | 0 | Knowledge transfer only — no concrete output whatsoever |

---

#### 🟢 V2. Quality of Practical Demonstrations (18 pts)

This is the highest-weighted indicator. Don't just check whether demos exist — evaluate whether each use case actually *requires* AI to solve, and whether the instructor demonstrates the thinking behind their tool choices.

For each demo case, ask three questions:

**Q1. Is there a simpler solution?**
Could this task be done easily with existing tools (native Notion features, Zapier, Google Sheets formulas, off-the-shelf SaaS)? If so, does adding AI bring meaningful improvement — or does it just take a longer route?
— Red flag example: "YouTube video → structured notes" → Whisper or Otter.ai handles this directly; no Agent workflow needed

**Q2. Is this a real recurring pain point, or just a tech demo?**
Does this workflow solve a genuine, high-frequency work problem? Or is it a "wow, you can do this too" demo that almost nobody actually needs in their daily work?
— Red flag example: "AI auto-controls browser to screenshot price comparisons" → unstable, hard to maintain, better alternatives exist

**Q3. Does the instructor explain *why* they chose this approach?**
Good demos don't just show *how* to do something — they explain the reasoning behind the tool choice: why not use a simpler solution, and what the tradeoffs are. Without this layer, students will be stuck the moment their situation differs slightly.

| Grade | Score | Criteria |
|-------|-------|----------|
| Excellent | 18 | Most cases address real high-frequency needs, no obvious simpler alternatives, and instructor explains the reasoning behind tool choices |
| Good | 12 | Real needs are addressed, but some cases have simpler alternatives, or the instructor never explains "why this approach" |
| Poor | 6 | Cases lean toward tech showmanship; most problems have more direct solutions |
| Failing | 0 | Cases are just a feature list; no real pain points addressed; or all problems have simpler non-AI solutions |

---

#### 🟢 V3. Technical Depth (12 pts)

Does the syllabus lay out a concrete technical path, or just list features?

| Grade | Score | Criteria |
|-------|-------|----------|
| Excellent | 12 | Syllabus clearly explains setup steps for each stage; students can predict they'll be able to reproduce independently |
| Good | 8 | Specific tool names are mentioned, but configuration process is unclear |
| Poor | 4 | Syllabus is mostly feature descriptions ("you'll learn how AI helps you do X") without a technical path |
| Failing | 0 | Completely generic syllabus — could apply to any AI tool on the market |

---

#### 🟢 V4. Post-Purchase Support (5 pts)

| Grade | Score | Criteria |
|-------|-------|----------|
| Excellent | 5 | Ongoing update mechanism + active community with instructor participation |
| Good | 3 | Student community exists, but engagement level is unclear |
| Poor | 1 | Recording replay only — no community or Q&A |
| Failing | 0 | No post-purchase support whatsoever |

---

#### 🟢 V5. AI Tool Efficiency Awareness (10 pts)

This indicator evaluates whether the instructor understands the *cost* of using AI — not just money, but efficiency cost and architectural cost. A mature AI practitioner knows that AI Agents aren't a universal hammer: sometimes a direct tool is faster, more stable, and cheaper in tokens than routing everything through AI.

**Core question: Does the instructor know when to use AI and when not to?**

**Tool selection judgment**
Does the instructor distinguish between tasks where AI is native vs. tasks where routing through AI creates unnecessary overhead?
- AI-native tasks: semantic understanding, content generation, judgment-based logic
- Not AI-native: operating interfaces, filling fixed forms, fetching structured data → MCP / API / existing tools are more stable

**MCP vs. Prompt-based operation awareness**
- ❌ Using prompts to have AI take screenshots → decide where to click → operate Canva: extremely high token consumption, unstable, prone to failure
- ✅ Calling Canva MCP directly: one instruction, precise execution, minimal token cost

If a course uses AI to operate UI interfaces as a selling point but never mentions MCP or direct API alternatives, this is a clear red flag.

**Token cost awareness**
Every AI action has a cost. A good course teaches students how to design lean workflows — not that more AI steps = more impressive.

| Grade | Score | Criteria |
|-------|-------|----------|
| Excellent | 10 | Explicitly discusses tool selection logic; distinguishes where AI fits vs. doesn't; demonstrates MCP / direct API knowledge with comparison |
| Good | 7 | Some tool selection judgment present, but not systematic; or mentions MCP without explaining when to use it |
| Poor | 3 | Tool selection is driven purely by "AI can do it" rather than "AI is the right choice"; uses AI to operate UIs without mentioning more efficient alternatives |
| Failing | 0 | Routing everything through AI is the selling point; zero efficiency cost awareness; actively teaches students to use AI for tasks that could call an API directly |

> Note: V5 is an advanced indicator. For courses clearly targeting complete beginners, the "Poor" threshold can be applied more leniently.

---

### Step 4: Personal Fit Analysis

Based on the user's background, evaluate whether this course is right for *them*:

| User Level | Course Level | Fit |
|-----------|-------------|-----|
| Beginner | Beginner course | ✅ Good fit |
| Beginner | Advanced course | ⚠️ May not keep up |
| Intermediate | Beginner course | ❌ Waste of money |
| Intermediate | Intermediate course | ✅ Good fit |
| Advanced | Beginner–Intermediate | ❌ Almost no value |
| Advanced | Advanced course | ✅ Check the differentiated parts |

Additional considerations:
- Does the user have a real work need for this topic? (No need = won't use what they learn)
- Course price vs. self-study alternative (what could they learn in the same time for free?)

---

### Step 5: Output the Evaluation Report

## 📊 AI Course Evaluation Report

**Course Name**: [Name]
**Evaluated**: [Date]

### Total Score: XX / 100

| Category | Indicator | Score | Max | Notes |
|----------|-----------|-------|-----|-------|
| 🔴 Warning | W1. Benefit claim integrity | X | 10 | ... |
| 🔴 Warning | W2. Content scarcity | X | 12 | ... |
| 🔴 Warning | W3. Audience specificity | X | 8 | ... |
| 🔴 Warning | W4. Instructor credibility | X | 15 | ... |
| 🟢 Quality | V1. Tangible deliverables | X | 10 | ... |
| 🟢 Quality | V2. Demo quality | X | 18 | ... |
| 🟢 Quality | V3. Technical depth | X | 12 | ... |
| 🟢 Quality | V4. Post-purchase support | X | 5 | ... |
| 🟢 Quality | V5. AI efficiency awareness | X | 10 | ... |

### 🎯 Personal Fit: [High / Medium / Low]

[One paragraph explaining why this course fits or doesn't fit this specific user]

### Final Recommendation

**[✅ Worth it / ⚠️ Conditionally worth it / ❌ Not recommended]**

[2–3 sentences. Direct. No filler.]

### If You Skip It: Alternatives

- [Free alternative 1]
- [Free alternative 2]
- [If spending money, a better investment direction]

---

## Scoring Bands

| Score | Verdict |
|-------|---------|
| 80–100 | High quality — worth the investment |
| 60–79 | Partial value — personal fit is the deciding factor |
| 40–59 | Proceed with caution — try free resources first |
| 0–39 | Cash-grab warning — not recommended |

---

## Important Notes

- Stay neutral — don't add points for "limited-time offer" or "great reviews"
- If the sales page has no public syllabus, give W3 / V3 the lowest grade
- To verify instructor background, use `web_search` with their name + relevant keywords
- The final recommendation must incorporate the user's background — never base it on score alone
