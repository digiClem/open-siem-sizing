# Contributing to Open SIEM Sizing

Thank you for contributing! This dataset helps security engineers worldwide make better sizing decisions.

## How to contribute

1. **Fork** this repository
2. **Edit** the relevant JSON file(s)
3. **Submit a Pull Request** with a clear description of what you changed and why

## Contribution guidelines

### Adding a log source

Edit `log-sources.json` and add your entry to the `sources` array:

```json
{
  "id": "my_new_source",
  "label": { "en": "My New Source", "fr": "Ma Nouvelle Source" },
  "gbPerDayPerUnit": 0.50,
  "description": { "en": "What this source logs", "fr": "Ce que cette source journalise" },
  "unitLabel": { "en": "instances", "fr": "instances" },
  "category": "endpoint",
  "defaultCount": 0
}
```

**Requirements:**
- `id` must be unique, lowercase, snake_case
- `gbPerDayPerUnit` should be a realistic median estimate for a typical production environment
- Include both `en` and `fr` translations (use machine translation if needed, we'll review)
- `category` must be one of: `endpoint`, `network`, `cloud`, `application`
- Include a source or methodology for your GB/day estimate in the PR description

### Correcting a volume estimate

If you have production telemetry showing a different GB/day for an existing source:

1. Note the current value and your proposed value
2. Describe your environment (number of units, configuration, SIEM platform)
3. Include any supporting data (screenshots, log analysis, vendor documentation)

We average estimates across multiple contributors to converge on realistic values.

### Adding a SIEM platform

Edit `siem-platforms.json`. The key fields to research:

- **compressionDefault** -- Typical compression ratio (e.g., 7:1 means 7 GB raw = 1 GB stored)
- **ramMultiplier / cpuMultiplier / storageMultiplier** -- Relative to Wazuh (1.0 baseline)
- **terminology** -- Component names specific to this platform
- **note** -- Key sizing considerations (max heap, scaling thresholds, etc.)

Include vendor documentation links in your PR.

### Adding a regulation

Edit `regulations.json`:

```json
{
  "id": "regulation_id",
  "label": "Regulation Name (Country)",
  "description": { "en": "Full name", "fr": "Nom complet" },
  "minHotDays": 30,
  "minTotalDays": 365,
  "region": "country_code"
}
```

**Requirements:**
- `minHotDays` = minimum days logs must be searchable/queryable
- `minTotalDays` = minimum total retention (including cold/archive storage)
- Include a link to the official regulation text in your PR

### Adding a language

Add your language code to all `label`, `description`, `unitLabel`, and `note` fields across all three JSON files. Example for German (`de`):

```json
"label": { "en": "Windows Servers", "fr": "Serveurs Windows", "de": "Windows-Server" }
```

## Quality standards

- All JSON must be valid (use `jq . file.json` to validate)
- Keep entries sorted by category, then alphabetically by id
- GB/day estimates should reflect **median production usage**, not worst-case or minimal
- Use official vendor documentation when available
- When in doubt, be conservative (overestimate slightly rather than underestimate)

## Review process

1. A maintainer will review your PR within a few days
2. We may ask for clarification or supporting data
3. Once approved, your changes will be merged and deployed to the calculator

## Code of Conduct

Be respectful, constructive, and factual. This is a data-driven project -- back your contributions with evidence.
