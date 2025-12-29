# Shell Script Header Template

> Template Version: 1.0  
> Applies To: All `.sh` files in desi-quasar-outflows  
> Last Updated: 2025-12-29

---

## Template

```bash
#!/usr/bin/env bash
# =============================================================================
# Script Name  : script-name.sh
# Description  : [One-line description of what the script does]
# Repository   : desi-quasar-outflows
# Author       : VintageDon (https://github.com/vintagedon)
# ORCID        : 0009-0008-7695-4093
# Created      : YYYY-MM-DD
# Phase        : [Phase XX - Phase Name]
# Link         : https://github.com/radioastronomyio/desi-quasar-outflows
# =============================================================================
#
# DESCRIPTION
#   [2-4 sentences explaining the script's purpose, what it operates on,
#   and what outputs it produces. Include any important behavioral notes.]
#
# USAGE
#   ./script-name.sh [options]
#
# EXAMPLES
#   ./script-name.sh
#       [Description of what this invocation does]
#
#   ./script-name.sh --verbose
#       [Description of what this invocation does]
#
# =============================================================================

set -euo pipefail  # Exit on error, undefined vars, pipe failures

# =============================================================================
# Configuration
# =============================================================================

# [Configuration variables with inline comments]

# =============================================================================
# Functions
# =============================================================================

# [Function definitions if needed]

# =============================================================================
# Main
# =============================================================================

main() {
    # [Main script logic]
}

main "$@"
```

---

## Field Descriptions

| Field | Required | Description |
|-------|----------|-------------|
| Script Name | Yes | Filename for reference |
| Description | Yes | Single line, verb-led description |
| Repository | Yes | Repository name |
| Author | Yes | Name with GitHub profile link |
| ORCID | Yes | Author ORCID identifier |
| Created | Yes | Creation date (YYYY-MM-DD) |
| Phase | Yes | Pipeline phase this script belongs to |
| Link | Yes | Full repository URL |
| DESCRIPTION block | Yes | Expanded multi-line explanation |
| USAGE block | Yes | Command syntax |
| EXAMPLES block | Yes | At least one usage example |

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

```bash
# =============================================================================
# Section Name
# =============================================================================
```

Standard sections (in order):

1. **Configuration** — Variables, paths, settings
2. **Functions** — Helper function definitions (if any)
3. **Main** — Entry point function

---

## Best Practices

```bash
# Always use strict mode
set -euo pipefail

# Use main() function pattern for cleaner structure
main() {
    # Script logic here
}

main "$@"

# Quote variables to prevent word splitting
echo "${variable}"

# Use lowercase for local variables, UPPERCASE for exports/constants
local data_path="/mnt/proj-fs02/desi-dr1"
export DATA_ROOT="/mnt/proj-fs02/desi-dr1"
```

---

## Example: Minimal Script

```bash
#!/usr/bin/env bash
# =============================================================================
# Script Name  : run-cloudy-batch.sh
# Description  : Submits Cloudy grid jobs for outflow candidate list
# Repository   : desi-quasar-outflows
# Author       : VintageDon (https://github.com/vintagedon)
# ORCID        : 0009-0008-7695-4093
# Created      : 2025-12-29
# Phase        : Phase 03 - Cloudy Modeling
# Link         : https://github.com/radioastronomyio/desi-quasar-outflows
# =============================================================================
#
# DESCRIPTION
#   Reads a candidate list CSV and submits Cloudy photoionization jobs
#   for each outflow system. Jobs are parallelized across available cores.
#
# USAGE
#   ./run-cloudy-batch.sh candidates.csv
#
# EXAMPLES
#   ./run-cloudy-batch.sh candidates.csv
#       Runs Cloudy grids for all candidates in the input file.
#
# =============================================================================

set -euo pipefail

# =============================================================================
# Configuration
# =============================================================================

CLOUDY_BIN="/opt/cloudy/cloudy.exe"
OUTPUT_DIR="/mnt/proj-fs02/desi-outflows/cloudy-results"
PARALLEL_JOBS=8

# =============================================================================
# Main
# =============================================================================

main() {
    local candidate_file="${1:-}"
    
    if [[ -z "${candidate_file}" ]]; then
        echo "Usage: $0 <candidate_file.csv>"
        exit 1
    fi
    
    echo "Processing candidates from ${candidate_file}"
    echo "Output directory: ${OUTPUT_DIR}"
}

main "$@"
```

---

## Notes

- Always use `#!/usr/bin/env bash` for portability
- `set -euo pipefail` catches common errors early
- Use `main()` function pattern even for simple scripts — it's easier to extend
- Keep Description line under 80 characters
- Use present tense, active voice ("Submits..." not "This script submits...")
