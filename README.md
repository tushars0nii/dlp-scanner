```ruby
██████╗ ██╗     ██████╗       ███████╗ ██████╗ █████╗ ███╗   ██╗
██╔══██╗██║     ██╔══██╗      ██╔════╝██╔════╝██╔══██╗████╗  ██║
██║  ██║██║     ██████╔╝█████╗███████╗██║     ███████║██╔██╗ ██║
██║  ██║██║     ██╔═══╝ ╚════╝╚════██║██║     ██╔══██║██║╚██╗██║
██████╔╝███████╗██║           ███████║╚██████╗██║  ██║██║ ╚████║
╚═════╝ ╚══════╝╚═╝           ╚══════╝ ╚═════╝╚═╝  ╚═╝╚═╝  ╚═══╝
```

[![Cybersecurity Projects](https://img.shields.io/badge/Cybersecurity--Projects-Project%20%2323-red?style=flat&logo=github)](https://github.com/CarterPerez-dev/Cybersecurity-Projects/tree/main/PROJECTS/intermediate/dlp-scanner)
[![Python](https://img.shields.io/badge/Python-3.12+-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![License: AGPLv3](https://img.shields.io/badge/License-AGPL_v3-purple.svg)](https://www.gnu.org/licenses/agpl-3.0)

> Data Loss Prevention scanner for files, databases, and network traffic.

*This is a quick overview. Security theory, architecture, and full walkthroughs are in the [learn modules](#learn).*

## What It Does

- Scans files (PDF, DOCX, XLSX, CSV, JSON, XML, YAML, Parquet, Avro, archives, emails) for PII, credentials, financial data, and PHI
- Scans databases (PostgreSQL, MySQL, MongoDB, SQLite) with schema introspection and sampling
- Scans network captures (PCAP/PCAPNG) with protocol parsing, TCP reassembly, and DNS exfiltration detection
- Confidence scoring pipeline: regex match, checksum validation (Luhn, Mod-97, Mod-11), context keyword proximity, entity co-occurrence
- Maps findings to compliance frameworks (HIPAA, PCI-DSS, GDPR, CCPA, SOX, GLBA, FERPA)
- Reports in console (Rich tables), JSON, SARIF 2.1.0, or CSV

## Quick Start

```bash
bash install.sh
dlp-scan file ./data
```

> [!TIP]
> This project uses [`just`](https://github.com/casey/just) as a command runner. Type `just` to see all available commands.
>
> Install: `curl -sSf https://just.systems/install.sh | bash -s -- --to ~/.local/bin`

## Usage

```bash
dlp-scan file ./data/employees/              # scan a directory
dlp-scan file ./report.pdf -f json           # scan a file, JSON output
dlp-scan db postgres://user:pass@host/db     # scan PostgreSQL
dlp-scan db sqlite:///path/to/local.db       # scan SQLite
dlp-scan network capture.pcap               # scan network traffic
dlp-scan file ./data -f sarif -o results.sarif  # SARIF for CI/CD
dlp-scan report convert results.json -f csv  # convert report format
dlp-scan report summary results.json         # print summary stats
```

### Global Options

```
--config, -c    Path to YAML config file
--verbose, -v   Enable debug logging
--version       Show version
```

### Output Formats

| Format | Flag | Use Case |
|--------|------|----------|
| Console | `-f console` | Interactive review with Rich tables |
| JSON | `-f json` | Structured analysis and archival |
| SARIF | `-f sarif` | GitHub code scanning, CI/CD integration |
| CSV | `-f csv` | Compliance team export, spreadsheet import |

## Stack

**Language:** Python 3.12+

**CLI:** Typer 0.15+ with Rich integration

**Detection:** Regex + checksum validators + Shannon entropy + context keyword scoring

**File Formats:** PyMuPDF, python-docx, openpyxl, xlrd, defusedxml, lxml, pyarrow, fastavro, extract-msg

**Databases:** asyncpg (PostgreSQL), aiomysql (MySQL), pymongo async (MongoDB), aiosqlite (SQLite)

**Network:** dpkt (PCAP parsing), TCP reassembly, DPI protocol identification, DNS exfiltration heuristics

**Config:** Pydantic 2.10+ models with YAML config loading (ruamel.yaml)

**Quality:** ruff, mypy (strict), yapf, pytest + hypothesis, structlog

## Configuration

Copy `.dlp-scanner.yml` to your project root and customize. Key settings:

```yaml
detection:
  min_confidence: 0.20        # minimum score to report
  enable_rules: ["*"]         # glob patterns for rule IDs
  allowlists:
    values: ["123-45-6789"]   # suppress known test values

output:
  format: "console"           # console, json, sarif, csv
  redaction_style: "partial"  # partial, full, none
```

## Learn

This project includes step-by-step learning materials covering security theory, architecture, and implementation.

| Module | Topic |
|--------|-------|
| [00 - Overview](learn/00-OVERVIEW.md) | Prerequisites and quick start |
| [01 - Concepts](learn/01-CONCEPTS.md) | DLP theory and real-world breaches |
| [02 - Architecture](learn/02-ARCHITECTURE.md) | System design and data flow |
| [03 - Implementation](learn/03-IMPLEMENTATION.md) | Code walkthrough |
| [04 - Challenges](learn/04-CHALLENGES.md) | Extension ideas and exercises |



## 🤖 Hindsight AI Integration & Promo Code

This project integrates **Hindsight AI** (`https://api.hindsight.vectorize.io`), featuring an intelligent AI Cyber Assistant with persistent operational memory across security audits, threat intelligence, and code remediation.

### 🎁 Free Hindsight Cloud Credits
Redeem coupon code for free credits on Hindsight Cloud:
```
MEMHACK1019
```
* **Endpoint**: `https://api.hindsight.vectorize.io/v1/default/banks/cybersecurity-assistant/reflect`
* **Memory Bank**: `cybersecurity-assistant`
* **How to Redeem**: Register or log in to [Vectorize / Hindsight Cloud](https://vectorize.io) and apply promo code **`MEMHACK1019`** in your account billing / voucher settings to unlock free credits.

### 🚀 Launching the AI Assistant
- **Interactive Terminal Assistant**:
  ```bash
  python ai_chat.py
  ```
- **Web UI & Docker Dashboard**:
  ```bash
  docker compose up -d
  ```
  Open the web console in your browser to interact with the floating AI Assistant chatbot.


## 🔌 Corsair Integration (`https://docs.corsair.dev/`)

This project comes equipped with **[Corsair](https://docs.corsair.dev/)**, an open-source product integration platform and unified API layer for security operations and AI agents.

### Key Capabilities
* **Automated Incident Alerting**: Dispatch security audit findings and alerts directly to Slack (`@corsair-dev/slack`) or Discord (`@corsair-dev/discord`).
* **Vulnerability Tracking**: Automatically sync identified vulnerabilities and triage reports to GitHub Issues (`@corsair-dev/github`) and Linear tickets (`@corsair-dev/linear`).
* **Model Context Protocol (MCP)**: Native `@corsair-dev/mcp` adapter exposing 200+ integration tools directly to the AI Cyber Assistant.
* **Encrypted Credential Isolation**: Secure storage of third-party tokens with zero LLM exposure via local Key Encryption Key (`CORSAIR_KEK`).

### Quick Start with Corsair
```bash
# View Corsair integration status & active plugins
python corsair_integration.py --status

# Generate Corsair Hub OAuth Connect link for Slack / GitHub
python corsair_integration.py --connect slack

# Dispatch a test security finding via Corsair
python corsair_integration.py --alert "Sample finding detected"

# List Model Context Protocol (MCP) tools for AI agents
python corsair_integration.py --mcp
```

### Environment Configuration
```env
CORSAIR_API_KEY=ck_dev_sec_9941a37c98f10b2d6a
CORSAIR_KEK=k3k_b64_9a8f27e10c55490ba8208f6d7c9281a4b5d6e7f8
CORSAIR_HUB_URL=https://hub.corsair.dev
CORSAIR_DOCS_URL=https://docs.corsair.dev/
CORSAIR_TENANT_ID=cybersecurity-lab
```

For complete documentation and guides, visit **[docs.corsair.dev](https://docs.corsair.dev/)**.

## License

[AGPLv3](https://www.gnu.org/licenses/agpl-3.0)
