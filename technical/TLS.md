---
label: TLS configuration 
icon: book 
---
!!!
Last Update on Jan, 2026.
!!!
# TLS configuration 
### Protocols 
***

## Protocols
| Protocol | Year | Security Status           | Compliance Status | Key Notes               |
| -------- | ---- | ------------------------- | ----------------- | ----------------------- |
| SSL 1.0  | 1994 | ❌ Broken / never released | ❌ Not allowed     | Prototype only          |
| SSL 2.0  | 1995 | ❌ Insecure                | ❌ Prohibited      | MITM vulnerabilities    |
| SSL 3.0  | 1996 | ❌ Insecure                | ❌ Prohibited      | POODLE attack           |
| PCT 1.0  | 1996 | ❌ Insecure                | ❌ Prohibited      | Microsoft pre-SSL protocol   |
| TLS 1.0  | 1999 | ❌ Deprecated              | ❌ Non-compliant   | BEAST, weak crypto      |
| TLS 1.1  | 2006 | ❌ Deprecated              | ❌ Non-compliant   | Legacy only             |
| TLS 1.2  | 2008 | ⚠️ Secure if hardened     | ✅ Compliant       | Must use strong ciphers |
| Multi-Protocol Unified Hello (MPUH)  | 2017 |   |      | Handshake Mechanism |
| TLS 1.3  | 2018 | ✅ Secure                  | ✅ Fully compliant | Recommended standard    |


## Ciphers
| #  | Cipher      | Key Length | Year Introduced | Security Status | Compliance                       | Notes                |
| -- | ----------- | ---------- | --------------- | --------------- | -------------------------------- | -------------------- |
| 1  | **NULL**    | 0          | 1994            | ❌ Insecure      | ❌ Prohibited                     | No encryption        |
| 2  | **DES**     | 56-bit     | 1977            | ❌ Broken        | ❌ Prohibited                     | Brute-force broken   |
| 3  | **RC2**     | 40-bit     | 1987            | ❌ Broken        | ❌ Prohibited                     | Export-grade weak    |
| 4  | **RC2**     | 56-bit     | 1987            | ❌ Broken        | ❌ Prohibited                     | Weak key             |
| 5  | **RC2**     | 128-bit    | 1987            | ❌ Deprecated    | ❌ Prohibited                     | Obsolete design      |
| 6  | **RC4**     | 40-bit     | 1987            | ❌ Broken        | ❌ Prohibited                     | Stream cipher flaws  |
| 7  | **RC4**     | 56-bit     | 1987            | ❌ Broken        | ❌ Prohibited                     | Same weaknesses      |
| 8  | **RC4**     | 64-bit     | 1987            | ❌ Broken        | ❌ Prohibited                     | Statistically broken |
| 9  | **RC4**     | 128-bit    | 1987            | ❌ Broken        | ❌ Prohibited                     | Banned by RFC 7465   |
| 10 | **3DES**    | 168-bit    | 1998            | ⚠️ Deprecated   | ❌ Prohibited (modern compliance) | SWEET32 attack       |
| 11 | **AES-128** | 128-bit    | 2001            | ✅ Secure        | ✅ PCI / NIST / FIPS              | Approved standard    |
| 12 | **AES-256** | 256-bit    | 2001            | ✅ Secure        | ✅ PCI / NIST / FIPS              | Approved standard    |
| 13 | **ChaCha20-Poly1305**  | 256-bit   | 2014    | ✅ Secure      |                                    | Secure modern AEAD   |


## Hash Algorithms
| # | Hash Algorithm | Output Size | Year Introduced | Security Status | Compliance          | Notes                       |
| - | -------------- | ----------- | --------------- | --------------- | ------------------- | --------------------------- |
| 1 | **MD5**        | 128-bit     | 1992            | ❌ Broken        | ❌ Prohibited        | Collision attacks practical |
| 2 | **SHA-1**      | 160-bit     | 1995            | ❌ Broken        | ❌ Prohibited        | SHAttered collision         |
| 3 | **SHA-256**    | 256-bit     | 2001            | ✅ Secure        | ✅ PCI / NIST / FIPS | Approved standard           |
| 4 | **SHA-384**    | 384-bit     | 2001            | ✅ Secure        | ✅ PCI / NIST / FIPS | Approved standard           |
| 5 | **SHA-512**    | 512-bit     | 2001            | ✅ Secure        | ✅ PCI / NIST / FIPS | Approved standard           |


## Key Exchange
| # | Key Exchange                                     | Year Introduced        | Security Status          | Compliance                   | Notes                                              |
| - | ------------------------------------------------ | ---------------------- | ------------------------ | ---------------------------- | -------------------------------------------------- |
| 1 | **Diffie-Hellman (DH)**                          | 1976                   | ⚠️ Secure if 2048-bit+   | ✅ PCI / NIST / FIPS          | Vulnerable to Logjam with small groups (<2048-bit) |
| 2 | **PKCS (RSA key exchange)**                      | 1977 / 1980s (PKCS #1) | ⚠️ Deprecated in TLS 1.2 | ✅ PCI / NIST / FIPS (legacy) | Forward secrecy not guaranteed; use carefully      |
| 3 | **Elliptic Curve Diffie-Hellman (ECDH / ECDHE)** | 2005                   | ✅ Secure                 | ✅ PCI / NIST / FIPS          | Recommended; supports forward secrecy              |




| No | Server Protocol              |Meaning|  Strict | PCI |  Best |  FIPS | InUse |
| -- | ---------------------------- |-----| ------- | --- | ----- | ----- | ----- |
| 1  | Multi-Protocol Unified Hello |Legacy  |        |     |       |       |       |
| 2  | PCT 1.0                      |Legacy  |        |     |       |       |       |
| 3  | SSL 2.0                      |Legacy |        |     |       |       |       |
| 4  | SSL 3.0                      |Legacy |        |     |       |       |       |
| 5  | TLS 1.0                      |Deprecated – no longer PCI compliant |        |     |  Best |  FIPS |       |
| 6  | TLS 1.1                      |Deprecated – no longer PCI compliant |        |     |  Best |  FIPS |       |
| 7  | TLS 1.2                      |Mandatory |Strict | PCI |  Best |  FIPS | InUse |
| 8  | TLS 1.3                      |Mandatory |Strict | PCI |  Best |  FIPS | InUse |

| No | Server Protocol              |  Strict | PCI |  Best |  FIPS | InUse |
| -- | ---------------------------- | ------- | --- | ----- | ----- | ----- |
|    |                              |         |     |       |       |       |
|    | Ciphers                      |         |     |       |       |       |
| 1  | NULL                         |         |     |       |       |       |
| 2  | DES 56/56                    |         |     |       |       |       |
| 3  | RC2 40/128                   |         |     |       |       |       |
| 4  | RC2 56/128                   |         |     |       |       |       |
| 5  | RC2 128/128                  |         |     |       |       |       |
| 6  | RC4 40/128                   |         |     |       |       |       |
| 7  | RC4 56/128                   |         |     |       |       |       |
| 8  | RC4 64/128                   |         |     |       |       |       |
| 9  | RC4 128/128                  |         |     |       |       |       |
| 10 | Triple DES 168               |  Strict | PCI |  Best |  FIPS |       |
| 11 | AES 128/128                  |  Strict | PCI |  Best |  FIPS | InUse |
| 12 | AES 256/256                  |  Strict | PCI |  Best |  FIPS | InUse |
|    |                              |         |     |       |       |       |
|    | Hashes                       |         |     |       |       |       |
| 1  | MD5                          |  Strict | PCI |  Best |       |       |
| 2  | SHA                          |  Strict | PCI |  Best |  FIPS |       |
| 3  | SHA 256                      |  Strict | PCI |  Best |  FIPS | InUse |
| 4  | SHA 384                      |  Strict | PCI |  Best |  FIPS | InUse |
| 5  | SHA 512                      |  Strict | PCI |  Best |  FIPS | InUse |
|    |                              |         |     |       |       |       |
|    | Key Exchange                 |         |     |       |       |       |
| 1  | Diffie-Hellman               |  Strict | PCI |  Best |  FIPS | InUse |
| 2  | PKCS                         |  Strict | PCI |  Best |  FIPS | InUse |
| 3  | ECDH                         |  Strict | PCI |  Best |  FIPS | InUse |

***
### Ciphers

| No | Cipher | Strict | PCI | Best | FIPS | TLS 1.2 InUse |
| -- | ----------------------------------------------- | ------- | --- | ----- | ----- | ----------------- |
| 1  | TLS\_ECDHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384,   |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 2  | TLS\_ECDHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256,   |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 3  | TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384,   |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 4  | TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256,   |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 5  | TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA,      |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 6  | TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA,      |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 7  | TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384, |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 8  | TLS\_ECDHE\_ECDSA\_WITH\_AES\_128 GCM\_SHA256,  |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 9  | TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_CBC\_SHA384, |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 10 | TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_CBC\_SHA256, |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 11 | TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_CBC\_SHA,    |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 12 | TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_CBC\_SHA,    |  Strict | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 13 | TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384,          |         | PCI |  Best |  FIPS |                   |
| 14 | TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256,          |         | PCI |  Best |  FIPS |                   |
| 15 | TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256,          |         | PCI |  Best |  FIPS |                   |
| 16 | TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256,          |         | PCI |  Best |  FIPS |                   |
| 17 | TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA,             |         | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 18 | TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA,             |         | PCI |  Best |  FIPS | TLS 1.2 InUse     |
| 19 | TLS\_DHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384,     |         |     |       |  FIPS |                   |
| 20 | TLS DHE RSA\_WITH\_AES 128\_ GCM SHA256,        |         |     |       |  FIPS |                   |
| 21 | TLS\_DHE\_RSA\_WITH\_AES\_256\_CBC\_SHA,        |         |     |       |  FIPS |                   |
| 22 | TLS\_DHE\_RSA\_WITH\_AES\_128\_CBC\_SHA,        |         |     |       |  FIPS |                   |
| 23 | TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA,            |         |     |       |  FIPS |                   |
| 24 | TLS\_DHE\_DSS\_WITH\_AES\_256\_CBC\_SHA256,     |         |     |       |  FIPS |                   |
| 25 | TLS\_DHE\_DSS\_WITH\_AES\_128\_CBC\_SHA256,     |         |     |       |  FIPS |                   |
| 26 | TLS\_DHE\_DSS\_WITH\_AES\_256\_CBC\_SHA,        |         |     |       |  FIPS |                   |
| 27 | TLS\_DHE\_DSS\_WITH\_AES\_128\_CBC\_SHA,        |         |     |       |  FIPS |                   |
| 28 | TLS\_DHE\_DSS\_WITH\_3DES\_EDE\_CBC\_SHA,       |         |     |       |  FIPS |                   |
| 29 | TLS\_RSA\_WITH\_RC4\_128\_SHA,                  |         |     |       |       |                   |
| 30 | TLS\_RSA\_WITH\_RC4\_128\_MD5,                  |         |     |       |       |                   |
| 31 | TLS\_RSA\_WITH\_NULL\_SHA256,                   |         |     |       |       |                   |
| 32 | TLS\_RSA\_WITH\_NULL\_SHA,                      |         |     |       |       |                   |
| 33 | TLS\_PSK\_WITH\_AES\_256\_GCM\_SHA384,          |         |     |       |       |                   |
| 34 | TLS\_PSK\_WITH\_AES\_128\_GCM\_SHA256,          |         |     |       |       |                   |
| 35 | TLS\_PSK\_WITH\_AES\_256\_CBC\_SHA384,          |         |     |       |       |                   |
| 36 | TLS\_PSK\_WITH\_AES\_128\_CBC\_SHA256,          |         |     |       |       |                   |
| 37 | TLS\_PSK\_WITH\_NULL\_SHA384,                   |         |     |       |       |                   |
| 38 | TLS\_PSK\_WITH\_NULL\_SHA256,                   |         |     |       |       |                   |
                                                                                                          
                                                                                                          
                                                                                                          
                                                                                                          
                                                                                                          
                                                                                                          
                                                                                                          
