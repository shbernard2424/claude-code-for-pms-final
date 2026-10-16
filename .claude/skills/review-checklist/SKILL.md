---
name: review-checklist
description: Reviews a product brief against a fixed four-point checklist before it goes any further. Use when the user says "review this brief", "run the review checklist", "check this brief", or points at a brief file and asks for a review. Input is a brief (file path or pasted text). Output is a pass/fail result for each check, with evidence and a suggested fix for any gap.
---

# Review checklist

Run the same four checks on any brief, every time. Do not add checks, skip checks, or change their wording unless the user asks.

## Input

A brief, given as a file path or pasted text. If the user gives no brief, ask which one. Read the whole brief before judging any check.

## The four checks

1. **Owner.** The brief names who owns it: a specific person, not a team or "TBD". Pass only if a named individual is clearly accountable for the brief or the work it describes.
2. **Success measure.** The brief says how we will know it worked: a metric, a signal, or an observable outcome, ideally with a baseline or target. Fail if it only describes what will be built, or says "improve" with nothing to measure against.
3. **Scope consistency.** The scope at the end matches the scope at the start. Compare what the opening says is in and out of scope with what the closing sections promise (deliverables, next steps, asks, "what we'll build"). Fail if anything appears at one end and not the other, or if the end quietly grows or shrinks the scope. List each mismatch.
4. **Problem before fix.** The brief explains the problem before it proposes a fix. Fail if the solution appears first, or if the problem is never stated on its own (a fix described as the problem counts as a fail). Note where each one first appears.

## How to judge

- Quote or point to the line that supports each verdict. A verdict with no evidence is not a verdict.
- Judge only what the brief says. Do not fill gaps from other files, and do not guess that something is "probably covered elsewhere". If it is not in the brief, it is a gap.
- Be strict but fair: partial counts as **Fail** with a note saying what is missing, so the user can see how close it is.

## Output

Use exactly this shape:

```
Brief: <title or file name>

1. Owner: PASS | FAIL
   Evidence: <quote or location>
   Fix: <only if FAIL>

2. Success measure: PASS | FAIL
   ...

3. Scope consistency: PASS | FAIL
   ...

4. Problem before fix: PASS | FAIL
   ...

Result: <n>/4 passed. <One sentence: ready to go further, or the single most important thing to fix first.>
```

Do not edit the brief. Offer fixes as suggestions only, and apply them only if the user asks.
