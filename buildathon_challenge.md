# Buildathon challenge: Build a trust agent

## The challenge (105 minutes)

An LLM gives an answer. A verification tool checks it and produces a trust report. Then what?

Build an agent that takes a trust report as its input and decides what happens next. Generate sample reports on the Ezio website, choose a decision that depends on the answer, and build the agent that makes the call.

What the agent does is up to you: any stack, any harness.

## What to build

1. Pick one of the four sample trust reports (see below) as your main report and build your agent around it.
2. The agent uses the evidence in the report, not just the top-line verdict.
3. The agent's next action depends on that evidence (approve, rewrite, escalate, block, or pull in another source).
4. The agent also runs on one of the other three reports and reaches a decision that fits that report.

## The input

1. Go to **ezioai.io** and select **Try Product**.
2. Enter the hackathon code: **EZIOHACK2026**
3. Generate your main report and one other from the four samples:
   - Nuclear energy
   - Work from home
   - EV market
   - AGI timelines
4. Export each report as a PDF. These are your agent's inputs.

Then decide who is relying on the answer and for what, for example a comms lead deciding whether to publish the work-from-home piece, or an analyst deciding whether the EV market answer can go into a client note.

Each report contains:

- **Analyzed text:** the original LLM response.
- **Verdict:** a one-line summary and an issue count.
- **Module scores:** Accuracy, Bias, Tone and Agreement, each shown as a 5-block bar.
- **Claim analysis:** each claim gets a verdict (e.g. Supported / Not enough evidence) and a source list with type (Official, News, Other), title and date.
- **Findings:** notes on sentiment, factual claims, framing bias and sycophancy, each with a severity (NOTE or CRITICAL) and reasoning.

The report is evidence, not the final word. Your agent can question it: only some claims are checked, some can't be verified, and sources vary in quality.

## Useful resources

- Website: ezioai.io → Try Product
- Hackathon code: EZIOHACK2026

## Deliverable

A 1–2 minute demo video showing the decision at stake and the agent taking in a report and deciding the next best action.

**Two reports in the demo.** The video must show the agent run on your main report and on one of the other three, even if the second run is only 20 seconds. A hard-coded script gives the same output for both; a real agent gives a different, sensible decision for each. A demo with only one report will not be scored.

## Scoring criteria

Each team is scored out of 100 points.

| Criterion | Points | Low | High |
|---|---|---|---|
| Evidence use | 35 | Reads only the top-line verdict. | Weighs claims, scores, findings and source quality, and treats unverified claims differently from contradicted ones. |
| Decision quality | 30 | The action is generic or doesn't follow from the report. | The action fits the case, and every reason traces back to a specific claim, score, finding or source. The agent also notes what the report couldn't check. |
| Human in the loop | 20 | Decides and acts with no human involved. | Hands off to an accountable human at the right moments, explains why, and updates its decision as the human responds. |
| Demo clarity | 15 | Hard to tell what the agent did or why. | Shows, on both reports, how the claim evidence was used to decide the next best action. |

## Schedule

- **0–10 min:** kickoff, generate your sample reports
- **10–85 min:** build
- **85–105 min:** demos

## Tips

- Generate and export your reports first, and get the agent reading one before adding anything else.
- The PDF is text-based, so pass it straight to your LLM or extract it with `pypdf`.
- Scores are bars (`█░░░░`), not numbers; count the filled blocks if your code branches on them.
- Pick the decision early: who is relying on this answer, and what would they do with it?
- Build against your main report, then test on your second report well before the deadline, not during the recording.
