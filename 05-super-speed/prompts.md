# 05 · Super Speed — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. You've spent three sessions finding out what went
wrong: the two piles of feedback that didn't agree, the numbers that
hid four people inside an average, and the code that settled it —
the shorter timeout is what did it.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.
The note says this shouldn't just be a setting we quietly flip. Using Kip and Meteor Mite, walk me through what he'd actually see change, next time she goes quiet.

### 2.
yes fold this into to the brief

### 3.
what are some things we could do to make the experience better for the handler and the responder

### 4.
add 1, 2, 6, 7, and 9 to the brief

### 5.
trim the Kip walkthrough, make it more concise

### 6.
Save the brief exactly as it stands now as 05-super-speed/brief.md. Show me the file when it's done.

### 7.
Take the brief you just wrote and build me a working prototype, an actual screen I can click through, not a description of one. Build it as a single file I can just open in my browser. Show me where this would actually happen, and make at least one thing on it respond when I click it.

### 8.
add a place to show scores on Meteor Mite's phone

### 9.
when Meteor Mite declines a pin, there needs to be something on Kips console letting them know it was turned down

### 10.
instead of the red banner at the top, I would expect the section in Yellow to have that information instead. If a ping is turned down, the status should be Not Available, and in Red, and the yellow box with the nudge sent should change to what you have in the red box above.

### 11.
add a button on Meteor Mite's phone that they can change from Available to Not Available, and have that reflect the status on Kip's console

### 12.
Change the information box to match the status color. Active is Green, Not Available is Red, so when the box says Meteor Mike is not available should be red.

### 13.
show a timer for 60 seconds once a ping is received on Meteor Mite's phone. If they don't click on Take it or Turn Down before the timer runs out, allow a feedback button to Kip - not available, no service, didn't hear it. Something that will help Kip understand why the ping was missed

### 14.
don't start the clock on Meteor Mite's phone until I click Check Availability on the console.
When there is no current ping, Meteor Mite's phone should say something like Open for Calls or No Current Pings.

### 15.
If Meteor Mite misses the ping and selects Not Available, ask Meteor Mite if they want to change the status on her phone to Not Available.

### 16.
Please do the same thing if Meteor Mite selects No Service, asking if they want to update their status to Not Available on her phone.

### 17.
When No Service is selected, please make sure the status message includes the reason: No Service, even if Meteor Mite changes her status to Not Available.

### 18.
Add the ability for the handler to mark the responder as available or not available, and have that reflect on Meteor Mite's phone
