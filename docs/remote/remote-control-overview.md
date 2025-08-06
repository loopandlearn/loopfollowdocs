🚧 Documentation Under Construction 🚧

## Remote Control Overview

You must configure *LoopFollow* and, in some cases, the *Nightscout* URL, to use remote commands, which requires credentials for the [Apple Push Notification System (APNS)](#apple-push-notifications-system-apns).

!!! abstract "Remote Control Updates in Development"
    The instructions in this section are subject to updates as changes are made to the *Trio* app and the *LoopFollow* app.

    * With *LoopFollow* 3.1.0 and earlier:
        * If you are using *Trio* 0.2.x or *Loop* 3.x, remote commands are routed via Nightscout
        * If you are using *Trio* 0.5.x or newer, remote commands are sent directly through APNS
    * Once *LoopFollow* 3.2.0 is released (currently being tested in `dev` branch):
        * If you are using *Trio* 0.2.x, remote commands are routed via Nightscout
        * If you are using *Loop* 3.x or newer, remote commands are sent directly through APNS
        * If you are using *Trio* 0.5.x or newer, remote commands are sent directly through APNS

    > Using APNS directly from *LoopFollow* provides faster feedback about commanding

* *Nightscout* Remote Command in *LoopFollow* makes the standard Careportal options easily available from inside the *LoopFollow* app
    * With this selection, the *LoopFollow* phone sends commands to *Nightscout* which then sends commands to the *Loop*/*Trio* phone
    * For that reason, the *Nightscout* display will be updated first
        * If there is an issue sending the careportal request from *Nightscout*, it might not make it to the *Loop*/*Trio* phone
        * After the next download from *Nightscout*, the display will update if commands do or do not make it through the full round trip
* *Loop* Remote Command (for *LoopFollow* dev only) and *Trio* Remote Command features use APNS 
    * With this selection, successful commands go directly via APNS to the *Loop*/*Trio* phone
    * The results show up in *Nightscout* after being uploaded from the *Loop*/*Trio* phone
    * The results are plotted or displayed in *LoopFollow* after being downloaded from the *Nightscout* URL as a new treatment

- - -

## *LoopFollow* Remote Options

### Remote Options: 3.1.0

The graphic below shows the top portion of the Remote Settings screen when None, `Nightscout` or `Trio Remote Control` is selected. This graphic is for *LoopFollow* 3.1.0 or earlier.

![LoopFollow remote options - all types](img/lf-remote-options.svg){width="400"}
{align="center"}

### Remote Options: Under Development

The graphic below is from the `dev` branch of *LoopFollow*. You must first enter a *Nightscout* URL before any remote options are offered and then only the option suitable for that *Nightscout* site can be selected.

* When following someone running Loop, the options are None or [Loop Remote Control](remote-control-loop.md){: target="_blank" }
* When following someone running Trio, the options are None or:
    * Trio 0.5.x and newer: [Trio Remote Control](remote-control-trio.md){: target="_blank" }
    * Trio 0.2.x: [Nightscout Remote Control](remote-control-nightscout.md#loopfollow--careportal-with-the-trio-app){: target="_blank" }

![LoopFollow remote options - all types](img/lf-remote-options_3.2.svg){width="600"}
{align="center"}



### Critical Configuration Information

If you plan to use the [*Apple* Push Notifications System (APNS)](#apple-push-notifications-system-apns), follow that link for instructions to find or create your keys.

If you are using a *Trio* *Nightscout* URL, be aware:

* If the user of the *Trio* app disables Remote Control and their *Trio* phone, then *LoopFollow* remote commands will be issued but not enacted

Depending on the selection you made, continue to one of these pages for more information on how to configure *LoopFollow* for that remote control option.

* [*Loop* Remote Control](remote-control-loop.md)
* [*Trio* Remote Control](remote-control-trio.md)
* [*Nightscout*](remote-control-nightscout.md)

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

Note that the `LOOP_DEVELOPER_TEAM_ID` is the Apple Developer ID used to build the *Loop* app.

If you are configuring for *Trio* remote control with *LoopFollow*, you do not need to enter the Apple Developer ID explicitly because is is included in the information *Trio* uploads to *Nightscout*.

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

* [*Loop* Remote Control](remote-control-loop.md) (*LoopFollow* dev branch only)
* [*Trio* Remote Control](remote-control-trio.md)
* [*Nightscout*](remote-control-nightscout.md)
