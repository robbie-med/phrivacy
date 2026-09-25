# 05 – Work apps, EHR, and MDM

## Sandboxed Google Play in the Clinical profile

Most work apps need Google Play Services for push notifications, maps, and SafetyNet/Play Integrity checks.

1. Switch to Clinical.
2. Open the GrapheneOS **App Store** and install **Google Play services**, **Google Play Store**, and **Google Services Framework** (sandboxed Google Play).
3. Sign in with your **work** Google account, or a new account used only for this profile. Some app downloads don't need a signed-in account; you can use the Play Store with a throwaway account or install through the MDM's managed Play.
4. **Settings → Apps → Sandboxed Google Play** exposes options like rerouting location requests to the OS. Turn it on unless an app needs Google's location.

## Play Integrity: the main compatibility risk

Some apps check **Play Integrity** and refuse to run on anything that isn't a Google-certified stock OS. GrapheneOS passes *basic* integrity but not *device* or *strong* integrity, by design.

- **Most apps work.** Outlook, Teams, Microsoft Authenticator, Duo, Okta Verify, Slack, Zoom, Doximity, and most VoIP apps generally run fine on GrapheneOS with sandboxed Play.
- **Some banking apps and a few enterprise apps** strictly require device integrity. (Banking apps belong in the Quarantine profile, not Clinical or Personal. See [02](02-profile-architecture.md#secondary-user--quarantine).) GrapheneOS maintains a community list of apps that work or break. Search the GrapheneOS forum for the app name before you commit.
- GrapheneOS has asked app developers to use the **hardware attestation API** to allow GrapheneOS explicitly. You can ask your vendor or IT department to do this.

### EHR mobile apps

| App family | Typical notes |
|---|---|
| **Epic** (Haiku, Canto, Rover, Limerick/Secure Chat) | Usually delivered through your organization's MDM or managed Play. Behavior depends on org configuration and the MDM's device checks. |
| **Oracle Health / Cerner** (PowerChart Touch, CareAware) | Same: org-controlled. |
| **athenahealth, eClinicalWorks, NextGen, Elation, Healthie, Akute, Atlas.md, Hint** (common in DPC/independent practice) | Often a plain Play Store install with no MDM. Usually the easiest to run on GrapheneOS. |

**Field reports welcome.** Open a PR or issue saying which app, which MDM, and whether it worked. Don't include your organization's name.

## MDM (Intune, Workspace ONE, etc.)

- **Enroll MDM only in the Clinical profile.** Ideally enroll as an Android Enterprise *work profile* inside the Clinical user. See [02](02-profile-architecture.md#alternative-employer-mandated-work-profile).
- Intune's "personally owned work profile" enrollment uses the Company Portal app and needs sandboxed Play in that profile.
- Compliance policies that require "**Play Integrity: device integrity**" or "**strong integrity**" will mark GrapheneOS non-compliant. Talk to IT:
  - Many orgs only enforce basic integrity + MAM (app protection policies) for BYOD. That works.
  - Ask whether a **hardware attestation** allowance or an exception is possible.
  - If not, ask for **a work-issued phone.** That's their cost, not your privacy.
- **Never accept device-owner (fully managed) enrollment on a personal phone.**
- Understand what a work-profile MDM *can* see: apps, policies, and data inside the work profile, plus some device info (model, OS version, serial number or IMEI depending on enrollment type). It can wipe the **work profile**. It can't read your personal profile's data.

## Authentication

- Put work MFA (Microsoft Authenticator, Duo, Okta Verify) in the Clinical profile.
- **Prefer passkeys or FIDO2 security keys** (a YubiKey on your keyring works over NFC or USB-C) over SMS codes. SMS codes to your personal number tie your personal number to work systems. Avoid that.
- If a work system *requires* SMS 2FA, point it at a work number (VoIP or work eSIM), not your personal line.

## Work email & calendar

- Outlook/Gmail for work lives only in Clinical.
- Turn off **"sync contacts to device"** in the work email app if you don't need it. The corporate directory is enough, and it avoids dumping thousands of contacts into the profile.
- Calendar: if you want to see work events from Personal, share only **free/busy** to a personal calendar, not event details (which can contain PHI).

## Dictation & AI scribes

- Ambient AI scribe apps (Abridge, Nuance DAX, Suki, Freed, etc.) record patient encounters. Install **only in Clinical**, only with a BAA, and only as your organization permits.
- Grant the **microphone** only while in use. GrapheneOS shows mic/camera indicators. Watch for them.
- Don't use general consumer AI assistants or voice typing that sends audio to non-BAA clouds for clinical content.
