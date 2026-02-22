# 🎯 CTF Methodology

## Phase 0: Pre-Challenge Setup (5 min)

- [ ] Create challenge folder: `challenges/<category>/<challenge-name>/`
- [ ] Open `notes.md` (use template)
- [ ] Read the full challenge description carefully
- [ ] Note: flag format, point value, hints, file attachments
- [ ] Download any provided files → `artifacts/`

---

## Phase 1: Reconnaissance & Enumeration

### For Web Challenges
```bash
# Identify tech stack
whatweb <url>
wappalyzer (browser ext)

# Directory/file brute force
ffuf -u http://target/FUZZ -w /usr/share/wordlists/dirb/common.txt
gobuster dir -u http://target -w wordlist.txt -x php,html,js,txt

# Parameter fuzzing
ffuf -u "http://target/page?FUZZ=value" -w params.txt

# JS file analysis
linkfinder.py -i http://target -d

# Check robots.txt, sitemap.xml, .git/, .env
curl http://target/robots.txt
curl http://target/.git/config
```

### For Binary/Pwn Challenges
```bash
file binary           # file type
checksec binary       # security mitigations
strings binary        # interesting strings
ltrace ./binary       # library calls
strace ./binary       # syscalls
objdump -d binary     # disassemble
readelf -a binary     # ELF info
```

### For Crypto Challenges
- Identify cipher type (block/stream/asymmetric)
- Look for weak key sizes, repeated IVs, ECB mode
- Check for known-plaintext attack vectors
- Look up on dcode.fr, cryptii.com, CyberChef

### For Forensics Challenges
```bash
file <artifact>
exiftool <artifact>
binwalk -e <artifact>      # extract embedded files
strings <artifact> | grep -i flag
steghide extract -sf image.jpg
zsteg image.png
volatility -f mem.dump imageinfo   # memory forensics
```

### For Reversing Challenges
```bash
file binary
strings binary
ghidra / ida / binary ninja    # decompile
gdb / pwndbg / peda            # dynamic analysis
ltrace / strace                # trace calls
```

---

## Phase 2: Vulnerability Identification

### Web Vulnerabilities Checklist
- [ ] SQL Injection (manual + sqlmap)
- [ ] XSS (reflected/stored/DOM)
- [ ] SSTI (Server-Side Template Injection) `{{7*7}}`
- [ ] LFI/RFI `../../../../etc/passwd`
- [ ] SSRF (internal service access)
- [ ] XXE (XML External Entity)
- [ ] IDOR (Insecure Direct Object Reference)
- [ ] Command Injection `; id`
- [ ] Deserialization
- [ ] JWT weaknesses (none alg, weak secret)
- [ ] OAuth/SAML flaws
- [ ] Race conditions
- [ ] Path traversal

### Pwn Checklist
- [ ] Buffer overflow (ret2win, ret2libc, ROP)
- [ ] Format string vulnerability
- [ ] Use-after-free / heap exploitation
- [ ] Integer overflow/underflow
- [ ] Off-by-one error
- [ ] Stack canary bypass
- [ ] PIE bypass (info leak)

---

## Phase 3: Exploitation

```
1. Understand the target behavior
2. Identify the exact vulnerability
3. Build a minimal PoC
4. Test PoC in safe environment
5. Refine → get reliable exploitation
6. Capture flag / escalate
```

### Useful Exploit Skeletons
```python
# pwntools skeleton (pwn)
from pwn import *
p = process('./binary')   # or remote('host', port)
context.arch = 'amd64'
# p = remote('chall.ctf.com', 1337)

payload = b'A' * offset
payload += p64(ret_addr)
p.sendline(payload)
p.interactive()
```

```python
# Web exploit skeleton
import requests
s = requests.Session()
TARGET = "http://target.ctf"

# login / auth
s.post(f"{TARGET}/login", data={"user":"admin","pass":"pass"})

# exploit
r = s.get(f"{TARGET}/vuln?param=payload")
print(r.text)
```

---

## Phase 4: Post-Exploitation (Pentest / HTB machines)

```bash
# Linux privesc
id && whoami
sudo -l
find / -perm -4000 2>/dev/null   # SUID binaries
crontab -l && cat /etc/crontab
env
cat /etc/passwd | grep -v nologin
ls -la /home/
linpeas.sh   # automated privesc enum

# Windows privesc
whoami /all
net user && net localgroup administrators
systeminfo
winPEAS.exe
```

---

## Phase 5: Flag Capture & Documentation

- [ ] Capture flag: `echo "CTF{...}" > flag.txt`
- [ ] Take screenshot of proof
- [ ] Document the exact steps in `notes.md`
- [ ] Save exploit script to `exploit.py`
- [ ] Update the challenge folder with artifacts
- [ ] Write final writeup → `writeups/<challenge>.md`

---

## Phase 6: Writeup (Post-CTF)

Follow the [writeup template](../templates/challenge-notes.md).

**Good writeups include:**
- Challenge description
- Initial observations
- Rabbit holes (what didn't work and why)
- The actual vulnerability identified
- Step-by-step exploit
- Code/commands used
- Flag

---

## ⏱️ Time Management in CTFs

| Priority | Action |
|---|---|
| First 30 min | Read ALL challenges, identify easiest |
| Per challenge | Set a 45-min timer; move on if stuck |
| Before switching | Write down current hypothesis |
| Final hour | Focus on challenges closest to solving |
