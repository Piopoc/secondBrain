---
date: 2026-05-18
source: [[WA - 11]]
tags: [security, xss-defense]
---
# Output Encoding
A security technique that converts special characters into their HTML entity equivalents (e.g., `<` becomes `&lt;`) before rendering them in the browser. This prevents the browser from interpreting user-supplied data as executable code, effectively mitigating [[Cross-Site Scripting (XSS)]].
