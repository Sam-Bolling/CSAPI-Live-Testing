# CSAPI Part 4 Working-Draft Integration Plan

## Purpose

This document records the recommended execution plan for adding OGC API - Connected Systems Part 4 (Sampling Features) to the official `opengeospatial/ogcapi-connected-systems` repository in a controlled way.

This is a private coordination runbook. It is intended to reduce improvisation before any changes are made in the official repository.

## Objective

Stand up Part 4 as a proper working draft branch in the official OGC repository, using the current `api/part4` content as seed material, Alex Robin's delivered package as a reconciliation input, and the existing `part3-working-draft` branch as the primary structural precedent.

## Non-Goals

- Do not push incomplete or speculative content directly to `master`.
- Do not invent missing clauses, requirements, schema details, or editorial framing.
- Do not assume Alex's delivered package is a complete standalone standard package.
- Do not treat extracted Part 1 content as publication-ready without an editorial pass.

## Source Inputs

### Delivered by Alex Robin

- Email guidance indicating the material can be added to the repository.
- Email guidance indicating it should remain on a separate branch while still under work.
- Local package delivered as `csapi_part4`, containing:
  - `figures/`
  - `openapi/`
  - `requirements/`
  - `sections/`

### Official Repository

- Repository: `https://github.com/opengeospatial/ogcapi-connected-systems`
- Existing Part 4 subtree on `master`: `api/part4`
- Existing Part 3 working-draft branch:
  - `https://github.com/opengeospatial/ogcapi-connected-systems/tree/part3-working-draft`
  - Root draft entry:
    `https://github.com/opengeospatial/ogcapi-connected-systems/blob/part3-working-draft/api/part3/standard/23-003r0.adoc`

### Working Hypothesis

The current Part 4 material appears to have been extracted from Part 1 and repurposed into a separate part because sampling features introduced enough additional subject matter and separation-of-concerns value to justify a standalone document.

That hypothesis is consistent with both:

- project history reported by the DWG; and
- the structure of the current materials, which look like extracted content blocks rather than a fully scaffolded standalone standard.

## Current State Findings

### 1. Part 4 is not absent from the official repository

The official repository already contains `api/part4` on `master`.

That subtree already includes most of the substance from Alex's delivered package, including:

- figures;
- OpenAPI material;
- requirements;
- sampling-feature sections.

### 2. Alex's delivered package is not a complete standalone draft package

The delivered package contains substantive source material, but it does not include a full top-level working-draft scaffold comparable to the Part 3 draft branch.

Observed gaps include the absence of a clear standalone draft root and supporting build/review packaging such as:

- a top-level `23-004r0.adoc` draft entrypoint;
- draft-local README/build instructions;
- explicit Metanorma configuration colocated with the draft package;
- committed review artifacts such as HTML/PDF outputs.

### 3. Alex's local package does appear to contain at least two items not presently mirrored in `master`

Additional files observed in the delivered package include:

- `sections/clause_3_references.adoc`
- `sections/text for annex C.txt`

These should be treated as inputs to review, not auto-merge material.

### 4. The main missing piece is packaging and editorial stand-up

The problem is not simply "get Part 4 into the repo." Most of the material is already there.

The actual gap is:

- turning the extracted Part 4 content into a coherent, reviewable standalone draft;
- making the branch structure match how OGC already handled Part 3 working-draft publication prep;
- resolving any residual Part 1 framing, references, and annex dependencies.

## Execution Status as of 2026-06-29

The scaffold, reconciliation, structural cleanup, and initial provenance cleanup
passes have now been executed to the extent safely supported by existing source
material.

Completed:

1. A dedicated `part4-working-draft` branch was created and used for all work.
2. A standalone `api/part4/standard/` scaffold was added around the existing upstream Part 4 seed content.
3. Alex Robin's delivered package was reconciled against the existing upstream `api/part4` subtree.
4. A remote GitHub Actions Metanorma build workflow was added for the branch.
5. The remote build now succeeds and produces review artifacts, including HTML, PDF, and XML outputs.
6. Standalone-draft root and section-order cleanup was completed to the extent safely grounded in existing source.
7. Requirements/reference provenance cleanup reduced the direct SensorML bibliography gap and documented the unresolved historical `/req/sampling-features` linkage issue instead of guessing.

Remaining:

1. The branch still carries standalone-draft completeness gaps such as missing Abstract, Preface, and Submitters material that should not be invented without source.
2. The historical `/req/sampling-features` base-class packaging issue remains unresolved and should not be silently normalized without explicit editorial direction.
3. `text for annex C.txt` remains intentionally unpromoted pending author/editor clarification.
4. The branch now needs a reviewer-readiness/build-validation pass and, if needed, a tighter reviewer-facing status note reflecting the current buildable-but-still-editorial state.

## Part 3 Precedent

The strongest precedent is the existing `part3-working-draft` branch.

That branch does not merely contain topic fragments. It contains a real draft package under `api/part3/standard/`, including:

- root draft file;
- supporting sections;
- requirements content;
- repository-facing draft README;
- build metadata;
- committed HTML/PDF artifacts for review circulation.

Key implication:

The Part 3 precedent says the right pattern is not "drop content into `master` and iterate there." The right pattern is "use a dedicated working-draft branch and stand up a coherent draft package that reviewers can build and inspect."

## Recommended Execution Plan

### Phase 1. Completed: Create a dedicated Part 4 working branch

A dedicated branch named:

- `part4-working-draft`

has already been created and used as intended.

### Phase 2. Completed: Treat existing `api/part4` on `master` as the seed baseline

The existing upstream `api/part4` subtree has been preserved and used as the seed baseline.

Alex's delivered package was used as a reconciliation input rather than as a destructive replacement.

### Phase 3. Completed: Stand up a proper standalone Part 4 draft package

A standalone draft package was created under `api/part4/standard/`, and a remote GitHub Actions Metanorma workflow now builds it successfully.

Current successful remote outputs include:

- HTML
- PDF
- XML
- supporting diagnostic artifacts

### Phase 4. Substantially completed: Standalone front matter and section-order cleanup

This pass has already been completed for the currently available source
material. The draft now reads more like a standalone working draft, but bounded
wrapper material is still used where no safely promotable standalone source was
available.

What was achieved:

- root-document framing was tightened;
- section ordering was cleaned up where safe;
- obvious extracted-from-Part-1 assumptions at the draft root were reduced;
- unresolved standalone sections were left explicitly bounded rather than guessed.

What remains open:

- missing standalone material such as Abstract, Preface, and Submitters content;
- any additional standalone front matter that cannot yet be grounded in existing source.

### Phase 5. Partially completed: Requirements and reference provenance cleanup

Because the content was pulled out of Part 1, this pass was mandatory even
though the branch already built. The initial pass has now been completed, but a
small number of unresolved author/editor questions remain open by design.

Completed:

- direct bibliography and anchor gaps were reduced where existing source clearly supported the fix;
- the `OGC-SML` bibliography entry was restored for the Part 4 pose discussion;
- the historical `/req/sampling-features` linkage issue was traced to earlier Part 1 source and Alex Robin's delivered package;
- unresolved provenance issues were documented instead of normalized by guesswork.

Remaining:

- the current standalone draft still does not promote a formal Part 4 base requirement class for `/req/sampling-features`;
- broader requirements/conformance packaging decisions around that historical base class remain open;
- annex/scratch-material status remains unresolved where the source is ambiguous.

### Phase 6. Remaining: Reviewer-readiness and branch status pass

This is now the recommended next execution step.

Run the remote build again and update the branch-facing status note so reviewers
can immediately understand:

- what now builds successfully;
- what has been integrated from upstream seed content versus Alex's delivered package;
- what remains editorially unresolved;
- whether the branch is ready for reviewer circulation as a working draft even if it is not publication-ready.

## Open Editorial Questions

These items should be resolved explicitly rather than guessed:

1. Does Alex have any missing top-level Part 4 scaffold files that were not included in the delivered package?
2. Is `text for annex C.txt` intended to become formal annex content, or is it only a working note?
3. Which references must move with the extracted material from Part 1 into Part 4?
4. Are there any remaining Part 4-related clauses still living only in Part 1 that must be migrated for completeness?
5. Is the intended document number and root file naming definitely `23-004r0`, or is another identifier already assigned internally?

## Validation Checklist

Before treating the branch as reviewer-ready, verify all of the following:

- `api/part4` seed content preserved from upstream.
- Delivered extras reconciled intentionally.
- Standalone root draft file exists.
- Remote Metanorma GitHub Actions build succeeds.
- Section includes resolve cleanly in the remote build.
- Generated HTML artifact renders.
- Generated PDF artifact renders.
- Generated XML artifact renders.
- Remaining standalone front-matter and section-order gaps are either fixed from existing source or documented explicitly.
- No avoidable references to Part 1-only framing remain at the draft root.
- Reference and requirements-linkage warnings have been reduced where justified by existing source.
- Annex content is intentionally included, intentionally excluded, or explicitly marked unresolved.
- Branch README/status note explains scope, build state, and remaining editorial gaps.

## Go / No-Go Criteria

### Go

Proceed with execution if:

- the goal remains to circulate a grounded working draft, not prematurely declare Part 4 publication-ready;
- the work can stay branch-scoped;
- unresolved editorial uncertainties are documented instead of guessed.

### No-Go

Do not proceed directly to `master` if:

- unresolved editorial gaps are being papered over with invented content;
- Part 1 extraction issues are still being handled by guesswork;
- reviewer circulation would still require people to reconstruct the intended draft from raw fragments instead of a buildable working branch.

## Recommended Next Deliverable

The next execution cycle should aim to produce:

- a fresh remote build/validation run after the latest provenance cleanup;
- confirmation that HTML, PDF, and XML review artifacts still generate successfully;
- a tighter branch-facing status note describing what remains open for author/editor review.

That is the right target for the next pass. The next pass should be framed as a
reviewer-readiness/status pass, not as final Part 4 completion and not as a new
content-cleanup cycle.

## Remaining Copy-Paste Execution Prompts

Recommended order from the current branch state:

1. Prompt 3 next.
2. Prompts 1 and 2 are retained below as historical execution records and reusable fallback instructions, but they are no longer the recommended next step from the current branch state.

### Prompt 1. Standalone Front Matter and Section-Order Cleanup Pass

```text
You are working in the repository `opengeospatial/ogcapi-connected-systems`.

IMPORTANT OPERATING RULES:
- Work only on `part4-working-draft`.
- Start by checking the current branch and syncing the latest `origin/part4-working-draft`.
- Do NOT merge or switch this work back to `master`.
- This pass is standalone-draft cleanup, not new standards authorship.
- Do NOT invent missing standards content, requirements, annex text, references, schema details, or editorial conclusions.
- If a missing standalone-draft section cannot be grounded in existing source material, document it explicitly instead of guessing.
- Use this private planning document as the execution brief:
  `C:\Users\sbolling\Documents\ogc-client-csapi-live-tests\docs\research\csapi-part4-working-draft-integration-plan.md`
- Use the existing Part 3 working-draft branch as the structural model:
  `https://github.com/opengeospatial/ogcapi-connected-systems/tree/part3-working-draft`

OBJECTIVE:
Make the existing Part 4 working-draft root read more like a standalone OGC draft and less like an extracted clause package, without inventing new content.

REQUIRED WORK:
1. Confirm you are on `part4-working-draft` and pull latest branch state.
2. Inspect the current `api/part4/standard/` draft root, its README/status note, and the corresponding Part 3 draft structure.
3. Review the current root draft entrypoint and identify obvious standalone-draft structural gaps such as:
   - missing or misplaced front matter;
   - section-order problems;
   - residual extracted-from-Part-1 framing at the draft root;
   - placeholder or weak standalone wording that can be improved using existing source.
4. Promote or re-home material only when its placement is clearly justified by:
   - current Part 4 source already in the repo;
   - Alex Robin's delivered package; or
   - obvious extracted-from-Part-1 standalone cleanup.
5. Tighten the draft root and include ordering where safe.
6. If any required standalone-draft element is still missing and cannot be safely completed from existing material, leave it as an explicit open issue rather than inventing text.
7. Update any concise branch-facing note if the new structure changes what reviewers need to know.

INTEGRITY CONSTRAINTS:
- Do NOT modify `master`.
- Do NOT fabricate missing content.
- Do NOT silently rewrite normative intent.
- Do NOT treat this pass as publication-ready completion.

BEFORE COMMITTING:
- Run `git status`.
- Review the changed files.
- Confirm the work remains branch-scoped and limited to standalone-draft cleanup.

COMMIT AND PUSH:
- Commit to `part4-working-draft` with a clear message such as:
  `Tighten Part 4 standalone draft structure`
- Push/sync the branch.

REPORT BACK WITH:
1. current branch;
2. commit hash;
3. `git status`;
4. files changed;
5. exact standalone-draft structure or section-order fixes made;
6. exact open structural gaps intentionally left unresolved.
```

### Prompt 2. Requirements and Reference Provenance Cleanup Pass

```text
You are working in the repository `opengeospatial/ogcapi-connected-systems`.

IMPORTANT OPERATING RULES:
- Work only on `part4-working-draft`.
- Start by checking the current branch and syncing the latest `origin/part4-working-draft`.
- Do NOT merge or switch this work back to `master`.
- This is a requirements/reference provenance pass, not a speculative rewrite.
- Do NOT invent missing standards content, annex text, references, or schema details.
- If something is uncertain, document it explicitly instead of guessing.

REFERENCE MATERIALS:
- Private execution plan:
  `C:\Users\sbolling\Documents\ogc-client-csapi-live-tests\docs\research\csapi-part4-working-draft-integration-plan.md`
- Alex Robin delivered package:
  `C:\Users\sbolling\OneDrive - Riverside Research\Documents\OGC CSAPI SWG Meeting Files\csapi_part4`
- Official Part 3 working-draft precedent:
  `https://github.com/opengeospatial/ogcapi-connected-systems/tree/part3-working-draft`
- Corresponding Part 1 source files in the same repository, to inspect directly during the provenance pass:
  - `api/part1/standard/23-001r0.adoc`
  - `api/part1/standard/sections/clause_3_references.adoc`
  - `api/part1/standard/sections/clause_13_requirements_class_sampling_features.adoc`

OBJECTIVE:
Reduce the remaining extracted-from-Part-1 reference and requirements-linkage problems in the Part 4 draft, but only where the fix is clearly supported by existing source material.

REQUIRED WORK:
1. Confirm you are on `part4-working-draft` and pull latest branch state.
2. Inspect the current Part 4 references and requirements-related source material directly, including:
   - `api/part4/standard/23-004r0.adoc`
   - `api/part4/standard/sections/clause_3_references.adoc`
   - `api/part4/sections/clause_13_sampling_feature_types.adoc`
   - `api/part4/requirements/`
3. Inspect the corresponding Part 1 source files directly, especially:
   - `api/part1/standard/23-001r0.adoc`
   - `api/part1/standard/sections/clause_3_references.adoc`
   - `api/part1/standard/sections/clause_13_requirements_class_sampling_features.adoc`
4. Review Alex Robin's delivered package only where it helps confirm provenance or placement.
5. Fix only the problems that are clearly justified by existing source, such as:
   - residual Part 1 framing that no longer fits standalone Part 4;
   - dangling cross-references;
   - root-document macros, bibliographic anchors, and clause-level assumptions inherited from Part 1;
   - missing standalone references if they are clearly required;
   - obviously misplaced or unhooked reference content;
   - requirements/conformance linkage problems that can be resolved from current material already in the repo.
6. Do NOT fabricate conformance classes, conformance tests, annex content, or bibliographic entries just to silence warnings.
7. If a warning reflects a genuine unresolved author/editor decision, document it rather than guessing.
8. Update any concise branch-facing status note if the remaining warning set changes materially.

INTEGRITY CONSTRAINTS:
- Preserve the existing Part 4 seed content unless a change is clearly justified by the provenance pass.
- Do NOT invent new technical substance.
- Do NOT claim the branch is final or publication-ready.
- Do NOT merge to `master`.

BEFORE COMMITTING:
- Run `git status`.
- Review diffs carefully.
- Confirm that all substantive changes are traceable either to:
  - Alex's delivered package; or
  - obvious standalone-draft cleanup from the Part 1 extraction and current Part 4 source.

COMMIT AND PUSH:
- Commit to `part4-working-draft` with a clear message such as:
  `Clean up Part 4 requirements and reference provenance`
- Push/sync the branch.

REPORT BACK WITH:
1. current branch;
2. commit hash;
3. `git status`;
4. files changed;
5. exact provenance fixes made;
6. exact warnings reduced or resolved;
7. unresolved questions or warning classes intentionally left open.
```

### Prompt 3. Reviewer-Readiness and Branch Status Pass

```text
You are working in the repository `opengeospatial/ogcapi-connected-systems`.

IMPORTANT OPERATING RULES:
- Work only on `part4-working-draft`.
- Start by checking the current branch and syncing the latest `origin/part4-working-draft`.
- Do NOT merge to `master`.
- This pass is for buildability, validation, review artifacts, and branch-readiness reporting.
- Do NOT introduce new speculative content just to make a build pass.

REFERENCE MATERIALS:
- Private execution plan:
  `C:\Users\sbolling\Documents\ogc-client-csapi-live-tests\docs\research\csapi-part4-working-draft-integration-plan.md`
- Part 3 working-draft precedent:
  `https://github.com/opengeospatial/ogcapi-connected-systems/tree/part3-working-draft`

OBJECTIVE:
Rebuild the Part 4 working-draft branch, confirm reviewer-usable artifacts still generate, and update the branch-facing status note so the branch can be circulated as a working draft with clearly stated open issues.

REQUIRED WORK:
1. Confirm you are on `part4-working-draft` and pull latest branch state.
2. Inspect the Part 4 draft scaffold, README/status note, and build instructions.
3. Run the relevant remote or local build path for the draft, using the existing branch workflow if that remains the safest path.
4. Validate:
   - the root draft entrypoint resolves correctly;
   - section includes resolve;
   - references render cleanly to the extent possible;
   - generated HTML/PDF/XML artifacts succeed if supported.
5. Confirm whether the current artifact-handling approach matches the intended branch workflow and Part 3 precedent.
6. Add or update a concise branch-facing status note describing:
   - what now builds;
   - what is review-ready;
   - what remains editorially open;
   - any warning classes that remain open but were intentionally not guessed away.
7. Do NOT paper over build or editorial problems with invented content.

INTEGRITY CONSTRAINTS:
- Do NOT merge to `master`.
- Do NOT claim completion if the branch still has open editorial or build blockers.
- Do NOT invent missing sections or references just to remove warnings.

BEFORE COMMITTING:
- Run `git status`.
- Verify the build outputs and changed files.
- Confirm whether HTML/PDF/XML artifacts were generated and whether they should be versioned based on the existing repo precedent.

COMMIT AND PUSH:
- Commit to `part4-working-draft` with a clear message such as:
  `Update Part 4 reviewer-readiness status`
- Push/sync the branch.

REPORT BACK WITH:
1. current branch;
2. commit hash;
3. `git status`;
4. build commands run;
5. whether HTML/PDF/XML artifacts were generated successfully;
6. files changed;
7. exact remaining blockers or open editorial issues;
8. whether the branch is ready for reviewer circulation as a working draft.
```
