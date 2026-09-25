# 07 – Hardening checklist

Menu paths are approximate and move between GrapheneOS releases. Use the Settings search if a path doesn't match.

## Lock screen & unlock (each profile)

- [ ] **Owner PIN/passphrase:** at least 6 digits. A passphrase is better. The Titan M2 secure element throttles guessing, so a random 6+ digit PIN is strong **as long as it's random**.
- [ ] **Clinical profile PIN:** *different* from Owner. This matters because Clinical holds PHI.
- [ ] **Scramble PIN input layout:** ON (defeats smudge and shoulder-surfing attacks).
- [ ] **Fingerprint:** optional. If available, consider **2-factor fingerprint unlock** (fingerprint + PIN).
- [ ] **Duress PIN/password:** set one (**Security & privacy → Device unlock → Duress password**). Entering it **wipes the device, including eSIMs**, irreversibly. Make sure your backups are current and you have your carrier's eSIM re-download process documented.
- [ ] **Lock screen notifications:** hide sensitive content. For Clinical-forwarded notifications, show "content hidden" at minimum.
- [ ] **Screen timeout** ≤ 1 minute. Set the lock to trigger immediately after timeout.

## Exploit protection

**Security & privacy → Exploit protection**

- [ ] **Auto reboot:** keep it enabled. The default is 18 hours of being locked; shorten to 8–12 h if you like. A reboot puts every profile back into Before-First-Unlock (BFU), where data is at rest and encrypted.
- [ ] **USB-C port:** "Charging-only when locked" or stricter. Data connections are refused while locked.
- [ ] **Memory tagging (MTE):** Enabled for the base OS by default on supported Pixels. Consider enabling it for **user-installed apps** too. Turn it off per app only if an app crashes.
- [ ] **Secure app spawning:** ON (default).
- [ ] **Wi-Fi / Bluetooth auto-turn-off timers:** set these (e.g., 10 minutes after disconnection).

## Network

- [ ] **Allow 2G:** OFF (**Network & internet → SIMs → [line]**). Defeats 2G downgrade and IMSI-catcher attacks.
- [ ] **Wi-Fi MAC randomization:** per network. GrapheneOS defaults to per-connection randomization. Leave it.
- [ ] **Private DNS:** optionally set a filtering DNS provider (e.g., Quad9 or a NextDNS profile).
- [ ] **VPN:** optional. If your employer requires a VPN, run it **only in Clinical**. VPNs are per profile.
- [ ] **Clinic guest Wi-Fi:** fine for VoIP, but assume it's hostile. All work apps should use TLS, and they do.

## Per-app permissions (GrapheneOS-specific)

| Permission | Use it for |
|---|---|
| **Network** | Revoke for apps that don't need the internet (calculator, offline notes, keyboard, gallery). |
| **Sensors** | Revoke by default. Grant to fitness or compass apps only. |
| **Contact Scopes** | Give an app only the specific contacts it needs, or none, instead of the whole address book. Great for messengers in Personal. |
| **Storage Scopes** | Give an app specific files or folders instead of all media. |
| **Location** | "While in use" + "approximate" unless precise location is needed. |
| **Microphone / Camera** | "Only this time" for most apps. Watch the privacy indicators. |

## Apps

- [ ] Install from the **GrapheneOS App Store** (GrapheneOS apps, sandboxed Play), **Play Store** (in profiles with sandboxed Play), or **Accrescent** / F-Droid-style sources for FOSS as you prefer. Avoid random APKs.
- [ ] **Vanadium** (GrapheneOS's hardened Chromium) as the default browser.
- [ ] Remove apps you no longer use, quarterly (see the [quarterly review](../checklists/quarterly-review.md)).

## Profiles

- [ ] Clinical: **Send notifications to current user** ON; **phone calls & SMS** OFF unless needed.
- [ ] Quarantine: no sandboxed Play unless required; **End session** after each use.
- [ ] Guest profile: disabled (**System → Multiple users → Allow guest** off). If you hand the phone to someone, use a dedicated low-privilege profile.
- [ ] **Allow multiple users from lock screen:** consider OFF so switching requires unlocking Owner first.

## Attestation

- [ ] **Auditor** app paired with a second device, with scheduled attestation. See [01](01-device-and-install.md#verify-the-install).
