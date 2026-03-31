# FFUF

## Overview

FFUF (Fuzz Faster U Fool) is a fast web fuzzing tool used for discovering hidden directories, files, parameters, virtual hosts, and endpoint behavior differences.

---

## Basic Directory Fuzzing

```bash
ffuf -u http://target.local/FUZZ -w /usr/share/wordlists/dirb/common.txt
```

---

## Common Filters and Matchers

- `-mc`: match status codes
- `-fc`: filter status codes
- `-fs`: filter by response size
- `-fw`: filter by words
- `-fl`: filter by lines

Example:

```bash
ffuf -u http://target.local/FUZZ -w wordlist.txt -mc 200,204,301,302,403
```

---

## VHost Fuzzing

```bash
ffuf -u http://target.local -H "Host: FUZZ.target.local" -w subdomains.txt -fs 1234
```

Use baseline filtering to remove default wildcard responses.

---

## Parameter Fuzzing

```bash
ffuf -u "http://target.local/page?FUZZ=test" -w params.txt -fs 0
```

POST JSON fuzzing:

```bash
ffuf -u http://target.local/api -X POST -H "Content-Type: application/json" -d '{"FUZZ":"test"}' -w keys.txt
```

---

## Recursion and Depth

```bash
ffuf -u http://target.local/FUZZ -w wordlist.txt -recursion -recursion-depth 2
```

Use carefully to control scan noise.

---

## Output Formats

```bash
ffuf -u http://target/FUZZ -w wordlist.txt -o ffuf.json -of json
```

---

## Workflow Tips

1. Run baseline request and note common size/words.
2. Start with small curated wordlist.
3. Filter wildcard responses.
4. Expand to deeper lists for interesting paths.
5. Validate findings manually.

---

## Practice Tasks

1. Discover hidden directories on a lab target.
2. Fuzz VHosts and identify valid hosts.
3. Find undocumented query parameters.
4. Compare results with Dirsearch/Gobuster.
5. Export JSON results and build summary report.
