# Plan — Free Website Offer updates

> This is a PLAN only. Nothing below is built yet — approve or edit first.

## A. Site copy / layout changes (index.html + questionnaire.html)

1. **Remove the word "Reserve" everywhere.**
   - Hero "slot" chips currently read **"Reserve Slot 1" / "Reserve Slot 2"** →
     relabel to **"Slot 1 — Open" / "Slot 2 — Open"**, each with a **different dot
     color** (Slot 1 = green, Slot 2 = amber) instead of two green dots.
   - Confirmed no other visible "Reserve" remains (the old reserve buttons were
     already removed). I'll grep to be sure.

2. **Make the questionnaire header identical to page one.**
   - Page-1 title line is now **"Small Businesses & Freelancers · In Charlotte
     County, FL"**. The questionnaire still says just "Small Businesses &
     Freelancers" → update it to match exactly (chips + ticker already match).

3. **Add hosting + domain (with estimated costs) to the "minimal cost" line.**
   - Current: *"You cover your own minimal costs to keep the site online."*
   - New: *"You cover only the running costs — website hosting (about
     $0–10/month) and your domain name (about $12–15/year). That's it."*
   - (Hosting can be **$0** on GitHub Pages / Netlify; I'll phrase it as a range
     so it's honest either way.)
   - The FAQ "Is this actually free?" answer will get the same cost detail.

4. **Add one FAQ: editing the site later.**
   - Q: **"How can I edit my site later?"**
   - A: *"Right now you can't edit it yourself — each site is delivered finished
     and ready to go, and self-editing or ongoing changes aren't part of this
     free offer yet. It's something I plan to offer down the road; until then,
     if you need a tweak after launch, just reach out and I'll help."*

5. **No other changes.**

## B. Three Gmail draft templates (from IsthisMyLife3737@gmail.com)

I'll create these as **drafts** in the IsthisMyLife3737@gmail.com account
(you send/personalize them). No emojis. Tone matches the site: bold, plain-spoken,
friendly-local.

### Email 1 — To the chosen applicants ("winners")
> Subject: You're in — your free website is happening
>
> Hi [First name],
>
> Out of everyone who applied, your business is one of the two I picked for a
> free, custom three-page website. Congratulations.
>
> Here's what happens next:
> 1. I'll send a few quick questions to fill any gaps from your application.
> 2. I'll design your homepage, services page, and about/contact page.
> 3. We'll do one round of review together, then I'll hand it off — it's 100%
>    yours.
>
> The only thing on you is the running cost to keep it online: hosting (about
> $0–10/month) and a domain (about $12–15/year). I'll point you to the cheapest
> reliable options.
>
> Reply here and we'll get started.
>
> — Diana

### Email 2 — To applicants not chosen ("not selected")
> Subject: Thank you for applying
>
> Hi [First name],
>
> Thank you for applying for the free website offer. I only had two spots this
> round, and they filled up fast — your business wasn't one of the two this
> time.
>
> I'd still love to help once I'm fully up and running. When I open paid spots,
> I'll come back to everyone who applied first — with $50 off for being early.
> I'll keep your details on file for that.
>
> Thanks again for trusting me with it.
>
> — Diana

### Email 3 — To yourself (dianaleff@gmail.com), new-application alert
> Subject: New free-website application — [First name] [Last name]
>
> New application received.
>
> Name: [First] [Last] ([Title])
> Business: [Business name]
> Email / phone: [email] / [phone]
> Service area: [service area]
> Goal: [goal]   Vibe: [vibe]
> Online now: [online presence]
> Must-haves: [req 1 / 2 / 3]
> Notes: [notes]
>
> Full row in the responses sheet.

## C. Automation wiring (what's already done vs. what you do)

- ✅ **Responses spreadsheet** created in your Drive: *"Free Website Offer —
  Questionnaire Responses."*
- The questionnaire posts to **Google Forms** → fill in your form IDs (config
  block in questionnaire.html) so rows flow into that sheet automatically.
- **Auto-email to yourself on each new submission** = the Apps Script trigger in
  README.md (emails dianaleff@gmail.com). Connectors can't run on a trigger;
  this 6-line script is the piece that makes it automatic.
- Emails 1 & 2 (winner / not-selected) are **drafts you send by hand** after you
  pick — that's intentional, since "winner" is your judgment call.

## Resolved (your answers)
1. Slot chips → "Slot 1 — Open" (green dot) / "Slot 2 — Open" (amber dot).
2. Emails signed **"Diana"**.
3. Not-selected email offers **$50 off** when paid spots open.
4. Editing FAQ phrased as **"How can I edit my site later?"** (answer: not yet).
