# Custodian: Real-Time Security Assistant

Custodian is a powerful, real-time secure coding assistant for VS Code. It uses Tree-sitter powered static analysis to detect vulnerability patterns as you type, providing immediate feedback to prevent security flaws before they are committed.

## Key Features

- **Real-Time Detection**: Analyzes code on every keystroke with ultra-low latency.
- **Multi-Language Support**: Support for Python, JS/TS, Java, C++/C, Go, Ruby, PHP, Rust, C#, and Scala.
- **Framework-Specific Detection**: Specialized rules for React, Vue, Angular, Flask, Django, Spring, Express, and Rails.
- **Deep Taint Analysis**: Sink-first tracing to identify how untrusted input reaches dangerous functions.
- **Maximum Coverage**: Optimized for high recall during trial runs—assuming data is tainted if the origin is unknown.
- **78 Vulnerability Rules**: Comprehensive detection across 26 security categories.

## Supported Languages & Frameworks

### Languages (11)
| Language | Key Vulnerabilities Detected |
| :--- | :--- |
| **Python** | SQLi, Command Injection, SSRF, XSS, Hardcoded Secrets, Insecure Deserialization, Weak Crypto, Path Traversal |
| **JavaScript/TypeScript** | DOM-XSS, Prototype Pollution, Insecure Client-Side Storage, Eval/Function usage |
| **Java** | JNDI Injection (Log4Shell style), Insecure Deserialization, SQLi (JDBC/Hibernate), JSP/Spring XSS |
| **C++ / C** | Buffer Overflows (`strcpy`, `gets`), Format String Vulnerabilities (`printf`), Memory Management issues |
| **Go** | Command Injection (`os/exec`), SQL Injection, Path Traversal |
| **Ruby** | Command Injection, SQL Injection, YAML Deserialization, ERB Template Injection, Mass Assignment |
| **PHP** | SQL Injection, Command Injection, XSS, File Inclusion, `eval` usage |
| **Rust** | Unsafe blocks (`unsafe { ... }`), Command Injection, FFI patterns |
| **C#** | SQL Injection (`SqlCommand`), Command Injection, XSS, Insecure Deserialization |
| **Scala** | SQL Injection, Command Injection (`sys.process`), Play Framework XSS |

### Frameworks (8)
| Framework | Vulnerabilities Detected |
| :--- | :--- |
| **React** | dangerouslySetInnerHTML XSS, Insecure href, Eval in handlers, Ref manipulation |
| **Vue.js** | v-html XSS, Template injection, Insecure v-bind:href |
| **Angular** | bypassSecurityTrust misuse, Template injection, innerHTML binding |
| **Flask** | SSTI, Unsafe Markup, Missing CSRF, Insecure session config |
| **Django** | Raw SQL, mark_safe XSS, Safe filter bypass, Missing CSRF |
| **Spring** | SpEL Injection, Mass assignment, Insecure CORS, Path traversal |
| **Express.js** | Missing helmet, Insecure CORS, Missing rate limiting, Eval in routes |
| **Rails** | Mass assignment, Raw SQL, html_safe XSS, Missing CSRF, Open redirect |

## Installation

### From VSIX File
```bash
code --install-extension custodian-0.1.0.vsix
```

Or install manually in VS Code:
1. Open VS Code
2. Go to Extensions (`Ctrl+Shift+X`)
3. Click the `...` menu → "Install from VSIX..."
4. Select `custodian-0.1.0.vsix`

## Usage

1. **Open a supported file**: `.py`, `.js`, `.jsx`, `.ts`, `.tsx`, `.java`, `.cpp`, `.c`, `.go`, `.rb`
2. **Start coding**: The extension activates automatically
3. **View diagnostics**: Vulnerabilities appear as squiggly lines
4. **Check Problems panel**: Press `Ctrl+Shift+M` to see all detected issues

### Confidence Levels
- **High**: Direct source-to-sink flow found (definite vulnerability)
- **Medium**: Sink reachable from unvalidated variable (likely vulnerable)
- **Low**: Dangerous sink with constant values (potential issue)

## Philosophy: Trial Run Mode

Custodian is currently in **Maximum Coverage Mode**. 
- **Silence is worse than noise**: We prioritize flagging potential issues over avoiding false positives.
- **Data Taint**: Any input originating from requests, users, or unvalidated functions is treated as high-risk.
- **Sink Focus**: Dangerous functions are always highlighted when they interact with non-constant data.

---
*Built for Secure Coding.*
