# ETC Eos Module Feature Request Summary

## Overview
This branch includes **7 commits ahead of `upstream/master`**, focused on:
- Macro trigger feedback/state
- Selected channel and command content variables
- Advanced patch metadata capture
- Patch notes reset behavior
- Constants tuning and release metadata

## Commits Included
- `38d9d66` — feedback for macros, channel texts
- `8f7cd24` — output for active chan
- `b87c7a0` — macros, selected chan, cmd_content
- `67c9b24` — advanced Patch Information
- `44a0128` — clear notes if empty
- `377f714` — fix spelling
- `70a80ae` — chore bump version

## Proposed Features (Copy-Ready)
### 1) Macro-fired feedback and state handling
- Add boolean feedback `macroisfired` that lights when a configured macro is fired.
- Track `macro_fired` and `last_macro` state values.
- Auto-reset `macro_fired` to `0` shortly after trigger to support momentary visual feedback.
- Include upgrade mapping for existing configurations.

Code references:
- [feedbacks.js](feedbacks.js#L5-L27)
- [main.js](main.js#L370-L384)
- [upgrades.js](upgrades.js#L3-L9)

### 2) Expose selected channel and command content
- Add `selected_chan` variable from active channel event parsing.
- Add `cmd_content` derived from command line OSC output.

Code references:
- [main.js](main.js#L359-L366)
- [main.js](main.js#L388-L402)
- [variables.js](variables.js#L25-L29)

### 3) Advanced patch metadata capture
- Parse `/eos/out/get/patch/.../list/...` and `/notes` OSC updates.
- Expose patch data as variables:
  - `patch_active_id`, `patch_label`, `patch_fix_manuf`, `patch_fix_model`
  - `patch_dmx_address`, `patch_dmx_portoffset`, `patch_dmx_address_intens`
  - `patch_current_level`, `patch_osc_gel`, `patch_text_1`..`patch_text_10`
  - `patch_part_count`, `patch_notes`

Code references:
- [main.js](main.js#L444-L487)
- [variables.js](variables.js#L35-L56)

### 4) DMX address formatting helper
- Convert raw DMX address into `port/offset` format for readable output.

Code references:
- [main.js](main.js#L455)
- [main.js](main.js#L735-L739)

### 5) Full-state patch request tied to active channel
- Request patch details for current active channel during state refresh.

Code references:
- [main.js](main.js#L653-L662)

### 6) Clear stale patch notes on patch updates
- Ensure `patch_notes` is reset when patch label data refreshes to prevent stale values.

Code references:
- [main.js](main.js#L470-L474)

### 7) Constants and release metadata adjustments
- Tune constants:
  - `WHEELS_PER_CAT`: `64 -> 16`
  - `NUM_GROUP_LABELS`: `30 -> 10`
  - Add `NUM_PATCH_LABELS = 1`
- Bump module version and package manager metadata.

Code references:
- [constants.js](constants.js#L1-L3)
- [package.json](package.json#L3)
- [package.json](package.json#L22-L23)

### 8) Minor wording fix
- Improve `cmd_content` variable description text.

Code reference:
- [variables.js](variables.js#L25)

---
