# Modern Spec Writing Guidelines

Write specifications that humans can understand.
Give AI systems enough information to create implementations and test requirements.

## Suggested Provisions

1. **Clear Scope**: State what the document specifies at the beginning.

2. **Normative References**: List all external specifications needed to interpret the document.
   Give their versions and links.
   Identify the external rules that implementations must use.

3. **Terms and Definitions**: Put definitions after normative references.
   Definitions MUST NOT contain requirements or recommendations.
   Import external terms without redefining them.
   Example: `From [RFC6749]: Client, Authorization Server`.

4. **Abbreviations**: Provide an abbreviations and symbols table before the main content.

5. **Actors**: Define actors before their requirements.
   Identify the actors that must conform to the specification.
   Identify external actors, such as browsers and intermediaries.

6. **Goal**: State the problem and the intended result.
   State the assumptions and limits of each security claim.

7. **Interactions and Cross-References**: Show interactions in a Mermaid `sequenceDiagram`.
   Enable `autonumber`.
   Do not add a second set of step numbers.
   Do not count notes as numbered messages.

   - Label each message with its provision IDs and key parameters.
   - Link each variable to its steps and provisions.
   - Link each provision to its steps.
   - Keep diagrams, tables, and provisions consistent.
   - Label optional paths and illustrative choices.

8. **Active Voice and Actor Ownership**: Make the actor the subject.
   Example: “The Client MUST verify the signature.”
   For external actors, specify what the implementation must send or expect.
   Do not promise that an external actor will obey an instruction.

9. **Labeled, Atomic Provisions**: Put one provision on each line or numbered item.
   Give each provision a unique ID.
   State the actor, condition, action, and expected result.
   Give each failure action its own provision.
   Reference the provision for the input rule or failed check.
   Distinguish receipt of a message from acceptance as valid.
   Use these prefixes:

   - `REQ`: MUST or MUST NOT.
   - `REC`: SHOULD or SHOULD NOT.
   - `PERM`: MAY.

10. **Simplified Technical English (STE)**: Use Simplified Technical English (ASD-STE100).
    Keep sentences short.
    Put one instruction in each sentence.
    Use the same term for the same concept.

11. **Structured Variable Constraints**: Use a Markdown table or JSON Schema.
    State types, allowed values, prohibited values, and presence rules.
    Distinguish prohibited values from unspecified cases.
    State whether lists are complete or permit extensions.
    State where case matters.
    Distinguish data values from their encoded forms.
    Explain which quotation marks are delimiters.
    Do not confuse delimiters with quotation marks inside data.

    Use these table columns:
    `Variable / Parameter`, `Context`, `Sequence Step & Provisions`,
    `Type`, `Presence`, `Allowed Values`, and `Disallowed Values`.

12. **Wire Examples and Tests**: Put wire messages in fenced code blocks.
    Use wire examples for typical flows and main errors.
    Mark illustrative examples as non-normative.
    Link them to steps and provisions.
    Examples MUST NOT add requirements.
    Check byte counts, escaping, and encoding.
    Identify placeholders and omitted data.
    Use test vectors or test requirements for detailed cases.
    Include valid, invalid, and boundary cases in those tests.
    A full wire message is not needed for each case.
    Give the expected result for each case and its governing provision.

13. **AI Interoperability Testing**: Test before the specification becomes final.
    Give the same document to at least two different AI models.
    Ask each model to create an implementation independently.
    Check whether the implementations interoperate.
    Check each implementation against the provisions.
    Check whether AI-generated test requirements agree with those provisions.
    Record the models, inputs, assumptions, and results.
    Use disagreements to find ambiguities in the document.

## Examples

### EXAMPLE 1: Atomic provisions

* **REQ1.1 (Step 1)**: To request Form Post Response Mode, the Client MUST include `response_mode` in the Authorization Request.
* **REQ1.2 (Step 1)**: When the Client requests Form Post Response Mode, the Client MUST set `response_mode` to `form_post`.

Each provision has one action and one ID.

### EXAMPLE 2: Variable constraints

| Variable / Parameter | Context | Sequence Step & Provisions | Type | Presence | Allowed Values | Disallowed Values |
| --- | --- | --- | --- | --- | --- | --- |
| `response_mode` | Requesting Form Post Response Mode | Step 1 (`REQ1.1`, `REQ1.2`) | String | Required | Exact string `form_post` | Any other value in this context |

### EXAMPLE 3: A test requirement

- **Provision**: `REQ1.2`.
- **Condition**: The Client requests Form Post Response Mode.
- **Observation**: Read `response_mode` in the generated request.
- **Expected result**: The decoded value is exactly `form_post`.

This test checks the Client's output.
It does not define how a server must handle other values.
