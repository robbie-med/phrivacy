# 03 – Numbers & telephony

This chapter matters most. **The phone number you give patients decides almost everything else.**

## The numbers model

| Number | Type | Given to | Lives in |
|---|---|---|---|
| **Personal** | Carrier eSIM #1 | Family, friends, banks (ideally not even banks, see [06](06-personal-number-opsec.md)) | Owner |
| **Patient-facing** | VoIP number on a BAA-covered platform | Patients and caregivers | Clinical |
| **Work/colleague** *(optional)* | Health-system extension, secure chat, or carrier eSIM #2 | Colleagues, nurses, admin, pharmacies | Clinical (or Owner if it's a carrier eSIM) |
| **Outbound caller ID** | Masked to the clinic's main number | What patients see when you call them | Clinical |

A minimal setup is **two numbers**: personal (carrier) plus patient-facing (VoIP). Add the third if you want colleagues to reach you without going through the patient channel.

## Why the patient number should NOT be a SIM

A carrier SIM line:

- Is tied to your legal identity through carrier records, CNAM, and data brokers.
- Carries SMS, which is unencrypted, has no BAA, and leaves PHI in the device's shared SMS database.
- Can't easily be routed to a covering colleague, an answering service, or an after-hours auto-reply.
- Is a SIM-swap target.
- Rings through at 2 a.m. unless you fight it with DND.

A VoIP number on a clinician-oriented platform:

- Can be covered by a **Business Associate Agreement**.
- Has office hours, auto-replies, and routing to a team or answering service.
- Keeps messages in an auditable, exportable system you can document into the chart.
- Can be **ported out and handed to your practice** if you leave, or retired without changing your personal number.
- Shows the practice name as caller ID.

## Platform options (verify BAAs, features, and pricing yourself)

| Option | Inbound patient number | Outbound masking | BAA | Notes |
|---|---|---|---|---|
| **Spruce Health** | Yes (new or ported) | Yes | Yes (clinician-focused) | Calls, secure messaging, SMS bridge, fax, team inboxes, after-hours routing. Popular with DPC and small practices. |
| **Doximity Dialer** | No | Yes, shows clinic/hospital number | Covered under Doximity's terms for US clinicians (verify) | Free for verified US clinicians. Outbound-only, which is a *feature*: patients can't call back to you. |
| **Google Workspace + Google Voice** | Yes | Yes | Yes, under a Workspace BAA (paid Workspace only) | **Consumer Google Voice has no BAA. Don't use it for PHI.** |
| **Business VoIP** (e.g., Quo/OpenPhone, RingCentral, Zoom Phone, Dialpad) | Yes | Yes | Varies by plan | Several offer HIPAA plans with a BAA. Confirm the plan tier and whether SMS is covered. |
| **Health-system tools** (Epic Secure Chat, TigerConnect, Vocera, Teams Phone) | Sometimes | Sometimes | Employer's | Use these if your employer provides them. They're already in the compliance program. |
| **Patient portal messaging** (MyChart, etc.) | n/a | n/a | Employer's | The default channel for non-urgent patient messages. Push patients here where possible. |

> **SMS is the weak link.** Many VoIP platforms can send and receive regular SMS with patients. Even under a BAA, SMS in transit is unencrypted. Get patient consent to text (see [template policy](../templates/patient-communication-policy.md)), keep PHI minimal, and prefer the platform's secure message link for anything sensitive.

## If patients *already* have your personal number

This is common, and fixable:

1. Sign up for a patient platform that supports **number porting** (port-in).
2. Get a **new personal number** first, as a new eSIM on your carrier or an MVNO.
3. Move family, friends, banks, and 2FA to the new personal number. See the [migration checklist](06-personal-number-opsec.md#migrating-to-a-new-personal-number).
4. **Port the old number into the patient platform.** Patients keep calling the number they know, but it now lands in a HIPAA-oriented system with office hours and routing.
5. Scrub the old number from personal accounts: messengers, Venmo, Amazon, etc. Otherwise patients who search it can still find the personal account.

## Outbound calls to patients

- **Default:** use the masking dialer (Doximity, Spruce, or your VoIP app) so patients see the **clinic's number**.
- **Emergency fallback from a carrier line:** dial `*67` before the number to block caller ID (US). It doesn't hide you from 911, toll-free numbers, or some carrier systems. It also means patients see "No Caller ID," and many won't answer.
- Never call a patient from your personal line without masking. It sits in their call log forever and syncs to their contact-discovery apps.

## Carrier telephony is device-wide

Things to know about SIM/eSIM behavior on Android/GrapheneOS:

- eSIMs belong to the **device**, managed from Owner. You can't assign "eSIM 2 → Clinical profile only."
- Any profile with **"Allow phone calls & SMS"** enabled can use the carrier lines. Treat call and SMS history on carrier lines as visible to the Owner profile.
- Therefore: **keep carrier lines personal**, and keep patient communication in VoIP apps inside Clinical. If you do carry a carrier work eSIM (e.g., employer-paid), use it for colleague calls, not patient PHI.
- **Dual eSIM:** Pixels support two active eSIMs (dual standby). Set the **default for calls/SMS/data** to the personal line so you never accidentally originate from the work line, or the reverse.

## Voice quality and reliability

- VoIP apps need data. Enable **Wi-Fi Calling** on the personal carrier line, and make sure the patient app works well on both cellular data and clinic Wi-Fi.
- VoIP apps in a secondary profile need that profile **running** (not ended) to ring. See [08](08-daily-operations.md) for how to balance this with "End session."
- Sandboxed Google Play in the Clinical profile provides FCM push, which most VoIP apps need to ring reliably. Exempt the patient-line app from battery optimization.
- **Test it:** have a colleague call the patient line while you're in Personal, while Clinical is in the background, while the phone is locked, and on cellular with Wi-Fi off.

## CNAM (caller ID name)

- Set the patient-facing number's CNAM to the **practice name**, not your personal name. Most business VoIP providers let you do this.
- Check what CNAM your **personal** line shows (call a friend with a carrier that displays names). Some carriers let you change or suppress it.
