# 08 – Daily operations

A setup you can't live with is a setup you'll abandon. Here's how to make it routine.

## A typical day

| Time | What you do |
|---|---|
| **Morning** | Unlock Owner. Switch to Clinical once and unlock it, so its apps start and the patient line can ring. Switch back to Personal. |
| **Clinic hours** | Stay in Clinical if you're charting or messaging heavily, or stay in Personal and rely on forwarded notifications. Tap a forwarded notification to jump into Clinical. |
| **Calling or texting a patient** | In Clinical, from the patient-line app, so it goes out from the patient-facing number. Never the stock dialer or SMS app. |
| **Evening (not on call)** | Switch Modes to "Off duty." The auto-reply covers the patient line. Optionally **End session** on Clinical for a hard stop. |
| **On-call nights** | Keep Clinical running. Use the "On call" mode so only the on-call or patient-line app rings through. |
| **Weekend / vacation** | End session on Clinical. Set vacation auto-replies and coverage on the patient platform. |

## Profile switching tips

- Quick Settings → **user icon** switches profiles. Add the tile if it's missing.
- **End session** (from the user switcher) stops a secondary profile and puts its data back at rest. It's the strongest boundary you have. Note: an ended profile won't receive calls or push notifications.
- A running secondary profile stays **After First Unlock (AFU)** until ended or until the device reboots. That's convenient, but less protected if the phone is seized.

## Notifications

- Forwarded Clinical notifications show a work/profile indicator. Confirm lock screen content is hidden.
- In the Clinical profile, set per-app channels. Patient calls: high priority. Patient messages: default. Marketing and admin: silent.

## Photos & files

- **Clinical:** capture clinical photos only through the EHR's secure capture. If you have to use the system camera in Clinical, upload to the chart and delete immediately (including from "trash").
- **Personal:** a personal photo backup service is fine because Personal never holds PHI.
- Don't use a single cloud storage account across both profiles.

## Backups

Backups are per profile. Plan them separately.

| Profile | What to back up | How |
|---|---|---|
| **Owner / Personal** | Photos, Signal, contacts, 2FA seeds, app data | App-native backups (Signal's backup, photo sync, contacts sync); **Seedvault** (built into GrapheneOS) to an encrypted USB drive or Nextcloud; your password manager's export for 2FA |
| **Clinical** | Usually *nothing local*. Data lives in the EHR, BAA platform, and work cloud. | Rely on vendor/employer systems. **Don't copy PHI into personal backups.** Keep a list of apps and settings so you can rebuild quickly. |

Test a restore at least once.

## Charging, travel, and borders

- Carry a known cable. The USB-C port setting protects you against "juice jacking" while the phone is locked.
- **Before crossing a border or going into a high-risk situation:** power the phone off (BFU is the strongest state). Consider ending the Clinical session or temporarily removing it if you may be compelled to unlock. You can rebuild it from employer and vendor systems.
- In the US, check your employer's policy on bringing devices with PHI access abroad.

## Leaving a job

1. Tell the patient platform and the practice. Decide who keeps the patient-facing number. If you plan to take it with you, get this in your contract up front.
2. Unenroll MDM and remove work accounts.
3. **Delete the Clinical profile entirely** (Settings → System → Multiple users → Clinical → Delete). This destroys its encryption keys.
4. Create a fresh Clinical profile for the next role.
