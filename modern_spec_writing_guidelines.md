# Modern Spec Writing Guidelines

Specifications serve AI systems, human readers, security analysts, and test developers. These guidelines aim to make behavior clear enough to implement, explain, assess, and test without inventing missing rules.

This is a working guideline. Its provisions govern specification writing; they do not themselves add requirements to the protocols being described. The words MUST, SHOULD, and MAY below express this guideline's writing rules.

The goal is guidance whose application produces less ambiguous specifications that humans can understand and AI systems can use to create implementations and test requirements. It applies to new specifications as well as revisions of existing ones.

Examples are experiments for evaluating and improving the guidance. Maintaining a mapping between an example and its original specification is a non-goal. Internal links between a specification's actors, interactions, provisions, constraints, and tests remain useful because they connect behavior to implementation and verification. The [OAuth example review](examples/oauth_2_0_form_post_response_mode_1_0_review.md) records lessons from the first experiment.

## Suggested Provisions

 1. **Clear Scope**: State clearly what the document specifies at the very beginning.

 2. **Normative References**: All external references required to interpret or implement the document MUST be listed here, with a version or date, authoritative link, and relevant sections. Distinguish normative dependencies from informative reading. A bibliography entry alone does not identify which dependency provisions apply. State which behavior each dependency supplies so readers and AI systems know what must be brought into context.

 3. **Terms and Definitions**: Follow Normative References with Terms and Definitions.

    * Definitions MUST NOT contain requirements or recommendations. Their sole purpose is to remove ambiguity where the same string might represent different concepts.

    * **Importing External Terms**: When using terms defined in Normative References without modification, do not redefine them. Explicitly declare them as imports (e.g., `From [RFC6749]: Client, Authorization Server`).

 4. **Abbreviations**: An abbreviations and symbols table MUST be provided before the main content.

 5. **Actors**: All actors MUST be explicitly defined before stating any requirements and recommendations. Distinguish between **Target Implementation Actors** (to whom normative requirements apply) and **External / Uncontrolled Actors** (such as standard browsers or network intermediaries).

 6. **Goal**: Clearly state the goal of the specification (including the problem it solves or the security/functional property it achieves). Separate intended benefits from guaranteed properties. State the assumptions, limits, and remaining exposure paths behind security claims; avoid universal claims that depend on unstated assumptions.

 7. **Interactions & Cross-Referencing**: Express the interactions among and within actors using a sequence diagram in Mermaid format (`sequenceDiagram`) with `autonumber` enabled for message numbering. Use stable event IDs (e.g., `FLOW-SUBMIT`) for cross-references; rendered numbers are navigation aids. Do not embed a competing numeric step sequence in message text or count notes as numbered messages. Label diagrams as normative or informative, and label implementation-specific paths as illustrative. A diagram MUST NOT narrow a permission stated in the provisions.

    * **Explicit Traceability**: Cross-reference events, variable parameters, and normative provisions so AI agents can map state transitions directly to validation and business logic:
      1. In the **Sequence Diagram**, annotate each message with its event ID, the relevant Provision IDs (e.g., `[REQ1]`, `[REQ3, PERM1]`), and key parameters.
      2. In the **Variable Constraints Table**, include an `Event & Provision IDs` column linking each parameter to its event(s) and governing provision(s).
      3. In the **Provisions (Requirements/Recommendations/Permissions)**, explicitly reference the corresponding event ID (e.g., `(FLOW-SUBMIT)`). For an existing example that uses step numbers, check every reference when revising the diagram.

 8. **Active Voice & Actor Ownership**: Preserve imported role definitions; describe an actor's responsibilities in this document without redefining its identity or adding eligibility conditions. Use active voice where an Actor is the explicit subject (e.g., "Actor1 MUST verify the signature of the message", instead of "The signature of the message MUST be verified").

    * **Handling Out-of-Scope Actors**: When a flow depends on the standard behavior of an external/uncontrolled actor (e.g., a standard web browser or OS), frame the requirement around what the target implementation actors (e.g., Server or Client) MUST output to trigger that behavior or MUST expect to receive from it.

 9. **Labeled, Atomic Provisions**: State one provision (requirement, recommendation, or permission) per line or numbered sub-list. All provisions MUST be uniquely labeled so they can be referenced unambiguously. Keep identifiers stable across revisions; do not reuse a removed identifier for a different obligation. Each provision MUST identify its actor, trigger or applicability condition, obligation, and observable outcome. Grouping MUST preserve conditions and ordering without making optional steps mandatory. Use standardized prefixes corresponding to RFC 2119 levels:

    * **`REQ`** for `MUST` / `MUST NOT` (Requirements)

    * **`REC`** for `SHOULD` / `SHOULD NOT` (Recommendations)

    * **`PERM`** for `MAY` (Permissions)

10. **Plain Technical Language**: Use consistent terms, explicit subjects, and short sentences. Controlled-language practices such as Simplified Technical English (ASD-STE100) can help. Claim compliance with a named controlled-language standard only if it has been checked. Language simplification MUST preserve technical qualifications and normative meaning.

11. **Structured Variable Constraints**: Describe values in a Markdown table or a suitable schema. Include `Variable / Parameter`, `Context / Representation Layer`, `Event & Provision IDs`, `Type`, `Presence / Multiplicity`, `Allowed Values / Constraints`, and `Invalid / Unspecified Handling`. Distinguish explicit prohibitions from unspecified behavior. State whether a set is exhaustive, extensible, or illustrative. An unspecified case MUST NOT become forbidden merely to complete a table or schema. A schema MUST identify what it validates and which cross-field, stateful, or external checks remain outside it.

    * **Representation Layers**: Distinguish a value from its presentation in prose, HTML attribute serialization, form encoding, and decoded application representation. Presentation delimiters are not data. Escaping a data character does not prohibit that character in the decoded value. Scope case sensitivity to the relevant field and layer; do not apply one blanket rule to protocol values, headers, media types, and HTML syntax.

12. **Wire Examples / Test Vectors**: Mark each example as normative or non-normative and link it to event and provision IDs. Non-normative examples illustrate permitted choices; they are not a source of additional requirements or a complete conformance oracle. Identify omitted context, placeholder values, and whether a message is a complete wire message or a display excerpt. Check lengths in octets, encoding round trips, escaping, and agreement between related messages. Separate replayable bytes from formatting line breaks. Include positive, negative, and boundary cases with expected outcomes justified by provisions; do not invent rejection rules for unspecified cases.

13. **AI Interoperability Testing**: When a feature reaches the implementable stage (and before going to final), feed the same identified document revision to at least two different AI models to independently create implementations and test interoperability. Record model identity as reported, date, prompts, supplied references, assumptions, implementation revisions, test cases, and observed results. Missing details MUST be stated rather than guessed. Derive expected outcomes from the specification's provisions and check implementations against them as well as against each other: two implementations can share the same misinterpretation. Distinguish interoperability, conformance, and security evidence; state which checks have not been performed.

14. **Behavioral Completeness**: Describe enough behavior for the intended implementation and test scope. For each interaction, state the actor, trigger, required inputs, preconditions, processing rules, outputs, and resulting state. Explain permitted alternatives, defaults, and relevant ordering or repetition rules. Identify behavior delegated to a normative dependency and explicitly flag unresolved decisions. Do not fill gaps with an arbitrary implementation choice. Distinguish required outcomes from illustrative ways to achieve them.

15. **Normative Authority and Conflicts**: State which content defines conformance and how imported requirements apply. Prose, tables, schemas, and diagrams MUST agree; stating precedence does not excuse a known contradiction. Specify keyword conventions. New specifications using BCP 14 SHOULD cite both [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) and [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174). Explain the keyword convention used by the document.

16. **Security, Failure Behavior, and Conformance**: Identify applicable roles, supported features, relevant trust boundaries, security assumptions, and dependencies. State preconditions, success outcomes, and failure behavior, including the response or state change on invalid input and failed validation. Distinguish receiving or parsing a message from accepting it as valid or acting on it. Identify checks delegated to normative dependencies by relevant section. Flag unspecified handling as an open question to resolve before implementations or tests depend on it. Map each testable provision to an observable result and test cases. For recommendations and permissions, explain applicable choices and test only the conditions that actually apply.

17. **Review for Ambiguity and Usability**: Apply the guidance to examples and ask whether independent readers can derive consistent behavior, implementation decisions, and test requirements. Record concrete ambiguities, contradictions, missing rules, and unnecessary complexity, then use the findings to revise the guidance. Check identifiers, internal references, diagrams, constraints, and wire examples for agreement. A comparison with an existing specification can expose a writing problem, but a difference alone is not evidence of ambiguity and does not require a permanent correspondence table. Revisit examples after changing the guidance and record which improvements have actually been evaluated.

## Examples

### EXAMPLE 1 (Provisions 7, 8, and 9)

The following authoring illustration splits an obligation into stable provisions. It is not a complete security protocol; a real specification would supply prerequisites, validation rules, and failure behavior.

* **REQ-FORM-ACTION (FLOW-RESPONSE)**: When the AS constructs the response form, the AS **MUST** set the form's `action` attribute to the Client's Redirection URI.
* **REQ-FORM-METHOD (FLOW-RESPONSE)**: When the AS constructs the response form, the AS **MUST** set the form's `method` attribute to `POST`.

These obligations illustrate explicit actor ownership and separate testable outcomes, using [OAuth 2.0 Form Post Response Mode, Section 2](https://openid.net/specs/oauth-v2-form-post-response-mode-1_0.html#FormPost). A test can inspect the destination and method independently; sample HTTP messages must agree with these provisions. These summaries do not relicense source material; see the [example's rights notice](examples/oauth_2_0_form_post_response_mode_1_0_modern_spec.md#source-and-rights-notice).

### EXAMPLE 2 (Provisions 11 and 16)

| Variable / Parameter | Context / Representation Layer | Event & Provision IDs | Type | Presence / Multiplicity | Allowed Values / Constraints | Invalid / Unspecified Handling |
| --- | --- | --- | --- | --- | --- | --- |
| `method` | HTML form attribute | `FLOW-RESPONSE`, `REQ-FORM-METHOD` | Method attribute | Required for this form | `POST`; serialization details follow the applicable HTML dependency | Other submission methods do not satisfy `REQ-FORM-METHOD`; runtime handling is specified separately |

### EXAMPLE 3 (Provisions 11 and 12)

An author-created encoding illustration, not an OAuth parameter validity rule:

| Representation layer | Value |
| --- | --- |
| Application string | `a"b&c` |
| Serialized HTML attribute | `value="a&quot;b&amp;c"` |
| Form-encoded field | `sample=a%22b%26c` |
| Decoded field value | `a"b&c` |

The quote inside the value survives the encoding round trip. It is distinct from the delimiters around the HTML attribute. Whether a particular protocol field permits this string is a separate constraint.

### EXAMPLE 4 (Provisions 9, 14, and 16)

For `REQ-FORM-METHOD`, a test requirement can be stated as:

- **Setup / trigger**: The AS constructs a response form for the mode described in Example 1.
- **Observation**: Inspect the generated form's method using the specified HTML interpretation rules.
- **Expected result**: The submission method is POST.
- **Failure case**: A form configured to submit using GET fails this requirement.

This checks the AS output. It does not imply that a client must accept every POST or invent a client rejection rule for GET. Those are separate behaviors that require their own provisions.
