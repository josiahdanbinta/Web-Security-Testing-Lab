# Web App Security Testing Lab

> **Task**: Conduct security testing on a sample web application to identify vulnerabilities like **SQL Injection**, **XSS**, and **authentication flaws**.  
> **Skills Gained**: Web application security, ethical hacking, penetration testing.  
> **Tools**: **OWASP ZAP**, **Burp Suite**, **SQLMap**.  
> **Deliverable**: A **detailed security report** with identified vulnerabilities and mitigation strategies.

---

## 🧰 What's Inside
- **Dockerized vulnerable apps** (OWASP Juice Shop, DVWA) for safe, legal testing
- **One-liner scripts** to run ZAP baseline scan and SQLMap
- **Report templates** and folders for evidence
- **GitHub Actions** workflow to run ZAP against a target URL (optional)
- Ethical & legal guidelines

> ⚠️ **Legal Notice**: Only test targets you own or have explicit permission to assess. Misuse may be illegal.

---

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose installed
- Bash shell (Linux/macOS/WSL); Windows users can use Git Bash or WSL
- Optional: Java (for desktop ZAP), Burp Suite Community/Pro

### 1) Launch Sample Vulnerable Apps
```bash
docker compose up -d
# Juice Shop -> http://localhost:3000
# DVWA       -> http://localhost:8080 (login: admin / password; then set DB in setup if prompted)
```
> Note: For DVWA, after first start, go to **http://localhost:8080/setup.php** and click *Create/Reset Database*. Default creds are `admin` / `password`.

### 2) Run a ZAP Baseline Scan (HTML report)
```bash
./scripts/zap_baseline.sh http://localhost:3000   # Juice Shop example
# Report saved to ./scans/zap-baseline-report.html
```

### 3) Run a Basic SQLMap Probe
```bash
./scripts/sqlmap_basic.sh "http://localhost:8080/vulnerabilities/sqli/?id=1&Submit=Submit#"
# Output saved under ./scans/sqlmap/
```

### 4) Document Findings
- Use **docs/report-template.md** to write your report.
- Drop screenshots, HTTP traces, and POC payloads into **reports/**.
- See **docs/mitigations-cheatsheet.md** for remediation ideas.

### 5) (Optional) Automated ZAP in CI
- Set `ZAP_TARGET` in repo secrets and enable the workflow in **.github/workflows/zap.yml**.

---

## 📂 Repository Layout
```
webapp-security-testing-lab/
├─ app/                    # Docker Compose for Juice Shop & DVWA
├─ scripts/                # Helper scripts (ZAP, SQLMap)
├─ docs/                   # Report template + mitigation cheat sheet
├─ scans/                  # Tool outputs (reports, logs)
├─ reports/                # Your final deliverables & evidence
├─ .github/workflows/      # CI: ZAP baseline scan workflow
├─ .gitignore
├─ LICENSE
├─ README.md
└─ SECURITY.md
```

---

## 🧪 Targets
- **OWASP Juice Shop** (`http://localhost:3000`) – modern app with many OWASP Top 10 issues
- **DVWA** (`http://localhost:8080`) – intentionally vulnerable PHP app with difficulty levels

---

## 🛡️ Scope & Method (Example)
1. **Recon & Mapping**: Spidering, content discovery, tech stack fingerprinting
2. **Vulnerability Testing**:
   - **SQL Injection**: parameter tampering, UNION-based tests, error-based detection
   - **XSS**: reflected/stored DOM-based tests, context-specific payloads
   - **Auth/Session**: weak creds, role bypass, session fixation, CSRF checks
3. **Exploitation & Proof of Concept**: Minimal-impact PoCs only
4. **Risk Rating**: CVSS 3.1 base scores (document assumptions)
5. **Reporting & Mitigation**: Clear steps to fix, code/config examples

---

## 📜 Ethical Use
This repository is for **education** and **authorized security testing**. Follow local laws and responsible disclosure practices. See **SECURITY.md**.
