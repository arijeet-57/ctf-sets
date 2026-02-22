# How to Start a New Challenge

## 1. Create the folder

```bash
# For CTF web challenge
mkdir -p challenges/web/challenge-name/{artifacts,scripts}
cp templates/challenge-notes.md challenges/web/challenge-name/notes.md

# For HTB/TryHackMe box
mkdir -p challenges/pwn/box-name/{scans,artifacts,loot}
cp templates/report-template.md challenges/pwn/box-name/report.md
```

## 2. Set target variable

```bash
export TARGET=10.10.10.x
echo $TARGET
```

## 3. Start logging your terminal (optional but useful)

```bash
script -a challenges/web/challenge-name/terminal.log
```

## 4. Begin enumeration per methodology

See [ctf-methodology.md](ctf-methodology.md) or [pentest-methodology.md](pentest-methodology.md)

## 5. After solving

```bash
# Move final exploit to scripts
cp challenges/web/challenge-name/exploit.py scripts/web/

# Write the final writeup
cp templates/challenge-notes.md writeups/challenge-name.md
# Fill it in cleanly for publishing
```
