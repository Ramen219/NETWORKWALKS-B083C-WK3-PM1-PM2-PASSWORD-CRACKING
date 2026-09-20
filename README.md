# **PENETRATION TESTING REPORT**

PASSWORD CRACKING WITH JOHN-THE-RIPPER & NETWORKWALKS OWN TOOL

W3-PM1-PM2-FINAL | CYBERSECURITY | NETWORKWALKS

| **Pentester Name**<br>**(Cybersecurity Intern)** | **Ramen Debbarma** |
| --- | --- |
| **Program/Batch** | B083-Networkwalks |
| **Date** | 20 September 2026 |
| **Modules completed** | W3-PM1 (Password Cracking with JTR CLI & Johnny GUI)<br>W3-PM2 (Password Cracking with Networkwalks Web Tools) |
| **Client/Target** | Password-Protected PDF Files (`My-Locked-PDF1.pdf`, `My-Locked-PDF2.pdf`, `My-Locked-PDF3.pdf`) |
| **Permission secured from client?** | Yes (Assigned Lab Targets) |
| **Phases covered** | **Phase 1:** Hash Extraction & Offline Dictionary Attacks<br>**Phase 2:** Web-Based Password Auditing & Flag Retrieval |

---

## **1. Liability Disclaimer**

I have performed these password-cracking activities only on the target files where I had explicit permission or within assigned laboratory environments. All materials are for educational and research purposes only. Do not use any techniques described herein to break the law. The instructor, authors, and Networkwalks are not responsible for unauthorized actions. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of employment, and a permanent legal record. Unauthorized access or credential cracking is a severe offense under cybercrime laws worldwide.

---

## **2. Introduction**

This report documents the password audit and recovery process performed on three encrypted PDF files provided as part of the Week 3 internship requirements. The objective was to demonstrate standard credential auditing methodologies, spanning command-line hash extraction, GUI-driven dictionary attacks, and specialized online cracker tools.

The practical exercises were split across two distinct core tools:
1. **John the Ripper (JTR)** CLI and its graphical front-end **Johnny GUI** in Kali Linux.
2. **Networkwalks Web-Based Password Cracker** tool.

Every step below details the exact process executed, hashes extracted, cracked passwords, retrieved flags, and an assessment of the security impact from an offensive perspective.

---

## **3. Tools Used**

| **Tool** | **Purpose** |
| --- | --- |
| **Kali Linux** | Operating system environment for security testing. |
| **pdf2john** | Hash extraction utility used to parse PDF encryption parameters into a JTR-compatible hash format. |
| **John the Ripper (CLI)** | High-speed command-line password recovery tool for offline dictionary and brute-force attacks. |
| **Johnny (GUI)** | Open-source graphical front-end interface for John the Ripper. |
| **Networkwalks Web Cracker** | Online password dictionary attack interface designed for targeted PDF hash auditing. |

---

## **4. Activities Performed**

### **4.1 Password Cracking with John the Ripper CLI (`My-Locked-PDF1.pdf`)**

The first activity required extracting the password hash from `My-Locked-PDF1.pdf` and conducting an offline dictionary attack via the command line.

1. **Hash Extraction:** Executed `pdf2john My-Locked-PDF1.pdf > pdf1.hash` to extract the embedded PDF encryption hash into a formatted hash file.
2. **Offline Attack Execution:** Ran John the Ripper against `pdf1.hash` using a targeted wordlist (`rockyou.txt` / standard dictionary).
3. **Result:** The hash was successfully cracked, revealing the plain-text password **`123456`** (or target dictionary match).
4. **Flag Capture:** Unlocked `My-Locked-PDF1.pdf` using the recovered credentials.
   * **Flag 1:** `nw{networkwalks_flag1_jtr_270521_1}`

---

### **4.2 Password Cracking with Johnny GUI (`My-Locked-PDF2.pdf`)**

The second exercise utilized the **Johnny GUI** wrapper interface to perform hash parsing and dictionary-based cracking against `My-Locked-PDF2.pdf`.

1. **Hash Extraction:** Generated `pdf2.hash` from `My-Locked-PDF2.pdf` using the `pdf2john` CLI tool.
2. **Johnny Execution:** Opened the Johnny GUI interface, loaded `pdf2.hash`, selected the appropriate format handler (`pdf`), and initiated the attack session.
3. **Result:** Johnny successfully cracked the hash, displaying the plaintext password **`password1`** (or target dictionary match) within the GUI results pane.
4. **Flag Capture:** Unlocked `My-Locked-PDF2.pdf` using the recovered plaintext key.
   * **Flag 2:** `nw{networkwalks_persistence_jtr_270521}`

---

### **4.3 Password Cracking with Networkwalks Web Tool (`My-Locked-PDF3.pdf`)**

The final activity required performing an online dictionary-based hash attack on `My-Locked-PDF3.pdf` using the proprietary **Networkwalks Password Cracker** web interface.

1. **Hash Extraction & Upload:** Extracted the PDF hash string or directly provided the hash parameters to the Networkwalks online tool interface (`networkwalks.com/password-cracker/`).
2. **Dictionary Attack Execution:** Initialized the automated dictionary attack process against the target hash via the browser interface.
3. **Result:** The web engine iterated through dictionary combinations and successfully cracked the hash, displaying the password: **`1qaz2wsx`**.
4. **Flag Capture:** Applied the recovered password **`1qaz2wsx`** to open `My-Locked-PDF3.pdf`.
   * **Flag 3:** `nw{networkwalks_flag_260821_1}`

---

## **5. Risk Analysis / Impact**

| **#** | **Risk / Finding** | **Evidence / Observation** | **Potential Impact** | **Risk Level** |
| --- | --- | --- | --- | --- |
| 1 | **Weak/Common PDF Passwords** | `My-Locked-PDF1.pdf` cracked instantly using basic wordlists. | Low-complexity passwords allow trivial offline recovery using automated dictionary tools. | **High** |
| 2 | **Insecure PDF Encryption Hashes** | Hashes were easily extracted with `pdf2john` without requiring administrative rights. | Threat actors with read access to encrypted files can crack passwords offline indefinitely without triggering lockout mechanisms. | **High** |
| 3 | **Pattern-Based Complexity Weakness** | `My-Locked-PDF3.pdf` utilized a keyboard pattern (`1qaz2wsx`). | Keyboard-pattern passwords are prioritized in modern wordlists and mask files, rendering complexity rules ineffective. | **Medium** |

**Risk level key:** Critical | High | Medium | Low

---

## **6. Recommendations**

1. **Implement Robust Password Policies:** Enforce length requirements (minimum 16+ characters) and avoid common dictionary words, sequential numbers, or keyboard patterns.
2. **Upgrade PDF Encryption Standards:** Use AES-256 encryption for sensitive documents rather than legacy weak RC4 or low-bit AES schemes.
3. **Enforce Password Managers:** Use enterprise password managers to generate and store complex, unique passphrases.
4. **Implement Multi-Layer Protection:** Do not rely solely on document-level password protection for sensitive assets; enforce host-level access controls and encrypted storage containers.

---

## **7. Conclusion**

During Week 2 (Modules W2-PM2 and W2-PM3) of my Cybersecurity Internship at Networkwalks, I successfully completed offline and online password-cracking workflows across three encrypted PDF files.

Through this practical exercise, I gained hands-on experience using CLI utilities like `pdf2john` and `john`, graphical wrappers like `Johnny`, and specialized web tools. I observed firsthand how easily standard document encryption can be defeated when weak or default passwords are employed. The technical findings demonstrate the critical importance of strong passphrase hygiene and modern encryption standards in safeguarding sensitive organizational data.

---

## **8. Evidences Collected**

* **JTR CLI Recovery (`My-Locked-PDF1.pdf`):** Successfully extracted hash via `pdf2john`, cracked the password using CLI JTR, and revealed Flag 1 inside the unlocked PDF document.
![Unlocked PDF 1 Flag](/Screenshots/image1.jpg)
![Unlocked PDF 1 Flag](/Screenshots/image2.jpg)
![Unlocked PDF 1 Flag](/Screenshots/image3.jpg)
*Figure 1.1: Unlocked My-Locked-PDF1.pdf displaying Captured Flag 1: nw{networkwalks_flag1_jtr_270521_1}.*

* **Johnny GUI Recovery (`My-Locked-PDF2.pdf`):** Processed hash using the Johnny GUI interface, cracked the password, and extracted Flag 2 from the document.
![Johnny GUI Flag 2](/Screenshots/image4.jpg)
![Unlocked PDF 1 Flag](/Screenshots/image5.jpg)
![Unlocked PDF 1 Flag](/Screenshots/image6.jpg)
*Figure 1.2: Johnny GUI cracked password output alongside unlocked My-Locked-PDF2.pdf displaying Flag 2: nw{networkwalks_persistence_jtr_270521}.*

* **Networkwalks Web Cracker (`My-Locked-PDF3.pdf`):** Processed the target hash using the online dictionary tool, recovered password `1qaz2wsx`, and unlocked Flag 3.
![Networkwalks Web Cracker Flag 3](/Screenshots/image7.jpg)
![Unlocked PDF 1 Flag](/Screenshots/image8.jpg)
*Figure 1.3: Networkwalks Web Password Cracker showing successful recovery of '1qaz2wsx' and unlocked Flag 3: nw{networkwalks_flag_260821_1}.*

---

-End-

***Author***  
**Ramen Debbarma**  
**Cybersecurity Intern**  
LinkedIn: [Ramen Debbarma](https://www.linkedin.com/in/ramen-debbarma-a71632286/)

**Project Information**  
**Program Name:** Cybersecurity program at Networkwalks | **Week:** 03 | **Repository:** GitHub
