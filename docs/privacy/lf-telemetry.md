---
## *LoopFollow* Anonymous Telemetry

*LoopFollow* sends a small anonymous report to the maintainers, once a
day and after you install a new version. It tells them which app and
*iOS* versions are in active use and how quickly people update. That
helps decide, for example, when it's safe to drop support for an older
*iOS* release, and shows early whether a new version is working well.
**No glucose data, no credentials, no logs leave your device.**

Usage stats are **on by default**. You can turn them off at any time in
*Settings* > *General Settings* > *Diagnostics* > *Send anonymous usage
stats*. If you already chose **No thanks** or turned the toggle off in
an earlier version, that choice is kept. When usage stats are off,
nothing is sent.

- - -

## What is sent

A typical report looks like this. You can see the exact report your own
install would send under *Settings* > *General Settings* > *Diagnostics*
> *What's sent*.

| Field | Example | Notes |
|:--|:--|:--|
| App version | `8.0.1` | |
| Build date | `2026-11-03` | The day this copy of the app was built. |
| Build commit | `46a9ed3` | A short code that identifies the exact source code the app was built from. |
| TestFlight or not | `true` / `false` | Whether the install came from TestFlight or a local Xcode build. |
| Instance | `LoopFollow` / `LoopFollow_.Second` / ... | If you have more than one *LoopFollow* installed side by side, this tells them apart. |
| IDFV | Apple per-vendor UUID | Apple's `identifierForVendor`: an opaque code that is the same for all apps from this developer on your device, and resets when all of them are removed. Together with *Instance*, it identifies one install. |
| Device | `iPhone15,2` | Apple's hardware identifier (not the marketing name). |
| Platform | `iOS` / `iPadOS` / `macCatalyst` | |
| iOS version | `17.5` | |
| Following app | `Loop` / `Trio` / ... | Which automated insulin delivery app *LoopFollow* is following, if known. Left out when not yet detected. |
| Uses *Dexcom* | `true` / `false` | Whether *Dexcom Share* is configured. **No username or password.** |
| Uses *Nightscout* | `true` / `false` | Whether a *Nightscout* site is configured. **No URL or API token.** |
| Background-refresh method | `Silent Tune` | Which background-refresh method is selected. |
| Display units | `mg/dL` / `mmol/L` | |
| Remote-command type | `None` / `Loop APNS` / ... | Which remote-command method is configured. |
| Appearance | `dark` / `light` / `system` | |
| Calendar / Contact integrations | `true` / `false` | Whether those features are turned on. |
| Cold launches in past 7 days | `12` | How many times the app was started from scratch in the last 7 days. High values can point to stability problems. |

Each report also says what triggered it, for example `cold_launch` (the
app started), `foreground` (the app was opened), `build_change` (first
start of a new version) or `timer` (the daily check). If the previous
attempt to send failed, it includes a short error category such as
`checkin_request_failed`.

The server adds two fields when it stores each report:

* `receivedAt` — the time the report was received.
* `dayBucket` — the date (in UTC), used to keep at most one report per
  install, day and version.

- - -

## What is **not** sent

Specifically and explicitly:

* No glucose values, insulin or carb data, treatments, or any other health data.
* No *Nightscout* URL or API token. Only a yes/no flag for whether *Nightscout* is configured.
* No *Dexcom* credentials. Only a yes/no flag for whether *Dexcom Share* is configured.
* No time zone.
* No remote-command secrets, no APNS keys.
* No GPS or location data.
* **No logs.** Logs are never sent automatically. The *Settings* > *Logs* sharing flow is unchanged and only triggered by you.

The receiving server also does not log your IP address: the *NGINX*
edge zeroes the last octet of *IPv4* addresses and keeps only the
`/64` prefix of *IPv6* addresses before anything is written to disk.

- - -

## Where it goes

Reports are sent over *HTTPS* to **`https://lf.bjorkert.se/api/telemetry/`**,
which is self-hosted by the maintainer. No third-party analytics
service is involved. Stored reports are kept on that server and are
not shared.

- - -

## How to opt out

The toggle is at *Settings* > *General Settings* > *Diagnostics* >
*Send anonymous usage stats*. Turning it off takes effect immediately
and stays off. From then on nothing is sent.

The *Diagnostics* section also has:

* *What's sent* — shows exactly what your install would send right now,
  with a *Copy* button if you want to look at it more closely.
* *Privacy* — a shorter in-app version of this page.

- - -

## How often

At most once every 24 hours, plus once on the first start of a new
version. *LoopFollow* checks whether a report is due when the app
starts, when you open it, and while it refreshes in the background, so
a report goes out even if the app is rarely opened.

If sending fails (no network, server unreachable, and so on), the app
waits an hour before it tries again, and the next report includes the
error category so the maintainers can see why reports go missing.

- - -

## For the curious

The *iOS* implementation lives at
[`LoopFollow/Helpers/Telemetry.swift`](https://github.com/loopandlearn/LoopFollow/blob/dev/LoopFollow/Helpers/Telemetry.swift)
on *GitHub*. The receiving server is a small *.NET* service in a
private repository on the maintainer's account.
