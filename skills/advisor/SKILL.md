---
name: advisor
description: Consult an advisor subagent when planning multi-step work, stuck after repeated attempts, changing approach,
  reviewing complex-task completion, or explicitly asked for a second opinion.
---

# Advisor

The main agent owns execution and the final answer. This skill requests bounded
delegation to the custom `advisor` role at the checkpoints below, subject to
higher-priority restrictions and the user's scope.

## 1. Select the checkpoint

- **Plan:** gather initial evidence, then consult before substantive changes to a
  multi-step task.
- **Stuck:** consult when repeated attempts stop producing useful evidence.
- **Change-of-approach:** consult before a material change in direction.
- **Completion:** for complex tasks, consult once the artifact and verification
  results exist, before declaring completion.
- **Explicit request:** review the decision the user identified.

Skip routine questions, trivial edits, and mechanical steps unless explicitly
requested. Normally consult once for planning and once for completion; additional
calls need new evidence or an unresolved consequential conflict. This is a soft
guideline, not an enforced quota. Continue when one concrete decision is selected.

## 2. Prepare the handoff

Supply this packet even when history inheritance is available; include only
task-relevant information and omit secrets. Mark unavailable evidence explicitly.

```text
Checkpoint and specific decision:
Goal and acceptance criteria:
User constraints and authorized scope:
Workspace and relevant absolute paths:
Current approach, alternatives, and attempts with outcomes:
Verified evidence (locations, commands/results, source links):
Uncertainties:
Previous advice and what changed (follow-ups only):
```

For completion, include actual changes or a targeted diff and distinguish checks
that passed, failed, were not run, or were environment-blocked. Continue when the
packet supports the decision without assuming access to the full conversation.

## 3. Consult

Briefly tell the user which decision is being checked. Select the `advisor` custom
role through the host's subagent interface (`agent_type: advisor` where supported).
Let the role configuration select its model and reasoning effort. Reuse the same
advisor for related follow-ups when supported; send changed evidence explicitly.

Wait for advice before dependent actions; independent in-scope work may continue.
If the role, model, or interface is unavailable or the call fails, report that
limit. Use main-agent review when appropriate, labeling it as such; do not silently
substitute a role, model, or nested CLI. This step ends with advice or an explicit
record that consultation did not complete.

## 4. Apply and verify

Evaluate advice against primary evidence and the user's acceptance criteria.
Implement in-scope corrections and run relevant checks. For a consequential
conflict, send the conflicting evidence and one focused reconciliation question;
seek a resolved decision, not repeated approval. Bring missing user choices or
permissions to the user instead of expanding scope.

Finish when the decision is supported, corrections are verified, or a remaining
limit is reported. Advice is neither authorization nor proof of completion;
report the actual verification status in the final answer.
