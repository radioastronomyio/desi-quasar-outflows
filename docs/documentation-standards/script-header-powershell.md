# PowerShell Script Header Template

> Template Version: 1.0  
> Applies To: All `.ps1` files in desi-quasar-outflows  
> Last Updated: 2025-12-29

---

## Template

```powershell
<#
.SYNOPSIS
    [One-line description of what the script does]

.DESCRIPTION
    [2-4 sentences explaining the script's purpose, what it operates on,
    and what outputs it produces. Include any important behavioral notes.]

.NOTES
    Repository  : desi-quasar-outflows
    Author      : VintageDon (https://github.com/vintagedon)
    ORCID       : 0009-0008-7695-4093
    Created     : YYYY-MM-DD
    Phase       : [Phase XX - Phase Name]

.EXAMPLE
    .\script-name.ps1

    [Description of what this invocation does]

.EXAMPLE
    .\script-name.ps1 -Parameter Value

    [Description of what this invocation does]

.LINK
    https://github.com/radioastronomyio/desi-quasar-outflows
#>

# =============================================================================
# Configuration
# =============================================================================

# [Configuration variables with inline comments]

# =============================================================================
# Functions
# =============================================================================

# [Function definitions if needed]

# =============================================================================
# Execution
# =============================================================================

# [Main script logic]
```

---

## Field Descriptions

| Field | Required | Description |
|-------|----------|-------------|
| `.SYNOPSIS` | Yes | Single line, verb-led description |
| `.DESCRIPTION` | Yes | Expanded explanation of purpose and behavior |
| `.NOTES` | Yes | Static metadata (repository, author, ORCID, dates, phase) |
| `.EXAMPLE` | Yes | At least one usage example with description |
| `.LINK` | Yes | Repository URL |
| `.PARAMETER` | If applicable | Document any script parameters |

---

## Phase Reference

| Phase | Name |
|-------|------|
| Phase 01 | Candidate Selection |
| Phase 02 | Spectral Fitting |
| Phase 03 | Cloudy Modeling |
| Phase 04 | Energetics Derivation |

---

## Section Comments

Use banner comments to separate logical sections:

```powershell
# =============================================================================
# Section Name
# =============================================================================
```

Standard sections (in order):

1. **Configuration** — Variables, paths, settings
2. **Functions** — Helper function definitions (if any)
3. **Execution** — Main script logic

---

## Example: Minimal Script

```powershell
<#
.SYNOPSIS
    Validates Cloudy output files for completeness.

.DESCRIPTION
    Scans the Cloudy results directory and validates that all expected output
    files are present and contain valid results. Reports any failed or
    incomplete jobs.

.NOTES
    Repository  : desi-quasar-outflows
    Author      : VintageDon (https://github.com/vintagedon)
    ORCID       : 0009-0008-7695-4093
    Created     : 2025-12-29
    Phase       : Phase 03 - Cloudy Modeling

.EXAMPLE
    .\validate-cloudy-output.ps1

    Validates all Cloudy output files in the default results directory.

.LINK
    https://github.com/radioastronomyio/desi-quasar-outflows
#>

# =============================================================================
# Configuration
# =============================================================================

$cloudyResultsPath = "\\proj-fs02\desi-outflows\cloudy-results"

# =============================================================================
# Execution
# =============================================================================

Get-ChildItem -Path $cloudyResultsPath -Filter "*.out" | ForEach-Object {
    # Validation logic here
}
```

---

## Notes

- PowerShell comment-based help (`.SYNOPSIS`, `.DESCRIPTION`, etc.) enables `Get-Help script-name.ps1`
- Keep `.SYNOPSIS` under 80 characters
- Use present tense, active voice ("Validates..." not "This script validates...")
- Phase field should match work-log phase names exactly
