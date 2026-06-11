# VirusTotal Guide for SOC Analysts

## What to Submit

| IOC Type | How to Submit | What You Learn |
|----------|--------------|----------------|
| File | Upload or hash lookup | AV detections, behavioral analysis, file metadata |
| IP Address | Enter in search | Passive DNS, malicious URL hosting, detection ratio |
| Domain | Enter in search | Historical IPs, malware distribution, category |
| URL | Enter in search | Redirects, final destination, malicious content |
| Hash (MD5/SHA256) | Enter in search | Existing analysis, file info, malware family |

## Reading VirusTotal Results

```
Detection ratio:  48/72 engines detected it
                  ├── > 30/72 = highly likely malicious
                  ├── 5–30/72 = suspicious, investigate further
                  ├── 1–4/72  = possibly FP (check vendor reputation)
                  └── 0/72    = clean (but new malware may not be detected)

Community score:  Positive = malicious, Negative = clean/FP

File metadata:
- Creation time   (manipulated? very old creation date on new file?)
- First submission date (first seen in wild)
- File type       (PDF claiming to be PDF but is actually EXE?)
- Imphash         (imports hash — links to malware family)
- SSDEEP          (fuzzy hash — finds similar malware variants)
```

## Privacy Warning

⚠️ **Never upload sensitive, classified, or customer data to VirusTotal.** Submitted files become visible to VT subscribers. Use hash lookup instead if privacy is a concern.

## Alternatives

| Tool | Best For |
|------|---------|
| Any.run | Interactive sandbox — see malware running live |
| Hybrid Analysis | Free sandboxing |
| Cuckoo Sandbox | Self-hosted sandbox (your lab) |
| MalwareBazaar | Search known malware samples |
