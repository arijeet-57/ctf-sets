# ⚡ Quick Checklist

## CTF Challenge Checklist

### Setup
- [ ] Create folder structure
- [ ] Read challenge description fully
- [ ] Note flag format
- [ ] Download attachments

### Web
- [ ] Check page source
- [ ] Check JS files / endpoints
- [ ] robots.txt / sitemap.xml / .git /
- [ ] Directory brute force (ffuf/gobuster)
- [ ] Parameter fuzzing
- [ ] SQLi test (`' " OR 1=1-- `)
- [ ] XSS test (`<script>alert(1)</script>`)
- [ ] SSTI test (`{{7*7}}` `${7*7}`)
- [ ] LFI test (`../../../etc/passwd`)
- [ ] Command injection (`; id`, `| whoami`)
- [ ] Check cookies / JWT
- [ ] Check headers (X-Debug, X-Admin, etc.)
- [ ] Try admin:admin, admin:password

### Crypto
- [ ] Identify cipher type
- [ ] Check key size / IV reuse
- [ ] Try CyberChef auto-detect
- [ ] Check dcode.fr for classic ciphers
- [ ] Frequency analysis if substitution
- [ ] RSA: check n, e values; small e attack

### Forensics
- [ ] file / exiftool on artifact
- [ ] binwalk -e (extract embedded files)
- [ ] strings | grep -i flag
- [ ] steghide / zsteg / stegsolve for images
- [ ] Wireshark (follow TCP/HTTP streams)
- [ ] Check hex for magic bytes

### Reversing
- [ ] file binary
- [ ] strings binary | grep -i flag
- [ ] ltrace / strace
- [ ] Ghidra decompile
- [ ] Look for strcmp / memcmp calls
- [ ] Patch binary if needed

### Pwn
- [ ] checksec binary
- [ ] Find buffer overflow offset (cyclic)
- [ ] Identify exploit type (ret2win, ret2libc, ROP)
- [ ] Check for format string (`%x %p %s`)
- [ ] Use pwntools skeleton

---

## HTB/Pentest Box Checklist

### Recon
- [ ] nmap full TCP scan
- [ ] nmap UDP scan (top 100)
- [ ] Service version identification

### Web (if port 80/443)
- [ ] nikto scan
- [ ] gobuster dir
- [ ] Check all pages manually
- [ ] Burp Suite intercept

### SMB (if 445 open)
- [ ] enum4linux
- [ ] smbclient -L
- [ ] smbmap

### SSH (if 22 open)
- [ ] Default creds
- [ ] Check for key reuse later

### Post-Exploitation
- [ ] id, whoami, hostname, uname -a
- [ ] sudo -l
- [ ] SUID: `find / -perm -4000 2>/dev/null`
- [ ] Crontabs
- [ ] Running linpeas
- [ ] Internal ports: `ss -tlnp`
- [ ] Passwords in files: `grep -r password /var/www 2>/dev/null`
- [ ] user.txt captured
- [ ] root.txt captured
- [ ] Writeup completed
