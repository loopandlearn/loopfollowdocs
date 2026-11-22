## *LoopFollow* for *Android*

*LoopFollow* for *Android* is the *LoopFollow* app for *Android* phones. It follows the *iOS* app feature by feature: the same home screen and graph, alarms, statistics, Nightscout and Dexcom Share data, remote control of *Loop* and *Trio*, and the same settings, including QR codes for moving settings between phones.

Like *LoopFollow* for *iOS*, it is not in an app store. You build it yourself, for free, in your own *GitHub* account, and install it on your phone. This page explains how, and what is different from the *iPhone* version.

!!! warning "Not a medical device"
    *LoopFollow* is a tool for following glucose and loop data. It is not a medical device.

    *LoopFollow* alarms are an extra layer, not your main alarm. A phone can delay or stop an app, lose its connection or run out of battery. Make sure other alarms are set up, for example in the CGM app or the loop app.

### Requirements

* An *Android* phone with *Android* 12 or newer
* A free *GitHub* account
* A web browser: *Chrome* on your phone or any browser on a computer

You do not need an *Apple* developer account, a computer or any program to build *LoopFollow* for *Android*.

- - -

## What is Different from the *iPhone* App

Most of the app looks and works the same as on an *iPhone*. These are the differences you will notice.

### Not Available on *Android*

* *Apple Watch*, *CarPlay*, widgets, the *Dynamic Island* and the app badge
* The calendar and contact-image features
* *LF Hub*

### Live Activity is a Notification

On *Android*, the Live Activity card is shown as a notification that stays while *LoopFollow* runs. It is updated by the app itself each time new data arrives, so there is no "Tap to update" and no renewal every 8 hours.

* It is on by default. If you turn the Live Activity off, a small notification with only the app name stays: *Android* requires one for an app that keeps running in the background.
* A glucose reading that is 12 minutes old or older is shown struck through.

### Keeping *LoopFollow* Running

*LoopFollow* keeps running in the background so it can download data and sound alarms. *Android* phones can still stop or delay apps to save battery.

* When asked, allow notifications and full-screen alerts. *Settings* > *Background Refresh* shows whether they are allowed, with a button to the right system page. *Alarm Settings* and a banner on the home screen tell you if one is turned off.
* During setup, *LoopFollow* asks *Android* to let it run without battery restrictions. Choose **Allow**. Without it, *Android* can pause *LoopFollow* and alarms can be late. If you skipped this, a banner on the home screen reminds you: go to *Settings* > *Background Refresh*, tap **Unrestricted battery use** and allow it.
* Some phone makers add their own battery savers. If alarms are late or missing, check your phone's battery settings for *LoopFollow*.

### Alarms

* Alarms play on the phone's alarm volume.
* While an alarm is sounding, the Snoozer is shown over the lock screen so you can snooze without unlocking. Everything else in the app needs the phone unlocked.
* With **Volume Buttons Snooze Alarms** turned on in *Alarm Settings*, the volume buttons snooze an alarm, as on the *iPhone*. Play/pause buttons on headphones and in cars do not.

### Remote Control

Remote control of *Loop* and *Trio* works, with these differences:

* You always enter the APNS Key ID and APNS Key in the remote settings, since the *Android* app is not built with an *Apple* developer account. See [Remote Control Overview](../remote/remote-control-overview.md).
* The *Android* app cannot receive the confirmation that *Loop* or *Trio* sends back. After you send a command, *LoopFollow* shows "Command Sent", and the result shows once *Loop* or *Trio* uploads it to *Nightscout*. *LoopFollow* checks *Nightscout* more often for a while after each command.
* Editing or deleting a meal or carb entry, and switching a *Loop* profile, have no "waiting" state. Check the result in *Nightscout* data before you send the command again.

### Your Settings and Passwords

* The *Nightscout* token, *Dexcom* password, APNS keys and other secrets are stored encrypted on the phone.
* *LoopFollow* data is not included in *Android* backups or in a transfer to a new phone. To move to a new phone, or to keep a copy of your settings, use *Settings* > *Import/Export* and the QR code. The QR code holds your secrets: keep it private.
* QR codes made on an *iPhone* work on *Android*, and the other way around.

### Other Differences

* The *Nightscout* address must start with `https://`, as on the *iPhone*.
* [Anonymous Telemetry](../privacy/lf-telemetry.md) works the same way, but the install identifier is a random number created by *LoopFollow*, and the device is reported as maker and model with the *Android* version. It is reset when the app is uninstalled.

- - -

## Build *LoopFollow* for *Android*

The steps below create your own private copy of the *LoopFollow* builder in *GitHub*, give it your signing key, build the app, and install it. It takes about 10 minutes the first time. Each later build is one button.

You do **not** fork *LoopFollow*. The source code is downloaded from [loopandlearn/LoopFollowAndroid](https://github.com/loopandlearn/LoopFollowAndroid){: target="_blank" } at every build.

!!! warning "Your build repository must stay private"
    Everything a build produces can be downloaded by anyone who can see the repository. The button in step 1 creates a private repository. Never change it to public, and do not fork the builder instead: a fork is always public.

    A private repository gets 2000 free *GitHub* Actions minutes per month, enough for many builds.

!!! info "Everything here runs in your browser"
    Your key and passwords are never sent anywhere, except into the *GitHub* secret you paste them into yourself. Only your *GitHub* username is sent to *GitHub*, to check that it exists.

### Step 1 – Create Your Private Build Repository { #build-step-1 }

First log in to [github.com](https://github.com){: target="_blank" } in this browser. No account? Create one for free.

<label class="lfab-label" for="lfab-user">Your GitHub username</label>
<input class="lfab-input" type="text" id="lfab-user" autocomplete="username" spellcheck="false" placeholder="my-github-name">
<span class="lfab-msg" id="lfab-userMsg"></span>

Use your username, shown in your *GitHub* profile, not your email.

<label class="lfab-label" for="lfab-repo">Name of your repository</label>
<input class="lfab-input" type="text" id="lfab-repo" spellcheck="false" placeholder="my-loopfollow">

Keep the suggestion. Already created your repository with another name? Type that exact name here.

Your repository: <code class="lfab-repoUrl"></code>

<a class="lfab-btn" id="lfab-createRepo" href="https://github.com/new" target="_blank" rel="noopener">Create my private repository</a>

On the *GitHub* page that opens, everything is already filled in: the template `loopandlearn/LoopFollowAndroid-Builder`, your account as owner, the name, and **Private**. Do not change anything, and leave **Include all branches** unticked.

1. Click the green **Create repository** button.
1. *GitHub* shows your new repository with a folder `.github` and a file `README.md`. Come back to this page for step 2.

!!! warning "Your new repository is empty (no files)?"
    It was not created from the template. Delete it (*Settings* > bottom of the page > *Delete this repository*), then tap **Create my private repository** again.

??? note "Updating your copy (only when this page says so)"
    The build steps are updated for you: at every build, your repository runs the version released by Loop and Learn, and nothing in your repository changes. You only replace your workflow file when the *LoopFollow* documentation announces it.

    1. Open the [newest workflow](https://github.com/loopandlearn/LoopFollowAndroid-Builder/blob/main/.github/workflows/build.yml){: target="_blank" } and copy the whole text.
    1. <a class="lfab-btn lfab-secondary" id="lfab-openWorkflowFile" href="#build-step-1" target="_blank" rel="noopener">Open my workflow file</a> and edit it (the pencil, or *Edit file* in the **⋯** menu).
    1. Replace the whole text with the copied workflow, then click **Commit changes…** twice. Your `KEYSTORE_SET` secret stays as it is.

### Step 2 – Your Signing Key { #build-step-2 }

The app is signed with your own key. **Always use the same key.** *Android* only installs an update signed with the same key as the app on the phone. With another key, you must uninstall *LoopFollow* first, which removes its settings.

=== "Create a new key"

    First time building *LoopFollow* for *Android*? A new key is created here in your browser. Nothing is sent anywhere.

    <label class="lfab-label" for="lfab-newPass">Choose a password (at least 8 characters, no spaces, no accented letters)</label>
    <input class="lfab-input" type="password" id="lfab-newPass" autocomplete="new-password">

    <label class="lfab-label" for="lfab-newPass2">Repeat the password</label>
    <input class="lfab-input" type="password" id="lfab-newPass2" autocomplete="new-password">

    <button class="lfab-btn" type="button" id="lfab-newGo">Create key</button> <span class="lfab-msg" id="lfab-newMsg"></span>

    <div class="lfab-box" id="lfab-backupBox" markdown hidden>

    **Save a backup of your key!**

    Download the file. Keep these three together, somewhere safe off your phone, for example in your own cloud storage:

    * the file `loopfollow-keystore.jks`
    * your password
    * the alias of the key: **`key0`**

    You need all three to build *LoopFollow* again if you ever lose your build repository.

    <button class="lfab-btn" type="button" id="lfab-downloadKs">Download backup (loopfollow-keystore.jks)</button>

    </div>

=== "I already have a key"

    For example the backup from an earlier build (`.jks`).

    <label class="lfab-label" for="lfab-ksFile">Key file</label>
    <input type="file" id="lfab-ksFile" accept=".jks,.keystore,.p12,.pfx,application/octet-stream">

    <label class="lfab-label" for="lfab-ksPass">Key file password</label>
    <input class="lfab-input" type="password" id="lfab-ksPass" autocomplete="off">

    <label class="lfab-label" for="lfab-ksAlias">Key alias</label>
    <select class="lfab-input" id="lfab-ksAliasSel" hidden></select>
    <input class="lfab-input" type="text" id="lfab-ksAlias" autocomplete="off" spellcheck="false" placeholder="key0">

    <label class="lfab-check"><input type="checkbox" id="lfab-samePass" checked> Key password is the same as the key file password</label>

    <div id="lfab-keyPassWrap" hidden>
    <label class="lfab-label" for="lfab-keyPass">Key password</label>
    <input class="lfab-input" type="password" id="lfab-keyPass" autocomplete="off">
    </div>

    <button class="lfab-btn" type="button" id="lfab-haveGo">Check and continue</button> <span class="lfab-msg" id="lfab-haveMsg"></span>

### Step 3 – Give the Key to Your Repository { #build-step-3 }

<span id="lfab-s3wait">Finish step 2 first.</span>

<div id="lfab-s3ready" markdown hidden>

1. <a class="lfab-btn lfab-secondary" id="lfab-openSecrets" href="#build-step-1" target="_blank" rel="noopener">Open the secrets page</a> of <code class="lfab-repoUrl"></code>

    "Page not found" (404)? Check that you are logged in to github.com in this browser: *GitHub* shows 404 for private repositories when you are not. Otherwise the username or repository name in step 1 does not match your repository.

1. Tap **Copy name**, then paste it into the small **Name** field: `KEYSTORE_SET` <button class="lfab-btn lfab-secondary" type="button" data-lfab-copy="name">Copy name</button>
1. Tap **Copy secret**, then paste the long code into the big **Secret** box: <code id="lfab-secretPreview"></code> <button class="lfab-btn" type="button" data-lfab-copy="secret">Copy secret</button> <span class="lfab-msg" id="lfab-copyMsg"></span>

    The secret is a very long code (thousands of characters), not the word KEYSTORE_SET.

1. Tap **Add secret**. You never need to do this again.

</div>

### Step 4 – Build the App { #build-step-4 }

1. <a class="lfab-btn" id="lfab-openActions" href="#build-step-1" target="_blank" rel="noopener">Open the build page</a> of <code class="lfab-repoUrl"></code>
1. If asked, click the green button to enable workflows. Use **Build LoopFollow** in the list. Ignore **LoopFollow Builder**: it holds the build steps and has no **Run workflow** button.
1. Click **Run workflow**. Check the choices, then click the green **Run workflow** button:
    * **LoopFollow version**: keep `main`, the released version.
      `dev` builds the development version, where new features are tested before a release. It is for experienced users and has minimal support. To go back from `dev` to `main`, wait until `main` has a newer version, or export your settings and uninstall first: *Android* does not install an older version over a newer one.
    * **Which app**: keep `LoopFollow`. Following more than one person? Choose `Second` or `Third` to build a separate app with its own settings, next to the first one. Use the same key for all of them.
    * **Name under the app icon**: leave it empty for `LoopFollow`, `LoopFollow_Second` or `LoopFollow_Third`, or type your own.
1. Wait about 10 minutes. A green check means it is done.

### Step 5 – Install on Your Phone { #build-step-5 }

!!! warning "Already have *LoopFollow* on this phone?"
    Before you install a build made with a **different key** than the app on your phone, export your settings with *Settings* > *Import/Export*. You have to uninstall the old app first, which removes its settings. An update with the same key keeps your settings.

1. Open this page on your phone, in *Chrome*, not in the *GitHub* app. The *GitHub* app cannot download builds. Log in to github.com if asked.
1. <a class="lfab-btn lfab-secondary" id="lfab-openRuns" href="#build-step-1" target="_blank" rel="noopener">Open my builds</a>
1. Tap the newest build with a green check.
1. Tap the link **📱 Download LoopFollow …** in the build summary.
1. When the download is done, tap the file and choose **Install**. If asked, allow installing apps from this source.
1. Open *LoopFollow* and follow the setup. Allow notifications and full-screen alerts, and allow unrestricted battery use (see [Keeping *LoopFollow* Running](#keeping-loopfollow-running)).

The app is kept on the build page for 14 days. It is not shown under *Code* in your repository.

### Updating *LoopFollow*

When a new version is released, open the build page from step 4 and run **Build LoopFollow** again, then install it as in step 5. With the same key, the new version installs over the old one and keeps your settings. Your repository never builds anything by itself.

<div id="lfab-msgs" hidden>
<span data-lfab-msg="copied">Long code copied: paste it in the big "Secret" box, then tap "Add secret".</span>
<span data-lfab-msg="copiedName">Name copied: paste it in the small "Name" field.</span>
<span data-lfab-msg="copiedShort">Copied ✓</span>
<span data-lfab-msg="userOk">✓ GitHub user found.</span>
<span data-lfab-msg="userBad">✗ No GitHub user with this name. Use your username, not your email.</span>
<span data-lfab-msg="needUser">Enter your GitHub username in step 1 first.</span>
<span data-lfab-msg="errPipe">Passwords and alias cannot contain the character |</span>
<span data-lfab-msg="errNoFile">Choose your key file.</span>
<span data-lfab-msg="errEmpty">Fill in password and alias.</span>
<span data-lfab-msg="errPass">Wrong key file password.</span>
<span data-lfab-msg="errKeyPass">Wrong key password.</span>
<span data-lfab-msg="errAlias">Alias not found in the key file. Available: {aliases}</span>
<span data-lfab-msg="errFormat">This does not look like a key file.</span>
<span data-lfab-msg="okHave">Key OK! Continue with step 3.</span>
<span data-lfab-msg="okHaveUnchecked">Key read. The password is checked when you build. Continue with step 3.</span>
<span data-lfab-msg="errShort">The password must be at least 8 characters.</span>
<span data-lfab-msg="errAscii">Use only a–z, A–Z, 0–9 and symbols such as ! ? # – no spaces, no accented letters and not |</span>
<span data-lfab-msg="errMatch">The passwords do not match.</span>
<span data-lfab-msg="working">Creating key…</span>
<span data-lfab-msg="okNew">Key created. Download the backup below, then continue with step 3.</span>
</div>

<small>The builder and these setup steps are based on [AAPS Builder](https://github.com/nightscout/aaps-builder){: target="_blank" } (AGPL-3.0).</small>
