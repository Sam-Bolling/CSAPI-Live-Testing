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

### Phase 1. Create a dedicated Part 4 working branch

Create a branch in the official repo named something like:

- `part4-working-draft`

Rationale:

- aligns with Alex's explicit recommendation to keep the work on a separate branch while under development;
- matches the existing Part 3 working-draft pattern;
- avoids contaminating `master` with half-integrated editorial work.

### Phase 2. Treat existing `api/part4` on `master` as the seed baseline

Do not discard what is already in `master`.

Instead:

- branch from current upstream state;
- preserve the existing `api/part4` subtree;
- use Alex's delivered package only to identify missing or divergent material.

### Phase 3. Stand up a proper standalone Part 4 draft package

Create a draft package structure modeled on Part 3 and aligned with how Parts 1 and 2 are organized for standards work.

Expected components:

- `api/part4/standard/23-004r0.adoc`
- `api/part4/standard/README.adoc`
- draft-local build and configuration files as needed
- section includes wired to the existing Part 4 source content

The goal is a reviewable draft, not just a content holding area.

### Phase 4. Reconcile Alex's extra content deliberately

Review and place the delivered extras only where they clearly belong:

- `clause_3_references.adoc`
- `text for annex C.txt`

Rules:

- if a file is clearly draft content, integrate it into the standalone package;
- if it is clearly scratch or working notes, keep it out of the formal draft until resolved;
- do not silently promote notes into normative or informative text.

### Phase 5. Run an editorial provenance pass against Part 1

Because the content was likely pulled out of Part 1, this pass is mandatory.

Check for:

- residual Part 1 framing that no longer makes sense in a standalone Part 4;
- dangling clause references;
- assumptions that depended on surrounding Part 1 text;
- bibliography and references that now need to live inside Part 4;
- annex text that may have been incompletely extracted;
- requirements language that may need context repairs after separation.

### Phase 6. Produce review artifacts

Follow the Part 3 pattern and generate working review outputs for the branch, ideally including:

- HTML draft artifact;
- PDF draft artifact.

This makes the branch usable for SWG/OAB review and avoids asking reviewers to infer the draft from raw fragments.

### Phase 7. Publish a branch-level status note

Add a concise branch-facing note describing:

- what is complete;
- what remains editorially open;
- what was carried over from existing Part 4 material;
- what was reconciled from Alex's package;
- which areas still need author/editor review.

## Open Editorial Questions

These items should be resolved explicitly rather than guessed:

1. Does Alex have any missing top-level Part 4 scaffold files that were not included in the delivered package?
2. Is `text for annex C.txt` intended to become formal annex content, or is it only a working note?
3. Which references must move with the extracted material from Part 1 into Part 4?
4. Are there any remaining Part 4-related clauses still living only in Part 1 that must be migrated for completeness?
5. Is the intended document number and root file naming definitely `23-004r0`, or is another identifier already assigned internally?

## Validation Checklist

Before treating the branch as review-ready, verify all of the following:

- `api/part4` seed content preserved from upstream.
- Delivered extras reconciled intentionally.
- Standalone root draft file exists and builds.
- Section includes resolve cleanly.
- No unresolved references to Part 1-only clause numbering remain.
- References section is complete for the standalone draft.
- Annex content is intentionally included or intentionally excluded.
- Generated HTML artifact renders.
- Generated PDF artifact renders.
- Branch README/status note explains scope and remaining editorial gaps.

## Go / No-Go Criteria

### Go

Proceed with execution if:

- the goal is to create a grounded working-draft branch, not prematurely declare Part 4 publication-ready;
- the work can stay branch-scoped;
- unresolved editorial uncertainties are documented instead of guessed.

### No-Go

Do not proceed directly to `master` if:

- the draft scaffold is still missing;
- annex status is unresolved;
- Part 1 extraction issues remain unreviewed;
- reviewers would be forced to reconstruct the intended draft from raw fragments.

## Recommended First Pass Deliverable

The first execution pass should aim to produce:

- a new `part4-working-draft` branch in the official repo;
- a coherent `api/part4/standard/` draft scaffold;
- reconciled source content from existing upstream Part 4 plus Alex's delivered extras;
- buildable review artifacts if tooling is available;
- a short status note listing remaining editorial decisions.

That is the right target for the first pass. The first pass should not be framed as "final Part 4 completion."

## Copy-Paste Execution Prompts

### Prompt 1. Branch and Scaffold Pass

```text
You are working in the repository `opengeospatial/ogcapi-connected-systems`.

IMPORTANT OPERATING RULES:
- Start by checking the current branch and syncing the latest `origin/master`.
- Do NOT work on `master` for this task.
- Create or reuse a dedicated working branch named `part4-working-draft`.
- This pass is mechanical scaffolding only.
- Do NOT invent standards content, requirements, schema details, annex text, or editorial conclusions.
- Preserve the existing upstream `api/part4` subtree.
- Use the existing Part 3 working-draft branch as the structural model:
  `https://github.com/opengeospatial/ogcapi-connected-systems/tree/part3-working-draft`
- Use this private planning document as the execution brief:
  `C:\Users\sbolling\Documents\ogc-client-csapi-live-tests\docs\research\csapi-part4-working-draft-integration-plan.md`

OBJECTIVE:
Stand up a proper standalone Part 4 working-draft scaffold around the existing upstream `api/part4` content, without yet doing the deeper editorial provenance cleanup.

SOURCE CONTEXT:
- Existing upstream Part 4 seed content already exists in `api/part4` on `master`.
- Part 4 is understood to have been pulled out of Part 1 and repurposed as a separate part.
- Alex Robin recommended keeping the work on a separate branch while still under development.

REQUIRED WORK:
1. Check branch status and sync latest `origin/master`.
2. Create or switch to `part4-working-draft`.
3. Inspect the current upstream `api/part4` subtree and the `api/part3/standard/` draft structure.
4. Create a standalone Part 4 draft scaffold modeled on Part 3, likely under `api/part4/standard/`.
5. Add the minimum root/build/readme structure needed for a coherent working draft, such as:
   - root draft entrypoint, likely `23-004r0.adoc`
   - draft-local `README.adoc`
   - build/config files if the Part 3 pattern clearly supports them
6. Wire the scaffold to the existing Part 4 source material already in the repo.
7. Do NOT yet make speculative editorial decisions about annexes, missing references, or uncertain extracted text unless the fix is purely mechanical and obvious.
8. Add a short branch-facing status note if helpful, but keep it concise and factual.

INTEGRITY CONSTRAINTS:
- Do NOT modify `master`.
- Do NOT delete existing Part 4 seed material.
- Do NOT fabricate missing content.
- Do NOT treat this pass as publication-ready completion.

BEFORE COMMITTING:
- Run `git status`.
- Review the changed files.
- Confirm the work remains branch-scoped and scaffold-focused.

COMMIT AND PUSH:
- Commit to `part4-working-draft` with a clear message such as:
  `Stand up Part 4 working draft scaffold`
- Push/sync the branch to `origin/part4-working-draft`.

REPORT BACK WITH:
1. current branch;
2. commit hash;
3. `git status`;
4. files added/changed;
5. brief summary of the scaffold created;
6. any mechanical issues or obvious gaps discovered but not resolved.
```

### Prompt 2. Content Reconciliation and Editorial Provenance Pass

```text
You are working in the repository `opengeospatial/ogcapi-connected-systems`.

IMPORTANT OPERATING RULES:
- Work only on `part4-working-draft`.
- Start by checking the current branch and syncing the latest `origin/part4-working-draft`.
- Do NOT merge or switch this work back to `master`.
- This is a reconciliation and editorial provenance pass, not a speculative rewrite.
- Do NOT invent missing standards content, annex text, references, or schema details.
- If something is uncertain, document it explicitly instead of guessing.

REFERENCE MATERIALS:
- Private execution plan:
  `C:\Users\sbolling\Documents\ogc-client-csapi-live-tests\docs\research\csapi-part4-working-draft-integration-plan.md`
- Alex Robin delivered package:
  `C:\Users\sbolling\OneDrive - Riverside Research\Documents\OGC CSAPI SWG Meeting Files\csapi_part4`
- Official Part 3 working-draft precedent:
  `https://github.com/opengeospatial/ogcapi-connected-systems/tree/part3-working-draft`

OBJECTIVE:
Reconcile Alex's delivered Part 4 package against the existing upstream Part 4 seed content and perform the extracted-from-Part-1 editorial provenance cleanup needed for a credible standalone Part 4 working draft.

REQUIRED WORK:
1. Confirm you are on `part4-working-draft` and pull latest branch state.
2. Compare the current branch's `api/part4` content against Alex's delivered package.
3. Integrate only the clear additions or deltas from Alex's package.
4. Review special attention files such as:
   - `sections/clause_3_references.adoc`
   - `sections/text for annex C.txt`
5. Promote content into the formal draft only if its placement is clear and justified.
6. Keep scratch or ambiguous material out of the formal draft if its status is uncertain.
7. Run an editorial provenance pass against the extracted Part 1 material and fix obvious issues such as:
   - residual Part 1 framing that no longer fits standalone Part 4;
   - dangling cross-references;
   - missing standalone references if they are clearly required;
   - include wiring or section ordering issues caused by the extraction.
8. Do NOT silently rewrite normative intent.
9. Do NOT fabricate any missing annex material or bibliographic content.
10. If a question remains unresolved, capture it in a concise status note rather than guessing.

INTEGRITY CONSTRAINTS:
- Preserve the existing Part 4 seed content unless a change is clearly justified by the reconciliation pass.
- Do NOT invent new technical substance.
- Do NOT claim the branch is final or publication-ready.
- Do NOT merge to `master`.

BEFORE COMMITTING:
- Run `git status`.
- Review diffs carefully.
- Confirm that all substantive changes are traceable either to:
  - Alex's delivered package; or
  - obvious standalone-draft cleanup from the Part 1 extraction.

COMMIT AND PUSH:
- Commit to `part4-working-draft` with a clear message such as:
  `Reconcile Part 4 source material and extracted-text cleanup`
- Push/sync the branch.

REPORT BACK WITH:
1. current branch;
2. commit hash;
3. `git status`;
4. files changed;
5. exact items integrated from Alex's package;
6. exact editorial provenance fixes made;
7. unresolved questions intentionally left open.
```

### Prompt 3. Build, Validation, and Review-Artifacts Pass

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
Make the Part 4 working-draft branch buildable and reviewable to the greatest safe extent possible, generate review artifacts if the repo tooling supports them, and document remaining blockers precisely.

REQUIRED WORK:
1. Confirm you are on `part4-working-draft` and pull latest branch state.
2. Inspect the Part 4 draft scaffold and build instructions.
3. Run the relevant build commands for the draft if the repo/tooling supports them.
4. Validate:
   - the root draft entrypoint resolves correctly;
   - section includes resolve;
   - references render cleanly to the extent possible;
   - any generated HTML/PDF artifacts build successfully if supported.
5. If the Part 3 pattern clearly supports committing generated review artifacts, do so for Part 4 as well.
6. Add or update a concise branch-facing status note describing:
   - what now builds;
   - what is review-ready;
   - what remains editorially open;
   - any blockers that prevented full artifact generation.
7. Do NOT paper over build or editorial problems with invented content.

INTEGRITY CONSTRAINTS:
- Do NOT merge to `master`.
- Do NOT claim completion if the branch still has open editorial or build blockers.
- Do NOT invent missing sections or references just to remove warnings.

BEFORE COMMITTING:
- Run `git status`.
- Verify the build outputs and changed files.
- Confirm whether HTML/PDF artifacts were generated and whether they should be versioned based on the existing repo precedent.

COMMIT AND PUSH:
- Commit to `part4-working-draft` with a clear message such as:
  `Build and validate Part 4 working draft artifacts`
- Push/sync the branch.

REPORT BACK WITH:
1. current branch;
2. commit hash;
3. `git status`;
4. build commands run;
5. whether HTML/PDF artifacts were generated successfully;
6. files changed;
7. exact remaining blockers or open editorial issues;
8. whether the branch is ready for reviewer circulation as a working draft.
```
