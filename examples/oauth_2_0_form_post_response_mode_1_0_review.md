# OAuth Form Post Example Review — Iteration 1

## Scope and method

Reviewed on November 6, 2026, against repository baseline `82e8634c8a1fbd4730aab19ceb0660b0ece89241`.

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
| F01 | `REQ3.1`, `REQ3.5`, `REQ3.7`; constraint rows for headers and input type | These make the example's status, hidden controls, and exact headers mandatory. They restrict implementation choices beyond the source's Section 2. | Separate source obligations from illustrative mechanisms. Provisions 12, 14, 15. |
| F02 | `REQ3.7`; diagram response message | The actor's obligation to issue cache instructions becomes an apparent guarantee about external caches. An output requirement cannot guarantee external compliance. | Retain actor ownership and distinguish instructions from environmental assumptions. Provisions 6, 8, 16. |
| F03 | `META1`, `REQ2`; input name/value constraints | The rewrite treats presentation quotes as a ban on data quotes. It also mixes serialized HTML with decoded values. This can corrupt values or generate incorrect rejection rules. Compare source Section 1.1 with the HTML dependency. | Define each representation layer and scope delimiter conventions. Provisions 11, 12. |
| F04 | `META2`; allowed/disallowed columns | One case-sensitivity default covers unlike syntactic layers. The table also implies exhaustive restrictions without consistently identifying their origin. | Scope constraints, document extension points, and distinguish unspecified from forbidden. Provisions 2, 11, 14. |
| F05 | Form action constraint; `REQ3.3` | “Exact ... registered” can be read as requiring a full registered URI in every case. RFC 6749 Section 3.1.2.3 distinguishes full-URI and component registration. “Validated” alone also hides the inherited validation rules. | Identify inherited conditions precisely instead of simplifying them into a stronger local rule. Provisions 2, 14, 16. |
| F06 | `PERM1.1`; diagram note 5 | The prose allows multiple techniques, while the diagram presents onload execution as standard flow. Readers or generators could require scripting. The definition also omits automatic submission, while the fallback discussion leaves its relationship to it unexplained. | Preserve descriptive behavior and permissions together; label illustrative paths and unresolved fallback interpretation. Provisions 7, 14, 15. |
| F07 | Diagram and all numeric step references | Manual labels number notes as steps while `autonumber` numbers messages. Consequently “Step 6” does not consistently identify one event. | Use stable event IDs and verify displayed numbering. Provision 7. |
| F08 | Actor descriptions and term imports | Imported roles are restated with extra descriptions, including an AS description that ties its identity to authentication and authorization behavior. The rewrite provides no section-level explanation of which statements are definitions versus flow assumptions. | Preserve imported identities and place local responsibilities separately. Provisions 3, 8, 14. |
| F09 | Goal | “Prevents ... browser history, or server access logs” is too broad. Body logging or other exposure paths are not excluded by using POST. Compare the qualified discussion in source Section 4. | State the precise protected representation, assumptions, and residual risks. Provisions 6, 16. |
| F10 | `REQ4.1`–`REQ4.3`; error-response parenthesis in `REQ3` | “Accept” does not distinguish endpoint support, parsing, validation, and authorization to act. Error applicability is asserted without mapping the conditions inherited from the applicable OAuth flow. | Document source-derived applicability and validation dependencies; do not invent acceptance or error rules. Provisions 14, 16. |
| F11 | Wire example 2 | The declared `Content-Length: 43` disagrees with the displayed ASCII body: 45 octets, excluding a trailing newline. | Recompute lengths from explicit bytes and state framing conventions. Provision 12. |
| F12 | References, normative section, example as a whole | HTML401 is an added dependency; RFC2119 is listed without a keyword-interpretation statement. There is no provision-level source map or source coverage check. Source Section 3's no-IANA-action statement and Section 4's security context are not explicitly accounted for as retained, moved, or intentionally omitted. | Record dependency changes, authority, and coverage, including non-requirement sections. Provisions 2, 14, 15, 17. |

## Primary-source coverage

This map accounts for the primary source's behavior, not every inherited OAuth or HTML requirement. “Present” means represented in the rewrite, not validated as equivalent.

| Source location / topic | Rewrite location | Review result |
| --- | --- | --- |
| Section 1.1: keywords and literal notation | References, `META1`, `REQ2` | Interpretation statement missing; notation overgeneralized. F03, F12. |
| Section 1.2: terms | Terms and actors | Imports present; local restatements need checking. F08. |
| Section 2: mode value and encoded submission | Definition, `REQ1`, `REQ3.2`, `REQ3.5`, `REQ3.6`, `REQ4.1`, `REQ4.2` | Core behavior present, with additions and unresolved distinctions. F01, F03–F06, F10. |
| Section 2: form destination and method | `REQ3.3`, `REQ3.4` | Present; destination constraint needs inherited-rule precision. F05. |
| Section 2: cache instructions | `REQ3.7` | Present but mechanism narrowed and outcome overstated. F01, F02. |
| Section 2: technique and content permissions | `PERM1.1`, `PERM1.2` | Present; diagram and fallback framing need alignment. F06. |
| Section 2: mechanism-independent client handling | `REQ4.3` | Present; distinguish handling from validity. F10. |
| Section 3: IANA; Section 4: security context | No IANA section; Goal | Omission not accounted for; security claim broadened. F09, F12. |
| Section 5: dependencies; Appendix A: illustration | References, wire examples, added normative details | Added HTML dependency and promotion of illustration. F01, F11, F12. |
| Appendices B/C: acknowledgments and notices | Source and rights notice | Source acknowledgment appendix remains accessible by link; provenance and rights have been added. No claim of exhaustive legal review. |

## Changes made in this iteration

The guideline now requires source mapping, preserved normative strength and descriptive semantics, explicit authority, representation-layer constraints, stable event IDs, scoped security claims, and observable test outcomes. It also replaces the unsourced token-verification illustration with two independently labeled form obligations and adds an encoding illustration.

The existing thirteen provision numbers are retained. Provisions 14–17 add provenance, authority, failure/conformance analysis, and review evidence. Plain technical language remains the aim; compliance with ASD-STE100 is no longer asserted without verification.

The OAuth example's protocol body is deliberately retained as the reviewed baseline, with a link to this report. Findings are open remediation work, not silently corrected or marked resolved. The next application of the revised guideline should revise the example, retain an old-to-new identifier map, and compare it against this coverage table before claiming equivalence.

## Validation and next experiments

- Manual comparison of the primary source and all sections of the example.
- Local calculation: `len(b"code=SplxlOBeZQQYbYS6WxSbIA&state=af0ifjsldkj") == 45`.
- Static inspection of diagram messages versus notes; no renderer execution.
- Guideline review for consistency with these findings and local Markdown link checks.
- No conformance, interoperability, or security test result is claimed.

Useful follow-up cases include encoded quotes and ampersands with round-trip equality, alternate source-permitted form mechanisms, source-defined cache instruction checks, redirect validation under the applicable registration model, and malformed or mismatched responses under the selected OAuth flow. Each needs a source-derived expected outcome before it becomes a conformance test. Repeat this review independently with another model using the same baseline before sharing these findings.
