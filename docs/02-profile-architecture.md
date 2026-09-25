# 02 – Profile architecture

GrapheneOS offers three ways to compartmentalize apps. Pick the one that fits each world.

| Mechanism | Isolation | Convenience | Can be fully stopped? | Good for |
|---|---|---|---|---|
| **Secondary user profile** | Strongest. Separate encryption keys, apps, accounts, contacts, files. | Must switch profiles to *use* apps (notifications can be forwarded). | Yes, with "End session" | **Clinical/work**, Quarantine |
| **Work profile** (managed profile, via employer MDM or Shelter) | Separate apps and data, but runs *inside* Owner and shares its lock screen session | Apps appear side-by-side with personal apps, with a badge | Pausable ("work apps off") | Employers that *require* an Android Enterprise work profile |
| **Private Space** | Separate profile nested in Owner, with its own lock | Hidden drawer section | Locking it stops it | Sensitive *personal* apps |

## Recommended layout

### Owner profile → "Personal"

- The Owner profile starts first after boot and manages the eSIMs and device-wide settings. Treat it as your personal life.
- Personal eSIM, the default dialer and SMS app for the personal line.
- Personal messengers (Signal, etc.), family apps, banking, personal email.
- **No work apps. No PHI. No patient contacts.**
- Sandboxed Google Play is optional here. Use it only if personal apps need it.

### Secondary user → "Clinical"

Create it under **Settings → System → Multiple users → Add user**. Name it something neutral like "Work" or "Clinic."

- Its **own** sandboxed Google Play and **work** Google/Microsoft account.
- The patient-line app (Spruce or similar), a caller-ID-masking dialer (e.g., Doximity), EHR mobile apps, work email, Teams/Slack/secure chat, the MFA authenticator for work SSO.
- MDM / Company Portal if your employer requires it. See [05](05-work-apps-and-mdm.md).
- Only work and colleague contacts. **Patient contact data stays in the EHR and the BAA platform, not in the Android contacts app.**

Settings for the Clinical user (from Owner: **Settings → System → Multiple users → Clinical**):

| Setting | Value | Why |
|---|---|---|
| **Send notifications to current user** | ON | See patient-line and on-call notifications while you're in Personal. Content display is controlled per app and profile. |
| **Allow phone calls & SMS** | Usually OFF | The patient line runs over VoIP, so carrier telephony isn't needed here. Turn it on only if you also use a *carrier* work eSIM from this profile (see [03](03-numbers-and-telephony.md#carrier-telephony-is-device-wide)). |
| **Install available apps** | Use as needed | Installs an app already present in Owner without re-downloading it. Remember that Play accounts are per-profile. |

### Optional: "Quarantine" secondary user

For apps that demand your phone number, contacts, or constant location, or that you simply don't trust: rideshare, retail, parking, social media, loyalty apps.

- No sandboxed Play unless an app requires it.
- Give it nothing: Contact Scopes with zero contacts, Storage Scopes with no files, Network off for apps that don't need it.
- End the session when you're done.

### Optional: Private Space (inside Owner)

For sensitive personal apps you want hidden and locked even while Owner is unlocked: health, dating, finances, journaling.

## Alternative: employer-mandated work profile

Some health systems' MDM (Intune, Workspace ONE, etc.) will only enroll a personally owned device as an **Android Enterprise work profile**. On GrapheneOS you can still do this, and the best place to do it is **inside the Clinical secondary user**, not inside Owner:

```
Owner (Personal)
Clinical user
  └── Work profile (employer MDM)  ← MDM sees only this
```

That way the employer's MDM never sees your Owner profile or anything personal. The patient-line app can live in the Clinical user outside the MDM-managed work profile, or inside it if your employer supplies the patient line.

If your employer insists on managing the *whole device* (fully managed / device owner mode), **decline and ask for a work-issued phone.** Don't let an employer become device owner of your personal phone.

## Profile hygiene rules

1. **One identity per profile.** Never sign a work account into Personal or a personal account into Clinical.
2. **No cross-profile sharing of files containing PHI.** If you share from Clinical to Personal, you've just moved PHI.
3. **Clipboard doesn't cross profiles.** Don't work around that by emailing things to yourself.
4. **Keyboards are per profile.** Turn off cloud-sync and learning features in Clinical, or use a keyboard with no network access (GrapheneOS's default AOSP keyboard doesn't have network access).
5. **Camera:** in Clinical, only take clinical photos through the EHR app's secure capture (Haiku/Rover media capture, etc.), never the system camera. In Personal, never photograph patients, rashes, or charts.
