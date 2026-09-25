# 09 – Incident response

Keep this chapter somewhere you can reach **without your phone**: printed, or in your password manager's notes.

## Lost or stolen phone

1. **Don't panic about GrapheneOS itself.** If the phone was locked, the profiles are encrypted. If it was powered off or has auto-rebooted, all data is at rest.
2. **Call your carrier** (from another phone) and suspend the lines. This stops SMS 2FA interception. Ask them to confirm your port-out lock is still in place.
3. **Report to work IT / privacy officer right away.** The device had PHI access. They'll wipe the work profile via MDM, revoke sessions, and decide whether breach analysis applies. Encrypted and locked devices are often *not* reportable breaches under HIPAA's encryption safe harbor, but that's **their** call, not yours.
4. **Revoke sessions:** EHR, email (Microsoft/Google "sign out everywhere"), the patient platform, Signal (unlink devices), and the password manager.
5. **Patient platform:** most can log out devices remotely. Do it.
6. **Replacement:** new Pixel, reinstall GrapheneOS, restore Personal from backup, rebuild Clinical from scratch.

> GrapheneOS has no "Find My Device" by design. If you want remote wipe of the whole device, the only built-in mechanisms are MDM (work profile only) and the duress PIN. Accept that tradeoff, or run a trusted remote-wipe app in Owner.

## Lost or stolen work laptop

See [10 – When the laptop is lost or stolen](10-passwords-and-laptop.md#when-the-laptop-is-lost-or-stolen).

## Patient found personal number or accounts

1. **Don't engage from the personal account.** Reply, if at all, from the patient line: "Please use this number for all communication with me. [policy]."
2. **Block** the patient on the personal channel.
3. **Find the leak:** messenger discovery? Venmo? Facebook "People you may know"? A family member? Fix it (see [06](06-personal-number-opsec.md)).
4. **Document** the event in a non-clinical note to practice management, per your practice's policy.
5. If it happens more than once, or with multiple patients, **change your personal number** (see [06 – Migration](06-personal-number-opsec.md#migrating-to-a-new-personal-number)).

## Harassment, threats, or stalking

1. **Safety first.** Immediate threat → 911.
2. **Preserve evidence.** Export the conversation from the patient platform. Take screenshots with timestamps, *in the Clinical profile*, and don't save them to Personal.
3. **Notify** practice management, risk management/legal, and security (if you're in a health system). Consider your malpractice carrier's risk hotline.
4. **Stop direct communication.** Route the patient through the front desk or another clinician.
5. Consider **discharge** from the practice through the formal process, a protective order, and your state's address confidentiality program.
6. **Harden personal exposure:** data-broker opt-outs, lock down social media, alert family, and consider a new personal number.

## SIM swap / port-out suspected

Signs: the phone suddenly shows "No service" or "SOS only," you get carrier emails about a SIM change or port, or 2FA codes arrive that you didn't request.

1. Call the carrier **from another phone** right away. Report fraud and reclaim the number.
2. From a trusted computer, change passwords for email first, then banks.
3. Check email for forwarding rules, recovery-address changes, and new devices.
4. Move remaining SMS-based 2FA to passkeys or an authenticator.
5. Report to the FTC at IdentityTheft.gov if accounts were compromised.

## Suspected malware / compromised app

1. Note which profile the app is in. That's your blast radius.
2. Uninstall the app. Revoke any accounts it touched.
3. If it's in Quarantine: delete and recreate the profile.
4. If it's in Clinical: tell IT, then delete and recreate the profile.
5. If it's in Owner and you're seriously worried: back up the essentials, factory reset, and reinstall GrapheneOS with the web installer. Use **Auditor** to confirm the OS is intact.

## PHI accidentally ended up in Personal

(For example, a patient texted your personal number a photo, or you took a clinical photo with the personal camera.)

1. Move the clinically relevant content into the chart through proper channels (e.g., re-request the photo through the patient platform, or use EHR secure capture).
2. **Delete it from Personal**, including the trash, any cloud backup copy, and Google Photos/Messages backups.
3. Tell your privacy officer if your organization requires it. Many do, even for small incidents.
4. Reply to the patient from the patient line with the policy. See the [templates](../templates/auto-replies.md).
