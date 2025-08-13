Week-3
**Presented by**: Muhammad Naveed
**Training Program**: Cybersecurity Fundamentals – KaiRiz

# ENUM4LINUX, Hydra. 
# Hydra - Password Cracking & Brute Force Tool

## Overview
Hydra (also called THC-Hydra) is a fast, flexible, and powerful network login cracker. 
It supports numerous protocols for attacking and is commonly used for brute-force or dictionary-based password attacks against a variety of services.

### Key Features
- Supports 50+ protocols (HTTP, HTTPS, FTP, SSH, Telnet, SMB, RDP, MySQL, etc.)
- Supports both **Dictionary Attacks** and **Brute Force Attacks**
- CLI and GUI (xHydra) available
- Parallelized login attempts for speed
- Extensible with additional modules

---

## Attack Types
1. **Brute Force Attacks** - Attempts all possible combinations until the correct one is found.
2. **Dictionary Attacks** - Uses a pre-compiled list of possible passwords.
3. **Hybrid Attacks** - Modifies dictionary words to generate variations.

---

## Hydra Styles
- **New Style** (Recommended): Uses modern syntax with options and parameters clearly defined.
- **Old Style**: Legacy command format (still supported for backward compatibility).

---

## Syntax Breakdown
General Command:
```
hydra [options] [protocol://target] [parameters]
```

Example (SSH Brute Force):
```
hydra -l username -P /path/to/passwords.txt ssh://192.168.1.10
```

**Important Options:**
- `-l` : Single username
- `-L` : File containing list of usernames
- `-p` : Single password
- `-P` : File containing list of passwords
- `-t` : Number of parallel connections
- `-s` : Specify port if non-default
- `-V` : Verbose mode (show each attempt)
- `-e` : Additional checks:
  - `-e s` : Try blank password
  - `-e n` : Try username as password
  - `-e r` : Try reversed username as password

---

## Common Protocol Examples

### 1. SSH Brute Force
```
hydra -l admin -P passwords.txt ssh://192.168.1.50
```

### 2. FTP Brute Force
```
hydra -L users.txt -P passwords.txt ftp://192.168.1.20
```

### 3. MySQL Brute Force
```
hydra -L users.txt -P passwords.txt mysql://192.168.1.15
```

### 4. HTTP POST Login Brute Force
```
hydra -l admin -P passwords.txt 192.168.1.100 http-post-form "/login.php:user=^USER^&pass=^PASS^:Invalid login"
```

---

## Workflow for Using Hydra
1. **Identify Target & Protocol**  
   - Use Nmap to scan open ports and detect services.
2. **Prepare Usernames and Password Lists**  
   - Example wordlists: `/usr/share/wordlists/rockyou.txt`
3. **Select Appropriate Module/Protocol**
4. **Run Hydra with Optimized Settings**
5. **Review Output** for valid credentials.

---

## Best Practices
- Use relevant and small wordlists for efficiency.
- Avoid targeting production systems without permission (legal implications).
- Combine Hydra with reconnaissance tools for better targeting.
- For web forms, carefully craft the `http-form` parameter to match the target.

---

## MITRE ATT&CK Mapping
- **T1110** - Brute Force
- **T1110.001** - Password Guessing
- **T1110.002** - Password Cracking
- **T1110.003** - Password Spraying

---

## Defensive Measures Against Hydra Attacks
- Implement account lockouts after failed login attempts.
- Use multi-factor authentication (MFA).
- Restrict login attempts by IP and geolocation.
- Monitor for abnormal login patterns.

---

## References
- [Hydra GitHub](https://github.com/vanhauser-thc/thc-hydra)
- [Kali Linux Hydra Documentation](https://www.kali.org/tools/hydra/)
