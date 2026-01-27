# Validation Prompt Template

Use this template to work through each validation issue systematically. Copy the prompt below, replace `{ISSUE_NUMBER}` with the actual issue number, and use it to start each validation session.

---

## Prompt Template

```
I'm working on validating the OGC-Client-CSAPI fork assessment. 

Please help me complete validation issue #{ISSUE_NUMBER} from this tracker:
https://github.com/Sam-Bolling/CSAPI-Live-Testing/issues/24

**Instructions:**

1. **Read the Issue**
   - Fetch and review issue #{ISSUE_NUMBER} to understand all claims being validated
   - Identify the specific claims, file paths, and metrics mentioned

2. **Locate the Code**
   - Search the OS4CSAPI/ogc-client-CSAPI repository for relevant files
   - Get the actual code from the repository
   - Document exact file paths with line numbers
   - Verify file sizes match any claims

3. **Examine Implementation**
   - Read and analyze the actual code
   - Extract key code snippets (5-20 lines each showing important patterns)
   - Explain how it works architecturally
   - Document any patterns or design decisions used

4. **Find and Review Tests**
   - Locate test files for this component
   - Count actual number of tests
   - Extract example tests (2-3 representative samples)
   - Review what aspects are tested vs. untested

5. **Verify Metrics**
   - For test count claims: Count actual tests and compare
   - For coverage claims: Look for coverage reports or analyze test completeness
   - For code size claims: Count lines or verify stated sizes
   - For compliance claims: Compare against specifications

6. **Test Functionality (if applicable)**
   - Write small test cases to verify claimed behavior
   - Test edge cases or error scenarios
   - Document results

7. **Create Validation Report**
   Generate a detailed report in issue #{ISSUE_NUMBER} with this structure:

   ```markdown
   ## Validation Report

   **Issue**: #{ISSUE_NUMBER}
   **Validated By**: [Your name/handle]
   **Date**: [Current date]
   **Repository Commit**: [SHA of commit examined]

   ---

   ## Claims Validation

   ### [Claim Category 1]
   **Claim**: [Quote the specific claim]
   **Location**: [File path(s) and line numbers]
   **Evidence**:
   ```[language]
   [Code snippet]
   ```
   **Verdict**: ✅ Confirmed / ⚠️ Partially Confirmed / ❌ Not Confirmed
   **Notes**: [Explanation of verdict]

   [Repeat for each claim]

   ---

   ## Code Analysis

   ### Architecture
   [Explain how the code is organized and structured]

   ### Key Implementation Details
   [Explain important patterns, algorithms, or design decisions]

   ### Code Samples
   [3-5 key snippets with explanations]

   ---

   ## Test Analysis

   ### Test Location
   [Where the tests are located]

   ### Test Count
   - **Claimed**: [Number from assessment]
   - **Actual**: [Number found]
   - **Verdict**: ✅ / ⚠️ / ❌

   ### Test Coverage
   - **Claimed**: [Percentage from assessment]
   - **Actual**: [Percentage found or estimated]
   - **Verdict**: ✅ / ⚠️ / ❌

   ### Example Tests
   ```[language]
   [1-2 representative test examples]
   ```

   ### What's Tested
   - [List of tested scenarios]

   ### What's Not Tested
   - [List of gaps in test coverage]

   ---

   ## Overall Verdict

   **Summary**: [1-2 paragraph summary of findings]

   **Claim Accuracy**: 
   - ✅ Confirmed: [X claims]
   - ⚠️ Partially: [Y claims]
   - ❌ Not Confirmed: [Z claims]

   **Confidence Level**: High / Medium / Low
   [Explain confidence level]

   **Recommendation**: 
   - [ ] Assessment claim is accurate - no changes needed
   - [ ] Assessment claim needs minor corrections - see notes
   - [ ] Assessment claim needs significant corrections - see notes

   ---

   ## Discrepancies

   [List any differences between claims and reality]

   ---

   ## Additional Findings

   [Anything interesting discovered that wasn't claimed]

   ---

   ## Next Steps

   [Any follow-up needed or questions for further investigation]
   ```

8. **Update Tracking**
   - Check off the issue in #24 (Master Tracker)
   - Link to the validation report
   - Note any blockers for downstream issues

**Important Guidelines:**
- Be thorough but objective - validate what exists, not what should exist
- Use actual code and test evidence, not assumptions
- Quote specific lines/sections when making claims
- If something is unclear or ambiguous, note it explicitly
- Include commit SHA so validation is tied to specific code version
- Use ✅ only for fully verified claims with clear evidence
- Use ⚠️ when claim is mostly true but has caveats or minor inaccuracies
- Use ❌ when claim cannot be verified or is demonstrably false

**Tools Available:**
- GitHub repository search for finding files
- GitHub file content retrieval for reading code
- grep/semantic search for finding specific patterns
- git blame for understanding code history
- Test execution to verify functionality

Please proceed with the validation systematically, gathering all evidence before rendering verdicts.
```

---

## Usage Example

When starting validation for issue #11 (GeoJSON Types), you would use:

```
I'm working on validating the OGC-Client-CSAPI fork assessment. 

Please help me complete validation issue #11 from this tracker:
https://github.com/Sam-Bolling/CSAPI-Live-Testing/issues/24

[... rest of template ...]
```

---

## Tips

1. **Start Fresh**: Begin each new validation session with the full template
2. **Be Specific**: Replace {ISSUE_NUMBER} with the actual number (e.g., #11, #13, etc.)
3. **Stay Focused**: Work on one issue at a time to completion
4. **Document Everything**: The validation report is the deliverable - make it comprehensive
5. **Link Issues**: Reference related issues when claims depend on each other
6. **Update Progress**: Keep issue #24 checkboxes current

---

## Quality Checklist

Before considering an issue complete, verify your validation report includes:

- [ ] All claims from the issue are addressed
- [ ] Code locations are documented with exact paths
- [ ] Code samples are included for key functionality
- [ ] Tests are located and counted
- [ ] Test samples are provided
- [ ] Every claim has a verdict (✅ / ⚠️ / ❌)
- [ ] Verdicts are supported with evidence
- [ ] Discrepancies are clearly documented
- [ ] Overall summary is provided
- [ ] Repository commit SHA is documented
