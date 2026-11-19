## How *LF Hub* Works

This page explains what *LoopFollow* does in Hub mode, what the *Ready* list means, and what happens when something stops working. For what *LF Hub* is, see [What is LF Hub](lf-hub-overview.md). For the setup steps, see [Set Up and Invite](lf-hub-onboarding.md).

!!! important "In the `dev` branch"
    *LF Hub* is available when you build the `dev` branch of *LoopFollow*. On the current release there is no *LF Hub* row in *Settings*.

- - -

## Hub Mode

Hub mode is the **LoopFollow Hub** choice under *Settings* → [*Background Refresh*](../setup/lf-features.md#background-refresh). When it is selected and the hub is ready:

* The hub checks the alarms and sends them to the phone. They ring as system alarms through AlarmKit, even while *LoopFollow* is closed.
* The hub sets the app badge and keeps the *Live Activity* up to date.
* *LoopFollow* does not keep itself running in the background. *iOS* may suspend it, which saves battery.
* When you open *LoopFollow*, it reads the data from the hub.

### Until the hub is ready, *LoopFollow* alarms by itself

Choosing **LoopFollow Hub** does not hand the alarms to the hub right away. Until the hub has confirmed that it can deliver this phone's alarms, *LoopFollow* checks the alarms itself and keeps itself running as it does with Silent Tune.

The hub sends this phone's alarms only while all of these are true:

* **LoopFollow Hub** is selected under *Background Refresh*.
* The hub has confirmed that alarms are on, that it has this phone's latest alarm list, that it is reading the person's data, and that its notifications reach this phone.
* The phone's recent checks of the hub have been healthy (see [When something stops working](#when-something-stops-working)).
* Notifications for *LoopFollow* are allowed and show alerts. Notifications delivered quietly count as off.
* *LoopFollow* is allowed to ring alarms through silent mode (AlarmKit).

If any of these stops being true, *LoopFollow* goes back to checking the alarms itself, with its own alarm sound settings.

- - -

## The *Ready* List

*Settings* → *LF Hub* shows a *Ready* list. Each row has a green check when it is in place. When something is missing, the row says what, and most rows have a button that fixes it (for example *Allow*, *Open Settings*, *Turn On*, *Register Again*, *Try Again* or *Go to APN*).

| Row | What it means |
|:--|:--|
| *LF Hub answers* | The hub responds to this phone. |
| *LF Hub is up to date* | Only shown when the hub is too old for this *LoopFollow*. Whoever runs the hub needs to update it. |
| *Background Refresh uses LF Hub* | **LoopFollow Hub** is selected under *Background Refresh*. Otherwise *LoopFollow* checks the alarms itself. |
| *Notifications allowed* | *iOS* lets *LoopFollow* show notifications with alerts. |
| *Alarms ring through silent mode* | AlarmKit is allowed. Until it is, the hub does not send this phone's alarms, and *LoopFollow* checks the alarms itself. |
| *Live Activity on* | The *Live Activity* is turned on in *LoopFollow*. Shown in Hub mode. |
| *APN key added* | An APN key is entered under *Settings* → *APN* on this phone, and the hub has it. Shown on a phone that set up the hub with the setup token. |
| *APN key shared by an admin* | Shown on a phone that joined with an invite. The hub uses an admin's APN key for this phone. This phone cannot fix the row itself. If it is not green, ask an admin to add an APN key on their phone, or install *LoopFollow* from the same build as the admin (see [The APN Key](#the-apn-key)). |
| *Notifications from LF Hub arrive* | The hub's notifications reach this phone, and Apple accepts the APN key. |
| *LF Hub reads (name)'s data* | The hub has a data source for the person, can read it, and has received a reading. |
| *LF Hub sends this phone's alarms* | The hub has confirmed that it delivers this phone's alarms. Until then: *"LF Hub takes over once the items above are ready. Until then, LoopFollow checks the alarms itself."* |

When every row is green, use *Send Test Alarm*, or *Send Test Alarm in 30 s* and lock the phone right away, to check that an alarm really rings on the locked phone.

### "LF Hub isn't sending alarms" banner

While **LoopFollow Hub** is selected but the hub is not sending this phone's alarms, the Home screen shows an orange banner: *"LF Hub isn't sending alarms. LoopFollow is alarming by itself."*

*Settings* and *Background Refresh* show the same warning: *"LF Hub is not sending this phone's alarms"*. Tap it to open the *LF Hub* page and see which row is missing.

- - -

## When Something Stops Working

*LoopFollow* checks that the hub is still working. A check is healthy when the hub answers for this phone, the hub's alarm engine is running, and the hub's notifications reach the phone.

**The phone checks the hub only when *LoopFollow* gets to run:**

* when *LoopFollow* is opened or comes back to the screen
* about once a minute while *LoopFollow* is open
* when *iOS* gives *LoopFollow* background time. *iOS* decides when this happens. While the phone is locked, it can be a long time between these.

**What happens after a problem starts:**

* When checks have been failing for **5 minutes**, *LoopFollow* goes back to alarming by itself and keeps itself running as it does with Silent Tune.
* When there has been no healthy check for **20 minutes**, *LoopFollow* raises one alert for the outage: a system alarm that rings through silent mode if AlarmKit is allowed, otherwise a time-sensitive notification. Depending on the cause, it says *"LF Hub not responding"*, *"LF Hub can't reach this phone"* or *"Apple rejects LF Hub's APN key"*.
* When the hub is healthy again, the alert is cleared.

!!! warning "If the hub stops while the phone is locked"
    Both of these steps happen only during a check, and a check needs *LoopFollow* to run. If the hub, the computer it runs on, its internet connection or Apple's push service stops working while the phone is locked and *LoopFollow* is suspended, nothing on the phone notices until *iOS* lets *LoopFollow* run again. That can take a long time. During that time, **no alarms may reach the phone**, neither from the hub nor from *LoopFollow*.

    Opening *LoopFollow* runs a check right away. A monitoring service for the hub (see [Get a Hub](lf-hub-get.md)) tells the person who runs it when the hub stops.

### *Live Activity* "Not updating"

The hub updates the *Live Activity* whenever the reading changes, and at least every 5 minutes. Each update tells *iOS* that it is out of date 15 minutes later. When no update arrives in time, the *Live Activity* shows a red *Not updating — open LoopFollow* badge (*Not updating* in the small layout). This means the hub has stopped updating it. Open *LoopFollow* to check.

### "LF Hub doesn't recognize this phone"

If the hub no longer accepts this phone, *LoopFollow* sends a notification and shows *LF Hub doesn't recognize this phone* at the top of *Settings* → *LF Hub*. This can happen when:

* another phone replaced this one when joining
* an admin removed this phone
* the hub address now leads to a different server

*LoopFollow* alarms by itself and keeps trying. If this phone was replaced or removed, tap *Disconnect* and join again with an invite.

- - -

## Data Sources

The hub reads *Dexcom Share* if it is set, otherwise *Nightscout*. Every phone, members included, receives the hub's data source settings and keeps a copy, so *LoopFollow* can read the data itself when it needs to, for example when the hub does not answer.

On a member's phone, the *Nightscout* and *Dexcom* settings show *Managed by LF Hub* and cannot be edited. On an admin's phone, *Change Data Source* asks first, because the change reaches everyone following the person.

!!! warning "Share invites only with people who should follow"
    A member receives the person's data source settings (the *Nightscout* address and token, or the *Dexcom* account). Share an invite only with someone who should follow that person.

- - -

## The APN Key

The hub needs an APN key to send notifications to the phones.

* An admin's phone sends the APN key from *Settings* → *APN* to the hub. The hub stores it encrypted.
* Family members on *LoopFollow* built with the same Apple Developer account need no key of their own. The hub uses an admin's key for them, and their *APN* settings show *Managed by LF Hub*.
* A phone that joined with an invite never sends its own APN key. If no admin has added a key yet, its *Ready* list says so.
* An admin's key only works for *LoopFollow* built with the same Apple Developer account. A family member who builds *LoopFollow* under their own account and joins with an invite gets no notifications from the hub, and *LoopFollow* on that phone keeps checking the alarms itself. To use *LF Hub*, that family member installs *LoopFollow* from the same build as the admin.

!!! tip "Use a separate APN key for the hub"
    An APN key can send notifications to every app in the Apple Developer team it belongs to. Consider creating a new APN key just for *LF Hub*, so that you can revoke it on its own if you ever need to.

- - -

## What Changes in Hub Mode

### Alarms

When the hub sends the alarms, they ring as system alarms:

* They ring at the phone's alarm volume and through silent mode and *Focus*.
* *Override System Volume*, *Volume Level* and *Audio During Calls* in *Alarm Settings* do not apply to them.
* An alarm repeats its sound without a delay between sounds, whatever repeat delay you set.
* Stop or snooze them with the alarm's own *Stop* and *Snooze* buttons. Don't count on the volume buttons to snooze them.

Which alarms you have, their limits and their snoozes still come from *LoopFollow* on each phone. Each phone has its own alarms.

### Calendar and contact

In Hub mode, *Save BG to Calendar* and *Enable Contact BG Updates* are not available and cannot be changed, because the app sleeps and would show old readings. When Hub mode starts, *LoopFollow* removes the BG calendar events and sets the contact images to show no value. Your settings are kept for when you leave Hub mode.

### Badge

The hub sets the app badge.

- - -

## Leaving the Hub

*Settings* → *LF Hub* → *Disconnect* takes this phone off the hub. This phone stops getting the hub's alarms, *LoopFollow* goes back to alarming by itself, and *Background Refresh* is set to *Silent Tune*. If you used another mode before, such as a Bluetooth heartbeat, choose it again under *Settings* → *Background Refresh*.

To use another *Background Refresh* mode without leaving the hub, change it under *Settings* → *Background Refresh*. *LoopFollow* then checks the alarms itself.
