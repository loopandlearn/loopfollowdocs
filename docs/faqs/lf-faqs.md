## Why do Notifications vanish before I can read them?

You need to modify your iPhone settings to make the banners persistent.

In iPhone Settings, select Notifications, then Apps and then *LoopFollow*.

For the banner style, select Persistent. Then each notification remains visibile until you swipe up.

This also means that the current banner might be out of date if you haven't looked at your phone for a while.

- - -

## Why do I get audible and visible glucose alerts every single minute?

If you are experiencing audible and visible glucose alerts every single minute, disable the *LoopFollow* > Settings > General > Persistent Notifications slider.

Note: this is completely different from the persistent notifications you may want enabled to see APNS messages returned from real-time responses to remote commands.


- - -

## Does using DASH as a Background App Refresh Type increase Pod failure rate?

No, it shouldn't.

What is happening under the hood: when you pick Dash as your heartbeat, LoopFollow connects to the pod's normal BLE service and just listens in on the same notifications Loop/Trio is already getting. It's not poking the pod or asking it for anything extra — it's eavesdropping on traffic that is happening anyway.

Because both apps, LoopFollow + (Trio or Loop), are on the same phone, iOS only opens one actual BLE connection to the pod and shares it between them. So from the pod's perspective there is just one controller talking to it, same as always. Whether one app is listening or two, the pod is doing the exact same radio work.

LoopFollow tagging along should be not affect the battery at all.

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
