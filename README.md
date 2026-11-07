# Modern Spec Writing Guidelines

This project develops guidelines for writing specification documents that are useful to AI systems, human readers, security analysts, and test developers.

The aim is to make specifications clear enough to support consistent interpretation, implementation, security analysis, and testing.

## Project documents

- [Modern Spec Writing Guidelines](modern_spec_writing_guidelines.md): The working guideline.
- [Examples](examples/): Applications of the guideline to existing specifications. The first example is [OAuth 2.0 Form Post Response Mode 1.0](examples/oauth_2_0_form_post_response_mode_1_0_modern_spec.md), an unvalidated, unofficial adaptation with source and rights notices and initial review findings.
- [Contribution guide](CONTRIBUTION.md): How to propose changes and record findings.
- [OAuth example review — iteration 1](examples/oauth_2_0_form_post_response_mode_1_0_review.md): Source comparison, findings, and the guideline changes they motivate.

## How the guideline improves

The guideline and its examples develop together through repeated application and review:

1. Apply the current guideline to an existing specification.
2. Review the result from the perspectives of implementers, human readers, security analysts, and test developers.
3. Record ambiguities, missing information, inconsistencies, and difficulties introduced by the guideline.
4. Propose guideline changes supported by those findings.
5. Apply the changes to the examples and check whether they resolve the problems.
6. Repeat with further examples and independent reviews.

Multiple AI models will participate in this process. Contributions should record which model was used, the material it received, and the findings that support a proposed change. Agreement between models is useful evidence, but each finding still needs to be checked against the source specification.

## Status

The guideline is a working document. Examples are exercises used to evaluate it; they are not authoritative replacements for the source specifications. A rewritten example may contain mistakes or unresolved interpretations.

For an existing specification, preserve its normative meaning and identify any proposed behavior changes separately. Improved presentation should not silently introduce new requirements or remove existing ones.

To contribute, read [CONTRIBUTION.md](CONTRIBUTION.md).

## License

Original project content is dedicated to the public domain under [CC0 1.0 Universal](LICENSE), to the extent permitted by law, with the fallback license provided by CC0. You may copy, modify, incorporate, and redistribute that content, including commercially, without an attribution requirement.

This dedication applies only to rights held by the project contributors. Third-party material, including text adapted from existing specifications, retains its applicable terms and notices. Inclusion in this repository does not place that material under CC0. Check the source specification's terms before reusing an example; where the applicable terms are not recorded, do not assume the whole example is covered by CC0.

## Acknowledgments

Thank you to the project's [contributors](https://github.com/sakimura/modern-spec-writing/graphs/contributors). This link provides a convenient record of GitHub contributions; it may not capture every form of help. Acknowledgment is voluntary and is not a condition of reuse under CC0.
