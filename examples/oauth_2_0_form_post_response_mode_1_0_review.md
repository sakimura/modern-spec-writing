# OAuth Form Post Example Review — Iteration 1

## Scope and method

Initially reviewed on November 6, 2026, against repository baseline `82e8634c8a1fbd4730aab19ceb0660b0ece89241`.

The initial review overemphasized fidelity to the original and introduced a mapping requirement. Following the project owner's scope clarification, this report now focuses on writing lessons: does the guidance produce a less ambiguous document that humans can understand and AI systems can use to create implementations and test requirements? The original was comparison material for this experiment; maintaining correspondence with it is not a deliverable.

Sources:

- [OAuth 2.0 Form Post Response Mode, Final, April 27, 2015](https://openid.net/specs/oauth-v2-form-post-response-mode-1_0.html): primary comparison source, especially Sections 1.1, 1.2, 2, and 4, and Appendix A.
- [RFC 6749, Section 3.1.2.3](https://www.rfc-editor.org/rfc/rfc6749#section-3.1.2.3): redirect URI matching context.
- [HTML 4.01 forms](https://www.w3.org/TR/html401/interact/forms.html): representation and form-submission context already introduced by the rewrite.
- [Mermaid sequence diagram documentation](https://mermaid.js.org/syntax/sequenceDiagram.html#sequencenumbers): numbering behavior.

This is one AI-assisted editorial and semantic review, not an independent multi-model experiment. The assistant identified itself as Codex; exact backend model version and sampling settings were not available. Task: compare the existing example against the original and improve the guideline from the findings. Inputs were the baseline guideline, example, contribution guide, this chat's task context, and the linked sources. Tools: repository inspection, web reading, and a local byte-count check. No implementation generation, browser protocol execution, interoperability testing, or full transitive dependency review was performed.

The report paraphrases and analyzes the source; it does not replace it. Underlying specification material retains the [rights identified in the example](oauth_2_0_form_post_response_mode_1_0_modern_spec.md#source-and-rights-notice). Original review commentary is covered by the repository's CC0 dedication.

## Findings

| ID | Example location | Finding and effect | Disposition and guideline lesson |
| --- | --- | --- | --- |
| F01 | `REQ3.1`, `REQ3.5`, `REQ3.7`; constraint rows for headers and input type | These make the example's status, hidden controls, and exact headers mandatory. The writing does not explain why those mechanisms define conformance rather than illustrate the intended outcome. A difference from the original alone is not a writing defect. | Specify whether concrete mechanisms are requirements or illustrations, so implementation and test generators do not infer unintended restrictions. Provisions 12, 14, 15. |
| F02 | `REQ3.7`; diagram response message | The actor's obligation to issue cache instructions becomes an apparent guarantee about external caches. An output requirement cannot guarantee external compliance. | Retain actor ownership and distinguish instructions from environmental assumptions. Provisions 6, 8, 16. |
| F03 | `META1`, `REQ2`; input name/value constraints | The rewrite treats presentation quotes as a ban on data quotes. It also mixes serialized HTML with decoded values. This can corrupt values or generate incorrect rejection rules. Compare source Section 1.1 with the HTML dependency. | Define each representation layer and scope delimiter conventions. Provisions 11, 12. |
| F04 | `META2`; allowed/disallowed columns | One case-sensitivity default covers unlike syntactic layers. The table also implies exhaustive restrictions without consistently identifying their origin. | Scope constraints, document extension points, and distinguish unspecified from forbidden. Provisions 2, 11, 14. |
| F05 | Form action constraint; `REQ3.3` | “Exact ... registered” can be read as requiring a full registered URI in every case. RFC 6749 Section 3.1.2.3 distinguishes full-URI and component registration. “Validated” alone also hides the inherited validation rules. | Identify inherited conditions precisely instead of simplifying them into a stronger local rule. Provisions 2, 14, 16. |
| F06 | `PERM1.1`; diagram note 5 | The prose allows multiple techniques, while the diagram presents onload execution as standard flow. Readers or generators could require scripting. The definition also omits automatic submission, while the fallback discussion leaves its relationship to it unexplained. | Preserve descriptive behavior and permissions together; label illustrative paths and unresolved fallback interpretation. Provisions 7, 14, 15. |
| F07 | Diagram and all numeric step references | Manual labels number notes as steps while `autonumber` numbers messages. Consequently “Step 6” does not consistently identify one event. | Use stable event IDs and verify displayed numbering. Provision 7. |
| F08 | Actor descriptions and term imports | Imported roles are restated with extra descriptions, including an AS description that ties its identity to authentication and authorization behavior. The rewrite provides no section-level explanation of which statements are definitions versus flow assumptions. | Preserve imported identities and place local responsibilities separately. Provisions 3, 8, 14. |
| F09 | Goal | “Prevents ... browser history, or server access logs” is too broad. Body logging or other exposure paths are not excluded by using POST. Compare the qualified discussion in source Section 4. | State the precise protected representation, assumptions, and residual risks. Provisions 6, 16. |
| F10 | `REQ4.1`–`REQ4.3`; error-response parenthesis in `REQ3` | “Accept” does not distinguish endpoint support, parsing, validation, and authorization to act. Error applicability is asserted without explaining the conditions of the applicable OAuth flow. | Explain applicability and validation dependencies so generated implementations and tests can distinguish receipt, validity, and processing. Provisions 14, 16. |
| F11 | Wire example 2 | The declared `Content-Length: 43` disagrees with the displayed ASCII body: 45 octets, excluding a trailing newline. | Recompute lengths from explicit bytes and state framing conventions. Provision 12. |
| F12 | References and normative section | RFC2119 is listed without a keyword-interpretation statement, and the roles of the dependencies are not explained. Readers must infer which external rules are needed to implement or test the document. | State keyword conventions and the behavior supplied by each normative dependency. Provisions 2, 15, 16. |

## What this experiment tells us

The useful findings concern unclear authority, inconsistent representations, hidden conditions, conflicting diagrams, overbroad claims, and invalid wire data. These can cause humans and AI systems to derive different implementations or tests. Differences from the original are useful prompts for investigation, but are not automatically defects: a more specific requirement can be appropriate if its purpose, applicability, and expected outcome are clear.

The earlier source coverage table has been removed. The review is evidence for improving writing guidance, not a maintained correspondence record or an assertion of semantic equivalence.

## Changes made in this iteration

The guideline now emphasizes explicit authority, behavioral completeness, representation-layer constraints, stable event IDs, scoped security claims, and observable test outcomes. It does not require mappings to an original specification. It also replaces the unsourced token-verification illustration with two independently labeled form obligations and adds an encoding illustration.

The existing thirteen provision numbers are retained. Provisions 14–17 address behavioral completeness, authority, failure/conformance analysis, and ambiguity review. Plain technical language remains the aim; compliance with ASD-STE100 is no longer asserted without verification.

The OAuth example's protocol body is deliberately retained as the reviewed baseline, with a link to this report. Findings are open remediation work, not silently corrected or marked resolved. The next application should revise the example and assess whether readers can derive its behavior and expected test outcomes without unstated assumptions.

## Validation and next experiments

- Manual comparison of the primary source and all sections of the example.
- Local calculation: `len(b"code=SplxlOBeZQQYbYS6WxSbIA&state=af0ifjsldkj") == 45`.
- Static inspection of diagram messages versus notes; no renderer execution.
- Guideline review for consistency with these findings and local Markdown link checks.
- No conformance, interoperability, or security test result is claimed.

Useful follow-up cases include encoded quotes and ampersands with round-trip equality, alternate source-permitted form mechanisms, source-defined cache instruction checks, redirect validation under the applicable registration model, and malformed or mismatched responses under the selected OAuth flow. Each needs an expected outcome justified by the resulting specification and its normative dependencies before it becomes a conformance test. Repeat this review independently with another model using the same baseline before sharing these findings.
