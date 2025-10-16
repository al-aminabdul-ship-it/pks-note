# 02 — Pen Test Lifecycle

Typical workflow:
1. Recon — passive info gathering (whois, shodan, google dorks)
2. Scanning — port & service discovery (nmap), app-level scans
3. Exploitation — use controlled exploits (SQLi, RCE, file upload)
4. Post-exploitation — persistence only in lab; document results
5. Reporting — evidence, impact, remediation steps

## Quick checklist for every exercise
- Confirm authorization and lab isolation
- Capture screenshots / logs
- Revert config changes when done
- Produce short remediation recommendations
