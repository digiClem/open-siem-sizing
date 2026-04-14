# Open SIEM Sizing Data

Community-maintained dataset for SIEM sizing calculations. Used by the [SIEM Sizing Calculator](https://opensiem-deployer.com/siem-sizing).

## What's in this repo

| File | Description |
|------|-------------|
| `log-sources.json` | Log source volumetrics (GB/day per unit) for 27+ source types |
| `siem-platforms.json` | SIEM platform specs (compression, RAM/CPU/storage multipliers, terminology) |
| `regulations.json` | Regulatory frameworks with minimum log retention requirements |

All data is bilingual (English + French).

## How the data is used

The [SIEM Sizing Calculator](https://opensiem-deployer.com/siem-sizing) uses this data to estimate:
- **Daily log volume** based on your infrastructure
- **Storage requirements** (hot + cold) per SIEM platform
- **Compute resources** (RAM, CPU, disk IOPS)
- **Compliance-driven retention** based on applicable regulations

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Quick contribution ideas

- **Add a log source** -- Know the typical GB/day for a product not listed? Add it to `log-sources.json`.
- **Correct a volume estimate** -- If you have production data showing a different GB/day for a source, submit a PR with your findings.
- **Add a SIEM platform** -- Elastic SIEM, Sumo Logic, Datadog, etc. Add the platform with compression ratios and resource multipliers.
- **Add a regulation** -- Know a country-specific cybersecurity regulation with log retention requirements? Add it.
- **Add a language** -- Currently EN/FR. Add your language to all label/description fields.

## Data format

### log-sources.json

```json
{
  "id": "unique_snake_case_id",
  "label": { "en": "Display Name", "fr": "Nom affiché" },
  "gbPerDayPerUnit": 0.25,
  "description": { "en": "What logs this source generates", "fr": "Description des logs" },
  "unitLabel": { "en": "servers", "fr": "serveurs" },
  "category": "endpoint | network | cloud | application",
  "defaultCount": 0
}
```

### siem-platforms.json

```json
{
  "id": "platform_id",
  "label": "Platform Name",
  "icon": "P",
  "compressionDefault": 5,
  "description": { "en": "...", "fr": "..." },
  "ramMultiplier": 1.0,
  "cpuMultiplier": 1.0,
  "storageMultiplier": 1.0,
  "note": { "en": "Sizing notes", "fr": "Notes de dimensionnement" },
  "terminology": {
    "indexer": { "en": "...", "fr": "..." },
    "forwarder": { "en": "...", "fr": "..." },
    "manager": { "en": "...", "fr": "..." },
    "dashboard": { "en": "...", "fr": "..." },
    "singleDesc": { "en": "...", "fr": "..." },
    "distributedDesc": { "en": "...", "fr": "..." },
    "clusterDesc": { "en": "...", "fr": "..." }
  }
}
```

### regulations.json

```json
{
  "id": "regulation_id",
  "label": "Regulation Name",
  "description": { "en": "...", "fr": "..." },
  "minHotDays": 30,
  "minTotalDays": 365,
  "region": "international | eu | us | france | germany | ..."
}
```

## Multiplier reference

For SIEM platforms, multipliers are relative to Wazuh (baseline = 1.0):

| Platform | RAM | CPU | Storage | Compression |
|----------|-----|-----|---------|-------------|
| Wazuh | 1.0x | 1.0x | 1.0x | 7:1 |
| Splunk | 1.5x | 1.3x | 1.2x | 2:1 |
| QRadar | 1.4x | 1.3x | 1.3x | 5:1 |
| Sentinel | 0.8x | 0.8x | 1.1x | 6:1 |
| LogRhythm | 1.6x | 1.3x | 2.0x | 2:1 |
| Graylog | 1.1x | 1.0x | 1.2x | 3:1 |

## License

This data is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) -- you can use, share, and adapt it as long as you give credit and share alike.

## Credits

Maintained by [Open SIEM Deployer](https://opensiem-deployer.com) and the community.
