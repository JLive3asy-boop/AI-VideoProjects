# AI Video Production Plan

## Overview

This document outlines a content strategy for producing short-form AI-generated videos across multiple niches. Each video will feature varied backgrounds, distinct personas, and automated publishing to YouTube.

---

## 1. Stock Trends — Weekly Shorts (Under 60 Seconds)

### Concept

Quick, digestible breakdowns of current and weekly stock market trends delivered in a punchy, visual format ideal for YouTube Shorts.

### Content Structure

Each video follows a tight format to stay under one minute:

1. **Hook (0–5s):** Bold on-screen text + voiceover — e.g., *"The S&P just did something it hasn't done in 3 months."*
2. **Trend Breakdown (5–40s):** 2–3 key data points with animated charts or ticker overlays. Cover what moved, why it moved, and what it signals.
3. **Takeaway (40–55s):** One clear, actionable insight or outlook for the week ahead.
4. **CTA (55–60s):** Subscribe prompt + teaser for the next video.

### Background Rotation

Rotate through distinct visual environments to keep the feed visually fresh:

- Clean dark-mode dashboard aesthetic with glowing chart overlays
- Minimalist office desk setup with a monitor displaying live tickers
- City skyline timelapse (New York, Chicago, London) with data overlays
- Abstract financial motion graphics (candlestick patterns, moving averages)

### AI Production Tools to Explore

- **Script Generation:** ChatGPT or Claude for writing concise, accurate scripts from weekly market data
- **Voiceover:** ElevenLabs or PlayHT for natural-sounding AI narration
- **Video Generation:** Synthesia, HeyGen, or Runway for avatar or motion-graphic-based video
- **Charts & Visuals:** Canva, After Effects templates, or automated chart rendering via Python (matplotlib/plotly exports)

### Publishing Cadence

- 2–3 Shorts per week (Monday recap, midweek movers, Friday outlook)

---

## 2. Health Tips — Authentic Western Nurse Persona

### Persona

A warm, knowledgeable nurse with a distinct Southern/Western American voice and demeanor. Think scrubs-optional, straight-talking, and trustworthy — the kind of nurse who calls you "hun" and actually means it. The tone is friendly, down-to-earth, and practical rather than clinical.

### Content Pillars

#### 2A. How to Cut Calories from Normal Meals

Practical, no-nonsense tips for reducing calorie intake without overhauling your entire diet.

**Example Topics:**

- Swapping sour cream for Greek yogurt in everyday recipes
- The "half-plate rule" — filling half your plate with vegetables before anything else
- Smart cooking oil swaps and portion tricks (measuring vs. pouring)
- Lower-calorie versions of comfort food classics (mac & cheese, casseroles, biscuits and gravy)
- Reading nutrition labels like a nurse — what actually matters
- Drink swaps: sweet tea makeovers, flavored water ideas, cutting liquid calories

**Video Format:**

- 3–7 minute videos with the nurse avatar in a home kitchen background
- Side-by-side meal comparisons with calorie counts on screen
- Friendly, conversational delivery — never preachy

#### 2B. Southern Holistic Medicine Practices

Exploring traditional and holistic health remedies rooted in Southern and Appalachian folk medicine, presented through a modern wellness lens.

**Example Topics:**

- The real benefits of apple cider vinegar — what the science says vs. what grandma said
- Herbal teas and their uses: chamomile for sleep, ginger for digestion, elderberry for immunity
- Honey and lemon remedies — when they work and when to see a doctor
- Epsom salt baths and muscle recovery
- The role of bone broth in gut health
- Poultices, salves, and old-time remedies that actually hold up
- Grounding, forest bathing, and outdoor wellness traditions

**Video Format:**

- 5–10 minute videos with a cozy front-porch or farmhouse kitchen background
- Close-up shots of herbs, teas, and remedy preparation
- Balance folk wisdom with modern evidence — always include a disclaimer when appropriate

#### 2C. Detailed Wilderness Survival Skills

Thorough, step-by-step survival instruction delivered with calm authority — the nurse who also happens to know her way around the backcountry.

**Example Topics:**

- Building a fire with minimal tools (ferro rod, flint and steel, friction methods)
- Water purification methods in the field (boiling, filtration, chemical treatment, solar disinfection)
- Basic wilderness first aid: treating cuts, sprains, blisters, snake bites, and hypothermia
- Building emergency shelters (debris hut, lean-to, tarp configurations)
- Navigating without GPS — reading terrain, using a compass, following water downhill
- Identifying edible vs. poisonous plants in the Southeast and Appalachian regions
- Signaling for rescue and what to keep in a basic survival kit
- Knot tying essentials: bowline, clove hitch, taut-line hitch

**Video Format:**

- 8–15 minute detailed tutorial videos
- Backgrounds rotate between dense forest, riverside camps, mountain overlooks, and open meadows
- Mix of AI avatar instruction with B-roll footage of techniques being demonstrated
- Calm, measured delivery — survival content should feel reassuring, not panicked

### Background Rotation (Health Content)

- Bright, modern home kitchen (calorie-cutting content)
- Rustic farmhouse kitchen or front porch with rocking chairs (holistic medicine)
- Outdoor wilderness settings — forest clearings, campsites, riverbanks (survival skills)
- Clean medical/wellness studio with soft lighting (general health tips)

### AI Production Tools to Explore

- **Avatar & Voice:** HeyGen or Synthesia with a custom Southern-accented female voice via ElevenLabs
- **Script Writing:** Claude or ChatGPT with detailed persona prompts to maintain consistent voice and tone
- **B-Roll & Backgrounds:** Runway Gen-3, Pika, or stock footage libraries (Storyblocks, Artgrid)
- **On-Screen Graphics:** Canva for calorie comparisons, ingredient lists, and survival diagrams

---

## 3. YouTube Upload Automation

### Goal

Once videos are rendered and export-ready, automate the upload process to YouTube using stored account credentials — eliminating the need to manually upload each video.

### Recommended Approach: YouTube Data API v3

#### Prerequisites

1. A Google Cloud project with the YouTube Data API v3 enabled
2. OAuth 2.0 credentials (Client ID and Client Secret) configured for the project
3. A refresh token generated through the initial OAuth consent flow
4. Python 3.8+ environment with required libraries

#### Key Libraries

```
google-api-python-client
google-auth
google-auth-oauthlib
google-auth-httplib2
```

#### Automation Workflow

1. **Authenticate:** Use stored OAuth refresh tokens to authenticate without manual login each time.
2. **Prepare Metadata:** Load video title, description, tags, category, and privacy status from a configuration file (JSON or YAML) that sits alongside each rendered video.
3. **Upload:** Use the `videos().insert()` method from the YouTube API to upload the video file with its metadata.
4. **Set Thumbnail:** Optionally upload a custom thumbnail via `thumbnails().set()`.
5. **Log Results:** Record the upload status, video ID, and URL to a log file for tracking.

#### Metadata Configuration Example

```json
{
  "file": "stock_trends_week12.mp4",
  "title": "S&P 500 Weekly Recap — What You Missed",
  "description": "Quick breakdown of this week's biggest market moves...",
  "tags": ["stocks", "investing", "S&P 500", "market recap"],
  "category_id": "22",
  "privacy_status": "public",
  "thumbnail": "stock_trends_week12_thumb.png"
}
```

#### Scheduling Options

- **Cron Job (Linux/Mac):** Schedule the upload script to run at specific times (e.g., every Monday at 8 AM).
- **Task Scheduler (Windows):** Same idea, different platform.
- **CI/CD Pipeline:** Use GitHub Actions or similar to trigger uploads when new video files are pushed to a repository or storage bucket.
- **Cloud Functions:** Run the upload script on AWS Lambda or Google Cloud Functions, triggered by new files landing in cloud storage.

#### Important Notes

- YouTube API has a daily upload quota — monitor usage to avoid hitting limits.
- Store credentials securely. Never hard-code tokens in scripts — use environment variables or a secrets manager.
- Always test uploads with `privacy_status: "private"` before going live.
- Review YouTube's Terms of Service and API policies to ensure compliance with automated uploading rules.

---

## 4. Production Pipeline Summary

| Phase | Action | Tools |
|-------|--------|-------|
| Scripting | Generate scripts per content pillar | Claude, ChatGPT |
| Voiceover | Produce AI narration with appropriate accent and tone | ElevenLabs, PlayHT |
| Video Assembly | Combine avatar, backgrounds, B-roll, and graphics | HeyGen, Synthesia, Runway |
| Editing | Final cuts, captions, transitions, and branding | CapCut, DaVinci Resolve, Premiere Pro |
| Quality Review | Watch each video, verify accuracy and tone | Manual review |
| Export | Render final files with metadata configs | Local or cloud render |
| Upload | Automated push to YouTube via API | Python + YouTube Data API v3 |

---

## 5. Disclaimers to Include

- **Stock content:** "This is not financial advice. Always do your own research before making investment decisions."
- **Health content:** "This content is for informational purposes only and is not a substitute for professional medical advice. Consult your healthcare provider before starting any new health practice."
- **Survival content:** "Practice these skills in safe, controlled environments before relying on them in an emergency. Always tell someone your plans before heading into the wilderness."
