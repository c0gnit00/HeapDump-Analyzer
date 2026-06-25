# HeapForensicAnalyzer

A forensic analysis tool for Java heap dumps, built for **HackTheBox — Eureka**. It extracts credentials, tokens, HTTP sessions, cryptographic material, and other sensitive artifacts from heap dump files.

## Features

- **Credential extraction** — passwords, API keys, AWS secrets, Bearer/Basic tokens
- **Username-password pair detection** — finds credentials appearing in proximity or explicit pairs
- **HTTP session reconstruction** — rebuilds request flows with associated auth headers
- **Cryptographic material detection** — private keys, certificates, high-entropy strings
- **Shannon entropy analysis** — flags suspicious encoded or encrypted strings
- **Threat intelligence matching** — checks findings against known malicious IPs, domains, and attack patterns (Log4Shell, path traversal, etc.)
- **Memory structure analysis** — parses Java object references and class metadata
- **Multiple output formats** — JSON, HTML (interactive), and plain text reports

## Usage

```bash
python3 heapdump_analyzer.py -f <heap_dump_file> -o <format>
```

### Options

| Flag | Description |
|---|---|
| `-f`, `--file` | Path to the Java heap dump file (required) |
| `-o`, `--output` | Output format: `json`, `html`, or `text` |
| `--all` | Generate all three report formats |

### Examples

```bash
# Generate a JSON report
python3 heapdump_analyzer.py -f heap.dump -o json

# Generate an interactive HTML report
python3 heapdump_analyzer.py -f heap.dump -o html

# Generate all report formats at once
python3 heapdump_analyzer.py -f heap.dump --all
```

## Output

Reports are saved to the current directory with a timestamped filename:

```
heap_forensic_report_20260625_143000.json
heap_forensic_report_20260625_143000.html
heap_forensic_report_20260625_143000.txt
```

Each report includes:

- Overall risk score (0–100)
- Critical findings with offsets and context
- Reconstructed HTTP sessions with endpoints and auth tokens
- Credential pairs ranked by confidence score
- Cryptographic material with entropy values
- Most referenced Java classes and objects

## Requirements

Python 3.10+ (standard library only — no external dependencies)

## Disclaimer

This tool is intended for **CTF and authorized forensic analysis only**. Do not use against systems you do not own or have explicit permission to analyze.

---

*Created by c0gnit00 — HackTheBox: Eureka*
