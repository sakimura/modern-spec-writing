# Modern Spec Writing Guidelines

Write specifications that humans can understand.

Give AI systems enough information to create implementations and test requirements.

## Suggested Provisions

### 1. Clear Scope

**1.1** State what the document specifies at the beginning.

### 2. Normative References

**2.1** List all external specifications needed to interpret the document.

**2.2** Give their versions and links.

**2.3** Identify the external rules that implementations must use.

### 3. Terms and Definitions

**3.1** Put definitions after normative references.

**3.2** Definitions MUST NOT contain requirements or recommendations.

**3.3** Import external terms without redefining them.

Example: `From [RFC6749]: Client, Authorization Server`.

### 4. Abbreviations

**4.1** Provide an abbreviations and symbols table before the main content.

### 5. Actors

**5.1** Define actors before their requirements.

**5.2** Identify the actors that must conform to the specification.

**5.3** Identify external actors, such as browsers and intermediaries.

### 6. Goal

**6.1** State the problem and the intended result.

**6.2** State the assumptions and limits of each security claim.

### 7. Interactions and Cross-References

**7.1** Show interactions in a Mermaid `sequenceDiagram`.

**7.2** Enable `autonumber`.

**7.3** Do not add a second set of step numbers.

**7.4** Do not count notes as numbered messages.

**7.5** Label each message with its provision IDs and key parameters.

**7.6** Link each variable to its steps and provisions.

**7.7** Link each provision to its steps.

**7.8** Keep diagrams, tables, and provisions consistent.

**7.9** Label optional paths and illustrative choices.

### 8. Active Voice and Actor Ownership

**8.1** Make the actor the subject.

**8.2** For external actors, specify what the implementation must send or expect.

**8.3** Do not promise that an external actor will obey an instruction.

Example: “The Client MUST verify the signature.”

### 9. Labeled, Atomic Provisions

**9.1** Put one provision on each line or numbered item.

**9.2** Give each provision a unique ID.

**9.3** State the actor, condition, action, and expected result.

**9.4** Give each failure action its own provision.

**9.5** Reference the provision for the input rule or failed check.

**9.6** Distinguish receipt of a message from acceptance as valid.

**9.7** Use these prefixes:

| Prefix | Keywords |
| --- | --- |
| `REQ` | MUST or MUST NOT. |
| `REC` | SHOULD or SHOULD NOT. |
| `PERM` | MAY. |

### 10. Simplified Technical English (STE)

**10.1** Use Simplified Technical English (ASD-STE100).

**10.2** Keep sentences short.

**10.3** Put one instruction in each sentence.

**10.4** Use the same term for the same concept.

### 11. Structured Variable Constraints

**11.1** Use a Markdown table or JSON Schema.

**11.2** State types, allowed values, prohibited values, and presence rules.

**11.3** Distinguish prohibited values from unspecified cases.

**11.4** State whether lists are complete or permit extensions.

**11.5** State where case matters.

**11.6** Distinguish data values from their encoded forms.

**11.7** Explain which quotation marks are delimiters.

**11.8** Do not confuse delimiters with quotation marks inside data.

**11.9** Use these table columns: `Variable / Parameter`, `Context`, `Sequence Step & Provisions`, `Type`, `Presence`, `Allowed Values`, and `Disallowed Values`.

### 12. Wire Examples and Tests

**12.1** Put wire messages in fenced code blocks.

**12.2** Use wire examples for typical flows and main errors.

**12.3** Mark illustrative examples as non-normative.

**12.4** Link them to steps and provisions.

**12.5** Examples MUST NOT add requirements.

**12.6** Check byte counts, escaping, and encoding.

**12.7** Identify placeholders and omitted data.

**12.8** Use test vectors or test requirements for detailed cases.

**12.9** Include valid, invalid, and boundary cases in those tests.

**12.10** Give the expected result for each case and its governing provision.

A full wire message is not needed for each case.

### 13. AI Interoperability Testing

**13.1** Test before the specification becomes final.

**13.2** Give the same document to at least two different AI models.

**13.3** Ask each model to create an implementation independently.

**13.4** Check whether the implementations interoperate.

**13.5** Check each implementation against the provisions.

**13.6** Check whether AI-generated test requirements agree with those provisions.

**13.7** Record the models, inputs, assumptions, and results.

**13.8** Use disagreements to find ambiguities in the document.

## Examples

### EXAMPLE 1: Atomic provisions

**REQ1.1 (Step 1)**: To request Form Post Response Mode, the Client MUST include `response_mode` in the Authorization Request.

**REQ1.2 (Step 1)**: When the Client requests Form Post Response Mode, the Client MUST set `response_mode` to `form_post`.

Each provision has one action and one ID.

The next pair shows a check and a separate failure action.
It uses [RFC 6749, Sections 3.1.2.3 and 3.1.2.4](https://www.rfc-editor.org/rfc/rfc6749.html#section-3.1.2.3).
It is not a complete OAuth validation procedure.

**REQ2.1 (Step 2)**: The Authorization Server MUST check a supplied `redirect_uri` under RFC 6749, Section 3.1.2.3.

**REQ2.2 (Step 2)**: If the check in `REQ2.1` fails, the Authorization Server MUST NOT automatically redirect the User Agent to that URI.

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
