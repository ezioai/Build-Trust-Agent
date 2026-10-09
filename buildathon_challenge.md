# Buildathon challenge: Build a trust agent

## The challenge (105 minutes)

Build an agent that takes an Ezio report as its input and acts on it. Pick a workflow from your own work where an LLM's answer feeds a real decision; your agent reads the Ezio report on that answer and decides what happens next.

What the agent does is up to you: any stack, any domain.

## Requirements

1. Use your own use case.
2. The agent takes the Ezio report (PDF) as its input.
3. The agent uses the whole report, not just the verdict line.
4. The agent's next action depends on the report (approve, rewrite, escalate, block, pull in another source, or request a new report).

## Getting the report (human step)

A person pastes the LLM response into Ezio, exports the PDF, and gives it to the agent.

## What the agent receives

- **Analyzed text:** the original LLM response.
- **Verdict:** a one-line summary (e.g. "2 of 2 checkable claims hold up, 3 could not be checked") and an issue count.
- **Module scores:** Accuracy, Bias, Tone and Agreement, each shown as a 5-block bar.
- **Claim analysis:** each claim gets a verdict (Supported / Not enough evidence) and a source list with type (Official, News, Other), title and date.
- **Findings:** Sentiment & Objectivity, Factual Claim Analysis, Framing Bias Detection and Sycophancy Detection, each with a severity (NOTE or CRITICAL) and reasoning.

## Sample use case (for inspiration only): Data Privacy

Your company takes on a client project and needs a data privacy policy that answers two questions:

- How long can we retain the client's data?
- What is considered private?

A person asks an LLM what GDPR requires, runs the response through Ezio, and exports the PDF. The Trust Agent takes that report as its input, then:

1. **Reads the report.**
   - Keeps "Supported" claims; treats "Not enough evidence" claims as unverified, not wrong.
   - Asks for a new report if Accuracy or Bias is low.
   - Sends a CRITICAL finding (e.g. one-sided framing) to a human or triggers a rewrite.
   - Notes the sources, giving more weight to Official ones.
2. **Checks two more sources.**
   - Company policy (RAG): your company's position.
   - Other company policy (RAG): the client's position.
3. **Decides.** Compares all three, resolves conflicts with a rule you choose (e.g. the strictest wins), and outputs a retention period, what counts as private data, and the source behind each point.

Sample policies are provided in `company_policy_meridian.md` and `client_policy_solace.md`.

## Deliverable

A 2-minute demo showing your use case, the agent taking in a report, and one moment where the report's contents changed what the agent did.

## Judging

- **Integration (35%):** does the report drive the agent, or is it only displayed?
- **Depth of use (30%):** how much of the report drives behavior?
- **Real-world fit (20%):** would someone actually use this?
- **Demo clarity (15%)**

## Schedule

- **0–10 min:** kickoff, pick your use case
- **10–85 min:** build
- **85–105 min:** demos

## Tips

- Generate your first report early so the agent has a real input to build against.
- The PDF is text-based, so pass it straight to your LLM or extract it with `pypdf`.
- Scores are bars (`█░░░░`), not numbers; count the filled blocks if your code branches on them.
- Ezio only assesses the claims it lists, so other statements in the response are unchecked.
- Feed the agent a second report with different results (e.g. a balanced answer) to show it branching.
