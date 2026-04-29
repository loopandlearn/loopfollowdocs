---
## *LoopFollow* Anonymous Telemetry

*LoopFollow* can send a small anonymous report once a day so the
maintainers can see which app and *iOS* versions are still in active use.
The data helps make decisions like when it's safe to drop support for
older *iOS* releases. **No glucose data, no credentials, no logs leave
your device.**

This is opt-out: the first time the app comes to the foreground after
installing or updating to a version that supports telemetry, you'll see
a one-time prompt to choose Yes or No. You can change your mind any
time in *Settings* > *General Settings* > *Diagnostics*.

- - -

## What is sent

A typical check-in looks like this — you can see the exact JSON your
own install would send under *Settings* > *General Settings* >
*Diagnostics* > *What's sent*.

| Field | Example | Notes |
|:--|:--|:--|
| App version | `6.0.7` | |
| Build number | `100` | |
| Build branch and commit | `dev`, `d691b34` | The git branch and short commit SHA of the build. |
| Build date | `2026-04-15` | |
| TestFlight or not | `true` / `false` | Whether the install came from TestFlight or a local Xcode build. |
| Instance | `LoopFollow` / `LoopFollow_2` / ... | If you have multiple *LoopFollow* installs side by side, this distinguishes them. |
| IDFV | Apple per-vendor UUID | Apple's `identifierForVendor` — opaque, scoped to *LoopFollow*'s bundle prefix, and resets when all of this developer's apps are removed from the device. Combined with the *Instance* field above, identifies a specific install. |
| Device | `iPhone15,2` | Apple's hardware identifier (not the marketing name). |
| Platform | `iOS` / `iPadOS` / `macCatalyst` | |
| iOS version | `17.5` | |
| Following app | `Loop` / `Trio` / ... | Which closed-loop app *LoopFollow* is following, if known. Field is omitted when not yet detected. |
| Uses *Dexcom* | `true` / `false` | Whether *Dexcom Share* is configured. **No username or password.** |
| Uses *Nightscout* | `true` / `false` | Whether a *Nightscout* site is configured. **No URL or API token.** |
| Background-refresh method | `Silent Tune` | Which background-refresh strategy is selected. |
| Display units | `mg/dL` / `mmol/L` | |
| Remote-command type | `none` / `Loop APNS` / ... | Which remote-command path is configured. |
| Appearance | `dark` / `light` / `system` | |
| Calendar / Contact integrations | `true` / `false` | Whether those features are turned on. |
| Cold launches in past 7 days | `12` | A count of process restarts; high values can flag stability issues. |

The server adds two fields when it stores each report:

* `receivedAt` — the time the report was received.
* `dayBucket` — a date label (e.g. `2026-04-29`) used to deduplicate.

- - -

## What is **not** sent

Specifically and explicitly:

* No glucose values, insulin or carb data, treatments, or any other health data.
* No *Nightscout* URL or API token. Only a yes/no flag for whether *Nightscout* is configured.
* No *Dexcom* credentials. Only a yes/no flag for whether *Dexcom Share* is configured.
* No time zone.
* No remote-command secrets, no APNS keys.
* No GPS or location data.
* **No logs.** Logs are never sent automatically. The existing *Settings* > *Logs* sharing flow is unchanged and only triggered by you.

The receiving server also does not log your IP address — the *NGINX*
edge zeroes the last octet of *IPv4* addresses and only retains the
`/64` prefix of *IPv6* addresses before anything is written to disk.

- - -

## Where it goes

Reports are sent over *HTTPS* to **`https://lf.bjorkert.se/api/telemetry/checkin`**,
which is self-hosted by the maintainer. There is no third-party
analytics service involved.

- - -

## How to opt out

The toggle lives at *Settings* > *General Settings* > *Diagnostics* >
*Send anonymous usage stats*. Turning it off is immediate and persistent.

The *Diagnostics* section also has:

* *What's sent* — renders the exact *JSON* your install would send right now,
  with a *Copy* button if you want to inspect it more closely.
* *Privacy* — a shorter in-app version of this page.

- - -

## How often

A check-in is sent at most once every 24 hours, or once after the app's
build SHA changes (whichever fires first). It runs in the background
while the app is active or refreshing in the background — *LoopFollow*
schedules the next check-in based on when the last one was actually
sent, so a relaunch a few hours after the previous send simply waits
out the remainder of the 24 hours.

If a send fails (network error, the server is unreachable, etc.) the
last-sent timestamp is not updated, so the next scheduled check tries
again.

- - -

## For the curious

The *iOS* implementation lives at
[`LoopFollow/Helpers/Telemetry.swift`](https://github.com/loopandlearn/LoopFollow/blob/dev/LoopFollow/Helpers/Telemetry.swift)
on *GitHub*. The receiving server is a small *.NET* service in a
private repository on the maintainer's account.
