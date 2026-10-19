## Apple Watch

*LoopFollow* includes an *Apple Watch* app. It shows the same glucose information as the *LoopFollow* app on your *iPhone*, adds glucose to your watch face, and can send [remote commands](../remote/remote-control-overview.md) to *Loop* or *Trio*.

The watch gets all of its information from *LoopFollow* on the paired *iPhone*. It does not connect to *Nightscout* or *Dexcom* by itself, and it does not store any passwords or keys. For current data, *LoopFollow* must be running on the *iPhone* and the watch must be connected to that *iPhone*.

!!! info "Requirements"
    * An *Apple Watch* paired with the *iPhone* that runs *LoopFollow*
    * watchOS 10 or newer (Apple Watch Series 4 or newer)

### Install the Watch App

The watch app comes with *LoopFollow*. If it does not appear on your watch after you install or update *LoopFollow*, open the *Watch* app on your *iPhone*, scroll to *Available Apps* and tap *Install* next to *LoopFollow*.

## Using the Watch App

Turn the Digital Crown, or swipe up and down, to move between the three pages.

### Glucose

| Following *Loop* (mg/dL) | Following *Trio* (mmol/L) |
|:--:|:--:|
| ![LoopFollow watch glucose page following Loop](img/watch-glucose-loop.png){width="200"} | ![LoopFollow watch glucose page following Trio](img/watch-glucose-trio.png){width="200"} |

* The latest glucose value with its trend arrow and the change since the previous reading
    * Colors follow the *LoopFollow* settings on your *iPhone*: green in range, yellow high, red low, or white when *Color BG Text* is off
    * The value is struck through when the latest reading is 12 minutes old or more
* Top left: insulin on board (IOB)
* Top right: minutes since the latest reading; an orange *iPhone* symbol means the watch cannot reach the *iPhone* right now
* Carbs on board (COB) and the time since *Loop* or *Trio* last reported
    * *Not looping* is shown in red when the loop has not reported for 15 minutes
* A graph of the last two hours
* Buttons for remote commands at the bottom, see [Remote Commands](#remote-commands)

When an alarm is sounding on the *iPhone*, its name is shown at the top of the page. Tap it to snooze the alarm on the *iPhone*. The watch app has no alarms of its own.

### Graph

![LoopFollow watch graph page](img/watch-graph-trio.png){width="200"}
{align="center"}

The graph shows readings, boluses (blue triangles), carbs (orange dots) and the prediction in the same colors as the *iPhone*. Tap the graph to switch between 1, 3, 6, 12 and 24 hours.

### Info

A list of the values from the *iPhone* information table, such as basal rate, target, ISF, carb ratio, pump reservoir, batteries and sensor and cannula age. Rows without data are hidden.

## Complications

You can add *LoopFollow* to your watch face. Edit the watch face, choose a complication slot and pick *LoopFollow*. All sizes show glucose, trend and the minutes since the reading; the rectangular size also shows a two-hour graph.

watchOS decides how often complications refresh, so a complication can lag behind the watch app. Always check the minutes shown next to the value.

## Remote Commands

!!! warning "Not medical advice"
    Remote commands can deliver insulin. Use them the same way you would from the *iPhone*, and follow the guidance of your diabetes care team.

The buttons on the glucose page send the same commands as the *LoopFollow* remote screens on the *iPhone*. They appear when [Loop Remote Control](../remote/remote-control-loop.md) or [Trio Remote Control](../remote/remote-control-trio.md) is set up in *LoopFollow*.

| Button | What it does |
|:--|:--|
| Overrides (left) | Start one of the override presets, or cancel the active override |
| **+** (middle) | Meal or Bolus |
| Temp Target (right) | *Trio* only: start one of the temp target presets saved in *LoopFollow*, or cancel the active temp target |

### Bolus

| Choose an amount | Confirm with the Digital Crown |
|:--:|:--:|
| ![LoopFollow watch bolus choices](img/watch-bolus.png){width="200"} | ![LoopFollow watch bolus confirmation](img/watch-bolus-confirm.png){width="200"} |

* *Recommended* shows the recommendation from *Loop* or *Trio*, as on the *iPhone*. It is hidden when it is 12 minutes old or more, and you are warned when it is 5 minutes old or more.
* The amounts below are your *LoopFollow* Quick-Pick boluses.
* *Other Amount* lets you set any amount with the Digital Crown, up to the *Max Bolus* in *LoopFollow*.

### Meal

![LoopFollow watch meal entry](img/watch-meal.png){width="200"}
{align="center"}

* The rows at the top are your *LoopFollow* Quick-Pick meals.
* Set carbs with the Digital Crown.
* Tap the row below carbs to add a time (from 2 hours ago to 1 hour ahead) and, for *Trio*, fat, protein and a bolus when *Meal with Fat/Protein* and *Meal with Bolus* are turned on in the *LoopFollow* *Remote Settings*.
* For *Loop*, the watch sends carbs only, with an absorption time of 3 hours.

### Safety Checks

* Anything that delivers insulin needs a full turn of the Digital Crown to confirm. The watch must have a passcode, *Wrist Detection* must be on, and the watch must be unlocked on your wrist.
* The *iPhone* checks every command against the same limits as the *iPhone* remote screens, such as *Max Bolus* and *Max Carbs*, before sending it.
* The watch only sends commands while it can reach the *iPhone*. Otherwise the buttons are grayed out. Commands are never saved to send later, and the *iPhone* ignores a command that arrives more than 60 seconds after it was made.

### After Sending

![LoopFollow watch command sent](img/watch-sent.png){width="200"}
{align="center"}

*Sent* means the *iPhone* has sent the command. It does **not** mean that *Loop* or *Trio* has acted on it. Wait for the notification from *Loop* or *Trio* that confirms the result, the same as when you send a command from the *iPhone*. The watch returns to the glucose page after a few seconds.

If something goes wrong, the watch shows the message from the *iPhone* and stays on that screen until you tap *OK*.

### Turn Off Watch Commands

Remote commands from the watch are on by default. To turn them off, open *LoopFollow* on the *iPhone*, go to *Remote Settings* and turn off *Allow Commands from Apple Watch*. The watch then shows glucose information only.
