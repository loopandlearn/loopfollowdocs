
!!! tip "Pro Tip: Frequent Glucose Alerts"
    If you are experiencing audible and visible glucose alerts every single minute, disable the *LoopFollow* > Settings > General > Persistent Notifications slider.

    Note: this is completely different from the persistent notifications you may want enabled to see APNS messages returned from real-time responses to remote commands.

- - -

## Why do I keep getting "App inactive for X minutes. Open to resume."? { #app-inactive-silent-tune }

This happens when *LoopFollow* isn't able to stay running in the background as intended. When *LoopFollow* is configured to use the *Silent Tune* method (playing silent audio to stay alive), the notification fires if that silent audio gets interrupted and the app becomes inactive.

A common reason is that another app temporarily takes control of audio — for example the iPhone alarm or apps like Microsoft Teams. While that other app holds the audio session, *LoopFollow* can't keep itself alive in the background. If it's just temporary, you can simply tap the notification to reopen the app and it will resume normally.

Another reason is if the app has been manually closed (swiping it away from the app switcher). In that case, the background activity stops completely, including *Silent Tune*, and the app needs to be opened again.

- - -

## Why do I keep getting "App inactive for X minutes. Verify Bluetooth connectivity."? { #app-inactive-bluetooth }

This happens when *LoopFollow* isn't able to stay running in the background as intended. When *LoopFollow* is configured to use a Bluetooth heartbeat (RileyLink, Dexcom, or Omnipod Dash), it relies on regular Bluetooth signals from that device to wake itself up in the background. The notification fires when those signals stop arriving for several minutes.

Common reasons:

* **The Bluetooth device is out of range.** The phone and the heartbeat device need to stay within Bluetooth range — typically a few meters and worse through walls.
* **Bluetooth is turned off** on the phone, or the phone is in Airplane Mode without Bluetooth re-enabled.
* **The Bluetooth device has a low or dead battery.** RileyLink-style devices and expired Dexcom transmitters/sensors keep working only as long as their internal battery has enough power to advertise.

If the connection comes back on its own, the alert will stop. If it does not, check Bluetooth on the phone, move closer to the heartbeat device, and consider whether the device's battery has run out.

- - -

## Version Compatibility

This section consolidates version requirements for *LoopFollow* to work with *Loop* and *Trio*, and provides historical context for how remote control has evolved.

It also lists updates to the method for using Browser Build.

### *LoopFollow* Version 6.0 and newer

With the addition of Live Activity to *LoopFollow*, the build directions for browser build were updated.

* If you use Browser Build, your automatic build will fail until you add the new Identifier, create the `LoopFollow App Group` and include the `LoopFollow App Group` in the capabilities for the *LoopFollow* Identifiers.
* Instructions start here: [Add LoopFollow App Group](../build/lf-browser-build.md#create-app-group){: target="_blank" } 

### *LoopFollow* and *Loop* Compatibility

| Feature | Minimum Versions Required |
|:--|:--|
| *Loop* Remote Control via APNS | *LoopFollow* 3.2 or newer; any version of *Loop* |
| Real-time APNS response from *Loop* phone | *LoopFollow* 4.6 or newer; *Loop* v3.11.1 or newer |

With *LoopFollow* 3.2 and newer, *Loop* remote commands include Meal, Bolus and Override control. *LoopFollow* no longer requires the *Nightscout* site to be configured with the APNS credentials — Read access for the *Nightscout* URL is sufficient.

With *LoopFollow* 3.1 and older, *Loop* remote commands were limited to Overrides, required the *Nightscout* site to be configured with the APNS credentials, and required a token with `careportal` access.

### *LoopFollow* and *Trio* Compatibility

!!! important "Breaking Change: *Trio* Remote Command Users"
    *Trio* users must have matching versions of *LoopFollow* and *Trio* for remote control to work.

    * *Trio* 0.6 (or newer) requires *LoopFollow* 4.0 (or newer)
    * *Trio* 0.5.1.28 (or older) requires *LoopFollow* 3.2.11 (or older)

    Remote control commands stop working if versions are not matched. You do **not** need to reconfigure your credentials when upgrading — your existing settings continue to work. However, *LoopFollow* Browser Build users must update their Identifiers when upgrading from v3.x: see [Legacy: Updating from v3.x](../build/lf-browser-build.md#legacy-updating-from-v3x){: target="_blank" }.

| Feature | Minimum Versions Required |
|:--|:--|
| *Trio* Remote Control via APNS | *LoopFollow* 4.0 or newer; *Trio* 0.6 or newer |
| Real-time APNS response from *Trio* phone | *LoopFollow* 4.0 or newer; *Trio* 0.6 or newer |
| *Nightscout* OpenAPS pill display | *Nightscout* 15.0.2 or newer with *Trio* 0.5.x or newer |

!!! note "*Nightscout* Careportal Remote Commands Removed"
    As of *LoopFollow* 6.x, *Nightscout* remote commands are no longer supported in *LoopFollow*. To remotely control *Trio* you must run *Trio* 0.5.x or newer and use *Trio* Remote Control (TRC) via APNS.

### APNS Keys Do Not Need to Be in Nightscout

With *LoopFollow* 3.2 and newer, the APNS credentials are entered directly in the *LoopFollow* app. They do **not** need to be embedded in the *Nightscout* site for remote control to work. This simplifies *Nightscout* configuration, especially for those using a paid *Nightscout* service.

The APNS credentials only need to be in *Nightscout* if you also use *Nightscout* Careportal or the *LoopCaregiver* app to send remote commands.

## *LoopFollow* Feature History

The feature history is summarized below in reverse chronological order.

| *LoopFollow* Version | Feature Added |
|:--|:--|
| 6.x | *Nightscout* Careportal remote commands removed; remote control is exclusively via direct APNS to *Loop* or *Trio* |
| 6.0 | Live Activity added - must use LoopFollow App Group to build<br>see [Add LoopFollow App Group](../build/lf-browser-build.md#create-app-group){: target="_blank" } |
| 4.6 | Real-time APNS notifications returned from the *Loop* phone (requires *Loop* v3.11.1 or newer) |
| 4.3 | Separate QR codes for *Nightscout* Site, Dexcom Share, Remote Settings, and Alarm Settings |
| 4.0 | *Trio* 0.6 remote control support; share remote configuration via QR code |
| 3.2 | *Loop* remote commands (Meal, Bolus, Override) sent directly via APNS; APNS credentials no longer required in *Nightscout* |
