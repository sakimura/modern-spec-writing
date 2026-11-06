# Contributing

Contributions should help the guideline produce better specification documents for AI systems, human readers, security analysts, and test developers.

## Contribution terms

By intentionally submitting original material for inclusion in this project, including through a pull request, you agree to apply [CC0 1.0 Universal](LICENSE) to your contribution to the extent you hold the relevant rights. CC0 provides a public-domain dedication to the extent permitted by law and a fallback license. It allows others to incorporate, edit, publish, and reuse your contribution, including commercially, without requiring attribution or further permission.

You confirm that you have authority to submit the material under these terms, including any permission needed from an employer or other rights holder. A GitHub username or pseudonym is acceptable; a legal name is not required. Acknowledgments are voluntary, and the project does not promise an exhaustive contributor list.

Identify third-party material separately, with its source, applicable terms, and required notices. Do not claim CC0 rights over material you do not own or have authority to dedicate. For adaptations of existing specifications, distinguish your original contributions from the source material and confirm that the source terms permit the proposed use. If the terms are unclear, flag that for review before the material is merged.

AI-assisted contributions follow the same rules: apply CC0 only to rights you hold, and identify known third-party material. These terms do not assert that all AI-generated material is copyrightable or free of third-party rights.

Each pull request should include the confirmation provided in the PR template. Maintainers should obtain confirmation before merging. Material submitted before these terms were introduced needs an applicable permission or the relevant rights holder's agreement; these terms do not retroactively grant rights to someone else's work.

## Proposing a change

Use an issue to discuss a problem or a pull request to propose a concrete change. Keep each proposal focused enough to review on its own.

Include:

- The problem and the readers or tasks it affects.
- The relevant guideline provision and example section.
- A concrete example of the ambiguity, omission, inconsistency, or implementation difficulty.
- The proposed change and why it helps.
- The checks performed, their results, and any unresolved questions.

When possible, update both the guideline and an example so reviewers can assess the effect of the change. Distinguish observations from suggestions that have not yet been evaluated.

## Adding or revising examples

Place applications of the guideline in `examples/` and use a descriptive filename. Record the source specification's title, version or date, and authoritative URL in the example. Cite the source sections needed to check the rewrite.

Preserve the source specification's normative meaning. If the source is ambiguous, record the ambiguity and any assumption made. Identify proposed behavior changes separately from editorial changes, including any added, removed, strengthened, or weakened requirements.

Keep requirements, recommendations, and permissions traceable to their source. Clearly distinguish source requirements, imported requirements, explanatory material, and proposed additions. Mark illustrative messages and test vectors as non-normative unless the source gives them normative status.

When changing identifiers or sequence steps, update all affected references in diagrams, tables, provisions, and examples.

## Working with multiple AI models

AI-assisted contributions are welcome. For each model-assisted application, review, or implementation experiment, record enough information in the issue or pull request for another contributor to understand and, where possible, repeat it:

- Model provider, model name or version as reported by the tool, and date of the run.
- Guideline and example revisions, preferably identified by commit hashes.
- Source specification version and any additional material supplied.
- Prompts, task boundaries, and relevant settings, with confidential information removed.
- Findings, assumptions, disagreements, and any human corrections.
- Validation performed and its results.

If model or run details are unavailable, say so. Do not guess them.

For independent comparisons, give each model the same source material and task before sharing the other models' results. Record any differences in inputs or access to tools that could affect the comparison. Check findings against the source rather than treating model agreement as proof of correctness.

When testing generated implementations, record the implementation revisions, model details, test setup, cases, and observed results. Distinguish successful interoperability from full conformance; a successful exchange alone does not demonstrate that error handling or security requirements are satisfied.

## Reviewing a contribution

Review the result from each intended reader's perspective:

- **AI systems and implementers:** Are actors, inputs, outputs, conditions, and obligations explicit? Can the behavior be implemented without inventing missing rules?
- **Human readers:** Are scope, terminology, structure, and explanations clear and consistent?
- **Security analysts:** Are security assumptions, trust boundaries, failure behavior, and security claims clear enough to assess?
- **Test developers:** Can provisions be linked to observable outcomes and positive, negative, and boundary cases?

Check that the rewrite preserves source behavior, that cross-references resolve, and that diagrams, constraints, provisions, and wire examples agree. If checks or experiments were not performed, state that directly.

## Submitting a pull request

Use a title that describes the change. In the description, summarize the problem, the resulting change, the supporting example or evidence, and validation results. Link related issues and identify open questions that need review.

Keep unrelated edits separate. Do not include credentials, private prompts or data, or material that you do not have permission to contribute. Cite external material and check its reuse terms before copying it.
