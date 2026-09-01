---
name: intent-distiller
description: Use when interpreting, extracting, rewriting, or reviewing prose whose author-specific point is obscured by generic background, polished expansion, repetition, or AI-assisted wording.
---

# Intent Distiller

## Scope

This context distinguishes what an author personally contributed from prose that merely makes a text complete or plausible. It applies to proposals, messages, meeting notes, and AI-expanded drafts.

It does not determine whether AI wrote the text. It is not a conventional summary rule: textual prominence, repetition, and coverage do not by themselves make a claim author-specific.

## Conceptual Model

Treat each semantic claim as one of three kinds:

| Kind | Meaning |
|---|---|
| **Core intent** | The author's own assertion, choice, rejection, priority, commitment, concern, hypothesis, tension, or decision-driving observation |
| **Support** | Concrete evidence, constraint, example, or reasoning needed to understand a core intent |
| **Scaffolding** | Generic background, obvious explanation, rhetorical framing, repetition, exhaustive coverage, or polished connective prose that the topic alone could have supplied |

The governing question is:

> Why did this particular author bother saying this?

A useful counterfactual is: *Would the same claim likely appear if someone knew only the topic, but none of this author's opinions, observations, choices, or concerns?* If yes, it is probably scaffolding. Polished style is not evidence that the underlying claim is generic.

## Author-Specific Signals

Evidence for core intent becomes stronger when a claim contains one or more of these signals:

- a choice between alternatives or an explicit priority;
- commitment, requirement, refusal, or disagreement;
- a cost, downside, or trade-off the author knowingly accepts;
- situation-specific experience, observation, constraint, or unusual detail;
- concern, discomfort, contradiction, or unresolved question;
- a non-obvious claim that changes what someone would decide or do.

These are judgment dimensions, not a numeric quota. A fact is support unless the author's noticing or interpretation of it is itself the point. Prominence and importance do not make a generic claim author-specific.

## Fidelity Rules

Within any extraction, summary, rewrite, or review governed by this context:

- The retained intent has source support and does not invent an author motive.
- The author's certainty, scope, conditions, and accepted degree of trade-off remain unchanged.
- Core intent is distinguishable from supporting evidence and from newly generated connective language.
- Ambiguous authorship or intent remains ambiguous; plausible inference is not presented as established intent.
- Omitting scaffolding does not remove a premise required to understand the retained intent.

Extraction and regeneration are different operations. A fluent paraphrase is a reconstruction rather than evidence. For example, “ROI may fall somewhat, but B has priority” does not support the stronger “ROI does not matter; choose B.”

This context supplies classification and fidelity criteria only. The active task or process determines whether the result is quoted, summarized, rewritten, reviewed, or presented in any particular format.
