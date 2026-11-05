## LF Hub

*LF Hub* is a small server that a family runs for *LoopFollow*. It follows one person's glucose data (from *Nightscout*, *Dexcom Share* or both) and sends the alarms, the app badge and the Live Activity to every family phone, so *LoopFollow* can stay closed. It also speaks readings for Speak BG.

Without *LF Hub*, *LoopFollow* has to keep itself running in the background (for example with Silent Tune) to check for alarms. With *LF Hub*, the hub does that work and sends the results to the phone through *Apple*'s push service.

!!! warning "Not a medical device"
    *LoopFollow* and *LF Hub* are open-source software that you build and run yourself. They are not medical devices, and this page is not medical advice.

    *LF Hub*'s alarms depend on the hub, its internet connection, *Apple*'s push service and your phone, and any of them can fail. Don't let *LF Hub* be the only way an alarm reaches someone. Talk to your care team about how you rely on alarms.

!!! note "Requirements"
    * Every phone needs iOS 26 or later. On older iOS versions, *LoopFollow* shows *"LF Hub requires iOS 26 or later."* and the LF Hub row does not appear in Settings.
    * Someone has to run the hub itself. That is covered in the *LF Hub* [setup guide](https://github.com/loopandlearn/lfhub/blob/main/docs/SETUP.md){: target="_blank" } and not on this page.
    * If you build *LoopFollow* in the browser, your build needs one extra step for *LF Hub*. See [Update for LF Hub](../build/lf-browser-build.md#update-for-lf-hub){: target="_blank" }.

### Words used on this page

* **APNs** (*Apple* Push Notification service): *Apple*'s system for sending notifications to an iPhone. *LF Hub* uses it to reach your phone.
* **APN key**: a file (ending in `.p8`) from an *Apple* Developer account that allows a server to send notifications through APNs. It is entered in *LoopFollow* under Settings → APN.
* **AlarmKit**: the iOS 26 feature that lets an app ring a system alarm, like the Clock app does. It rings even when the phone is in silent mode or a Focus is on.
* **Background Refresh mode**: the setting under Settings → [Background Refresh](lf-setup.md#background-refresh){: target="_blank" } that decides how *LoopFollow* stays up to date while it is not on screen. *LF Hub* adds a mode called **LoopFollow Hub**.
* **Setup token**: a secret password chosen by whoever runs the hub. Anyone with the setup token can join the hub as an admin.
* **Invite**: a one-time QR code (or link) made by an admin that lets one more phone join the hub as a member.
* **Admin** and **member**: the two roles a phone can have on the hub. See [Admins and members](#admins-and-members).

- - -

## How Hub Mode Works

When the **LoopFollow Hub** Background Refresh mode is selected and the hub is ready:

* The hub checks the alarms and sends them to the phone. They ring as system alarms through AlarmKit, even while *LoopFollow* is closed.
* The hub sets the app badge and keeps the Live Activity up to date.
* *LoopFollow* does not keep itself running in the background. iOS may suspend it, which saves battery.
* When you open *LoopFollow*, it reads the data from the hub.

The **Ready** list under Settings → LF Hub says:

> The hub sends the alarms, badge and Live Activity, so LoopFollow can stay closed. Alarms depend on the network and Apple's push service. If the hub stops working, LoopFollow alarms by itself only when iOS lets it run, which can take a long time while the phone is locked.

### Until the hub is ready, *LoopFollow* alarms by itself

Choosing the LoopFollow Hub mode does not hand the alarms to the hub right away. Until the hub has confirmed that it can deliver this phone's alarms, *LoopFollow* checks the alarms itself and keeps itself running as it does with Silent Tune.

The hub sends this phone's alarms only while all of these are true:

* LoopFollow Hub is selected under Background Refresh.
* The hub has confirmed that alarms are on, that it has this phone's latest alarm list, that it is reading the person's data, and that its notifications reach this phone.
* The phone's recent checks of the hub have been healthy (see [When something stops working](#when-something-stops-working)).
* Notifications for *LoopFollow* are allowed and show alerts. Notifications delivered quietly count as off.
* *LoopFollow* is allowed to ring alarms through silent mode (AlarmKit).

If any of these stops being true, *LoopFollow* goes back to checking the alarms itself.

- - -

## The Ready Checklist

Settings → LF Hub shows a **Ready** list. Each item has a green check when it is in place. When something is missing, the item explains what, and most items have a button that fixes it (for example **Allow**, **Open Settings**, **Turn On**, **Register Again**, **Try Again** or **Go to APN**).

| Item | What it means |
|:--|:--|
| LF Hub answers | The hub responds to this phone. |
| LF Hub is up to date | Only shown when the hub is too old for this *LoopFollow*. The hub needs an update. |
| Background Refresh uses LF Hub | LoopFollow Hub is selected under Background Refresh. Otherwise *LoopFollow* checks the alarms itself. |
| Notifications allowed | iOS lets *LoopFollow* show notifications with alerts. |
| Alarms ring through silent mode | AlarmKit is allowed. Otherwise alarms follow the ringer switch. |
| Live Activity on | The Live Activity is turned on in *LoopFollow*. Shown in Hub mode. |
| APN key added, or APN key shared by an admin | The hub has an APN key it can use to notify this phone. |
| Notifications from LF Hub arrive | The hub's notifications are reaching this phone, and *Apple* accepts the APN key. |
| LF Hub reads (name)'s data | The hub has a data source for the person, can read it, and has received a reading. |
| LF Hub sends this phone's alarms | The hub has confirmed that it delivers this phone's alarms. Until then: *"LF Hub takes over once the items above are ready. Until then, LoopFollow checks the alarms itself."* |

Once every item is green, use **Send Test Alarm**, or **Send Test Alarm in 30 s** and lock the phone right away, to check that an alarm really rings on the locked phone.

### "LF Hub isn't sending alarms" banner

While LoopFollow Hub is selected but the hub is not sending this phone's alarms, the Home screen shows an orange banner:

> LF Hub isn't sending alarms. LoopFollow is alarming by itself.

Settings and Background Refresh show the same warning: *"LF Hub is not sending this phone's alarms"*. Tap it to open the LF Hub page and see which Ready item is missing.

- - -

## When Something Stops Working

*LoopFollow* checks the hub to see that it is still working. A check is healthy when the hub answers for this phone, the hub's alarm engine is running, and the hub's notifications are reaching the phone.

**The phone checks the hub only when *LoopFollow* gets to run:**

* when *LoopFollow* is opened or comes back to the screen;
* about once a minute while *LoopFollow* is open;
* when iOS gives *LoopFollow* background time. iOS decides when this happens. While the phone is locked, it can be a long time between these.

**What happens after a problem starts:**

* When checks have been failing for **5 minutes**, *LoopFollow* goes back to alarming by itself and keeps itself running as it does with Silent Tune.
* When there has been no healthy check for **20 minutes**, *LoopFollow* raises one alert for the outage: a system alarm that rings through silent mode if AlarmKit is allowed, otherwise a time-sensitive notification. Depending on the cause, it says *"LF Hub not responding"*, *"LF Hub can't reach this phone"* or *"Apple rejects LF Hub's APN key"*.
* When the hub is healthy again, the alert is cleared.

!!! warning "If the hub fails while the phone is locked"
    Both of these steps happen only during a check, and a check needs *LoopFollow* to run. If the hub, the computer it runs on, its internet connection or *Apple*'s push service stops working while the phone is locked and *LoopFollow* is suspended, nothing on the phone notices until iOS lets *LoopFollow* run again. That can take a long time. During that time, **no alarms may reach the phone**, neither from the hub nor from *LoopFollow*.

    Opening *LoopFollow* runs a check right away.

### Live Activity "Not updating"

The hub updates the Live Activity whenever the reading changes, and at least every 5 minutes. Each update tells iOS that it is out of date 15 minutes later. When no update arrives in time, the Live Activity shows a red **Not updating — open LoopFollow** badge (**Not updating** in the small layout). This means the hub has stopped updating it. Open *LoopFollow* to check.

### "LF Hub doesn't recognize this phone"

If the hub no longer accepts this phone, *LoopFollow* sends a notification and shows **LF Hub doesn't recognize this phone** at the top of Settings → LF Hub. This can happen when:

* another phone replaced this one when joining,
* an admin removed this phone, or
* the hub address now leads to a different server.

*LoopFollow* alarms by itself and keeps trying. If this phone was replaced or removed, tap **Disconnect** and join again with an invite.

- - -

## Joining a Hub

There are two ways to join. Which one you use decides the phone's role.

* **Set Up as Owner** (with the setup token): the phone joins as an **admin**. This is how the first phone connects.
* **Join with Invite** (with an invite QR code or link): the phone joins as a **member**.

### Set up as owner

1. Before you start, make sure *Nightscout* and/or *Dexcom* work in *LoopFollow*, and that an APN key is entered under Settings → [APN](lf-setup.md#apn){: target="_blank" }. See [*Apple* Push Notifications System (APNS)](../remote/remote-control-overview.md#apple-push-notifications-system-apns){: target="_blank" } for how to get a key.
2. Open Settings → LF Hub. Under **Set Up as Owner**, enter the hub's address (for example `https://hub.example.com`) and the setup token, then tap **Continue**.
3. On a new hub, enter the person's name and a name for this phone, then tap **Connect**. Connecting creates the person on the hub.
4. *LoopFollow* asks **Use LF Hub for Background Refresh?** Tap **Use LF Hub**, or choose it later under Background Refresh.
5. Work through the [Ready checklist](#the-ready-checklist) until every item is green, then send a test alarm with the phone locked.

!!! warning "Keep the setup token secret"
    Anyone with the setup token can join as an admin, take over any phone on the hub and read the person's data source settings. Don't share it with family members. Use invites instead.

### Join with an invite

On an admin's phone, open Settings → LF Hub → **Invite Family Member**. It shows a QR code and a **Share Invite Link** button. The invite works once and expires; the screen shows when.

On the new phone, either:

* choose **Join a Family Hub** when *LoopFollow* starts for the first time, or
* open Settings → LF Hub → **Join with Invite**, then tap **Scan Invite Code** or paste the invite link.

*LoopFollow* shows the hub's address and the person's name. Only join a hub you know.

!!! warning "Share invites only with people who should follow"
    A member receives the person's data source settings (the *Nightscout* address and token, or the *Dexcom* account). Share an invite only with someone who should follow that person.

### Replace, copy or start fresh

If the hub already has phones, you choose how this phone joins:

* **Replace** a phone: this phone takes over that phone's alarms and settings. Use this for a phone you no longer use. The old phone is no longer recognized by the hub. If the old phone was used in the last 15 minutes, *LoopFollow* asks first, since it may still be in use. A phone joining with an invite cannot replace an admin's phone.
* **Copy Settings from** a phone: this phone joins as a new phone that starts with a copy of that phone's alarms and settings.
* **New Device** (or **Start fresh**): this phone joins with its own alarms.

You also give the phone a name. Everyone who manages *LF Hub* sees this name in the list of phones.

- - -

## Admins and Members

**Admins** manage the hub for the family. An admin can:

* change the person's data source; the change reaches every phone following that person;
* invite family members;
* remove phones (the hub then stops sending to them);
* make another phone an admin, or make an admin a member. The hub always keeps at least one admin.

**Members** follow, with their own alarms. A member cannot change the data source, invite, or manage phones.

### Data sources

The hub reads *Dexcom* if it is set, otherwise *Nightscout*. Every phone, members included, receives the hub's data source settings and keeps a copy, so *LoopFollow* can read the data itself when it needs to, for example when the hub does not answer.

On a member's phone, the *Nightscout* and *Dexcom* settings show **Managed by LF Hub** and cannot be edited. On an admin's phone, **Change Data Source** asks first, because the change reaches everyone following the person.

### The APN key

The hub needs an APN key to send notifications to the phones.

* The admin's phone sends the APN key from Settings → APN to the hub. The hub stores it encrypted.
* Family members on the same *LoopFollow* build (built with the same *Apple* Developer team) need no key of their own. The hub uses an admin's key for them, and their APN settings show **Managed by LF Hub**.
* A phone that joined with an invite never sends its own APN key. If no admin has added a key yet, its Ready list says so.
* An admin's key only works for *LoopFollow* built with the same *Apple* Developer account. A family member who builds *LoopFollow* under their own account and joins with an invite gets no notifications from the hub, and *LoopFollow* on that phone keeps checking the alarms itself. To use *LF Hub*, that family member installs *LoopFollow* from the same build as the admin.

!!! tip "Use a separate APN key for the hub"
    An APN key can send notifications to every app in the *Apple* Developer team it belongs to. Consider creating a new APN key just for *LF Hub*, rather than reusing a key you already use for other things, so that you can revoke it on its own if you ever need to.

- - -

## What Changes in Hub Mode

### Alarms

When the hub sends the alarms, they ring as system alarms:

* They ring at the phone's alarm volume and through silent mode and Focus.
* **Override System Volume**, **Volume Level** and **Audio During Calls** in Alarm Settings do not apply to them.
* An alarm repeats its sound without a delay between sounds, whatever repeat delay you set.
* Stop or snooze them with the alarm's own buttons. The volume buttons may not snooze them.

Your alarms themselves (which alarms, their limits, snoozes) still come from *LoopFollow* on each phone. Each phone has its own alarms.

### Calendar and contact

In Hub mode, **Save BG to Calendar** and **Enable Contact BG Updates** are not available and cannot be changed, because the app sleeps and would show old readings. When Hub mode starts, *LoopFollow* removes the BG calendar events and sets the contact images to show no value. Your settings are kept for when you leave Hub mode.

### Badge

The hub sets the app badge.

- - -

## Leaving the Hub

Settings → LF Hub → **Disconnect** removes this phone from the hub. This phone stops getting *LF Hub*'s alarms, *LoopFollow* goes back to alarming by itself, and Background Refresh goes back to Silent Tune.

To use another Background Refresh mode without leaving the hub, change it under Settings → Background Refresh. *LoopFollow* then checks the alarms itself.
