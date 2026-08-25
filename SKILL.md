---
name: crypto-grind
description: >
  Audit cryptographic research by grinding the joins between claims,
  constructions, representations, distributions, parameters, proofs, and
  implementations. Generate falsifiable attack hypotheses, test them with
  reproducible evidence and discriminating controls, and follow surviving
  findings only as far as the evidence supports.
---

# Crypto Grind

## Purpose

Use this skill to analyze a cryptographic paper, construction, protocol, proof, or implementation for overlooked weaknesses.

The method is **grinding**: identify places where a security argument crosses a join, determine what structure or signal survives that join, turn promising observations into falsifiable candidates, and test them reproducibly.

Two questions drive the analysis:

1. Which efficiently computable public maps preserve, expose, destroy, or collapse information that may matter to security?
2. What distribution is actually induced by the construction, rather than the distribution suggested by notation, intuition, or an idealized argument?

Do not begin from a predetermined attack type. Begin from the target's claims and structure.

Generation is deliberately high in volume and low in precision. That is affordable only because nothing a generator proposes counts as evidence until it passes the admission step in section 5. Never let a proposal's confidence, fluency, or detail substitute for that step.

## Process

### 1. Identify the target and claims

Use the latest available version of the target and record which version or date was analyzed.

Extract the security-relevant claims and the assumptions or components on which they depend.

Do not strengthen the authors' claims in order to attack them.

### 2. Find the joins

Look for transitions where a property must survive from one object or model to another, including:

- representation and encoding changes;
- projections, reductions, embeddings, rounding, or truncation;
- sampling, conditioning, or rejection;
- mathematical objects and serialization;
- theorem assumptions and concrete parameters;
- abstract primitives and protocol composition;
- ideal distributions and implemented distributions;
- specification and implementation.

Do not assume that a property established on one side of a join automatically survives the other.

### 3. Grind along both axes

#### Public maps and algebraic structure

Inspect efficiently computable public transformations.

Ask what information survives, disappears, becomes visible, or becomes easier to exploit after the map is applied. Look for useful invariants, aliases, projections, decompositions, or relations.

The map itself need not be incorrect. A correct public transformation may still expose structure useful to an attacker.

#### Induced distributions

Determine the distribution the construction actually produces after all sampling, reduction, conditioning, rejection, truncation, rounding, or deterministic derivation.

Compare that distribution with the one required or suggested by the security argument.

When practical, derive the distribution exactly before relying on experiments.

### 4. Form a candidate

Turn each promising direction into a falsifiable candidate:

```text
Claim:
The security-relevant statement being tested.

Relation:
The mathematical or algorithmic relation that may undermine it.

Predicted observable:
What must be observed if the hypothesis is correct.
```

Record any conditions or concrete parameters needed for the test.

### 5. Test with evidence and a discriminating control

Prefer, in order:

1. exact derivation;
2. minimal deterministic witness;
3. exhaustive enumeration over a manageable space;
4. deterministic computation;
5. controlled statistical experiment.

Use the parameters actually specified by the target. A run at convenient parameters rather than the specified ones is not evidence, and a bound that fails to separate at a small modulus may separate at the stated sequence.

Before treating an experiment as evidence, define a discriminating control whose expected outcome is fixed **before** it runs. A control demonstrates that the apparatus separates the hypothesized effect from a neighbouring case. Whether it is required to pass or to fail is secondary; a negative control that must fail and a positive control that must reproduce a case already known to hold are both valid. What is excluded is a check whose outcome would have been accepted either way.

A useful result has the form:

```text
target construction: predicted effect appears
control construction: predicted effect disappears
```

Treat a timeout, an out-of-memory kill, a cancellation, or a tool failure as an unresolved path. It is never a refutation.

### 6. Establish the security bridge

After confirming a local relation, follow its consequence explicitly:

```text
confirmed relation
        ↓
effect on the primitive or construction
        ↓
effect on the surrounding protocol or proof, if any
        ↓
advertised security property
```

Stop wherever the demonstrated chain stops.

Do not promote a result at one layer into a stronger claim at another layer without establishing the intermediate steps.

### 7. Push the survivor

Do not stop at the first witness.

Where relevant, determine:

- how broadly the phenomenon generalizes;
- exact exceptions or safe cases;
- affected parameter ranges;
- probability under the actual distribution;
- whether smaller or stronger witnesses exist;
- whether the effect survives realistic surrounding structure;
- whether it composes with another public operation;
- the smallest repair that removes it;
- the first boundary beyond which the argument stops working.

Push toward either a stronger consequence or a proved boundary. Both are useful outcomes. A push may also end unresolved, with neither in hand; record that rather than reporting the original result as final.

This is what separates grinding from ordinary auditing. Auditing asks whether a candidate flaw is real and stops when it has an answer. Grinding treats every verified limitation of a real flaw as the next candidate, so a confirmed result is an input rather than an endpoint.

### 8. Classify conservatively

Keep qualitatively different outcomes separate.

Useful classifications include:

- **BREAK** - the demonstrated relation reaches an advertised security property.
- **DEFECT** - a specification, construction, or mathematical statement is demonstrably wrong or structurally unsound without a complete bridge to the advertised security property.
- **PROOF GAP** - the argument does not establish the claimed result, without evidence that the construction itself is insecure.
- **PARAMETER ERROR** - concrete parameter or security accounting is incorrect.
- **COVERAGE GAP** - an experiment or argument does not cover the property or regime for which it is being used.
- **KNOWN RESULT** - the issue is already public or corrected.
- **UNRESOLVED** - the candidate cannot currently be confirmed or rejected.
- **NON-ISSUE** - the candidate is falsified or prevented by a demonstrated property.

Never coerce one category into another.

In particular:

```text
unresolved != secure
proof gap != break
local result != stronger-layer result
specification result != implementation result
failed search != evidence of security
```

Absence of a bridge to a security property does not by itself make a defect. A validated relation that falsifies nothing the source states, and narrows nothing a consumer of it relies on, is an observation and should be recorded as one rather than promoted.

Results belonging to other authors are cited at the point of use and never counted as findings, however load-bearing they are.

Preserve every material condition in summaries.

### 9. Check current status and reproducibility

Before presenting an admitted finding as new, check the current target version, relevant corrections or errata, closely related work, and public implementations where applicable.

Record enough information for another researcher to reproduce the result.

Report the whole distribution of outcomes, including targets that produced no attack, paths left unresolved, and strengthenings that were tried and failed. Output consisting only of breaks is indistinguishable from a selection procedure with an unknown filter on it.

## Parallel work

If independent subagents or workers are available, use them when parallelism is useful, for example for:

- reconstructing claims and assumptions;
- public-map/algebraic exploration;
- distribution analysis;
- parameter arithmetic;
- independent reproduction;
- checking prior work and corrections.

Do not establish correctness by majority vote.

The main analysis must reconcile the evidence, controls, conditions, and security bridge before classifying a result.

## Output

For each admitted finding, produce a compact record:

```text
TARGET
VERSION

CLAIM
SOURCE LOCATION

JOIN OR STRUCTURE EXAMINED

CANDIDATE
- relation
- predicted observable
- conditions

WITNESS / EXPERIMENT

CONTROL

RESULT

SECURITY BRIDGE

CLASSIFICATION

BOUNDARY / LIMITATIONS

REPRODUCTION

NOVELTY STATUS
```

The goal is not to generate a large number of speculative attacks. The goal is to convert promising structural observations into results that can be checked, bounded, and stated at the strength the evidence supports.
