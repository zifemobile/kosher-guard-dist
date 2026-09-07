# Kosher Guard

**Download the app (tap on the flip phone):**
https://github.com/zifemobile/kosher-guard-dist/releases/download/latest/kosherguard-debug.apk

## What it is

Kosher Guard keeps specific approved apps kosher on an Android phone. Right
now that's Chase and Google Maps. It blocks all web browsers, makes links
inside approved apps go nowhere, covers images and other unwanted content
with dead black boxes, and can stop pictures from ever downloading. It never
touches, changes, or hacks the other apps - it works entirely from the
outside, using Android's built-in accessibility and VPN features. That's why
banking apps keep working perfectly and Google's security checks (Play
Integrity) are unaffected.

## Install (one time, ~5 minutes)

1. **Download** the app using the link above, on the phone.
2. **Open the downloaded file** (in Files or Downloads) and tap Install.
   If the phone says installs are blocked, tap Settings on that popup and
   allow "Install unknown apps" for the app you opened it from, then try again.
3. **Fix the "Restricted setting" block** (Android does this for apps that
   didn't come from the Play Store):
   Settings > Apps > See all apps > Kosher Guard > tap the **3-dot menu** at
   the top right > **Allow restricted settings** > confirm.
4. **Turn on the guard:** open Kosher Guard, tap
   **"1. Enable accessibility service"**. In the settings screen that opens,
   find **Kosher Guard**, tap it, switch it **On**, and tap Allow.
   Back in the app, the top line should say **"Accessibility service: ACTIVE"**.
5. **Turn on the image blocker:** tap **"3. Toggle network image block (VPN)"**
   and tap OK on the connection popup. (This is a local filter on the phone
   itself - it is not a real VPN and nothing goes to any server.)

That's it. From now on it runs by itself.

## Fleet reports (automatic)

Phones quietly send their owner report to the owner's private dashboard by
themselves: once a day, after every blocked uninstall/disable attempt, and
after every update. The user never sees or does anything. The owner opens the
dashboard link (kept private, given at setup) and sees every phone by its
label with its latest report. The app can only ever SUBMIT reports - it
cannot read anyone's.

## Owner report

"Owner report (share)" (PIN required) produces a per-phone summary - guard and
switch states, counts of everything blocked (browsers, links, covered taps,
uninstall attempts, picture hosts), and the last 15 events - ready to share by
WhatsApp/email or save. This is how the store proves the guard stayed on and
working.

## The owner PIN

On first launch the owner sets a PIN (4+ digits, only a hash is stored on the
phone). After that, pausing the guard, flipping any switch, calibrating, or
turning the VPN off all need the PIN. A user without the PIN can't weaken
anything - and the uninstall watchdog bounces any attempt to uninstall,
force-stop, or disable Kosher Guard from Settings or the Play Store.

## Need to browse or install something? (Pause button)

The big button at the top of the Kosher Guard screen -
**"PAUSE GUARD FOR 15 MINUTES"** - turns off the browser block, link bounce,
and all covers for 15 minutes (the picture blocker stays on). Use it when you
need to open a link, update an app, or do maintenance; the button counts down
and you can tap it again to turn the guard back on early. It switches back on
by itself when the time is up.

## What it does today

- **No browsers.** Chrome, Firefox, Samsung Internet, Brave, Edge,
  DuckDuckGo and ~10 others close instantly if opened.
- **Links in Chase go nowhere.** Tap any marketing or external link inside
  Chase and it snaps right back.
- **No pictures in Chase (switch).** Chase's own image server (chasecdn.com)
  is blocked so promo images never download while the "Block pictures in
  Chase" switch is on. More image domains get added as we find them (see
  "Adding more image blocks" below).
- **Google Maps stays kosher.** Star ratings, review text, review counts,
  the Reviews/Photos tabs, and place photos are covered by black boxes.
  Photos don't download at all. The Explore tab is dead. Maps, search, and
  navigation work completely normally.
- **Black boxes are dead zones.** Tapping a covered area does nothing - the
  content behind it can't be opened by accident.
- **Every protection is a switch.** The owner PIN (set once per phone)
  protects all of them: Block links in Chase, Block pictures in Chase, Block
  WhatsApp Status, Block WhatsApp photos & videos. Channels and the browser
  block stay always-on.
- **WhatsApp: no Channels, optional no Status.** Channels never open - the
  tab, rows, and follow buttons are covered and dead, and channel screens
  bounce closed. Status blocking has its own switch in the app
  ("Block WhatsApp Status", on by default). Chats and calls are never
  touched.
- **Log of everything.** Every block and cover is listed with a timestamp in
  the app, so we can always see what fired.

## Covering something new (calibration mode)

If an image or promo is still visible somewhere:

1. Open the screen that has it (e.g. a Chase page).
2. Open Kosher Guard and tap **"2. Calibrate masks"**, then switch straight
   back to the app (you have 4 seconds).
3. A bar appears at the top showing exactly which app and screen you're on.
4. **Drag a box** over each thing you want covered.
5. Tap **Save** to cover it on this screen only, or **Save all** to cover it
   on every screen of that app. Tap **Done**.
6. The boxes appear from then on. To redo, just calibrate again - the new
   boxes replace the old ones.

## Adding more image blocks (Chase)

To catch every last image domain:

1. Make sure the VPN toggle is ON.
2. Browse Chase normally for a few minutes (log in, open accounts, offers).
3. Open Kosher Guard and tap **"Toggle event log / DNS query log"** - you'll
   see every address Chase contacted.
4. Send me that list (a photo of the screen is fine). I'll add the
   picture-serving addresses to the block list. Anything that might carry
   account or banking data is never blocked - if we're not sure, it's allowed.

## How the settings files work (for reference)

Each app has a small settings file (JSON) you don't need to touch by hand:

- **chase.json** - Chase: which screens count as "browser" (they get bounced),
  which image addresses to block, where the cover boxes go.
- **maps.json** - Google Maps: photo/review/rating/Explore rules, image
  addresses to block.
- **whatsapp.json** - WhatsApp: Channels rules (always on) and Status rules
  (behind the in-app switch). WhatsApp's pictures and chats share the same
  servers, so the VPN is deliberately off for WhatsApp - blocking is done on
  the screen, not the network.
- **browsers.json** - the list of blocked browser apps.
- Anything you save in calibration mode overrides these files automatically,
  and survives app updates of Kosher Guard itself. If Chase or Maps updates
  and something reappears, just recalibrate - no code changes needed.

## Safety and privacy facts

- **Nothing leaves the phone.** No account, no server, no analytics. The
  "VPN" is a local filter that only answers name lookups for the two approved
  apps; everything else never touches it.
- **Banking is never at risk.** Only picture-serving addresses are blocked,
  and only for approved apps. Chase's login, balances, transfers, and check
  deposit are untouched. If anything is uncertain, it's allowed.
- **Fails safe, never fatal.** If Chase or Maps updates and a rule misses,
  the content simply reappears - nothing crashes, nothing locks up. Worst
  case you recalibrate.
- **Apps are never modified.** Chase and Maps are byte-for-byte the Play
  Store versions. Google's Play Integrity checks pass exactly as before.
- **Easy off.** Turn off the accessibility service or the VPN toggle and the
  phone is 100% stock again.

## Test checklist

- [ ] Chase login works exactly as normal (balances load, transfers work).
- [ ] Chase promo areas are covered / blank.
- [ ] Tapping any link inside Chase snaps back instead of opening.
- [ ] Chrome cannot open (flashes and returns home).
- [ ] Maps: search, navigation, and map tiles work normally.
- [ ] Maps: no star ratings, no reviews, no photos; Explore tab is dead.
- [ ] Tapping a covered area does nothing.
- [ ] Play Integrity checker app reports normal verdicts.
