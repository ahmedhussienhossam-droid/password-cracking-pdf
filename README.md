# PDF Password Cracking — JTR vs Online Tools

## Overview
This repo documents two tasks (PM1 & PM2) from the Network Security course (ECE 445): cracking the passwords of three protected PDF files (`My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`) using two different approaches — a local offline tool (John the Ripper) and an online tool set (Networkwalks).

## Target Files & Results

| File | Hash file | Extracted Hash (start) | Password Cracked |
|---|---|---|---|
| My Locked PDF1.pdf | `hashes/hash1.txt` | `$pdf$4*4*128*-1028*1*16*ca7f72f1...` | `good-luck` |
| My Locked PDF2.pdf | `hashes/hash2.txt` | `$pdf$4*4*128*-1028*1*16*0853f2cd...` | `password1` |
| My Locked PDF3.pdf | `hashes/hash3.txt` | `$pdf$4*4*128*-1028*1*16*34eb542e...` | `1qaz2wsx` |

## Task 1 — Password Cracking with JTR (John the Ripper)

**Tools:** John the Ripper (JTR) + Johnny (GUI frontend), `onlinehashcrack.com` (PDF hash extractor)

**Steps (repeated for each of the 3 PDFs):**
1. Downloaded the target locked PDF.
2. Uploaded it to the PDF Hash Extractor on `onlinehashcrack.com` to generate a crackable hash in pdf2john/hashcat format.
3. Saved the extracted hash into `hashes/hash1.txt`, `hash2.txt`, and `hash3.txt` respectively.
4. Opened Johnny → **Open password file** → selected the hash file → **Start new attack**.
5. Johnny cracked each hash and returned the password, used to unlock the matching PDF.

**Results:** `good-luck`, `password1`, `1qaz2wsx` (see table above)

**Screenshots:** see `task1-jtr/screenshots/`
- `onlinehashcrack-pdf-hash-extraction.png`
- `johnny-password-cracked.png`

## Task 2 — Password Cracking with Networkwalks Online Tools

**Tools:** `networkwalks.com/hash-calculator`, `networkwalks.com/password-cracker`

**Steps (repeated for each of the 3 PDFs):**
1. Uploaded the target locked PDF to the Networkwalks **Hash Calculator** (PDF tab) — parsed locally in-browser, nothing uploaded to a server.
2. Generated the same `$pdf$...` hash as the onlinehashcrack extraction (confirms both extraction methods agree).
3. Copied the hash and pasted it into the **Password Cracker** (dictionary attack tool).
4. Ran the attack — tool iterated through a wordlist, reporting `pw/s` and progress, until a match was found.
5. Opened each PDF using its recovered password.

**Results:** Matched Task 1 exactly — `good-luck`, `password1`, `1qaz2wsx`

**Screenshots:** see `task2-networkwalks/screenshots/`
- `hash-calculator-pdf-hash.png`
- `password-cracker-attack-match.png`

## Flags Captured
While going through the Networkwalks learning path, 4 flags were captured along the way:

| Flag | Value |
|---|---|
| Flag 1 | `nw{cybersecurity_flag_captured_2608}` |
| Flag 2 | `nw{networkwalks_flag1_jtr_270521_1}` |
| Flag 3 | `nw{networkwalks_persistence_jtr_270521}` |
| Flag 4 | `nw{networkwalks_flag_260821_1}` |

**Screenshots:** see `flags/screenshots/`

## Comparison

| | JTR (Johnny) | Networkwalks (Online) |
|---|---|---|
| Setup | Requires installing JTR + Johnny (or Kali) | No installation needed, browser-based |
| Hash extraction | External tool (onlinehashcrack.com) | Built-in Hash Calculator, parses PDF locally |
| Speed | Depends on local machine specs | Depends on server load / connection |
| Offline use | Yes (once hash is extracted) | No (requires internet) |
| Ease of use | Slightly more technical (GUI still helps) | Very straightforward, step-by-step UI |

## Conclusion
Both methods successfully cracked the passwords of all three PDFs from identical hashes, confirming the result across a local offline tool and an online cracking service. The passwords (`good-luck`, `password1`, `1qaz2wsx`) are all common dictionary-style passwords, showing how quickly weak PDF passwords can be broken regardless of the tool used — reinforcing the importance of strong password policies for sensitive documents.

---
*Network Security (ECE 445) — Delta University*
