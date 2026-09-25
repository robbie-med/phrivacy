# phrivacy

**Tools, tactics, and techniques (TTT) for US primary care and family physicians who run their personal life, their work life, and a patient-facing phone number from one GrapheneOS Pixel.**

Plenty of us give patients a way to reach us directly: after-hours questions, post-visit follow-up, direct primary care, rural practice, small independent clinics. That's good medicine. It shouldn't mean patients can find your spouse on Venmo, clinical photos end up in your family photo backup, or a lost phone becomes a reportable breach.

This repo is a practical playbook for keeping three worlds apart on one device:

| World | Who has access | Where it lives on the phone |
|---|---|---|
| **Personal** | Family, friends, banks, your kid's school | Owner profile, personal eSIM |
| **Work** | Colleagues, the clinic, the hospital, the EHR | Separate user profile (or work profile) |
| **Patient-facing** | Patients and their families | A VoIP/secure-messaging number inside the work profile, *never* a personal SIM |

> **Not legal, compliance, or medical-board advice.** HIPAA, state privacy laws, and employer policies differ. Run anything that touches PHI past your compliance officer or privacy counsel. Vendor features and GrapheneOS menus change. Check current docs before you rely on a detail here.

---

## The short version

1. **Buy a supported Pixel** (Pixel 10 series or newer) and install GrapheneOS with the official web installer. Relock the bootloader. → [01-device-and-install](docs/01-device-and-install.md)
2. **Split the phone into profiles.** Owner = personal. A separate *Clinical* user profile holds the EHR, the patient line, work email, and MDM. Optionally add a *Quarantine* profile for apps you don't trust. → [02-profile-architecture](docs/02-profile-architecture.md)
3. **Never give patients a carrier SIM number.** Give them a number on a HIPAA-oriented platform that will sign a BAA (Spruce, a Workspace/enterprise voice product, your health system's tool). Use a caller-ID-masking dialer for outbound calls. → [03-numbers-and-telephony](docs/03-numbers-and-telephony.md)
4. **Set boundaries in software.** Office-hours routing, after-hours auto-replies, an emergency voicemail greeting, DND Modes. → [04-patient-communication](docs/04-patient-communication.md)
5. **Keep the work stack contained.** EHR apps, MDM, and authenticators go in the Clinical profile with their own sandboxed Google Play. → [05-work-apps-and-mdm](docs/05-work-apps-and-mdm.md)
6. **Protect the personal number like a password.** Messenger discovery, data brokers, carrier port-out locks. → [06-personal-number-opsec](docs/06-personal-number-opsec.md)
7. **Harden the device.** Duress PIN, auto-reboot, USB-C lockdown, per-app network and sensor permissions. → [07-hardening-checklist](docs/07-hardening-checklist.md)
8. **Run it every day** without friction. → [08-daily-operations](docs/08-daily-operations.md)
9. **Know what to do when something goes wrong.** Lost phone, harassing patient, SIM swap. → [09-incident-response](docs/09-incident-response.md)

## Contents

### Guides
- [00 – Threat model](docs/00-threat-model.md)
- [01 – Device selection & GrapheneOS install](docs/01-device-and-install.md)
- [02 – Profile architecture](docs/02-profile-architecture.md)
- [03 – Numbers & telephony](docs/03-numbers-and-telephony.md)
- [04 – Patient communication & boundaries](docs/04-patient-communication.md)
- [05 – Work apps, EHR, and MDM](docs/05-work-apps-and-mdm.md)
- [06 – Personal number OPSEC](docs/06-personal-number-opsec.md)
- [07 – Hardening checklist](docs/07-hardening-checklist.md)
- [08 – Daily operations](docs/08-daily-operations.md)
- [09 – Incident response](docs/09-incident-response.md)

### Checklists
- [Initial setup checklist](checklists/setup-checklist.md)
- [Quarterly review checklist](checklists/quarterly-review.md)

### Templates
- [Patient communication policy](templates/patient-communication-policy.md) (hand to patients / put in intake packet)
- [Voicemail greetings](templates/voicemail-greetings.md)
- [Auto-replies & canned responses](templates/auto-replies.md)

## Architecture at a glance

```
┌──────────────────────────── Pixel (GrapheneOS) ────────────────────────────┐
│                                                                             │
│  OWNER PROFILE — "Personal"               CLINICAL PROFILE — "Work"         │
│  ─────────────────────────                ─────────────────────────         │
│  • Personal eSIM (carrier)                • Sandboxed Google Play (own)     │
│  • Dialer / SMS for personal line         • MDM / Company Portal (if req'd) │
│  • Signal, family apps, banking           • EHR mobile (Haiku/Canto/etc.)   │
│  • Personal Google acct (optional)        • Patient line app (Spruce, etc.) │
│  • Personal photos & backups              • Masked-caller-ID dialer         │
│                                           • Work email, Teams/Slack         │
│  Notifications from Clinical  ◄───────────  "Send notifications to          │
│  forwarded here (optional)                   current user" = ON             │
│                                                                             │
│  PRIVATE SPACE (optional)                 QUARANTINE PROFILE (optional)     │
│  • Sensitive personal apps                • Apps that demand phone number,  │
│                                             contacts, or look shady         │
└─────────────────────────────────────────────────────────────────────────────┘

Patient ──► Patient-facing VoIP number ──► Clinical profile app ──► (after hours) auto-reply / on-call
Family  ──► Personal carrier number ─────► Owner profile dialer
You ────► Patient (outbound) ────────────► Masked dialer shows CLINIC number, not yours
```

## Principles

- **Compartmentalize by identity, not by app.** Each world gets its own profile, accounts, contacts, photos, and backups.
- **The patient-facing number is disposable and transferable.** You can route it to an answering service, a covering colleague, or retire it without changing your personal life.
- **No PHI in the personal profile. Ever.** No clinical photos in your personal camera roll, no patient texts over carrier SMS, no patient names in personal contacts.
- **Friction is the enemy of security.** If the setup is annoying you'll route around it at 2 a.m. The daily-ops guide is there to keep it livable.
- **Verify, don't trust.** GrapheneOS, carrier, and vendor features move fast. Every guide links to the source of truth.

## Contributing

Corrections and field reports are welcome, especially "this EHR/MDM works (or doesn't) on GrapheneOS." See [CONTRIBUTING.md](CONTRIBUTING.md). **Don't include patient information, employer-identifying details, or anything that identifies you** in issues or PRs.
