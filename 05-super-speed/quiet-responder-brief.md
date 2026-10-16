# Coming back after a bad stretch — one-page brief (draft)

For: Helen Achebe · From: Dispatch PM · 16 Oct 2026 · Status: draft, not agreed with engineering

## The problem in one line
After 4.2, four responders (Vesper, Meteor Mite, The Undertow, Farlight) went from ~12 pings a week to ~1. Today the only way a responder's rank goes up is by taking a ping, and a low rank means they aren't pinged, so a bad run of misses has no way out. (Wen's 2019 TODO in `history.py` asked whether scores should ease back; nobody answered it.)

## Who it's for
**Primary: a responder who has gone quiet.** Their handler (Aunt Dot, Kip) is the person who notices and writes in. Today they get silence: no pings, no explanation, 30+ tickets saying "phone never goes off".
**Secondary: the handler**, who currently can't tell "my responder is being passed over" from "nothing is happening in our area".

## What changes for them
1. **Responder:** a quiet spell no longer sticks. If they have taken nothing for a while, the system offers them an occasional ping in their home area (the area they cover and where pings were lost). One take puts them back in normal rotation. They feel it as "my phone is ringing again", not as a setting.
2. **Responder:** a missed ping (no answer in time) stops counting against them as hard as a turn-down. Today both cost the same 0.12. A miss is not a refusal, and the 60s wait is new.
3. **Handler:** the console shows a quiet marker with the plain reason, instead of leaving them to raise a ticket. See the walkthrough below.

### What Kip sees, next time Meteor Mite goes quiet
*Illustrative: days, wording and thresholds are placeholders, not agreed with Wen Li or Sofia.*

**Today:** a few misses sink Meteor Mite's score, her phone stops ringing, and she can't earn it back. Kip sees no alert and no reason, and finds out only when work dries up.

**After:** around day 4–5 without a ping, her console card reads *"Meteor Mite hasn't been pinged in 5 days. Recent pings were missed, not turned down. She's still marked available."* At the same time she gets one comeback ping for an Eastgate callout. If she takes it, she's back in rotation and the marker clears. If she misses it, the marker stays and she gets another later. Kip gets no boost button and sees no scores, and The Gale is unaffected.

**Weak spot:** with no delivered/opened data, a missed comeback ping could mean a dead phone, so the marker says what happened.

### Smaller touches (wording and status, little engineering)
- **Responder is told why.** Her first comeback ping carries a short note, e.g. "You've been passed over lately after a few missed pings. This one's for you." Tone is for Sofia to set.
- **Responder sees her own recent pings.** A simple history ("3 missed, 12–14 Aug") lets her tell "my phone failed" from "the system stopped asking."
- **Handler gets a "check availability" prompt** on the quiet marker, to confirm she's marked available or message her. It's a nudge to the responder, not a routing change, so it stays inside "no dial."
- **The marker always states the cause in plain words** (missed vs turned down, still marked available), so it answers the question without a ticket.
- **Support sees whether it helped.** If a flagged responder's handler still writes in, Nadia can see the flag didn't work. That's our early read, with no new dashboard.

(Mechanically, 1 and 2 are the "ease back" and "miss vs decline" options. Helen asked for the experience first, so the numbers are left for engineering.)

## What it deliberately doesn't do
- **Doesn't revert 4.2.** Nearby and wide-area responders still get the proximity weighting they asked for.
- **Doesn't give handlers a dial.** Routing config ships with the release by design. The handler sees status only and can't force pings.
- **Doesn't touch the ping wait.** Declines took ~22s, max 40s, so the 60s wait isn't proven to be the cause. Accept time isn't in the data, so that stays a separate question.
- **Doesn't force ranking for the responder who really is unavailable.** Comeback pings go only to people marked available.
- **No mutual aid / shared cover** (Q4 exploration), **no cover-identity or tenure data** (Security Policy 4.1).
- **Doesn't change the Responder Availability Record.** Supply reads it, and a new pattern of pings changes callout load there. Flag to Supply before launch rather than discover it.

## How we'd know it worked
No success metric was ever set for 4.2, so set one now: the quiet four back above ~8 pings/wk; share of callouts with no taken ping back to ~5.5% (was 11.1% after 4.2); overall taken rate not worse than 73%.

## What I don't know yet (don't present as settled)
- The cause is a **working hypothesis**: a burst of misses on 12–14 Aug sank them and nothing lifts them. Unproven. Stormwrack also missed 3 in a row and stayed busy.
- Wen Li hasn't answered: Marcus's 14 Aug question (does the proximity change apply to decliners?), how scores are stored and carried across a release, and real rank scores for 12–17 Aug. The brief is drafted but not sent (`00-rook/company/notes/wen-li-brief.md`).
- No prior-year August data, so seasonal isn't ruled out directly. Ask Ravi or Marcus.
- Whether to give returners the occasional ping depends on whether the phone app shows delivered or opened pings, which we can't see.
- Marcus's 4.2 regroup and whether Helen has seen the findings are both unconfirmed.

## Next
Wen Li answers (this week) → decide ease-back vs miss-weighting with Marcus → clickable mockup of the two views (responder phone, Kip's console), which Sofia owns.
