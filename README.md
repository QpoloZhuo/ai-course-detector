# AI Course Detector — Claude Skill

A Claude skill that evaluates whether an AI course is worth buying — or just another cash-grab.

Most AI courses sell a promise. This skill helps you cut through the hype and make an informed decision in under 5 minutes.

---

## What It Does

Paste a course URL or sales page. The skill scores it across **9 weighted indicators (100 pts total)** and gives you a direct recommendation based on both the course quality *and* your personal skill level.

---

## Scoring Framework

| # | Indicator | Max | What It Catches |
|---|-----------|-----|----------------|
| W1 | Benefit claim integrity | 10 | Inflated ROI numbers, vague "10x" promises |
| W2 | Content scarcity | 12 | Repackaged official docs, YouTube tutorials in disguise |
| W3 | Audience specificity | 8 | "Suitable for everyone" = designed for no one |
| W4 | Instructor credibility | 15 | Self-proclaimed experts with no verifiable work |
| V1 | Tangible deliverables | 10 | Courses that teach "mindset" instead of tools |
| V2 | Demo quality | 18 | Tech showmanship vs. real recurring pain points |
| V3 | Technical depth | 12 | Feature lists disguised as syllabuses |
| V4 | Post-purchase support | 5 | Recording-only "communities" |
| V5 | AI efficiency awareness | 10 | Instructors who route everything through AI when MCP/API is faster |

### Score Bands

| Score | Verdict |
|-------|---------|
| 80–100 | High quality — worth the investment |
| 60–79 | Partial value — personal fit is the deciding factor |
| 40–59 | Proceed with caution |
| 0–39 | Cash-grab warning — not recommended |

---

## What Makes This Different

Most course review frameworks only ask "is this course good?" This skill asks a second, more important question: **"Is this course good *for you*?"**

Before scoring, it collects your current AI skill level and whether you have a real work need for the topic. A course can score 75/100 and still be a waste of money if you're already past beginner level.

### The V5 Indicator: AI Efficiency Awareness

This is the indicator most course reviews miss entirely.

A good AI instructor knows that **AI Agents aren't a universal hammer**. Some tasks are better handled by direct tools:

- ❌ Using prompts to have AI screenshot → judge → click through Canva: slow, unstable, expensive in tokens
- ✅ Calling Canva MCP directly: one instruction, precise, minimal token cost

If a course teaches AI-operated UI automation as a feature without mentioning MCP or direct API alternatives, that's a sign the instructor hasn't thought deeply about efficiency — they're optimizing for impressive demos, not practical workflows.

---

## Installation

1. Download `SKILL.md`
2. Place it in your Claude skills directory:
   ```
   /mnt/skills/user/ai-course-detector/SKILL.md
   ```
3. Trigger it by sharing any AI course URL or asking "is this course worth it?"

For the Chinese version, use `SKILL.zh.md` instead.

---

## Example Output

```
📊 AI Course Evaluation Report
Course: AI Agent Workshop by [Instructor]

Total Score: 59 / 100

W1. Benefit claim integrity     3 / 10   Numbers exist but math is suspicious
W2. Content scarcity            8 / 12   Partial differentiation
W3. Audience specificity        8 / 8    Clearly targets non-engineers
W4. Instructor credibility     10 / 15   Public presence, limited portfolio
V1. Tangible deliverables      10 / 10   Walk away with a deployable Skill
V2. Demo quality               12 / 18   Real needs, but "why this approach" never explained
V3. Technical depth             4 / 12   Syllabus lists features, not steps
V4. Post-purchase support       1 / 5    Recording only
V5. AI efficiency awareness     3 / 10   Browser automation demo with no MCP mention

Personal Fit: Low (Advanced user)
Recommendation: ❌ Not recommended
```

---

## Languages

- `SKILL.md` — English
- `SKILL.zh.md` — Traditional Chinese (繁體中文)

---

## Contributing

Found a pattern of low-quality AI courses not captured by the current indicators? Open an issue or PR. The goal is to keep this framework sharp as the AI course market evolves.

---

## License

MIT
