# HANDOFF — Kevin Mehner: Speed-to-Lead system + lifeinsplanning.com
_Written Oct 21, 2026 for continuing in Claude Code (or any new session)._

## 0. Who / what
- **Kevin Mehner**, newly licensed Utah life & health agent (Resident Producer #1139802, NPN 22376845, lines: Life, Accident & Health; issued 10-05-2026). Independent agent with **North American Senior Benefits (NASB)**, Orem / Utah County. Future team brand "kin" (not a legal entity).
- Legal entity for business/A2P: **Kevin Mehner LLC**. Customer-facing name: **Kevin Mehner / Life Insurance Planning** (lifeinsplanning.com). **Do not put NASB on the public site** (Kevin's call; he's an agent, not NASB).
- Working style: answer questions in chat; only build deliverables when asked. Talks plainly, wants simple, no clutter for older clients.

## 1. The goal (one problem at a time)
Build a **speed-to-lead texting system** for Integrity Connect final-expense leads, on **GoHighLevel (GHL) Starter, $97/mo, owned by Kevin** (decided against Agent CRM / Twilio-custom). Broker 360 ($199, NASB-built CRM) stays for post-sale/admin for now; Knock It Pro stays for door-knock routing for now. Long-term: wean off both, one kin-owned system (knock map, policy tracking, nurture, quoting API; e-apps stay in carrier portals/iGO; GHL Unlimited $297 when recruits join).

Flow when a lead lands: parse lead → create GHL contact → within ~1 min send intro text + MMS card (8am–9pm only) → wait for reply → branch → if no reply, nudge, then "I'll be in your area tomorrow" → Kevin door-knocks within 24h regardless.

## 2. Lead source (what we know)
- Leads: **"NASB LEGACY (REALTIME INQUIRY)"** via Integrity Connect; land in Integrity CRM; exportable PDF/Excel ("Lead Mailer(s)" PDF).
- Fields: Inquiry Id, First Name, Last Name, Age, Address, City, State, Zip, County, Phone, Email, Height, Requested Coverage On (MM/DD/YYYY HH:MM), Current Carrier, Carrier, History of Cancer, Credit Rating, Wants Legacy Plan?, Would like to protect family?, Desired Coverage Amount.
- Sample leads were Salt Lake County (Magna, Sandy), ages 66–68, $10k–$20k coverage.
- **UNKNOWN / BLOCKING:** how Kevin is notified of a new lead in real time (email? app push? any webhook/"send to automation tools" setting in Integrity CRM). Integrity's site says realtime data campaigns email the agent and leads can be "sent to your preferred automation tools" but doesn't document how. **Get one real new-lead email forwarded** before building intake. Fallback if no fielded email: poll the Integrity export.

## 3. GHL status (as of Oct 21)
- GHL account exists (Kevin signed up Starter). Trust Center (A2P) wizard in progress: Business details ✅ (Profile, Business details, Address, Contact), Campaign details: Messaging volume ✅, **Chat widget setup — pending** (needs website URL; widget id `6ad8f2c3efcd72a99d917886`, consent text already names Kevin Mehner LLC), **User consent — pending**.
- Domain **lifeinsplanning.com** — Kevin says this is the website (assume purchased; confirm where DNS lives — GHL Settings → Domains or a registrar).
- Not yet done: phone number purchase (801/385), wallet funding, custom fields, workflows, Zapier intake, LeadConnector app.

### A2P paste-in answers
- Use case: **Low Volume Mixed** (or Mixed; if only Marketing/Promotional offered, that's acceptable).
- Campaign description: "Licensed insurance agent responding to consumers who submitted an online request for final expense life insurance information through a lead vendor. Messages introduce the agent, confirm the request, schedule an appointment (in person or virtual), send appointment reminders, and answer questions. Conversational, one-to-one."
- Opt-in description: "Consumers opt in two ways: (1) by submitting the text opt-in widget on lifeinsplanning.com with the consent checkbox shown; (2) by submitting a web form on a licensed lead vendor's site (Integrity / NASB Legacy inquiry) requesting final expense life insurance information and consenting to contact by text from a licensed agent, with consent recorded by TrustedForm/Jornaya certificate. Opt-in is not a condition of purchase; every first message includes STOP instructions."
- Opt-out confirmation: "You've been unsubscribed from Kevin Mehner / North American Senior Benefits texts. Reply START to resubscribe." HELP: "Kevin Mehner, licensed agent. Call (801) XXX-XXXX. Reply STOP to opt out."
- Sample messages: (1) intro below; (2) "Perfect, {{first_name}}. I can stop by Tuesday at 2:00 or Wednesday at 10:30. Which works, and what's the best address?"; (3) "Reminder: Kevin will see you tomorrow at 2:00 PM. Reply if you need to reschedule."; (4) "Just making sure this came through, {{first_name}}. Were you hoping to meet in person or over the phone?"
- Toggles: embedded links Yes, embedded phone numbers Yes, age-gated No, direct lending No.
- Opt-in proof: ask Integrity (leads@integrityconnect.com / 800-960-4196) for a screenshot of the NASB Legacy consumer form with TCPA consent language; fallback = screenshot of a lead in Manage Leads showing TrustedForm cert.
- Fees ≈ $4 brand + ≈ $15 campaign from GHL wallet. Brand 1–3 business days, campaign 3–7 more. Don't send real texts until Approved.
- Website requirements for approval: live page on owned domain, who you are, privacy policy containing **"Mobile phone numbers and SMS consent will not be shared with or sold to third parties or affiliates for marketing or promotional purposes."** + SMS terms (frequency varies, msg & data rates, STOP/HELP, not a condition of purchase). The built site already has all of this.

### Intro text (final wording — mirrors the lead card; avoid "state regulated")
"Hey {First}, this is Kevin Mehner with North American Senior Benefits. I was assigned your request about the Legacy Plan to protect your family — looks like you were looking at around ${Coverage} in coverage. I'm local here in Utah County. Most of my clients like to go over it in person, but I'm happy to do it by phone or Zoom too. Which do you prefer? Reply STOP to opt out."
(+ MMS attachment: `mms/kevin-agent-card.jpg`)

### Reply flows
- In person → offer 2 slots + ask best address → confirm → reminder morning-of.
- Virtual/phone/Zoom → offer 2 slots → send Zoom/call link → reminder.
- Question ("what is this / how much / who gave you my info") → push to Kevin, answer personally (template: "You filled out a request on {date} for final expense coverage info. Usually $30–80/mo depending on age/health. 15 minutes to see what you qualify for. In person or by phone?").
- Not interested → "No problem {First}, I'll leave you be. If anything changes I'm here." tag `cold`.
- STOP → auto opt-out.
- No reply 15 min → nudge. No reply by 6 PM (or next morning if late lead) → "I'll be out in {city} tomorrow between X and Y, I'll swing by and drop off your info either way." tag `knock-24h`.

### Build steps remaining (GHL direct)
1. Sub-account "kin"; Agency Settings → Billing → Wallet $25 + auto-recharge.
2. Settings → Phone Numbers → buy 801/385; forward calls to cell; install **LeadConnector** iOS app.
3. Settings → Custom Fields: `Age` (number), `Desired Coverage` (number), `Inquiry ID` (text).
4. Finish Trust Center (website URL = https://lifeinsplanning.com, widget on site, user consent text above).
5. Intake: Zapier (free) → parser.zapier.com mailbox → Gmail filter forwards Integrity lead emails → Zap: Email Parser "New Email" → LeadConnector "Add/Update Contact" (map fields; tag `integrity-lead`; source Integrity).
6. Workflow "Integrity Speed-to-Lead": trigger Contact Tag Added `integrity-lead`; Settings: Time Window 8:00–21:00 America/Denver, Stop on Response OFF; Send SMS (intro + card attachment) → Wait: Customer Replied, timeout 15m → If/Else on `{{contact.last_message}}` (person/house/come by | phone/zoom/virtual/call | stop/not interested/no thanks | else) → branches above; timeout path: nudge → Wait until 18:00 → area-tomorrow text → tag `knock-24h`.
7. Workflow "Knock List": tag `knock-24h` → Smart List "Today's Knocks" (name, address, city, age, coverage) → CSV to Knock It Pro for now.
8. Test with fake Integrity email + Kevin's own cell before approval; go live on next real lead.

## 4. Website — lifeinsplanning.com (this folder)
- **Built, not yet live.** Brand: "Life Insurance Planning", Kevin by name, footer "© 2026 Kevin Mehner LLC · Independent licensed insurance agent · Orem, Utah". No NASB mention. Senior-friendly: 19px base, high contrast, navy #1d3561 / teal #1f7a6d, Source Serif 4 + Inter (Google Fonts).
- `index.html` — Home (hero + headshot, What I do, How it works, Carriers (13 logos), Licensing, Text messaging consent block, footer). `privacy-policy/index.html` — Privacy Policy & SMS Terms. `assets/` — headshot + 13 logo JPGs (cropped from NASB's "Top Rated Providers" page; carriers may require official artwork/approval — swap in official files if asked). `CNAME` for GitHub Pages.
- `ghl-embed/*.html` — same pages with images base64-inlined, for pasting into a GHL Custom HTML element (alternative hosting path).
- **Placeholders to fill:** `XXX-XXXX` / `tel:+1801XXXXXXX` (new GHL number) and `EMAIL_PLACEHOLDER` (privacy page).
- **TODO before A2P submit:** paste the GHL chat-widget snippet before `</body>` in index.html (placeholder comment is there).
- Carriers shown (Kevin's quoting screen lists: Corebridge/AIG SIWL, Americo, Foresters, Liberty Bankers, Mutual of Omaha, Occidental FC/SC (American-Amicable), Royal Neighbors, Transamerica (FE Express, Immediate Solution), CVS/Aetna). Also included from NASB page: Gerber, National Guardian, United Home Life, Aflac — confirm Kevin is appointed or remove.
- Hosting options: (a) GitHub Pages / Railway static from this folder, DNS A/CNAME at wherever lifeinsplanning.com is registered; (b) GHL Sites with the embed files. Kevin wants **real-time design iteration** → prefer (a) with a local preview.

## 5. MMS card
`mms/kevin-agent-card.jpg` (1080×1350, ~125 KB): headshot, NASB logo (white, transparent), "Kevin Mehner — Licensed Life & Health Agent — Utah Resident Producer · Serving Utah County — Utah License #1139802 · NPN 22376845". Footer line removed per Kevin. Source `mms/card-source.html` (render 1080×1350 with Playwright). Possible tweak: "Serving Utah & Salt Lake Counties" (leads were SLC).

## 6. Compliance notes to keep honoring
- Quiet hours 8am–9pm recipient-local; honor any opt-out wording; keep consent records; mirror lead-card language ("Legacy Plan"); no government-affiliation implication.
- Run intro text + card + any NASB logo use past NASB compliance; carriers' logo use technically needs their approval.
- Not a lawyer: TCPA/state mini-TCPA caveats given to Kevin.

## 7. Other artifacts from this project (claude.ai)
- Utah 17-03 Sprint course (passed exam): https://claude.ai/artifact/DYqbWXxQYLXp81mcHQkFCW ; shared fresh copy: https://claude.ai/artifact/NAveimNfk6bBSgLKQ6V8te
- Kitchen Table Cheat Sheet (Design): https://claude.ai/artifact/JmwP19XGTuoEdsBGHwFRAg
- Texas Life Agent Sprint (for his buddy; needs Share → anyone with link): https://claude.ai/artifact/U9bJudfTA5DCLspJGsYJ7Q
- Project docs: claude/speed-to-lead-build.md, claude/17-03-course-notes.md, claude/kin-handoff.md
