## Get a Hub

There are two ways to get an *LF Hub* for your family.

- - -

## Hosted for you

Families can buy *LF Hub* as a service, the way many people pay for a hosted *Nightscout* site, instead of running a server themselves. *LF Hub* is available from [10be](https://ns.10be.de/en). We are also talking with more providers, and this page will list them as they offer *LF Hub*.

- - -

## Run it yourself

*LF Hub* is open source: [github.com/loopandlearn/lfhub](https://github.com/loopandlearn/lfhub). Running it yourself suits someone who is comfortable with servers. The full instructions are in the [LF Hub setup guide](https://github.com/loopandlearn/lfhub/blob/main/docs/SETUP.md). In short:

1. **A machine that is always on.** A small cloud server, a home server or a Raspberry Pi. The hub runs as a container (`ghcr.io/loopandlearn/lfhub`, for both arm64 and amd64).
1. **A database.** PostgreSQL 14 or newer, which can run next to the hub.
1. **An address with HTTPS.** A domain name and a reverse proxy such as Caddy, Traefik or nginx in front of the hub. The phones only talk to the hub over HTTPS.
1. **Three secrets** that you create once and keep in a password manager:
    * the *master key*, which encrypts the stored *Nightscout* token, *Dexcom* login and APN keys
    * the *setup token*, which makes a phone an owner of the hub. Use it only for your own phones. Family members join with an invite from the app.
    * an optional *status key* for a monitoring service
1. **Start it** with Docker Compose or Kubernetes. The setup guide has examples of both. Run exactly one hub per database.
1. **Check it.** `https://<your hub address>/healthz` should answer `ok`.
1. **Connect the first phone** with the hub's address and the setup token, see [Set Up and Invite](lf-hub-onboarding.md).

Once it runs:

* **Monitor it.** Add a monitoring service such as UptimeRobot for `https://<your hub address>/status?key=<status key>&fresh=1`. It answers with an error when the hub, its database or the data source has a problem, including when the latest glucose reading is 12 minutes old or more.
* **Back it up.** Back up the database regularly, and keep the master key in a separate safe place. A backup can only be read with it.
* **Keep it up to date.** Pull the new image and restart the hub. *LoopFollow* shows the hub's version and the newest version under *Settings* → *LF Hub*, and reminds an owner every two weeks while a newer hub is out.

!!! info "Your family's health data"
    The hub stores the *Nightscout* token or *Dexcom* login, the phones' APN keys and recent glucose data. Whoever runs the hub can reach that data. Run it yourself, or choose a provider you trust.
