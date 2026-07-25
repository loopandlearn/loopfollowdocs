- - -

## New Feature Highlights

### Version 7.0.0

!!! tip ""
    New with *LoopFollow* v7.0.0:

    * Requires iOS 18 or newer
    * A [first-run onboarding guide](../setup/lf-setup.md#the-onboarding-guide){: target="_blank" } walks new users through setup; system permissions are requested only when first needed
    * A [status banner](../setup/lf-features.md#status-banner){: target="_blank" } explains Nightscout, Dexcom Share, and heartbeat problems instead of silently showing no data
    * [Custom alarm sounds](../setup/lf-features.md#custom-sounds){: target="_blank" } — use your own audio files as alarm tones
    * [Skip options](../setup/lf-features.md#skip-options){: target="_blank" } keep Low/High BG alarms silent while glucose is already correcting, and the phone battery alarm silent while charging
    * The [predictive Low BG alert](../setup/lf-features.md#predictive-low-alert){: target="_blank" } now works for *Trio* (watching all four forecast lines) and is fixed for *Loop*
    * New [*Nightscout* Database Size](../setup/lf-setup.md#information-display){: target="_blank" } information row and alarm
    * [Color thresholds](../setup/lf-setup.md#color-thresholds){: target="_blank" } for Information Display rows
    * Search added to the alarms list, the Add Alarm sheet, and the [Menu](../setup/lf-setup.md#menu-screen){: target="_blank" }
    * [APNS credentials can be exported/imported](../setup/lf-setup.md#importexport){: target="_blank" } via QR code
    * The [Live Activity](../setup/lf-setup.md#live-activity){: target="_blank" } and the [remote control](../remote/remote-control-trio.md#overrides){: target="_blank" } screens show the active override or temp target with its remaining time
    * Graph updates:
        * All graphs rebuilt on native Swift Charts
        * Dragging on the small graph moves the main chart in real time
    * Rec. Bolus is shown using the pump's bolus increment

### Version 6.2

!!! tip ""
    New with *LoopFollow* v6.2:

    * [WebSocket](../setup/lf-setup.md#websocket){: target="_blank" }, enabled by default, allows near real-time updates from Nightscout
    * [Show Yesterday's BG](../setup/lf-setup.md#graph){: target="_blank" } can be enabled using Settings: Graph
    * [Information Display](../setup/lf-setup.md#information-display){: target="_blank" } supports large fonts; when needed, the label and value are split into two rows
    * Remote Quick Pick buttons are now available for [Loop](../remote/remote-control-loop.md#quick-pick-boluses-and-meals){: target="_blank" } and [Trio](../remote/remote-control-trio.md#quick-pick-boluses-and-meals){: target="_blank" } 
    * Handle glucose duplicates to fix delta glucose always showing zero
    * Fix glucose history being truncated when multiple apps upload to the same account
    * Improve auto-restart for Live Activity
    * Suppress an audible banner that could sound during silent Live Activity renewal
    * Improve handling of profiles from Nightscout, including a new Run Diagnostics button in Remote Settings that detects common remote-command failures
    * Debug logging is now on by default, and Share Logs prompts for a short problem description that is bundled with the logs
    * Trio Updates:
        * Trio Remote Control is the only option offered for Trio (Nightscout option is removed)
        * Trio forecast cone display truncated to match Trio method
        * Trio forecast lines match Trio colors
        * Trio Override / Temp Target display colors match Trio colors

### Versions 6.0 and 6.1

!!! tip ""
    New with *LoopFollow* v6.0 and v6.1:
    
    * Live Activity and Live Activity upgrades
    * More accurate statistics with user choice of range
    * Smarter unit handling
    * Fixes for alarms, the graphs, and the remote-command UI
    * Settings rows updated for clarity
    * For Trio users: choice of cone of uncertainty or forecast lines

### Version 5.0

!!! tip ""
    New with *LoopFollow* v5.0:
    
    * [Menu Screen](../setup/lf-setup.md#menu-screen){: target="_blank"}
    * [Treatments](../setup/lf-features.md#treatments){: target="_blank"}
    * [Statistics](../setup/lf-features.md#statistics){: target="_blank"} 

- - -

## *LoopFollow* Feature History

The feature history is summarized below in reverse chronological order.

| *LoopFollow* Version | Feature Added |
|:--|:--|
| 7.0 | Requires iOS 18 or newer; first-run onboarding guide; graphs rebuilt on native Swift Charts |
| 6.2 | WebSocket for near real-time *Nightscout* updates; Quick Pick remote buttons; Run Diagnostics for remote setup |
| 6.1 | Live Activity requires APN credentials<br>see [APN Settings](../setup/lf-setup.md#apn){: target="_blank" } |
| 6.0 | Live Activity added - Browser Builders must use LoopFollow App Group to build<br>see [Browser Build: Add LoopFollow App Group](../build/lf-browser-build.md#create-app-group){: target="_blank" } |
| 4.6 | Real-time APNS notifications returned from the *Loop* phone (requires *Loop* v3.11.1 or newer) |
| 4.3 | Separate QR codes for *Nightscout* Site, Dexcom Share, Remote Settings, and Alarm Settings |
| 4.0 | *Trio* 0.6 remote control support; share remote configuration via QR code |
| 3.2 | *Loop* remote commands (Meal, Bolus, Override) sent directly via APNS; APNS credentials no longer required in *Nightscout* |

- - -

## APNS Keys Do Not Need to Be in Nightscout

With *LoopFollow* 3.2 and newer, the APNS credentials are entered directly in the *LoopFollow* app. They do **not** need to be embedded in the *Nightscout* site for remote control to work. This simplifies *Nightscout* configuration.

The APNS credentials only need to be in *Nightscout* if you also use *Nightscout* Careportal or the *LoopCaregiver* app to send remote commands.

- - -

## Version Compatibility

This section consolidates version requirements for *LoopFollow* to work with *Loop* and *Trio*, and provides historical context for how remote control has evolved.

It also lists updates to the method for using Browser Build.

### *LoopFollow* Version 6.1 and newer

After testing *LoopFollow* Live Activity in version 6.0.0 and doing extensive research, it became clear that Live Activity with *LoopFollow* is not reliable without the use of Apple Push Notification credentials.

This means that if you want to use Live Activity with *LoopFollow*, you need to create those credentials and enter them in *LoopFollow* [APN Settings](../setup/lf-setup.md#apn){: target="_blank" }.

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

    Remote control commands stop working if versions are not matched. You do **not** need to reconfigure your credentials when upgrading — your existing settings continue to work. However, *LoopFollow* Browser Build users had to update their Identifiers when upgrading from v3.x to add Push Notification capability. This is automatic when running Add Identifiers.

| Feature | Minimum Versions Required |
|:--|:--|
| *Trio* Remote Control via APNS | *LoopFollow* 4.0 or newer; *Trio* 0.6 or newer |
| Real-time APNS response from *Trio* phone | *LoopFollow* 4.0 or newer; *Trio* 0.6 or newer |
| Nightscout Careportal (Temp Targets only) | Available for all *Trio* versions |
| *Nightscout* OpenAPS pill display | *Nightscout* 15.0.2 or newer with *Trio* 0.5.x or newer |

#### Very Old Configurations

The information below is of historical interest only.

With *Trio* 0.2.x, *LoopFollow* only supported Temp Targets via the *Nightscout* Careportal, which required a token with `careportal` access. Once updated to *Trio* 0.5.x or newer, the full *Trio* Remote Control options are available.

For those following a looper using *Trio* 0.2.x, the only remote setting option in *LoopFollow* is *Nightscout* (Careportal). With this selection:

* The *LoopFollow* phone sends commands to *Nightscout*, which then forwards commands to the *Trio* phone
* The *Nightscout* display will be updated first
* If there is an issue sending the Careportal request, it might not reach the *Trio* phone
* After the next *Nightscout* download, *LoopFollow* display will reflect whether commands completed the full round trip

