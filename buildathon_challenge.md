# Buildathon challenge: Build a trust agent

## The challenge (105 minutes)

An LLM gives an answer. A verification tool checks it and produces a trust report. Then what?

Build an agent that takes a trust report as its input and decides what happens next. Pick a workflow from your own work where an AI answer feeds a real decision.

What the agent does is up to you: any stack, any domain.

## Requirements

1. Use your own use case.
2. The agent takes a trust report (PDF) as its input.
3. The agent uses the evidence in the report, not just the top-line verdict.
4. The agent's next action depends on that evidence (approve, rewrite, escalate, block, or pull in another source).

## The input

You get a set of sample trust reports at kickoff, each with different results. They were generated with Ezio. You can build against these alone, or generate your own report for your use case.

Each report contains:

- **Analyzed text:** the original LLM response.
- **Verdict:** a one-line summary and an issue count.
- **Module scores:** Accuracy, Bias, Tone and Agreement, each shown as a 5-block bar.
- **Claim analysis:** each claim gets a verdict (Supported / Not enough evidence) and a source list with type (Official, News, Other), title and date.
- **Findings:** notes on sentiment, factual claims, framing bias and sycophancy, each with a severity (NOTE or CRITICAL) and reasoning.

The report is evidence, not the final word. Your agent can question it: only some claims are checked, some can't be verified, and sources vary in quality.

## Sample use case (for inspiration only): Data Privacy

Your company takes on a client project and needs a data privacy policy that answers two questions:

- How long can we retain the client's data?
- What is considered private?

Someone asks an LLM what GDPR requires and gets a trust report on the answer. The agent takes that report as its input, then:

1. **Reads the report.** Keeps supported claims, treats unverified claims as unverified (not wrong), and sends critical findings to a human.
2. **Checks two more sources.** Your company's policy and the client's policy.
3. **Decides.** Compares all three, resolves conflicts with a rule you choose (e.g. the strictest wins), and outputs a retention period, what counts as private data, and the source behind each point.

Sample policies are provided in `company_policy_meridian.md` and `client_policy_solace.md`.

## Deliverable

A 2-minute demo showing your use case, the agent taking in a report, and one moment where the evidence changed what the agent did.

## Scoring criteria

Each team is scored out of 100 points.

| Criterion | Points | Low | High |
|---|---|---|---|
| Evidence-driven action | 35 | The agent behaves the same whatever the report says. | Different reports produce visibly different outcomes. |
| Evidence handling | 30 | Reads only the top-line verdict. | Weighs claims, scores, findings and source quality, and treats unverified claims differently from wrong ones. |
| Real-world fit | 20 | Copied from the sample with no changes. | A real use case with sensible points where a human steps in. |
| Demo clarity | 15 | Hard to tell what the agent did or why. | Shows the moment the evidence changed the outcome, within 2 minutes. |

**Tie-breaker:** the higher Evidence-driven action score wins.

## Schedule

- **0–10 min:** kickoff, pick your use case
- **10–85 min:** build
- **85–105 min:** demos

## Tips

- Start with one sample report and get the agent reading it before adding anything else.
- The PDF is text-based, so pass it straight to your LLM or extract it with `pypdf`.
- Scores are bars (`█░░░░`), not numbers; count the filled blocks if your code branches on them.
- Run the agent on a second report with different results to show it branching.
