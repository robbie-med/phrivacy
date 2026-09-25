# 10 – Password managers & the work-only laptop

The phone is only half the setup. Your credentials and your computer need the same separation between personal and work. This chapter assumes a **personally owned laptop that you use only for work**, not a laptop your employer issued and manages. (If your employer issues and manages the laptop, follow its policies. Most of this still applies to what you do on it.)

## Password managers

### One vault per world, not one vault with folders

| Vault | Holds | Installed in |
|---|---|---|
| **Personal** | Email, family accounts, personal services | Owner (phone), personal computer |
| **Finance** *(optional; can live in Personal)* | Banks, brokerage, payment apps, insurance | Quarantine (phone), personal computer |
| **Work** | EHR, SSO, patient platform, work email, vendor portals, practice admin | Clinical (phone), work-only laptop |

Why separate *accounts* instead of folders in one account:

- A compromised work laptop or Clinical profile can then only expose work credentials.
- If you leave a job, the work vault leaves with it. No untangling.
- Your employer may already provide one (1Password Business, Bitwarden Enterprise, Keeper). **Use theirs for work, and keep your personal vault out of it.** Employer "families" add-ons that link to your personal vault blur the line, so skip them.

### Choosing a manager for GrapheneOS

| Option | Works without Google Play? | Notes |
|---|---|---|
| **Bitwarden** (cloud or self-hosted Vaultwarden) | Yes | Open source, supports multiple accounts in one app, supports passkeys. A good default. |
| **KeePassXC** (desktop) + **KeePassDX** (Android) | Yes | Offline database files. Sync with Syncthing or a file you control. Most private option, but more work. |
| **Proton Pass** | Yes (check the current release) | Pairs well with Proton Mail and alias services. |
| **1Password** | Generally yes | Common as an employer-provided work vault. |
| **Google Password Manager** | No | Tied to Play Services and a Google account. Not for a de-Googled Personal profile. |

### Setup rules

- **Autofill is per profile.** In each profile, set **Settings → Passwords & accounts → Preferred service** to that profile's vault.
- **Passkeys:** store them in the vault for that world (Bitwarden, 1Password, and Proton Pass all support Android passkeys). A **hardware security key** (YubiKey or similar) is the strongest option for work SSO and your email accounts, and it works on both phone (NFC/USB-C) and laptop.
- **TOTP codes:** keep them *outside* the password vault for your most important accounts (email, password manager, bank). Use a separate authenticator app (Aegis in Owner, or your employer's authenticator in Clinical). If all your eggs are in one vault, one breach gets both factors.
- **No PHI in vault notes.** No patient names, MRNs, or "secure note: Mrs. X's gate code."
- **Emergency kit off-device:** master passwords and recovery codes on paper in a safe place, or with a trusted person. Remember: a **duress PIN wipes the phone**. Your vaults must survive that.
- **Master passwords:** a unique, long passphrase for each vault. The work master password must never match any personal one.

## The personally owned, work-only laptop

Treat it as **the desktop extension of your Clinical profile.** Nothing personal ever touches it.

### Baseline

- [ ] **Full-disk encryption:** FileVault (macOS), BitLocker (Windows Pro), or LUKS (Linux). Store the recovery key in the **work** vault, plus a paper copy. Encryption is what can keep a lost laptop from being a reportable breach.
- [ ] **Strong login** plus biometrics or a security key, with **auto-lock ≤ 5 minutes** and lock on lid close.
- [ ] **Automatic OS, browser, and firmware updates.**
- [ ] **One user account, work only.** No family logins, no personal Apple ID or Microsoft account if you can avoid it. If the OS requires an account, create a work-only one.
- [ ] **Firewall on; disable file sharing, AirDrop "Everyone," and remote login.**
- [ ] **No personal apps:** no personal Signal/WhatsApp desktop, personal email, personal cloud drives, or games.
- [ ] **Label it** (asset tag or practice sticker, no personal name). Keep an inventory entry: serial number, encryption status, and date of the last check.

### Employer access requirements

Many health systems block personally owned computers from EHR and email unless the device meets **Conditional Access** or BYOD rules.

- **Best case: web and VDI only.** Epic Hyperspace through Citrix or a similar VDI, and Outlook/Teams in the browser. PHI stays on the employer's servers, not your disk.
- **Browser-based app protection** (e.g., Microsoft Edge with Intune app protection) is a reasonable middle ground. It manages the *browser*, not the machine.
- **Full MDM enrollment of a personal laptop:** acceptable on a work-only machine, since nothing personal is on it. Understand that the employer can then wipe it. Never enroll a laptop that also holds personal data.
- **Independent / DPC practice:** *you* are the covered entity. This laptop belongs in your HIPAA risk analysis and device inventory. Document encryption, updates, and who has access.

### Phone ↔ laptop syncing: what's allowed

| Thing | Sync? | How |
|---|---|---|
| **Work password vault** | ✅ | Same work vault account on Clinical and the laptop |
| **Patient-line platform** | ✅ | The platform's desktop or web app. Outbound calls and texts still go out from the patient-facing number, and threads stay in one place. |
| **Work email, calendar, chat** | ✅ | Through the employer's cloud (M365/Workspace) |
| **Files with PHI** | ⚠️ Only through BAA-covered storage | The employer's OneDrive/SharePoint/Drive under a BAA, or the EHR. **Never** personal Dropbox, iCloud, Google Drive, or USB sticks. |
| **Clinical photos** | ❌ | Photos go phone → EHR secure capture → chart. Never phone → laptop. |
| **Personal password vault** | ❌ | Not on the work laptop |
| **Signal / personal messengers** | ❌ | Linked devices see your whole personal message history. Don't link them to the work laptop. |
| **"Phone Link" / KDE Connect / notification mirroring** | ❌ (or Clinical-only) | These mirror notifications, SMS, and clipboard. At most, pair them with the **Clinical** profile, never Owner. |
| **Clipboard sync / universal clipboard** | ❌ | It leaks across worlds silently. |
| **Browser sync** | Work account only | A dedicated work browser profile signed in to the work identity. No personal extensions, bookmarks, or history. |

### Backups

- Prefer **nothing to back up.** Work data lives in the EHR and the employer's or practice's cloud.
- If you must keep local files (practice admin, contracts), back them up to **BAA-covered** storage or an **encrypted** external drive kept at the practice, never to a personal cloud.
- Keep a written **rebuild list** (apps, settings, VPN/VDI configs) so a wiped laptop is a two-hour job, not a crisis.

### When the laptop is lost or stolen

Follow [09 – Lost or stolen phone](09-incident-response.md#lost-or-stolen-phone), with these changes:

1. Tell IT or your privacy officer immediately. **Know whether it was encrypted and locked.** That fact drives the breach analysis.
2. Revoke the laptop's sessions: work vault ("deauthorize sessions"), M365/Google, the patient platform, VDI.
3. Remote-wipe it through MDM if it was enrolled.
4. Change the work vault master password if there's any chance the laptop was unlocked.

## Your personal computer (the mirror image)

- **No work accounts, EHR bookmarks, work vault, or patient-platform logins.**
- If you absolutely must check something work-related from home on a personal machine, use a **separate OS user** or at least a separate browser profile, and never download attachments.
