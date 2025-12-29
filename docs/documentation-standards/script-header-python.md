# Python Script Header Template

> Template Version: 1.0  
> Applies To: All `.py` files in desi-quasar-outflows  
> Last Updated: 2025-12-29

---

## Template

```python
#!/usr/bin/env python3
"""
Script Name  : script_name.py
Description  : [One-line description of what the script does]
Repository   : desi-quasar-outflows
Author       : VintageDon (https://github.com/vintagedon)
ORCID        : 0009-0008-7695-4093
Created      : YYYY-MM-DD
Phase        : [Phase XX - Phase Name]
Link         : https://github.com/radioastronomyio/desi-quasar-outflows

Description
-----------
[2-4 sentences explaining the script's purpose, what it operates on,
and what outputs it produces. Include any important behavioral notes.]

Usage
-----
    python script_name.py [options]

Examples
--------
    python script_name.py
        [Description of what this invocation does]

    python script_name.py --verbose
        [Description of what this invocation does]
"""

# =============================================================================
# Imports
# =============================================================================

from pathlib import Path

# =============================================================================
# Configuration
# =============================================================================

# [Configuration constants with inline comments]

# =============================================================================
# Functions
# =============================================================================


def main() -> None:
    """Entry point for script execution."""
    pass


# =============================================================================
# Entry Point
# =============================================================================

if __name__ == "__main__":
    main()
```

---

## Field Descriptions

| Field | Required | Description |
|-------|----------|-------------|
| Script Name | Yes | Filename for reference (snake_case) |
| Description | Yes | Single line, verb-led description |
| Repository | Yes | Repository name |
| Author | Yes | Name with GitHub profile link |
| ORCID | Yes | Author ORCID identifier |
| Created | Yes | Creation date (YYYY-MM-DD) |
| Phase | Yes | Pipeline phase this script belongs to |
| Link | Yes | Full repository URL |
| Description section | Yes | Expanded multi-line explanation |
| Usage section | Yes | Command syntax |
| Examples section | Yes | At least one usage example |

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

```python
# =============================================================================
# Section Name
# =============================================================================
```

Standard sections (in order):

1. **Imports** — Standard library, third-party, local imports (in that order)
2. **Configuration** — Constants, paths, settings
3. **Functions** — Function and class definitions
4. **Entry Point** — `if __name__ == "__main__":` block

---

## Docstring Style

Use NumPy-style docstrings for functions:

```python
def measure_column_density(
    wavelength: np.ndarray,
    flux: np.ndarray,
    ion: str = "CIV"
) -> dict:
    """
    Measure column density using Apparent Optical Depth method.

    Parameters
    ----------
    wavelength : np.ndarray
        Rest-frame wavelength array in Angstroms.
    flux : np.ndarray
        Normalized flux array.
    ion : str, optional
        Ion species to measure. Default is "CIV".

    Returns
    -------
    dict
        Column density result with keys:
        log_N, log_N_err, ew, v_min, v_max.

    Raises
    ------
    ValueError
        If ion is not in supported list.
    """
    pass
```

---

## Example: Minimal Script

```python
#!/usr/bin/env python3
"""
Script Name  : select_outflow_candidates.py
Description  : Queries ARD for blueshifted CIV absorption systems
Repository   : desi-quasar-outflows
Author       : VintageDon (https://github.com/vintagedon)
ORCID        : 0009-0008-7695-4093
Created      : 2025-12-29
Phase        : Phase 01 - Candidate Selection
Link         : https://github.com/radioastronomyio/desi-quasar-outflows

Description
-----------
Filters the upstream QSO ARD table to identify outflow candidates based on
blueshifted CIV absorption (v_abs > 3000 km/s) and diagnostic ion availability.
Outputs a candidate list for spectral fitting.

Usage
-----
    python select_outflow_candidates.py [--output candidates.csv]

Examples
--------
    python select_outflow_candidates.py
        Selects candidates and prints summary to stdout.

    python select_outflow_candidates.py --output candidates.csv
        Selects candidates and writes to CSV file.
"""

# =============================================================================
# Imports
# =============================================================================

from pathlib import Path

import pandas as pd
import psycopg2

# =============================================================================
# Configuration
# =============================================================================

PG_CONNECTION = "postgresql://user@proj-pg01:5432/desi_ard"
MIN_VELOCITY = 3000  # km/s threshold for outflow classification

# =============================================================================
# Functions
# =============================================================================


def query_candidates(min_v: float = MIN_VELOCITY) -> pd.DataFrame:
    """
    Query ARD for outflow candidates above velocity threshold.

    Parameters
    ----------
    min_v : float
        Minimum absorption velocity in km/s.

    Returns
    -------
    pd.DataFrame
        Candidate QSOs with columns: targetid, z_sys, civ_vabs, civ_ew.
    """
    query = f"""
    SELECT targetid, z_sys, civ_vabs, civ_ew, bal_prob
    FROM ard.qso_ard
    WHERE civ_vabs > {min_v}
      AND civ_nc IS NOT NULL
    ORDER BY civ_vabs DESC
    """
    # Implementation here
    pass


def main() -> None:
    """Entry point for script execution."""
    print(f"Selecting candidates with v > {MIN_VELOCITY} km/s")


# =============================================================================
# Entry Point
# =============================================================================

if __name__ == "__main__":
    main()
```

---

## Type Hints

Always use type hints for function signatures:

```python
from pathlib import Path
from typing import Optional

import numpy as np
import pandas as pd


def run_cloudy_grid(
    input_file: Path,
    output_dir: Optional[Path] = None,
    log_nh_range: tuple[float, float] = (19.0, 23.0),
) -> dict[str, np.ndarray]:
    """Run Cloudy photoionization grid and return results."""
    pass
```

---

## Notes

- Use `#!/usr/bin/env python3` for portability
- Module docstring goes immediately after shebang
- Keep Description line under 80 characters
- Use present tense, active voice ("Queries..." not "This script queries...")
- Use `pathlib.Path` instead of string paths
- Use type hints for all function parameters and return values
- Follow PEP 8 style guide
