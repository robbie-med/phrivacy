# Initial setup checklist

Work through this in order. Plan for an evening for the device plus a week of migrating accounts.

## Before you start
- [ ] Read [00 – Threat model](../docs/00-threat-model.md)
- [ ] Choose the patient-facing platform and **sign its BAA** ([03](../docs/03-numbers-and-telephony.md#platform-options-verify-baas-features-and-pricing-yourself))
- [ ] Ask IT what your employer's MDM requires for BYOD ([05](../docs/05-work-apps-and-mdm.md#mdm-intune-workspace-one-etc))
- [ ] Carrier: get eSIM transfer/activation instructions; **set account PIN and port-out lock**
- [ ] Back up the old phone (personal data only)

## Device
- [ ] Buy an unlocked Pixel 10+ that's on the GrapheneOS supported list
- [ ] Install via the web installer, **relock the bootloader**, disable OEM unlocking ([01](../docs/01-device-and-install.md))
- [ ] Verify with Auditor
- [ ] Owner: sandboxed Play (temporarily, no sign-in) → enable privileged eSIM management → activate personal eSIM
- [ ] Set the default calls/SMS/data line

## Profiles
- [ ] Owner = Personal: PIN, fingerprint, personal apps ([02](../docs/02-profile-architecture.md))
- [ ] Create **Clinical** user: separate PIN, notifications forwarded, calls & SMS off
- [ ] Clinical: sandboxed Play, work account, MDM (work profile if required), authenticator
- [ ] Clinical: patient-line app, EHR, email, secure chat (masking dialer optional, as a fallback)
- [ ] Create **Quarantine** user: separate PIN, own sandboxed Play (throwaway or no account), banking and untrusted apps
- [ ] Remove sandboxed Play from Owner once eSIMs are active
- [ ] Optional: Private Space

## Numbers
- [ ] Patient-facing number provisioned (new or **ported from old personal number**)
- [ ] CNAM = practice name
- [ ] Office hours, after-hours auto-reply, voicemail greeting ([templates](../templates/))
- [ ] Team inbox / answering-service routing
- [ ] Test outbound: calls and texts from the patient-line app show the patient-facing number
- [ ] Test inbound call: Personal in foreground, Clinical in background, phone locked, cellular only

## Personal number
- [ ] Signal: number hidden, username set, registration lock ([06](../docs/06-personal-number-opsec.md))
- [ ] WhatsApp/Telegram/Venmo/social privacy settings
- [ ] Remove personal number from NPI/PECOS/board/CAQH listings
- [ ] Start data-broker opt-outs
- [ ] Move SMS 2FA to passkeys/authenticator where possible

## Hardening
- [ ] Everything in [07 – Hardening checklist](../docs/07-hardening-checklist.md)
- [ ] Duress PIN set **after** backups and eSIM recovery info are ready

## Patients
- [ ] Communication policy finalized and in the intake packet ([template](../templates/patient-communication-policy.md))
- [ ] Texting-consent documentation workflow in the EHR
- [ ] Staff trained on the patient line and escalation

## Emergency kit (off-phone)
- [ ] Printed or password-manager copy of [09 – Incident response](../docs/09-incident-response.md)
- [ ] Carrier fraud line, IT help desk, privacy officer contacts
- [ ] Recovery codes for email, password manager, and the patient platform
