# 00 – Threat model

Know who you're defending against before you change a setting. For a physician whose number is known to patients, most threats are mundane. That's why they matter: they're the ones that actually happen.

## Assets

| Asset | Why it matters |
|---|---|
| **Personal phone number** | It's the key to your identity: bank 2FA, messenger accounts, data-broker profiles, your home address. |
| **Personal life data**: photos, location, contacts, family accounts | Boundary violations, stalking, and embarrassment. |
| **PHI on the device**: messages, photos, EHR cache, call logs | HIPAA breach exposure, board complaints, patient harm. |
| **Work credentials**: SSO, MFA, EHR sessions | Account takeover at your employer or health system. |
| **Your time and attention** | Burnout is a real risk. An always-reachable number erodes the boundary between on and off. |

## Adversaries & scenarios

| # | Adversary | Realistic scenario | Primary controls |
|---|---|---|---|
| 1 | **Well-meaning patient** | Texts at 11 p.m. about a non-urgent refill. Expects a reply. | Patient-facing VoIP line, after-hours auto-reply, published policy ([04](04-patient-communication.md)) |
| 2 | **Boundary-crossing or obsessive patient** | Saves your number, finds your personal Venmo/WhatsApp/Instagram through contact discovery, shows up at your house. | Personal number never given out. Messenger discovery off. Data-broker opt-outs ([06](06-personal-number-opsec.md)) |
| 3 | **Patient's apps** | The patient's phone uploads their contacts, including you, to Facebook, LinkedIn, Truecaller, and caller-ID apps. Your name and number get linked globally. | Patient-facing number is a *practice* identity (CNAM = practice name), never the personal one |
| 4 | **Data brokers / people-search sites** | Personal number → home address → family members. | Opt-outs, a separate number for commerce, masked email ([06](06-personal-number-opsec.md)) |
| 5 | **SIM-swap / port-out fraudster** | Steals your personal number to reset bank or email accounts. | Carrier port-out lock/PIN, app-based 2FA or passkeys, not SMS ([06](06-personal-number-opsec.md)) |
| 6 | **Lost or stolen device** | Phone left in a clinic exam room or an Uber. | Strong PIN, auto-reboot, profiles at rest (BFU), remote wipe via MDM for work profile ([07](07-hardening-checklist.md), [09](09-incident-response.md)) |
| 7 | **Employer MDM overreach** | Hospital MDM wants full-device management of a personally owned phone. | Enroll MDM *only* inside the Clinical profile. Never on Owner ([05](05-work-apps-and-mdm.md)) |
| 8 | **Malicious or leaky apps** | A "free" app harvests contacts or location. | Contact Scopes, Storage Scopes, Network/Sensors permissions, Quarantine profile ([02](02-profile-architecture.md), [07](07-hardening-checklist.md)) |
| 9 | **Phishing / smishing** | Fake "EHR password expired" text to the patient line. | Separate profiles, passkeys/FIDO2, verify through known channels |
| 10 | **Compelled or coerced unlock** | Someone forces you to unlock (domestic situation, robbery). | Duress PIN, lockdown, BFU state ([07](07-hardening-checklist.md)) |

## Out of scope

- **Targeted nation-state attacks.** GrapheneOS helps a lot, but if this is your threat model you need specialist help, not a README.
- **Legal process against your employer's systems.** Work data in employer systems is discoverable no matter how your phone is configured.
- **Compliance program design.** This repo helps you *personally* avoid creating PHI exposure on your device. It doesn't replace your organization's HIPAA risk analysis.

## The three rules everything else follows from

1. **Patients get a number that isn't tied to your identity and can be handed off or retired.**
2. **PHI lives only in the Clinical profile, inside apps covered by a BAA.**
3. **The personal number never appears anywhere a patient or a work system can see it.**
