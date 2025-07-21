🚧 Documentation Under Construction 🚧

## Remote Control Overview

You must configure *LoopFollow* and the *Nightscout* URL to use remote commands. 

* *Nightscout* Remote Command in *LoopFollow* makes the standard Careportal options easily available from inside the *LoopFollow* app
    * With this selection, the *LoopFollow* phone sends commands to *Nightscout* which then sends commands to the *Loop*/*Trio* phone
    * For that reason, the *Nightscout* display will be updated first
        * If there is an issue sending the careportal request from *Nightscout*, it might not make it to the *Loop*/*Trio* phone
        * After the next download from *Nightscout*, the display will update if commands do or do not make it through the full round trip
* *Loop* and *Trio* Remote Command features use the [Apple Push Notification System (APNS)](#apple-push-notifications-system-apns)
    * With this selection, successful commands go directly through APNS
    * The results show up in *Nightscout* after being uploaded from the *Loop*/*Trio* phone
    * The results are plotted or displayed in *LoopFollow* after being downloaded from the *Nightscout* URL as a new treatment

- - -

## *LoopFollow* Remote Options

The graphic below shows the top portion of the Remote Settings screen when None, `Nightscout` or `Trio Remote Control` is selected. The choice for `Loop Remote Control` is in development and this graphic will be updated once it is available in the `dev` branch.

![LoopFollow remote options - all types](img/lf-remote-options.svg){width="400"}
{align="center"}

### Critical Configuration Information

If you plan to use the [*Apple* Push Notifications System (APNS)](#apple-push-notifications-system-apns), follow that link for instructions to find or create your keys.

If you are using a *Trio* *Nightscout* URL, be sure to read about [*Trio* Remote Control](#trio-remote-control) on this page. 

* If the user of the *Trio* app disables Remote Control, then *LoopFollow* remote commands will be issued but not enacted

Depending on the selection you made, continue to one of these pages for more information on how to configure *LoopFollow* for that remote control option.

* [*Nightscout*](remote-control-nightscout.md)
* [*Loop* Remote Control](remote-control-loop.md)
* [*Trio* Remote Control](remote-control-trio.md)

- - -

## *Trio* Remote Control

> The graphics displayed on this page are associated with *Trio* version 0.5.x or newer. The same setting is available in older version of *Trio* but in a different location in the menu structure.

**Default:** _OFF_

Remote control must be enabled on the *Trio* phone or no remote information is accepted by the *Trio* phone.

> You can search for this screen in *Trio* settings or go through the sequence: Trio, Settings, Features, Remote Control.

Once Remote Control is enabled, a Shared Secret is available. This is only used if you want to use *Trio* Remote Control with *LoopFollow*.

The graphic below is on the *Trio* phone:

![Trio remote control settings](img/trio-enable-remote-control.png){width="300"}
{align="center"}

When Remote Control is enabled on the *Trio* app and the *LoopFollow* phone is properly configured, you can add carbs, send boluses, set or cancel overrides or temporary targets from the *LoopFollow* phone to the *Trio* phone via *Apple* push notifications.

The `SHARED SECRET` should be copied from the *Trio* phone and added to the [`Shared Secret`](#shared-secret) row of the *LoopFollow* Remote Settings screen as part of the configuration for using *LoopFollow*.

!!! warning "Important"
    The ability for the *Trio* app to be remotely controlled will be **disabled** when `Enable Remote Control` is turned OFF on the *Trio* phone, even if you have *LoopFollow* configured with the correct shared secret or your *Nightscout* URL has Careportal access. This is for the protection of the *Trio* user, so that they **always** are the primary controller of their insulin dosing app.

- - -

## *Apple* Push Notifications System (APNS)

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

Note that the `LOOP_DEVELOPER_TEAM_ID` is the Apple Developer ID (TEAMID) used to build the *Loop* app.

### New APNS

When using *Trio*, you do not need to add the config vars to *Nightscout* that are required for *Loop* remote control. If you already have them, it doesn't hurt anything, but you do not need to add them to use remote control with Trio.

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
    - Either click on the blue **`Create a new key`** button **OR** the plus button (<font color="#2997FF">:material-plus-circle:</font>)  to add a new key.
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

## Next Step

Depending on the selection you made, continue to one of these pages for more information on how to configure *LoopFollow* for your desired remote control option.

* [*Nightscout*](remote-control-nightscout.md)
* [*Loop* Remote Control](remote-control-loop.md)
* [*Trio* Remote Control](remote-control-trio.md)
