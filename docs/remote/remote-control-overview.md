🚧 Documentation Under Construction 🚧

## Remote Control Overview

*LoopFollow* remote commands are sent directly using the [Apple Push Notification System (APNS)](#apple-push-notifications-system-apns) for all Open-Source Automated Insulin Delivery systems that support this feature.

The *Loop* app and the open beta version of the *Trio* app (0.5.x or newer) support direct APNS from *LoopFollow*.

!!! warning "Browser Build Update"
    If you use Browser Build, follow the one-time updates needed to transition from *LoopFollow* v3.2 to *LoopFollow* v4.0:

    * [Browser Build Update for LoopFollow v4.0](../build/build-options.md#browser-build-update-for-loopfollow-v40){: target="_blank" }
- - -

## *LoopFollow* Remote Options

> With the release of *LoopFollow* 3.2, remote options for the *Loop* app are updated.

The graphic below shows the Remote Settings screen for *LoopFollow*. You must first enter a *Nightscout* URL before any remote options are offered and then only the option suitable for that *Nightscout* site can be selected.

* When following someone running Loop, the options are None or [Loop Remote Control](remote-control-loop.md){: target="_blank" }
* When following someone running Trio, the options are None or:
    * Trio 0.5.x and newer: [Trio Remote Control](remote-control-trio.md){: target="_blank" }
    * Trio 0.2.x: [Nightscout Remote Control](remote-control-nightscout.md#loopfollow--careportal-with-the-trio-app){: target="_blank" }

![LoopFollow remote options - all types](img/lf-remote-options_3.2.svg){width="600"}
{align="center"}

### Critical Configuration Information

If you plan to use *LoopFollow* Remote Control with a looper using the *Loop* app version 3.x or the *Trio* app version 0.5 or newer, and you don't have your APNS recorded or configured, see the instructions in [*Apple* Push Notifications System (APNS)](#apple-push-notifications-system-apns).

If your looper is using *Trio* 0.2.x, use this link for configuration:

* [*Nightscout* Remote Control](remote-control-nightscout.md)

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

To show the QR Code, go into Remote settings and click the button Export Remote Settings as QR Code and the QR code will show on screen. This process works for both Loop and for Trio, with the generated QR Code specific to the app that is being followed.

![Export settings](img/export-settings.png){width="600"}
{align="center"}

### Import from QR Code

!!! tip "Setting up a Second Device for Remote Control"
    With version 4.0 and newer, you can set up a second device with all the Nightscout and Remote Control Settings by scanning a QR code from a LoopFollow device that is already configured. 
    
    Do **not** use this option if the person using the second device only needs to monitor with LoopFollow.

    In that case, just use the Nightscout URL with token as described in [Add Nightscout](../setup/lf-setup.md#add-nightscout).

You can scan a QR code from a LoopFollow device that is already configured to get the settings for Nightscout URL, Token and all remote settings. This process works for both Loop and for Trio, with the QR Code specific to the app that is being followed.

> **Only do this for another caregiver who needs the same Nightscout and remote control capabilities.**

There are different directions depending on whether the target phone already has the Nightscout URL entered or not:

* [Nightscout URL Configured](#nightscout-url-configured)
* [Nightscout URL Not Configured](#nightscout-url-not-configured)

#### Nightscout URL Configured

With a device that already has the Nightscout address set, go to the Settings: Remote Control screen. you must select "None" to reveal the "Import Remote Settings from QR Code" button.

Clicking that will take you to the remote screen where you can use the button Import Remote Settings from QR Code.

Use the Camera to scan a QR Code from the other phone.

This will populate the Nightscout URL, token and remote settings.

![Import remote settings](img/import-from-qr-code.png){width="300"}
{align="center"}

#### Nightscout URL Not Configured

With a device that does not have a Nightscout address set, there will be a button in Settings named Import Settings.

![Import settings](img/import-settings.png){width="600"}
{align="center"}

Clicking that will take you to the remote screen where you can use the button Import Remote Settings from QR Code.

Use the Camera to scan a QR Code from the other phone.

This will populate the Nightscout URL, token and remote settings.

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

* When using *LoopFollow* 3.2 or newer, the addition of those `config` variables in *Nightscout* is only required to support sending remote commands to the *Loop* app from *Nightscout* `Careportal` and from *LoopCaregiver*.
* With *LoopFollow* 3.2 and newer versions, the *LoopFollow* Remote Control features are available for both the *Loop* and *Trio* apps when the APNS credentials are entered in the *LoopFollow* app, along with other specific credentials for each app.

If you are configuring for *Trio* remote control with *LoopFollow*, you do not need to enter the Apple Developer ID explicitly because it is included in the information *Trio* uploads to *Nightscout*.

### New APNS

When using *Trio*, you do not need to add the config vars to *Nightscout* that are required for *Loop* remote control from *Nightscout* `Careportal` and *LoopCaregiver*. If you already have them, it doesn't hurt anything, but you do not need to add them to use remote control with *Trio*. 

With *LoopFollow* 3.2 and newer, the config vars will not need to be embedded in *Nightscout* for *Loop* Remote Control from *LoopFollow*, although they are still needed to issue remote commands with the *Nightscout* *Careportal* and the *LoopCaregiver* app.

If you do not have APNS credentials, you need to create a key and grant it access to the &nbsp;<span translate="no">Apple Push Notification Service (APNS)</span>. 

> Note - these directions are copied from *LoopDocs* so it suggests you name the key *Nightscout*. It is probably best to stick with that naming for APNS keys whether you are using *Loop* or *Trio*.

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
7. Double-click to open the `AuthKey_AAAAAAAAAA.p8.txt` file. It will look similar to the screenshot below. You need to highlight **ALL OF THE CONTENTS** of that file and copy it and then paste it both into your Secrets Reference file and into the row for *LoopFollow* [APNS Key](#apns-key). Yes, *allllll* of the contents.  
    So, the easiest way is to:
      * **Click inside that file**
      * Highlight **all** the text, and then
      * Copy **all** the text to the clipboard (Cf. screenshot below).
        * On a *Mac*, press ++command+"A"++ to select all, then press ++command+"C"++ to copy the selection. 
        * On a **PC**, press ++control+"A"++ to select all, then press ++control+"C"++ to copy the selection.

    > ![img/apns-copy-key.png](img/apns-copy-key.png)

8. The APNS Key ID is the 10-character name embedded in the filename: `AuthKey_AAAAAAAAAA.p8.txt`. You can also see it if you return to Apple Developer's [`Certificates, Identifiers & Profiles`](https://developer.apple.com/account/resources/authkeys/list) as highlighted in this graphic. You copy that APNS Key ID and then paste it both into your Secrets Reference file and into the row for *LoopFollow* [APNS Key ID](#apns-key-id)

    > ![APNS KEY ID is highlighted by red rectangle](img/apns-key-id.png)

- - -

## Next Step

Depending on the selection you made, continue to one of these pages for more information on how to configure *LoopFollow* for your desired remote control option.

* [*Loop* Remote Control](remote-control-loop.md)
* [*Trio* Remote Control](remote-control-trio.md)
* [*Nightscout* Remote Control](remote-control-nightscout.md) (`Trio 0.2.x only`)

## Background Information

There has been a lot of recent changes to remote control with LoopFollow.

The historical notes are in this section.


!!! tip "`Loop` Remote Control with *LoopFollow* 3.2"
    With the release of *LoopFollow* 3.2, the remote control features accessible from LoopFollow match those available from the *LoopCaregiver* app.

    You must update to *LoopFollow* 3.2 or newer and configure remote settings in the *LoopFollow* app to use these features.

!!! important "Breaking Change: Trio Remote Command Users"
    Trio users must have matching code for LoopFollow and Trio.

    * Trio 0.6 (or newer) requires LoopFollow 4.0 (or newer)
    * Trio 0.5.1.28 (or older) requires LoopFollow 3.2.11 (or older)

    See [Trio Remote Control](trio-remote-control.md){: target="_blank" } for more information.

    For Browser Builders:

    * [Browser Build Update for LoopFollow v4.0](../build/build-options.md#browser-build-update-for-loopfollow-v40){: target="_blank" }


### Changes for *LoopFollow* Remote Control of the *Loop* App

* With *LoopFollow* 3.2 and newer
    * *Loop* remote commands from *LoopFollow* include Meal, Bolus and Override control
        * *LoopFollow* no longer requires the *Nightscout* site be configured with the APNS credentials
        * Read access for the *Nightscout* URL is sufficient
* With *LoopFollow* 3.1 and older
    * *Loop* remote commands were limited to Overrides, required the *Nightscout* site be configured with the APNS credentials and required a token with `careportal` access

> With *Trio* 0.2.x, *LoopFollow* only supports temp targets and requires a token with `careportal` access. Once updated to *Trio* 0.5.x or newer, the full Trio Remote Control options are available.


### *LoopFollow* Remote Control

* *LoopFollow* Remote Control sends messages to the loopers phone using APNS
    * **Loop**: Requires *LoopFollow* 3.2 or newer
    * **Trio**: Requires matched code versions:
        * Trio 0.6 (or newer) requires LoopFollow 4.0 (or newer)
        * Trio 0.5.1.28 (or older) requires LoopFollow 3.2.11 (or older)
    * Commands go via APNS to the *Loop*/*Trio* phone
        * An immediate success or failure for **sending** the message to APNS is received
        * There still could be a communication failure between APNS and the looper's phone or the command could be rejected by the looper's app
    * **Trio v0.6 or newer** an APNS response is returned to *LoopFollow*
        * A success or failure message is pushed back to the *LoopFollow* phone from the *Trio* phone when a remote command is received and handled
    * The results show up in *Nightscout* after being uploaded from the *Loop*/*Trio* phone
    * The results are plotted or displayed in *LoopFollow* after being downloaded from the *Nightscout* URL as a new treatment
    * APNS keys do not need to be embedded in the *Nightscout* site
        * This simplifies configuration of *Nightscout*, especially for those who use a paid service for *Nightscout*
* For those following a looper using *Trio* 0.2.x, the only option for the Remote Setting is *Nightscout*, which uses Careportal
    * With this selection, the *LoopFollow* phone sends commands to *Nightscout*, which then sends commands to the *Trio* phone
    * For that reason, the *Nightscout* display will be updated first
        * If there is an issue sending the careportal request from *Nightscout*, it might not make it to the *Trio* phone
        * After the next download from *Nightscout*, the display will update if commands do or do not make it through the full round trip

