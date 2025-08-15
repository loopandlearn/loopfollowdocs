🚧 Documentation Under Construction 🚧

## Remote Control Overview

*LoopFollow* remote commands are sent directly using the [Apple Push Notification System (APNS)](#apple-push-notifications-system-apns) for all Open-Source Automated Insulin Delivery systems that support this feature. At this time, the *Loop* app and the open beta version of the *Trio* app (0.5.x or newer) support direct APNS from *LoopFollow*.

!!! tip "`Loop` Remote Control with *LoopFollow* 3.2"
    With the release of *LoopFollow* 3.2, the remote control features accessible from LoopFollow match those available from the *LoopCaregiver* app.

    You must update to *LoopFollow* 3.2 or newer and configure remote settings in the *LoopFollow* app to use these features.


### Changes for *LoopFollow* Remote Control of the *Loop* App

* With *LoopFollow* 3.2 and newer
    * *Loop* remote commands from *LoopFollow* include Meal, Bolus and Override control
        * *LoopFollow* no longer requires the *Nightscout* site be configured with the APNS credentials
        * Read access for the *Nightscout* URL is sufficient
* With *LoopFollow* 3.1 and older
    * *Loop* remote commands are limited to Overrides, require the *Nightscout* site be configured with the APNS credentials and require a token with `careportal` access

> With *Trio* 0.2.x, *LoopFollow* only supports temp targets and requires a token with `careportal` access. Once updated to *Trio* 0.5.x or newer, the full Trio Remote Control options are available.

!!! abstract "Remote Control Updates in Development"
    The instructions in this section depend on the version of the *Trio* app and the *LoopFollow* app.

    * With *LoopFollow* 3.2 or newer:
        * Remote commands are sent directly through APNS for both the *Loop* app and the *Trio* open beta version
            * If you are using *Trio* 0.2.x, remote commands are routed via *Nightscout* and are limited to modifying `Temp Targets`
    * With *LoopFollow* 3.1 and earlier:
        * Using the *Loop* app:
            * remote commands are routed via *Nightscout*
            * Only Overrides can be modified using *LoopFollow* and only if *Nightscout* site has the APNS keys embedded
        * Using the *Trio* app
            * If you are using *Trio* 0.5.x or newer, remote commands are sent directly through APNS
            * If you are using *Trio* 0.2.x, remote commands are routed via *Nightscout*

    > Using APNS directly from *LoopFollow* provides faster feedback about commanding.
    
    > With *LoopFollow* 3.2, APNS keys will not need to be embedded in the *Nightscout* site for remote control of the *Loop* app from *LoopFollow*, which may simplify configuration for those who use a paid service for *Nightscout*.

### *LoopFollow* Remote Control

* *LoopFollow* Remote Control send messages to the loopers phone using APNS
    * Requires *LoopFollow* 3.2 or newer to use with the *Loop* app (version 3.x)
    * Requires *Trio* 0.5 or newer for the *Trio* app
    * Commands go via APNS to the *Loop*/*Trio* phone
        * An immediate success or failure for sending the message to APNS is recieved
        * There still could be a communication failure between APNS and the looper's phone or the command could be rejected by the looper's app
    * The results show up in *Nightscout* after being uploaded from the *Loop*/*Trio* phone
    * The results are plotted or displayed in *LoopFollow* after being downloaded from the *Nightscout* URL as a new treatment
    * APNS keys do not need to be embedded in the *Nightscout* site
        * This simplifies configuration of *Nightscout*, especially for those who use a paid service for *Nightscout*
* For those following a looper using *Trio* 0.2.x, the only option for the Remote Setting is *Nightscout*, which uses Careportal
    * With this selection, the *LoopFollow* phone sends commands to *Nightscout*, which then sends commands to the *Trio* phone
    * For that reason, the *Nightscout* display will be updated first
        * If there is an issue sending the careportal request from *Nightscout*, it might not make it to the *Trio* phone
        * After the next download from *Nightscout*, the display will update if commands do or do not make it through the full round trip

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

If you plan to use the [*Apple* Push Notifications System (APNS)](#apple-push-notifications-system-apns), follow that link for instructions to find or create your keys.

If you are using a *Trio* *Nightscout* URL, be aware:

* If the user of the *Trio* app disables Remote Control on their *Trio* phone, then *LoopFollow* remote commands will be issued but not enacted

Depending on the selection you made, continue to one of these pages for more information on how to configure *LoopFollow* for that remote control option.

* [*Loop* Remote Control](remote-control-loop.md)
* [*Trio* Remote Control](remote-control-trio.md)
* [*Nightscout*](remote-control-nightscout.md)

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

* Once *LoopFollow* 3.2 is released, the addition of those `config` variables in *Nightscout* is only required to support sending remote commands from *Nightscout* `Careportal` and from *LoopCaregiver*.
* *LoopFollow* 3.2 and newer versions only require the APNS credentials to be entered in the *LoopFollow* app for both the *Loop* and *Trio* Remote Control features.

If you are configuring for *Trio* remote control with *LoopFollow*, you do not need to enter the Apple Developer ID explicitly because it is included in the information *Trio* uploads to *Nightscout*.

### New APNS

When using *Trio*, you do not need to add the config vars to *Nightscout* that are required for *Loop* remote control from *Nightscout* `Careportal` and *LoopCaregiver*. If you already have them, it doesn't hurt anything, but you do not need to add them to use remote control with *Trio*. 

Once *LoopFollow* 3.2 is released, the config vars will not need to be embedded in *Nightscout* for *Loop* Remote Control from *LoopFollow*.

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
* [*Nightscout*](remote-control-nightscout.md)
