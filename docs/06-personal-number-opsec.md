# 06 – Personal number OPSEC

Your personal number is an identifier that data brokers, messengers, and payment apps use to link you everywhere. Once a patient has it, they can often find your spouse, your kids' names, and your home address. Protect it.

## How a phone number leaks your life

| Leak path | What happens | Fix |
|---|---|---|
| **Messenger contact discovery** (WhatsApp, Signal, Telegram, iMessage/RCS) | Anyone who saves your number sees your profile photo, name, "about," and online status. | Set privacy to contacts-only or nobody. Use Signal usernames and hide your number. Don't use a family photo as your avatar. |
| **Payment apps** (Venmo, Cash App, Zelle) | Venmo's default public feed and "find friends" link your number to your transactions and friends list. | Set Venmo transactions and friends list to private. Turn off "find me by phone." |
| **Social apps** (Facebook, Instagram, LinkedIn, TikTok) | "People you may know" is driven by contact uploads, *including patients uploading your number.* | Remove your phone number from these accounts, or set "who can look you up by phone" to "only me." |
| **Caller-ID apps** (Truecaller, Hiya, etc.) | Crowdsourced from millions of address books. Your number may already be labeled with your name. | Request unlisting from each service. |
| **Data brokers / people-search sites** | Number → name → address → relatives. | Opt out (below). |
| **Retail / loyalty / 2FA** | Every "enter your phone number" at checkout feeds brokers. | Use a separate commerce number (below). |

## A separate commerce number (optional but powerful)

Use a **third, low-stakes number** for stores, restaurants, loyalty programs, deliveries, and web signups. It can be a cheap VoIP number or a MySudo-style app. Put those apps in the **Quarantine** profile. Your real personal number then goes only to family, close friends, and the most critical accounts.

## Messenger settings checklist

**Signal**
- Settings → Privacy → Phone number → *Who can see my number:* **Nobody**; *Who can find me by number:* **Nobody** (then share a username instead).
- Set a username; share that instead of your number.
- Enable **Registration Lock**.

**WhatsApp** (if you must)
- Privacy → Last seen, Profile photo, About → **My contacts**.
- Two-step verification PIN on.
- Never give the WhatsApp number to patients. It is your personal number.

**Telegram**
- Privacy → Phone number → *Who can see:* **Nobody**; *Who can find me by number:* **My contacts**.

**Google Messages (RCS)**
- RCS reveals read receipts and typing indicators, and depends on Google. Fine for personal use. Don't use it for patients.

## Carrier account security (SIM-swap / port-out protection)

Do this **for every carrier line**, today:

- Set an **account PIN / passcode** and a **number transfer PIN** that aren't guessable (not your birthday or NPI).
- Turn on the carrier's **port-out lock / number lock / SIM protection** feature. Most major US carriers have one; the name varies.
- Use a unique email address and a strong password for the carrier account.
- Remove your personal number as a 2FA method from important accounts (email, bank, Apple/Google, EHR) wherever passkeys or an authenticator are available.

## Data broker opt-outs

- Search your name, number, and address on the major people-search sites. Opt out of each one (it's tedious; paid services automate it).
- Many states now have broker-deletion mechanisms (e.g., California's DELETE Act "DROP" platform). Use them if you live in one.
- **Physician-specific:** your **NPI registry** entry is public and includes a practice address and phone number. Make sure both are the **practice's**, never your home or cell. The same goes for state medical board lookups, DEA registration, Medicare enrollment (PECOS), and CAQH. Many boards let you designate a public address separate from a confidential one.
- Home address: consider a PO box or a registered agent for your practice LLC, and check whether your state has an address-confidentiality program for medical professionals.

## Migrating to a new personal number

If patients have your old personal number, see [03 – If patients already have your personal number](03-numbers-and-telephony.md#if-patients-already-have-your-personal-number). Then:

1. Add the new personal eSIM (see [01](01-device-and-install.md#esim-activation-on-grapheneos)).
2. Update in this order: **email accounts → password manager → banks → government (IRS, SSA, DMV) → insurance → utilities → messengers → everything else.**
3. Re-register Signal/WhatsApp on the new number (Signal: Settings → Account → Change phone number).
4. Tell family and friends through a channel that doesn't expose the new number to patients.
5. Port the old number into the patient platform.
6. After 30–60 days, search the old number on people-search sites and messengers to confirm it no longer resolves to your personal identity.

## Email hygiene (same idea, different identifier)

- Patients should have a **practice** email or portal only.
- Use email aliases (SimpleLogin, Firefox Relay, iCloud Hide My Email, Fastmail masked email) for signups, so your personal address isn't the join key across data brokers either.
