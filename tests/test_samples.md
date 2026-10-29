
# Test Results

Python version used: [Python 3.15.2];
Operating system: Windows;
Date: [29-10-2026];

| # | Input | Expected result | Actual result | Pass/Fail |
|---|---|---|---|---|
| 1 | https://www.example.com/login | No listed warning signs | No listed warning signs found. This does NOT prove safety. | Pass |
| 2 | http://192.0.2.10/account | IP address + HTTP | - Uses an IP address instead of a familiar domain.- Uses HTTP. HTTPS alone does not prove trust.| Pass |
| 3 | http://example.com@sample.invalid/login | @ symbol + HTTP | - Contains an @ symbol; inspect carefully.- Uses HTTP. HTTPS alone does not prove trust. | Pass |
| 4 | https://a.b.c.d.e.example.invalid/path | Many hostname segments |- Contains many hostname segments/subdomains. | Pass |
| 5 | https://xn--example.invalid/ | Punycode-style hostname | - Contains a punycode-style hostname.| Pass |

## Notes

- **Test Execution**: All 5 test cases executed as expected with a 100% pass rate (`5/5`).
- **Static Heuristic Scope**: The tool evaluates lexical and structural URL patterns purely offline (regex/parsing); it does not perform DNS resolution, active HTTP requests, or live domain-reputation lookups.
- **Limitation & False Negatives**: A clean result (e.g., Test Case 1) indicates absence of common structural heuristics, not verified safety. Legitimate-looking URLs hosted on compromised domains will not be flagged by string patterns alone.
- **Combined Indicators**: Multi-trigger detection works properly—URLs with multiple anomalies (e.g., insecure protocol `http://` combined with an IP address or `@` character) reliably surface all matching flags.
- **Safe Handling**: Because test samples use RFC-reserved/documentation TLDs (`.invalid`, `192.0.2.0/24`) and the script never opens target links, test execution is completely safe from malicious redirects.


