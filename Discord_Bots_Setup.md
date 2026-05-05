# Discord Bots — 5 AI Personality Bots That Drive Engagement

**Goal:** Discord that feels alive 24/7. 5 bots, each a distinct personality that starts conversations, replies, DMs members, and brings fresh ideas. Founder shows up for the human moments — bots handle the rest.

---

## The 5 bot personas

### 1. **CURATOR** — Inspiration + cool video drops
- **Personality:** Curious, taste-driven, always finds the next thing
- **What it does:**
  - Posts 1-2 cool AI videos per day in #inspiration channel
  - Pulls from TikTok / IG / Twitter / Reddit r/aivideo
  - Tags the post with "could you recreate this in Videfy?" prompt
  - Comments on member posts with "this reminds me of [X]"
- **How:** Cron job + RSS/Apify scraper → Claude API picks captions + commentary → posts via Discord webhook
- **Triggers:** Daily 10 AM ET + 6 PM ET · plus reactive when member posts in #show-your-work

### 2. **COACH** — Active outreach + encouragement
- **Personality:** Warm, encouraging, low-pressure check-in
- **What it does:**
  - DMs members idle 7+ days: "hey, how's the project going?"
  - Replies to members posting wins with congrats + follow-up question
  - Asks members what they're stuck on, recommends specific Videfy features
  - Welcomes new members 10 min after join with personal-feeling DM (not auto-bot tone)
- **How:** Discord activity tracker + Claude API for personalized DMs · uses member's recent post history as context
- **Triggers:** Daily idle-check at 9 AM · reactive on new posts in #show-your-work

### 3. **CRITIC** — Constructive feedback bot
- **Personality:** Sharp eye, kind delivery, specific suggestions
- **What it does:**
  - Replies to every #show-your-work post within 5 min
  - Comments: "what's working" · "what could push further" · "specific tweak to try"
  - Suggests 1 of the 20 Prompt Pack prompts that could level up the work
  - Tags member back into a relevant Videfy feature
- **How:** Discord webhook listener + Claude API with vision (analyzes the video/image they posted) · trained on Videfy brand voice
- **Triggers:** Reactive · new post in #show-your-work or #feedback

### 4. **CONNECTOR** — Community-builder
- **Personality:** Notices patterns, introduces people, asks group questions
- **What it does:**
  - Notices when 2 members are working on similar things → DMs both: "you should meet, you're both building [X]"
  - Posts 3-5x/week group questions in #welcome ("what tool stack are you using right now?" / "favorite hook this week?")
  - Highlights members getting traction — "@[user] just hit 10K views with [X], here's the workflow they used"
  - Pings members in relevant threads when topic matches their interests
- **How:** Vector embedding of member posts (Pinecone / Supabase) + Claude API for similarity matching
- **Triggers:** Weekly Mon 11 AM batch · reactive on similarity hits

### 5. **BRAINSTORM** — Daily challenges + idea generation
- **Personality:** Playful, generative, low-stakes creative push
- **What it does:**
  - Posts daily challenge in #prompts-and-tips: "today's challenge — make a 15-sec ad for [random brand]. show your work."
  - Generates 3-5 fresh prompt ideas/day in different genres
  - Reacts to member submissions with another related challenge or idea twist
  - Hosts Friday "remix" — picks a member's work, asks community to remix it
- **How:** OpenAI/Claude API + scheduled posts via webhook · pulls from Videfy prompt library + Curator's day's finds
- **Triggers:** Daily 8 AM ET challenge · Friday 12 PM ET remix · reactive on submissions

---

## Tech build options

### Option A — Full custom (recommended for max control)
- **Stack:** Node.js or Python · Discord.js / discord.py · Claude API for personalities · Pinecone for vector memory · Vercel/Railway for hosting
- **Build time:** ~30-40 hours total (6-8 hrs per bot)
- **Cost:** $30-80/mo for hosting + $50-150/mo for AI API calls (Claude Sonnet)
- **Best for:** distinct personality voice · Videfy-specific brand match · long-term flexibility
- **Who builds:** Co-creator or contractor ($1.5-3K total one-time build)

### Option B — Hybrid (faster ship)
- Use existing AI Discord bots for shells:
  - **Carl-bot AI** — reactive responses
  - **PaisleyAI** — personality bots out of the box
  - **AnthropicGPT bot** — Claude-powered Discord bot
- Add custom Claude API hooks for the Curator + Coach + Brainstorm scheduled posts
- **Build time:** ~10-15 hours
- **Cost:** $50-100/mo total
- **Best for:** ship in week 1, iterate later

### Option C — Minimum viable (this week)
- Skip bots #1, #4 for now. Ship #2, #3, #5 only.
- Use **Mee6 + custom webhooks + cron jobs** triggering Claude API
- **Build time:** 6-10 hours
- **Cost:** $20-40/mo
- **Best for:** launch week reality

---

## Recommended this week

**Ship Option C tonight.** Get the 3 most-impactful bots (Coach + Critic + Brainstorm) live for Mon launch. Curator + Connector ship Wk 2-3.

### Tonight's build order
1. **CRITIC** first — reactive to #show-your-work · proves bot voice works
2. **BRAINSTORM** second — schedules daily challenges · drives daily engagement
3. **COACH** third — DM check-ins · highest-touch member experience
4. (Wk 2) **CURATOR** — content discovery loop
5. (Wk 3) **CONNECTOR** — needs member volume to be useful

---

## Personality + tone rules (lock before deploy)

- **All bots use first-person warm voice** · NOT "the bot" or "as an AI"
- **Names them differently** in #welcome so members know which bot is which (e.g., "Vee-Curator" / "Vee-Coach" / "Vee-Critic")
- **Bots can disagree, joke, push back** · not always agreeable
- **Founder reviews bot logs daily Wk 1-2** — kill bot voice that doesn't match brand
- **Bots refer members to founder for big asks** ("for that one I'd ask Alex directly")

---

## What success looks like Wk 1

- Day 1: bots active, 1-2 messages from each
- Day 3: members reply to Coach DM at >40% rate
- Day 5: Critic comments getting reactions (👀 / 🔥 / 💯)
- Day 7: Brainstorm daily challenge has 3-5 member responses
- Day 14: members posting "haha I love when [bot name] does X" — bots becoming part of culture

---

## Risks + mitigation

| Risk | Mitigation |
|------|-----------|
| Bot voice feels fake / corporate | Founder voice-checks every bot output Wk 1-2 · adjusts prompts |
| Bots dominate channels (drown human voice) | Hard caps: max 3 bot posts/channel/day · members > bots ratio |
| Critic gives bad feedback | Critic only suggests · doesn't reject · founder spot-checks first 30 outputs |
| Coach DMs feel spammy | Coach DMs limited to 1 per member per week · easy opt-out command |
| AI API costs spiral | Set monthly cap · usage dashboard · cut Curator if over budget |

---

## Founder presence rule (still applies)

Bots scaffold the room. Founder is still the personality.

- **Daily:** 30 min in Discord across channels
- **Weekly:** Wed 2 PM ET office hours · live voice
- **Monthly:** 1:1 voice DM with top 5 contributors

Bots automate the constant. Founder does the personal.

---

## Build files needed (when ready to ship)

- `discord_bots/critic.js` — Discord listener + Claude API call + brand voice prompt
- `discord_bots/brainstorm.js` — cron + Discord webhook + prompt generator
- `discord_bots/coach.js` — activity tracker + Claude API + DM sender
- `.env` — Claude API key · Discord bot tokens (5 separate or one shared)
- Hosting: Railway or Vercel (free tier OK for low volume)

Co-creator can ship Option C in 1 weekend if they have basic JS/Python. Or hire Fiverr Discord bot dev for $400-800 turnkey.
