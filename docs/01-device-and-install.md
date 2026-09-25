# 01 – Device selection & GrapheneOS install

## Why GrapheneOS on a Pixel

- **Real user-profile isolation.** Each profile has its own encryption keys and can be fully shut down. GrapheneOS extends stock Android's profile features (notification forwarding, higher profile limits, app install across profiles).
- **Sandboxed Google Play.** Google Play Services runs as a regular, unprivileged app, *per profile*. Your EHR can have Play in the Clinical profile while your personal profile has none, or its own separate instance.
- **Per-app privacy controls** stock Android doesn't have: Network permission, Sensors permission, Contact Scopes, Storage Scopes.
- **Hardening:** hardened memory allocator, memory tagging (MTE) on supported Pixels, auto-reboot, USB-C port control, duress PIN, and more.
- **Pixel hardware** provides verified boot with a user-installed OS, a secure element (Titan M2), and timely firmware updates, which is why GrapheneOS supports only Pixels.

## Choosing the device

- **Pixel 10 series or newer** (10, 10 Pro, 10 Pro XL, 10 Pro Fold, and successors).
- **Before buying, confirm the exact model is on the [official supported devices list](https://grapheneos.org/faq#supported-devices).** Support for a new Pixel generation can lag Google's launch.
- **Buy unlocked, directly from Google or a reputable retailer.** Carrier-branded Pixels (especially Verizon) often have OEM unlocking permanently disabled, and then you can't install GrapheneOS at all.
- **eSIM-only in the US:** US-market Pixel 10 models have no physical SIM tray. That's fine for this setup (two eSIMs can be active at once), but it affects the install steps. See [eSIM activation](#esim-activation-on-grapheneos) below.
- **Storage:** get at least 256 GB. Each profile keeps its own copy of apps and data, and a Clinical profile with an EHR, Teams, Outlook, and sandboxed Play adds up.

## Installation

Use the **official web installer**: <https://grapheneos.org/install/web>. Follow it exactly. Don't use third-party "pre-installed GrapheneOS" phones or unofficial builds.

High-level steps (the official guide is authoritative):

1. Update the stock OS once, then enable **Developer options → OEM unlocking**. This needs an internet connection at least once on stock.
2. Boot to the bootloader, connect to a computer with a Chromium-based browser, and unlock the bootloader.
3. Flash the factory images with the web installer.
4. **Relock the bootloader.** This is not optional. An unlocked bootloader defeats verified boot.
5. On first boot, **disable OEM unlocking** again in Developer options, then turn Developer options off.

### Verify the install

- The boot screen shows a yellow "your device is loading a different operating system" notice with a verified-boot key hash. Compare that hash against the one published in the install guide.
- Better: install the **Auditor** app (from the GrapheneOS App Store) and pair it with a second device for hardware-based attestation. Attestation can be scheduled to run periodically.

## eSIM activation on GrapheneOS

Downloading or transferring an eSIM needs Google's privileged eSIM management component, which GrapheneOS keeps disabled by default.

1. In the **Owner** profile, install **sandboxed Google Play** from the GrapheneOS **App Store** app.
2. Go to **Settings → Network & internet → eSIM** (menu names vary by release) and enable **"Allow Privileged eSIM Management."**
3. Add the eSIM through the carrier's QR code, activation code, or transfer flow.
4. Once your eSIMs are installed and working, you can turn the privileged eSIM toggle back off. Installed eSIMs keep working. You'll need it again to add, transfer, or delete an eSIM.

> **Keep Personal de-Googled:** you don't need to sign in to Play to activate an eSIM. Once the eSIMs work, uninstall sandboxed Play from Owner. Google then lives only in the Clinical and Quarantine profiles. Reinstall it temporarily whenever you need to add or transfer an eSIM.

## First-boot decisions

| Decision | Recommendation |
|---|---|
| Owner profile PIN/password | 6+ digit PIN minimum. A passphrase is better. See [07](07-hardening-checklist.md). |
| Fingerprint | Fine for convenience. Consider 2-factor fingerprint unlock (fingerprint + PIN) if your release has it. |
| Google in Owner | None. Banking and other Play-dependent personal apps go in the Quarantine profile ([02](02-profile-architecture.md#secondary-user--quarantine)). |
| Backups | Plan per profile. See [08](08-daily-operations.md#backups). |

## Updates

GrapheneOS updates arrive over the air and install in the background. **Reboot promptly when prompted.** Also update apps in each profile. Apps in a stopped profile don't update until that profile runs.
