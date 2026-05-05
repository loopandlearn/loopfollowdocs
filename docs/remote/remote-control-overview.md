## Remote Control Overview

*LoopFollow* remote commands are sent directly using the [Apple Push Notification System (APNS)](#apple-push-notifications-system-apns) for all Open-Source Automated Insulin Delivery systems that support this feature.

* *Trio* and *Loop* accept a direct APNS message sent from *LoopFollow*
    * minimum versions: *Trio* 0.6.x; all versions of *Loop*
* *Trio* and *Loop* send a direct APNS message back to the originating *LoopFollow* phone with a success or error message
    * minimum versions: *Trio* 0.6.x; *Loop* 3.11.1
* This is subject to the *Apple* APNS servers but tends to be faster and more reliable than going through the Nightscout careportal

> The return APNS message is only available for a meal or bolus entry.

!!! important "Breaking Change: Trio Remote Command Users"
    Trio users must have matching code for LoopFollow and Trio.

    * Trio 0.6 (or newer) requires LoopFollow 4.0 (or newer)
    * Trio 0.5.1.28 (or older) requires LoopFollow 3.2.11 (or older)

    See [Trio Remote Control](remote-control-trio.md){: target="_blank" } for more information.

- - -

## *LoopFollow* Remote Options

For a full summary of version requirements and feature history, see [Version Compatibility](../faqs/lf-history.md#version-compatibility){: target="_blank" }.

The graphic below shows the Remote Settings screen for *LoopFollow*. You must first enter a *Nightscout* URL before any remote options are offered and then only the option suitable for that *Nightscout* site can be selected.

* When following someone running Loop, the options are None or [Loop Remote Control](remote-control-loop.md){: target="_blank" }
* When following someone running Trio, the options are None or:
    * Trio 0.5.x and newer: [Trio Remote Control](remote-control-trio.md){: target="_blank" }
    * Trio 0.2.x: [Nightscout Remote Control](remote-control-nightscout.md#loopfollow-careportal-with-the-trio-app){: target="_blank" }

![LoopFollow remote options - all types](img/lf-remote-options_3.2.svg){width="600"}
{align="center"}

### Critical Configuration Information

If you plan to use *LoopFollow* Remote Control with a looper using the *Loop* app version 3.x or the *Trio* app version 0.5 or newer, and you don't have your APNS key information recorded or configured, see the instructions in [*Apple* Push Notifications System (APNS)](#apple-push-notifications-system-apns).

If your looper is using *Trio* 0.2.x, use this link for configuration:

* [*Nightscout* Remote Control](remote-control-nightscout.md){: target="_blank" }

- - -

## Loop Follow Remote Control Configuration

If you are configuring Remote Control for the first time, follow the appropriate directions for either Loop or Trio:

* [Configure Remote Control for Loop](remote-control-loop.md#configure-loopfollow-for-remote-control){: target="_blank" }
* [Configure Remote Control for Trio](remote-control-trio.md#configure-loopfollow-for-remote-control){: target="_blank" }

If you are configuring a second phone to use remote control, you can transfer the settings from one phone to another.

### Export Remote Settings with QR Code

To share your remote settings with another device, follow the directions in this section to generate the QR code. Then follow the directions in [Import from QR Code](#import-from-qr-code) to read the code on the other device.

!!! important "QR Code Contains Secret Information"
    Never share your QR code as a screenshot online or send it to someone that is not supposed to have access to remote capabilities for your looper.
    
    If in doubt revoke access to the key at [https://developer.apple.com/account/resources/authkeys/list](https://developer.apple.com/account/resources/authkeys/list) and generate a new one.

To show the QR Code, go into Remote settings on the phone that is already configured for remote control. Click the button Import/Export Settings and then choose Export Remote Settings. You can access this same function by going to Settings->Import/Export Settings directly.

> This process works for both Loop Remote Control and for Trio Remote Control.

![Export settings](img/export-settings.png){width="600"}
{align="center"}

### Import from QR Code

!!! tip "Setting up a Second Device for Remote Control"
    With version 4.3 and newer, you can set up a second device using a selection of QR codes from a LoopFollow phone that is already configured.
    
    You can share *Nightscout* Site, Dexcom Share and Alarm Settings if someone only needs to follow the looper.
    
    You can share Remote Control Configurations if someone needs to send remote commands.

**If a follower only needs to monitor and get alarms**

* Do **not** use the QR code for Remote Control Settings
* Limit the sharing to the other QR codes for *Nightscout* Site, Dexcom Share and Alarm Settings

This process works for both Loop and for Trio.

For more information: see [Import/Export Settings](../setup/lf-setup.md#importexport){ target="_blank" }

- - -

## *Apple* Push Notifications System (APNS)

!!! tip "One Set of APNS Credentials"
    **If you support multiple people, you only need one APNS key for a given Developer ID.**

    * You can follow someone who is using the *Trio* app and another person who is using the *Loop* app. 
    * You enter the same APNS credentials for each instance of *LoopFollow* that you are using for your multiple loopers
    * The looper's app (*Loop* or *Trio*) must be built with the Developer ID used to create the APNS key.


### Existing APNS

If you previously configured remote control with the *Loop* app, you already have an *Apple* Push Notification System (APNS) Key ID and Key. These were added to the config vars in your *Nightscout* site.

* For *Loop*, these keys must be added to Nightscout for you to use the Careportal feature
* For *Trio*, these keys do not need to be added to Nightscout to use the Careportal feature

If you do not have existing APNS Keys, skip ahead to [New APNS](#new-apns).

When you configured APNS for the *Loop* app and saved information in your *Nightscout* config vars, they used the names in the table below. The same APNS Key ID and Key are what you need to add to the *LoopFollow* app when configuring for Remote Control with APNS.

| <div style="width:200px"></div>Config Var | Format of Config Var Value |
|:--|:--|
| `LOOP_APNS_KEY_ID`|AAAAAAAAAA|
| `LOOP_APNS_KEY`|-----BEGIN PRIVATE KEY-----<br>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA<br>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA<br>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA<br>AAAAAAAA<br>-----END PRIVATE KEY-----|
| `LOOP_DEVELOPER_TEAM_ID`|AAAAAAAAAA|

Note that the `LOOP_DEVELOPER_TEAM_ID` is the Apple Developer ID used to build the *Loop* app.

* When using *LoopFollow* for remote control, the addition of those `config` variables in *Nightscout* is only required to support sending remote commands to the *Loop* app from *Nightscout* `Careportal` and from *LoopCaregiver*.
* The *LoopFollow* Remote Control features are available for both the *Loop* and *Trio* apps when the APNS credentials are entered in the *LoopFollow* app in the [APN Settings](../setup/lf-setup.md#apn){: target="_blank" }, along with other specific credentials for each app under [Remote Settings](../setup/lf-setup.md#remote){: target="_blank" }.

If you are configuring for *Trio* remote control with *LoopFollow*, you do not need to enter the Apple Developer ID explicitly because it is included in the information *Trio* uploads to *Nightscout*.

### New APNS

When using *Trio*, you do not need to add the config vars to *Nightscout* that are required for *Loop* remote control from *Nightscout* `Careportal` and *LoopCaregiver*. If you already have them, it doesn't hurt anything, but you do not need to add them to use remote control with *Trio*. 

When using *Loop* Remote Control from *LoopFollow*, the config vars do not need to be embedded in *Nightscout*; although they are still needed to issue remote commands with the *Nightscout* *Careportal* and the *LoopCaregiver* app.

If you do not have APNS credentials, you need to create a key and grant it access to the &nbsp;<span translate="no">Apple Push Notification Service (APNS)</span>. 

> It is recommended to name the key *Nightscout* for APNS keys, whether you are using *Loop* or *Trio*.

!!! info "Reminder"
    This only works with the **paid** Apple Developer ID.

!!! warning "*Apple* changed the APN system"
    *Apple* changed the way APN are created. Your old ones should still work, but if they don't, create new ones and update all the places where they are used.

    When creating new APN keys, you have the option for "Sandbox", "Production" or "Sandbox & Production". Be sure to choose "Sandbox & Production".

1. To get started, go to the `Keys` section under Apple Developer's [`Certificates, Identifiers & Profiles`](https://developer.apple.com/account/resources/authkeys/list) and login with the *Apple ID* associated with your developer team that you used to build the *Trio* app.
2. If not already open in your browser (compare with the below screenshot), 
    - Click on **`Keys`** (located in the left-hand column). 
    - Either click on the blue **`Create a key`** button **OR** the plus button (<font color="#2997FF">:material-plus-circle:</font>)  to add a key.
    > ![img/apns-add-key.png](img/apns-add-key.png)
3. In the form that appears, do the following:
    - Click the checkbox for enabling **`Apple Push Notifications service (APNs)`**
    - Enter a name for the key such as `Nightscout` (you can name it however you want, just make sure you know what the key is for by the name you choose).
    - Then click the **`Configure`** button to the right of the name
    - Choose **`Sandbox & Production`** and then **`Save`**
    - Tap on the **`Continue`** button, upper right
  > ![updated instructions for creating and configuring an APNS key](img/key-apns.svg)
4. In the screen that follows, click the blue **`Register`** button.  
   > ![img/apns-register.png](img/apns-register.png)
5. In the screen that follows, click the blue **`Download`** button.  
    This step will download a file with a name that starts with `AuthKey` and ends with `.p8`.
> ![img/apns-download.png](img/apns-download.png)
6. Find your `AuthKey` downloaded file in your downloads folder. It's a good idea to store this file where you can find it again if you need it. 
    The next task is to rename the file so you can open it. 
    Highlight the filename and choose rename, then add ".txt" after ".p8". In other words, modify `AuthKey_AAAAAAAAAA.p8` to `AuthKey_AAAAAAAAAA.p8.txt` and click on `Use .txt` when questioned.
> ![rename the p8 file](img/apns-rename.png){width=200}
{align=center}
7. Double-click to open the `AuthKey_AAAAAAAAAA.p8.txt` file. It will look similar to the screenshot below. You need to highlight **ALL OF THE CONTENTS** of that file and copy it and then paste it both into your Secrets Reference file and into the row for *LoopFollow* APNS Key. Yes, *allllll* of the contents.  
    So, the easiest way is to:
      * **Click inside that file**
      * Highlight **all** the text, and then
      * Copy **all** the text to the clipboard (Cf. screenshot below).
        * On a *Mac*, press ++command+"A"++ to select all, then press ++command+"C"++ to copy the selection. 
        * On a **PC**, press ++control+"A"++ to select all, then press ++control+"C"++ to copy the selection.

    > ![img/apns-copy-key.png](img/apns-copy-key.png)

8. The APNS Key ID is the 10-character name embedded in the filename: `AuthKey_AAAAAAAAAA.p8.txt`. You can also see it if you return to Apple Developer's [`Certificates, Identifiers & Profiles`](https://developer.apple.com/account/resources/authkeys/list) as highlighted in this graphic. You copy that APNS Key ID and then paste it both into your Secrets Reference file and into the row for *LoopFollow* APNS Key ID.

    > ![APNS KEY ID is highlighted by red rectangle](img/apns-key-id.png)

- - -

## Quick-Pick Boluses and Meals

When you open a remote bolus or meal screen, *LoopFollow* may show a row of **Quick-Pick** buttons at the top. Tapping a button fills in the entry fields with that amount — nothing is sent until you review and confirm on the screen as usual.

Quick-Picks are shown on:

* *Trio* Remote Control: **Bolus** screen and **Meal** screen
* *Loop* Remote Control: **Bolus** screen and **Carbs** screen

The buttons are built from the entries you have successfully sent in the past, scored by:

* **Time of day** — entries used at similar times score higher
* **Day of week** — weekday and weekend patterns are kept separate
* **Recency** — older entries gradually fade out

Up to five suggestions are shown, and the section is hidden entirely until there is enough history. The history is stored only on this device.

## Next Step

Depending on the selection you made, continue to one of these pages for more information on how to configure *LoopFollow* for your desired remote control option.

The APN credentials are entered in *LoopFollow* under Settings in the APN row.

The other remote credential are entered as described in the appropriate link.

* [*Loop* Remote Control](remote-control-loop.md)
* [*Trio* Remote Control](remote-control-trio.md)
* [*Nightscout* Remote Control](remote-control-nightscout.md) (`Trio 0.2.x only`)


