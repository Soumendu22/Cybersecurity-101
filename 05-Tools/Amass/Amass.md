# Amass

## Overview

Amass is an asset discovery and attack surface mapping tool for DNS enumeration and graph-based reconnaissance.

---

## Passive Enumeration

```bash
amass enum -passive -d example.com
```

---

## Active Enumeration

```bash
amass enum -active -d example.com
```

Active mode can be noisier and should be used according to engagement rules.

---

## Intel and ASN Discovery

```bash
amass intel -d example.com
amass intel -org "Example Corp"
```

---

## Output and Data Management

```bash
amass enum -passive -d example.com -o amass.txt
```

Use database-backed workflows for long-term attack surface tracking.

---

## Comparing with Subfinder

- Subfinder: fast passive subdomain results
- Amass: deeper mapping and relationship intelligence

Combine both and deduplicate:

```bash
cat subfinder.txt amass.txt | sort -u > all-subs.txt
```

---

## Practice Tasks

1. Run passive + active amass in lab and compare results.
2. Correlate Amass and Subfinder output.
3. Identify potential forgotten assets from intel mode.
4. Build periodic attack surface monitoring routine.
5. Track newly discovered assets over time.
