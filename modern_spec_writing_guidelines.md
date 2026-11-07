# Modern Spec Writing Guidelines

The consumer of the spec will increasingly be AI agents.
Humans will feed AI Agents the specifications to create implementations.

In this respect, we need to write specifications in such a way that it will be clear for AI Agents. That in turn will make the spec more understandable for humans as well.

## Suggested Provisions

 1. **Clear Scope**: State clearly what the document specifies at the very beginning.

 2. **Normative References**: All external references that need to be brought into context for the interpretation of the document MUST be listed here (akin to `include` or `import` in programming languages).

 3. **Terms and Definitions**: Follow Normative References with Terms and Definitions.

    * Definitions MUST NOT contain requirements or recommendations. Their sole purpose is to remove ambiguity where the same string might represent different concepts.

    * **Importing External Terms**: When using terms defined in Normative References without modification, do not redefine them. Explicitly declare them as imports (e.g., `From [RFC6749]: Client, Authorization Server`).

 4. **Abbreviations**: An abbreviations and symbols table MUST be provided before the main content.

 5. **Actors**: All actors MUST be explicitly defined before stating any requirements and recommendations. Distinguish between **Target Implementation Actors** (to whom normative requirements apply) and **External / Uncontrolled Actors** (such as standard browsers or network intermediaries).

 6. **Goal**: Clearly state the goal of the specification (including the problem it solves or the security/functional property it achieves).

 7. **Interactions & Cross-Referencing**: Express the interactions among and within actors using a sequence diagram in Mermaid format (`sequenceDiagram`) with `autonumber` enabled.

    * **Explicit Traceability**: Cross-reference sequence steps, variable parameters, and normative provisions so AI agents can map state transitions directly to validation and business logic:
      1. In the **Sequence Diagram**, annotate each message with the relevant Provision IDs (e.g., `[REQ1]`, `[REQ3, PERM1]`) and key parameters.
      2. In the **Variable Constraints Table**, include a `Sequence Step & Provisions` column linking each parameter to its sequence step(s) and governing provision(s).
      3. In the **Provisions (Requirements/Recommendations/Permissions)**, explicitly reference the corresponding sequence step (e.g., `(Step 4)`).

 8. **Active Voice & Actor Ownership**: Use active voice where an Actor is the explicit subject (e.g., "Actor1 MUST verify the signature of the message", instead of "The signature of the message MUST be verified").

    * **Handling Out-of-Scope Actors**: When a flow depends on the standard behavior of an external/uncontrolled actor (e.g., a standard web browser or OS), frame the requirement around what the target implementation actors (e.g., Server or Client) MUST output to trigger that behavior or MUST expect to receive from it.

 9. **Labeled, Atomic Provisions**: State one provision (requirement, recommendation, or permission) per line or numbered sub-list. All provisions MUST be uniquely labeled so they can be referenced unambiguously. Use standardized prefixes corresponding to RFC 2119 levels:

    * **`REQ`** for `MUST` / `MUST NOT` (Requirements)

    * **`REC`** for `SHOULD` / `SHOULD NOT` (Recommendations)

    * **`PERM`** for `MAY` (Permissions)

10. **Simplified Technical English (STE)**: Use Simplified Technical English (ASD-STE100). Combined with provisions 7, 8, and 9 above, it will look like EXAMPLE 1 below.

11. **Structured Variable Constraints**: For variable values, parameters, and attributes, explicitly specify what is allowed and what is not. Format these constraints as a structured Markdown table (with columns: `Variable / Parameter`, `Context`, `Sequence Step & Provisions`, `Type`, `Allowed Values`, `Disallowed Values`) or a JSON Schema so AI agents can directly generate validation logic. Also state meta-rules (e.g., whether quotation marks in the spec are literal or delimiters).

12. **Wire Examples / Test Vectors (Non-Normative)**: Include concrete, machine-readable examples of inputs, outputs, and protocol messages in fenced code blocks. Clearly mark them as non-normative and link them to the corresponding Sequence Diagram step and Provisions. This serves as ground-truth context for AI code generation.

13. **AI Interoperability Testing**: When a feature reaches the implementable stage (and before going to final), feed the document to at least two different AI models to independently create implementations, and test if those implementations successfully interoperate.

## Examples

### EXAMPLE 1 (Provisions 7, 8, 9, and 10)

* **REQ1 (Step 2)**: When Actor1 receives the token in Step 2, Actor1 **MUST**:

  1. Extract the `iss` parameter value from the token payload;

  2. Obtain the verification key corresponding to the `iss` value;

  3. Verify the digital signature of the token.

*(Note: We can now point to the signature verification requirement unambiguously as **REQ1.3**, and know immediately that it executes at **Step 2** of the sequence diagram.)*

### EXAMPLE 2 (Provisions 7 and 11 - Cross-Referenced Variable Constraints Table)

| Variable / Parameter | Context | Sequence Step & Provisions | Type | Allowed Values | Disallowed Values | 
| ----- | ----- | ----- | ----- | ----- | ----- | 
| `response_mode` | Authorization Request | Steps 1, 2 (`REQ1.1`, `REQ1.2`, `REQ2`) | String | Exact string `form_post` | Quoted strings (e.g., `"form_post"`), case variations (`FORM_POST`), empty string. | 
