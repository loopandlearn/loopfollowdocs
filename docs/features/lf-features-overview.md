
🚧 Documentation Under Construction 🚧

<!--todo-->
<!--Notes: be sure to add this info

-->

## *LoopFollow* Features

Most features are self-explanatory. Use the [Settings Screen](../setup/lf-setup.md#settings-screen){: target="_blank" } to navigate to the appropriate section to adjust the app settings.

Some features require more explanation. 

- - -

## Toolbar Tab Customization

The toolbar at the bottom of the *LoopFollow* screen supports up to 5 tabs, but there are 6 options that could be placed there. With version 3.1, the tab display is now customizable.

Historically the 5 tabs were:

* tab 1: Home
* tab 2: Alarms or Remote Control
* tab 3: Snoozer
* tab 4: Nightscout site
* tab 5: Settings

The updated design is that tabs 2 and 4 are optional and tab 5 can be either settings or the hellip; More icon.

The new arrangement is:

* tab 1: Home
* tab 2: Configurable
* tab 3: Snoozer
* tab 4: Configurable
* tab 5: Configurable (Settings or hellip; More)

These options can be placed in the toolbar for rapid access in your choice of tab 2, tab 4, the More Menu or Hidden:

* Alarms
* Remote
* Nightscout site

![Several tab selections](img/lf-tab-custom.svg){width="700"}
{align="center"}


- - -

## Background Refresh Settings

LoopFollow has traditionally provided an option to play a silent audio as a trick to allow it to wake up when in the background or when the phone is locked. This has several drawbacks including battery drain and limited reliability.

With LoopFollow version 2.2.9 or higher, an additional method is provided using an external device to provide a heartbeat. This can be a radiolink device, if you have one available, or a used Dexcom Transmitter (G5/ G6/ ONE/ Anubis) or Sensor (G7/ ONE+). The batteries on Dexcom devices continue to provide power to the Bluetooth system, giving a heartbeat at about 5 minute intervals. The radiolink devices provide a heartbeat every minute.

For more information, see the Bluetooth Heartbeat section.

- - -

## Real-Time Watch Updates using Contact

Updated Method for Watch Display of Real Time Glucose
Follow your Looper’s BG value in real time on your Apple watch by adding a complication! Note: a new method is required because old “calendar” method no longer works for iOS 18. You must have LoopFollow v2.2.8 or newer to use this method.

Features include:

Options for delta value or arrow
Dynamic font size

Step-by-Step Instructions to Set Up LoopFollow Contact Complication on Your Apple Watch
Video, How to add a complication for real-time watch display

Bullet List with Instructions:

Enable BG Updates in Loop Follow
Open the Loop Follow app on your iPhone
Go to Settings > Integrations > Contact
Toggle on “Enable Contact BG Updates”
If a permission prompt appears, tap “Allow” to let Loop Follow access your contacts
(The app will automatically create a contact named LoopFollow – BG for you.)
Open the Watch App
On your iPhone, open the Watch app
Tap “My Watch” at the bottom, if it isn’t already selected
Choose a Watch Face
Scroll down and tap “Face Gallery” or choose an existing watch face under My Faces
Pick a watch face that supports complications (e.g., Infograph Modular or Modular)
Customize the Complications
Tap the watch face you selected to edit its settings
Find a Complication slot where you want the glucose contact to appear
Select the slot, select the ‘Contacts’ complication, select ‘More…’, scroll through the contacts, and choose LoopFollow – BG
Save Your Watch Face
Tap “Add” or “Set as Current Watch Face” to apply the changes
Check your Apple Watch to confirm the LoopFollow – BG complication is showing your glucose data
(OPTIONAL) If you follow more than one Looper
Repeat these steps. You can follow up to 3 Loopers using the various LoopFollow-1….-3 builds
Each contact will have a distinct name and show up with a different color on your watch face
You’re ready to monitor your glucose data directly on your Apple Watch!


- - -

## Remote Control with *LoopFollow*

There are separate pages for the 3 different remote control options. (No page is provided if `None` is selected).

The table below indicates the options for Remote Control and includes the minimum token access for each option.

* The *Loop* Remote Control option will be available in the `dev` branch as soon as [PR 434](https://github.com/loopandlearn/LoopFollow/pull/434) is approved and merged

| *LoopFollow* Remote Type | Minimum Token Access| *LoopFollow* Status |
|:--|:--|:--|
| **None** | Read | OK (Read) |
| ***Nightscout*** | Read & Careportal | OK (Read & Write) |
| **Loop Remote Control** <br>- in development| Read | OK (Read) |
| **Trio Remote Control** <br>- Trio 0.5.x or newer | Read | OK (Read) |

