---
label: PCI DSS
icon: book 
order: 999
---
!!!
Last Update on Jan, 2026.
!!!
# PCI DSS

**Account Data**

- Cardholder Data Includes
    - Primary Account Number (PAN)
        - Storage Restriction [Data kept to minimum]
        - Stored as Readable  [No]
            - Exception :   business must provide justifications
                - Masked (Unreversible)  : Either X mark or some logic.
                - Hash (Unreversible) : Hashing and salting.
                - Encryption : Only strong encryption + key management (KEK & KDK)
            - Not allowed
                - Encoded (Reversible):  Not Allowed.
    - Cardholder Name
        - Storage Restriction [Data kept to minimum]
        - Stored as Readable  [Yes]
    - Expiration Date
        - Storage Restriction [Data kept to minimum]
        - Stored as Readable  [Yes]
    - Service Code
        - Storage Restriction [Data kept to minimum]
        - Stored as Readable  [Yes]
- Sensitive Authentication Data Includes
    - Full Track Data (Magnetic Stripe data or equivalent on chip)
        - Storage Restriction [No, Cannot be stored after Authorization]
        - Stored as Readable  [No]
            - Exception : Encrypted until Authorization, immediately to be removed after Authorization
    - Card Verification code
        - Storage Restriction [No, Cannot be stored after Authorization]
        - Stored as Readable  [No]
            - Exception : Encrypted until Authorization, immediately to be removed after Authorization
    - Pins/Pin Blocks
        - Storage Restriction [No, Cannot be stored after Authorization]
        - Stored as Readable  [No]
            - Exception : Encrypted until Authorization  immediately to be removed after Authorization (offline ex: airplane)

---

Card numbers schema

- BIN 6
    - 123456MMMMMM1234
    - M = Masking 6 digits
- BIN 8
    - 12345678MMMM1234
    - M = Masking 4 digits

---

Continuous Assurance (Or Any significant change)

- Daily
    - log review  (SIEM)
- Quarterly days cycle:
    - Internal VA
    - External VA (ASV: External Vendor, Qualys)
    - User Management Review
    - Wireless scans
    - Process is Mandatory tool CDD is Optional
- Semi-annual:
    - Firewall Cleansing
    - Segmentation PT
- Annual:
    - Internal Application PT
    - External Application PT
    - Internal Network PT
    - External Network PT

---

V3 vs V4

| Version 3 | Version 4 |
| --- | --- |
| 12 Requirements  | 12 Requirements  |
| Unauthenticated Vulnerabilities  scan  | Authenticated Vulnerabilities scan  |
| Password local users 7 characters  | Password local users  12 characters and complex |
| Password Services account 7 characters  | Password Services account 15 characters and complex  |
| MFA for admin users  | MFA is must on machines for all users  |
| Key management repo is not needed | Key management repo is needed  |
| Encryption algo min AES 128 | Encryption algo min AES 256 |
| No targeted risk  | Targeted risk & controls & frequency  |
| No RACI matrix  | RACI for each item  |
| 16 digits PAN first 6 and last 4 | 16 digits PAN first 6 and last 4 |
| Only PCI controls | Custom controls  |

---

Resources 

- Documents
    - https://www.pcisecuritystandards.org/document_library/
- PCI DSS v4
    - https://docs-prv.pcisecuritystandards.org/PCI DSS/Standard/PCI-DSS-v4_0_1.pdf
