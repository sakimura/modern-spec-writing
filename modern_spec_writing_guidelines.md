# Modern Spec Writing Guidelines

## Scope

This document gives rules for specification authors and editors.
The rules cover specification content, structure, and tests of implementations.

## Normative references

| Reference | Version | Rules used in this document |
| --- | --- | --- |
| [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119.html) | March 1997 | Requirement, recommendation, and permission levels |
| [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174.html) | May 2017 | Use of uppercase keywords for these levels |
| [ASD-STE100](https://www.asd-ste100.org/) | Issue 9, January 15, 2025 | English writing rules and vocabulary |
| [Mermaid sequence diagrams](https://mermaid.js.org/syntax/sequenceDiagram.html) | Mermaid 12.3.0 documentation | Sequence diagram syntax |
| [GitHub Flavored Markdown](https://github.github.com/gfm/) | 0.29-gfm, April 6, 2019 | Headings, tables, and fenced code blocks |

## Terms and definitions

**Specification.** A document that states rules for a system, protocol, format, or procedure.

**Provision.** A statement that gives a requirement, recommendation, or permission.

**Target actor.** A participant to which the specification assigns provisions.

**External actor.** A participant outside the scope of the specification's conformance rules.

**Wire message.** Data that a protocol sends between implementations.

**Variable.** A named value that can change.

## Abbreviations

| Abbreviation | Meaning |
| --- | --- |
| AI | Artificial intelligence |
| ID | Identifier |
| JSON | JavaScript Object Notation |
| RFC | Request for Comments |
| STE | Simplified Technical English |

## Actors

**Author.** A person who writes or edits a specification. The Author is the target actor in this guideline.

**AI Model.** An external actor that can make an implementation or write test requirements from a specification.

## Goal

Ambiguity can cause differences between implementations and between test results.

The first goal is to make specifications clear to humans.
The second goal is to give AI systems enough information in those specifications to make implementations and write test requirements.

## Interoperability test sequence

This informative diagram shows the test procedure in `REQ13.1`.
Model A and Model B are example labels.
The order of the replies is illustrative.
Assumption. Each model sends both requested outputs to the Author.
The replies are inputs to the checks in Step 5.
The Author examines differences in Step 6 if the results differ.

```mermaid
sequenceDiagram
    autonumber
    actor Author
    participant A as AI Model A
    participant B as AI Model B
    Author->>A: [REQ13.2, REQ13.3, REQ13.9] Specification and requests
    Author->>B: [REQ13.2, REQ13.3, REQ13.9] Same specification and requests
    A-->>Author: [REQ13.4, REQ13.5, REQ13.6] Implementation and test requirements
    B-->>Author: [REQ13.4, REQ13.5, REQ13.6] Implementation and test requirements
    Author->>Author: [REQ13.4, REQ13.5, REQ13.6] Check implementations and test requirements
    Author->>Author: [REQ13.7, REQ13.8] Record models, inputs, assumptions, and results
```

## Provisions

The uppercase keywords MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY have the meanings in RFC 2119 and RFC 8174.
Each provision applies when its condition is true.
A condition in a section applies to the provisions in that section.

### 1. Clear Scope

**REQ1.1** The Author MUST give the scope of the specification at the beginning.

### 2. Normative References

**REQ2.1** The Author MUST give a list of the external specifications necessary to interpret the specification.

**REQ2.2** The Author MUST give a version and a link for each normative reference.

**REQ2.3** The Author MUST identify the applicable rules in each normative reference.

### 3. Terms and Definitions

**REQ3.1** The Author MUST put the definitions after the normative references.

**REQ3.2** The Author MUST keep requirements and recommendations out of definitions.

**REQ3.3** When a term comes from a normative reference, the Author MUST identify that reference in the definitions.

**REQ3.4** The Author MUST NOT give a new definition to an imported term.

### 4. Abbreviations

**REQ4.1** If the specification uses abbreviations or symbols, the Author MUST put their meanings in a table before the provisions.

### 5. Actors

**REQ5.1** The Author MUST put the definitions of the actors before their provisions.

**REQ5.2** The Author MUST identify the target actors.

**REQ5.3** If interactions involve external actors, the Author MUST identify them.

### 6. Goal

**REQ6.1** The Author MUST give the problem and the intended result.

**REQ6.2** For each security claim, the Author MUST give its assumptions and limits.

### 7. Interactions and Cross-References

These provisions apply to specifications that define interactions.

**REQ7.1** The Author MUST show the interactions in a Mermaid sequence diagram.

**REQ7.2** The Author MUST use `autonumber` in each sequence diagram.

**REQ7.3** The Author MUST NOT add manual step numbers to the diagram.

**REQ7.4** The Author MUST NOT refer to a diagram note as a numbered step.

**REQ7.5** For each message, the Author MUST give its provision IDs and key parameters.

**REQ7.6** For each variable used in an interaction, the Author MUST identify its steps and provisions.

**REQ7.7** For each provision that applies to an interaction, the Author MUST identify its steps.

**REQ7.8** The Author MUST make the diagrams, tables, and provisions agree.

**REQ7.9** The Author MUST identify optional paths and illustrative choices in the diagram or its description.

### 8. Active Voice and Actor Ownership

**REQ8.1** The Author MUST make the actor the subject of each provision.

**REQ8.2** For each interaction with an external actor, the Author MUST give the required behavior of the target actor.

**REQ8.3** The Author MUST identify each assumption about the behavior of an external actor.

### 9. Labeled, Atomic Provisions

**REQ9.1** The Author MUST put each provision in a separate paragraph or numbered item.

**REQ9.2** The Author MUST give each provision a unique ID.

**REQ9.3** The Author MUST identify the actor, condition, action, and expected result of each provision.

**REQ9.4** For each specified failure action, the Author MUST write a separate provision.

**REQ9.5** For each failure action, the Author MUST identify the provision for the input rule or failed check.

**REQ9.6** For a received message, the Author MUST give separate conditions for receipt and acceptance as valid.

**REQ9.7** The Author MUST use the prefix in the table for each provision ID.

| Prefix | Keywords |
| --- | --- |
| `REQ` | MUST or MUST NOT |
| `REC` | SHOULD or SHOULD NOT |
| `PERM` | MAY |

### 10. Simplified Technical English

**REQ10.1** The Author MUST use ASD-STE100 for the English text of the specification.

**REQ10.2** The Author MUST use short sentences.

**REQ10.3** The Author MUST put one instruction in each sentence.

**REQ10.4** The Author MUST use the same term for the same concept.

### 11. Structured Variable Constraints

These provisions apply when the specification defines variables.

**REQ11.1** The Author MUST put variable constraints in a Markdown table or JSON Schema.

**REQ11.2** For each variable, the Author MUST give its type, presence, permitted values, and prohibited values.

**REQ11.3** The Author MUST show which values the specification prohibits and which values it does not specify.

**REQ11.4** For each list of values, the Author MUST show if extensions are possible.

**REQ11.5** The Author MUST show where letter case changes the meaning of a value.

**REQ11.6** For encoded values, the Author MUST show the data values separately from their encoded forms.

**REQ11.7** If quotation marks show the limits of a value, the Author MUST identify those marks.

**REQ11.8** If data contains quotation marks, the Author MUST identify them separately from the marks that enclose the value.

**REQ11.9** For a variable constraint table, the Author MUST use the columns in the table below.

The list of provision ID prefixes is complete. The prefix is case-sensitive.

| Variable / Parameter | Context | Sequence Step & Provisions | Type | Presence | Allowed Values | Disallowed Values |
| --- | --- | --- | --- | --- | --- | --- |
| Provision ID prefix | Beginning of a provision ID | `REQ9.7` | Text | Required | `REQ`, `REC`, or `PERM` as specified by the keyword | All other values |
| Specification version | Input to each AI Model | Steps 1 and 2, `REQ13.2` | Document version | Required | Same version for all models | Different versions for different models |
| Number of AI Models | Models that get the specification | Steps 1 and 2, `REQ13.2` | Integer | Required | Two or more different models | Fewer than two different models |

### 12. Wire Examples and Tests

**REQ12.1** If an example contains wire messages, the Author MUST put them in fenced code blocks.

**REQ12.2** If the specification defines a wire protocol, the Author MUST show typical flows and main errors in wire examples.

**REQ12.3** The Author MUST identify illustrative examples as non-normative.

**REQ12.4** For each example, the Author MUST identify its applicable steps and provisions.

**REQ12.5** The Author MUST NOT add requirements in examples.

**REQ12.6** For wire examples, the Author MUST make sure that byte counts, escaping, and encoding are correct.

**REQ12.7** For each wire example, the Author MUST identify placeholders and omitted data.

**REQ12.8** For detailed cases, the Author MUST use test vectors or test requirements.

**REQ12.9** The Author MUST include valid, invalid, and boundary cases in the tests.

**REQ12.10** For each case, the Author MUST give the expected result and the provision that specifies it.

### 13. AI Interoperability Testing

These provisions apply to specifications for protocols that independent implementations can use to exchange messages.

**REQ13.1 (Steps 1 to 6)** Before the specification becomes final, the Author MUST do the interoperability test in this section.

**REQ13.2 (Steps 1 and 2)** The Author MUST give the same specification version to at least two different AI Models.

**REQ13.3 (Steps 1 and 2)** The Author MUST tell each AI Model to make an independent implementation.

**REQ13.4 (Steps 3 to 5)** The Author MUST do a test that shows if the implementations exchange messages correctly.

**REQ13.5 (Steps 3 to 5)** The Author MUST compare each implementation with the provisions.

**REQ13.6 (Steps 3 to 5)** The Author MUST compare the generated test requirements with the provisions.

**REQ13.7 (Step 6)** The Author MUST record the models, inputs, assumptions, and results.

**REQ13.8 (Step 6)** If the results differ, the Author MUST examine the differences for ambiguities in the specification.

**REQ13.9 (Steps 1 and 2)** The Author MUST tell each AI Model to write test requirements.

## Examples (non-normative)

### Separate provisions for a check and a failure action

This example illustrates `REQ9.4` and `REQ9.5`.

**REQ-EX1** Before review, the Author MUST make sure that each provision ID is unique.

**REQ-EX2** If the check in `REQ-EX1` finds a duplicate, the Author MUST correct the duplicate ID.

### Test requirements

These cases check a provision ID for a requirement with the keyword MUST.
Each ID is a sample input.

| Input | Case | Expected result | Provision |
| --- | --- | --- | --- |
| `REQ1.1` | Valid | The prefix is correct for MUST. | `REQ9.7` |
| `REC1.1` | Invalid | The prefix is incorrect for MUST. | `REQ9.7` |
| `req1.1` | Invalid case | The prefix is incorrect because it has lowercase letters. | `REQ9.7`, `REQ11.5` |
| `1.1` | Boundary with no prefix | The ID has no prefix and fails the check. | `REQ9.7` |

The [OAuth Form Post example](examples/oauth_2_0_form_post_response_mode_1_0_modern_spec.md) shows an application to a wire protocol.
