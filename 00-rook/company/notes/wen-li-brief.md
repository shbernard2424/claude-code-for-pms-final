# Brief for Wen Li: who gets pinged after 4.2

From: Rook Dispatch PM
For: Wen Li (staff engineer, ping-ranking logic)
Data: rook-database `pings`, `callouts`, `responders`, `support_tickets`, 29 Jun to 6 Sep 2026. All names are cover names. Nothing here identifies anyone.

## What I'm asking for
About 30 minutes, and answers to six questions at the end. There is no doc for how Dispatch decides who gets pinged, and you built it. I'd also like us to write that description together afterwards.

## What I found, in short
1. On 12 Aug, missed pings jumped from about 2% of pings to 18%. The taken rate fell from about 77% to 64%. It has partly recovered (73% in the week of 31 Aug).
2. Four responders (Vesper, The Undertow, Meteor Mite, Farlight) went from about 49 pings a week combined to 3. Their share of all pings fell from 28% to 2% and is still falling. The other 12 held roughly steady.
3. The drop is in their own home areas. They were taking 90%+ of home-area pings before 4.2, and then they stopped being asked.
4. "Seasonal" doesn't explain it. Callouts dipped 10–20%, but the miss spike starts on 12 Aug and the quiet four are concentrated.

I don't know why. That's where I need you.

## Missed and taken, before and after 12 Aug
| Period | Pings | Taken % | Missed % |
|---|---|---|---|
| 29 Jun to 11 Aug | 1,085 | 76.6 | 2.3 |
| 12 Aug to 6 Sep | 611 | 64.0 | 18.0 |

## The quiet four's share of all pings, by week
| Week of | Quiet four pings | All pings | Share |
|---|---|---|---|
| 29 Jun | 49 | 172 | 28.5% |
| 6 Jul | 48 | 170 | 28.2% |
| 13 Jul | 48 | 174 | 27.6% |
| 20 Jul | 50 | 176 | 28.4% |
| 27 Jul | 50 | 170 | 29.4% |
| 3 Aug | 49 | 172 | 28.5% |
| 10 Aug (4.2 ships Wed 12th) | 43 | 177 | 24.3% |
| 17 Aug | 16 | 158 | 10.1% |
| 24 Aug | 6 | 162 | 3.7% |
| 31 Aug | 3 | 165 | 1.8% |

The 10 Aug week includes two days before 4.2, so 24% understates the drop.

## Pings per week in each responder's home area (the heatmap, as a table)
The heatmap itself (responder by callout area, before and after) is in the session. This is its home-area diagonal.

| Responder | Home area | Before | After |
|---|---|---|---|
| **Vesper** | Old Town | 11.4 | 2.7 |
| **The Undertow** | Harborside | 10.0 | 2.4 |
| **Meteor Mite** | Eastgate | 9.9 | 2.4 |
| **Farlight** | Uptown | 9.4 | 1.6 |
| The Gale | Eastgate | 12.1 | 14.6 |
| Nightwell | Midtown | 12.1 | 10.2 |
| Stormwrack | Southport | 10.8 | 10.8 |
| Captain Vantage | Hillcrest | 9.4 | 8.1 |
| Halfmoon | Westbury | 8.9 | 6.2 |
| Falkirk | Kingsbridge | 8.6 | 7.5 |
| Corporal Ashgrove | Northfield | 8.3 | 5.7 |
| Cindermark | Mill District | 7.3 | 5.9 |
| Bulwark | Foundry Row | 7.0 | 5.9 |
| Ironvale | Riverside | 6.5 | 6.2 |
| The Drift | Greenway | 5.7 | 4.3 |
| The Longcast | Lakeshore | 5.6 | 5.1 |

Meteor Mite and The Gale share Eastgate, and only Meteor Mite dropped. After 4.2, other responders started getting pings for the quiet four's areas, such as Old Town and Uptown.

## What I ruled out
- **Fewer callouts in their areas:** their areas are busy (Eastgate is the busiest) and fell only 10–18%.
- **Lower ping order when asked:** their average position when pinged barely moved. They just stopped being pinged.
- **A miss streak alone:** Stormwrack had 3 misses in a row on 12–13 Aug and stayed busy. Three of the four had similar streaks on 13–14 Aug.
- **The 60s wait alone:** gaps between pings suggest declines take about 22 seconds at most 40 seconds, the same before and after. Accept times aren't in the data.

## What I can't see
- Routing scores, rank, or travel times. They aren't in the database.
- Whether phones received or opened pings. The phone app code isn't in the repo.

## Questions for you
1. Does the 4.2 proximity weighting apply to responders who decline? Marcus asked this on 14 Aug and I can't find an answer.
2. How does recent acceptance accumulate, and can a responder recover from a burst of misses? I see no decay in the code (the 2019 TODO).
3. Can you or Marcus pull the actual routing scores and ranks for the quiet four, for 12 to 20 Aug and for the same four days before 4.2?
4. Did a miss count the same as a decline in 4.1? In 4.2, `offer.py` records both as declined.
5. Why do some callouts end after a single declined or missed ping? About 11% of callouts after 4.2 never got a taken ping, double the 5.5% before.
6. Did anything in 4.2 change how responders accept, decline or mark themselves available, or how the phone app delivers pings?

## What I'm not claiming
- I haven't proven a cause. The hypothesis is that a burst of misses sinks a responder's score and they can't climb back, but Stormwrack contradicts it as a stand-alone explanation.
- Priya advised against reverting 4.2. That is her opinion, not a decision, and I'm not proposing a revert here.
