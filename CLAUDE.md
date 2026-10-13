# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

Source: rook-wiki (read Oct 2026) and Priya's handoff doc
(`00-rook/company/notes/handoff-from-priya.docx`). I am the new PM for
**Rook Dispatch** (started Mon 24 Aug 2026). Wiki comments name people by
role only; the mapping below comes from the Team directory.

### Company and products
- Rook Industries sells coordination and provisioning software to masked,
  independent responders and the handlers/quartermasters who support them.
  Subscription, priced per active responder. 241 staff, HQ Site Aleph,
  offices in Berlin and Singapore. Ships monthly; point releases are 4.x.
- **Rook Dispatch** (mine): handlers use a web console, responders use a
  phone app. Incident in, rank available responders, ping the top one, they
  take it or not, else on to the next. Routing config ships with the
  release; handlers cannot change it at runtime.
- **Rook Supply**: requisitions, quartermaster approval, maintenance,
  field failure reports. Reads the Responder Availability Record that
  Dispatch writes, and schedules gear maintenance into low-callout
  periods. Any change to how Dispatch computes availability or callout
  load lands in Supply with no change on their side.
- **Confidentiality:** cover identities are never stored; no mapping to
  legal identities exists. Read Security Policy 4.1 before touching
  responder records. Never try to work out who anyone is.

### People (comment role -> person)
- Engineering manager = **Marcus Oyelaran**, Site Aleph. Runs Dispatch
  engineering. First stop when unsure. Can pull rough numbers.
- Staff engineer = **Wen Li**, Berlin. Built the ping-ranking logic; no
  doc exists, so ask her directly. Was away 14-24 Aug.
- Support lead = **Nadia Hoffmann**, Berlin. Owns tickets; has the
  breakdown of the two 4.2 complaint themes. Worth a standing 15 minutes.
- Product designer = **Sofia Marino**, Site Aleph. Owns console and phone
  app; ran the September customer interviews.
- Data analyst = **Ravi Menon**, Singapore. Owns the numbers; reports
  weekly on how often responders take pings (the real acceptance data).
- **Helen Achebe**, Director of Product, Site Aleph. My manager. Owns
  roadmap and commitments.
- **Priya Raghunathan**: previous Dispatch PM, left 21 Aug. Owner of every
  Q3 roadmap item. Reachable only via the engineering manager.
- Handlers seen in interviews: Aunt Dot (Vesper), Mr. Ambrose (Captain
  Vantage), Halloran (Sgt. Bulwark; also appears in Supply briefs),
  Kip (Meteor Mite, The Gale).

### Vocabulary
- **Callout**: request for a responder to attend an incident. **Ping**: a
  callout offered to one responder's phone. **Taken / Turned down /
  Missed** (no answer in time; logged separately from turned down, both
  move the ping on).
- **Ping wait**: how long a ping sits before counting as missed. Same for
  everyone. **Acceptance rate** = taken / pings; headline metric.
  **Time-to-accept** = median seconds, ping to taken. **Coverage gap** =
  nobody with the needed capability tags was available (distinct from low
  acceptance).
- **Routing priority**: score that orders responders. Inputs: proximity
  (travel-time estimate), availability, capability match, recent
  acceptance history. Turning down or missing a ping lowers recent
  acceptance, which lowers later rank.
- Capability tags: flight, structural-entry, hazmat-tolerant, cold-weather,
  aquatic, crowd-management, de-escalation. **Mutual aid** (responders
  covering for each other) is unsupported, Q4 exploration.

### Where things stand (as of 13 Oct 2026)
- **Releases:** 4.0 (7 Apr) nav, profile redesign, override audit log
  listed. 4.1 (16 Jun) travel-time proximity, bulk callout, push
  reliability. 4.2 (12 Aug) proximity weighted up vs. acceptance history;
  ping wait 90s to 60s; filter persistence; 3 defect fixes.
- **4.2 problem:** since 12 Aug, callout tickets ~3x normal, still
  elevated 26 Aug, no trend since in the wiki. Split ~2/3 "phone never goes
  off", ~1/3 "gone before I could answer". The second is explained by the
  60s ping wait. Handoff and engineering manager called it seasonal; the
  rook-database (pings, 29 Jun-6 Sep) does not support that:
  - Missed pings jumped ~2% -> 21% the week of 12 Aug, still 13% in the
    week of 31 Aug. Taken: 75-78% before, 54% the week of 10 Aug, 73% by
    31 Aug. Callout volume dipped ~10-20% (some real softness), which
    does not explain per-ping outcomes.
  - Four responders went nearly silent: Vesper (Aunt Dot), Meteor Mite
    (Kip), The Undertow, Farlight. ~12 pings/wk each before; 1/wk by late
    Aug; 59% of their remaining pings missed. The other 12 held steady
    or got more (The Gale, Kip's other responder, is among the busiest).
    Matches Kip's and Aunt Dot's interviews. Aggregate rate hides this.
  - Not seen in data: why they missed. Not the ping order (their position
    when pinged is ~1.4, same as others); they stopped being asked.
- **Routing code** (`00-rook/code/dispatch-routing/`, 4.2 state only; git
  has no 4.1 history): score = 0.60 proximity + 0.25 recent acceptance
  + 0.15 capability (was 0.45/0.40/0.15). Decline and miss both cost
  0.12; a take earns 0.08; no decay (2019 TODO). Nobody is filtered
  out, so capability is only a weight. **Working hypothesis, unproven:**
  a burst of misses (60s wait) sinks a responder and they can't climb
  back. Open: the engineering manager's 14 Aug question (does the
  proximity change apply to decliners?) was never answered.
- The 4.2 purpose: fairness to nearby/wide-area responders (Priya's
  handoff, release notes). No success metric or baseline was ever set.
- Priya advised against reverting 4.2. Hold that as her opinion, not a
  decision. The engineering manager planned to regroup with me on 4.2 a week
  after I started; confirm that happened.
- **Roadmap is stale** (last reviewed 30 Jun, all Priya's). Ping timeout
  tuning and proximity change shipped in 4.2. **Availability Confidence**
  is still "Committed 4.2" but is not in the 4.2 notes; Priya says items
  were squeezed out. Needs a conversation with Helen: which Q3 commitments
  still stand. **Requisition approval chains**: Committed 4.3 (Supply
  brief; scope creeps past one approval step). **Handler phone app** and
  **Shared cover between responders**: Q4, exploring.
- **Briefs:** Bulk Callout and Routing Override Audit Log read as unstarted
  but the changelog lists them shipped (4.1, 4.0). Handler Phone App (Sep;
  Sofia, unstaffed). Requisition Approval Chains (Jul; Supply).
- **Owed to me / to do:** write the missing description of how Dispatch
  decides who gets pinged (with Wen Li). Filter-persistence tickets are
  noise; do not let them eat my time.
- **Open next:** rook-database is read-only SQL (tables: callouts,
  handlers, pings, responders, support_tickets) with no travel time or
  rank scores. Still unchecked: unfilled callouts, whether support
  tickets match the quiet four, their first miss streaks, and Ravi's
  weekly report. Check the Helen conversation and Wen Li's answer to the
  14 Aug question before presenting a cause.
- Scenario files `05-super-speed/director-request.txt` and
  `06-sidekicks/scheduled-run-output.txt` already exist and assume the
  quiet-responder cause is found; treat them as later-module material.
- **Tickets (147, 29 Jun-7 Sep):** 40 before 12 Aug, 107 after. After: 30 "quiet phone" (+2 "first ping in days, then gone"), 13 "moved on before I could answer", 14 filter side-effects. None of the first 40 were about quiet phones. Quiet tickets come from 4 of 12 handlers and name Farlight, The Undertow, Corporal Ashgrove, Halfmoon (not Vesper or Meteor Mite). Ticket text is often near-identical across handlers. Interviews and tickets share only Mr. Ambrose; interviews undercount quiet and skip Supply (26 tickets).
- **Quiet four before 4.2 were normal:** 11-14 pings/wk, 69-81% taken, 1-4% missed, no miss run over 1. In 12-16 Aug they missed 17 of 31 pings (55%) vs 21% for the other 12; three had 3+ misses in a row on 13-14 Aug (Vesper max 2). Stormwrack also had 3 misses on 12-13 Aug and stayed busy, so a streak alone doesn't sink anyone. Their share of first pings fell 28% to 9%; pings per callout rose 1.23 to 1.39. They cover busy areas, and Meteor Mite and The Gale share Eastgate, so distance alone doesn't explain it.
- **Response time:** pings has no answer time. Gap to the next ping gives decline time: median ~22s, max 40s, same before and after 4.2, so the 60s wait cut off no declines. Accept time is not in the data, so whether 60s hurts accepts is unknown. This weakens "the timer alone caused the extra misses" (missed 2-6/wk before, 21-38/wk after; timer confirmed 92s then 62s).
- **Code and docs:** a miss and a decline are treated the same (offer.py calls record_declined for anything not taken). Whether that was true in 4.1 is unknown, probably unchanged. Nothing documents a 4.2 change to how responders accept, decline or mark availability; phone app code is not in the repo.
- **Still open:** Wen Li (14 Aug question, how recent acceptance accumulates, 4.1 behavior); Sofia or Wen Li on whether the app logs delivered, opened or answered pings and shipped anything in 4.2; Ravi's weekly time-to-accept; Helen and the 4.2 regroup.
