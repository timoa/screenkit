# ScreenKit

The cheapest solution to show content on TV screens (monitoring, dashboard, digital signage, etc.) with a modern browser, automatic rotation of the content and configuration per screen!

This project is based on:

* [Chilipie Kiosk][chilipie-kiosk-project]: Linux distro optimised for RPi and to run in kiosk mode
* [Chromium][chromium-project]: Latest version of Chromium (Chrome open source version) that provides a modern browser that support SVG, modern JS, etc.
* [Tab Rotate][tab-rotate-project]: Chrome extension that run in fullscreen and rotate between multiple tabs
* [Tab Rotate Server][tab-rotate-server-project]: Webserver that manages the content per screen for the Tab Rotate Chrome extension
* Dedicated Google account: This Google account will syncronised the settings and extensions between the screens

## How does it work

1) [Chilipie Kiosk][chilipie-kiosk-project] will boot the RPi and launches the [Chromium browser][chromium-project] in full screen without the mouse cursor and with a nice background image
2) The [Tab Rotate extension][tab-rotate-project] will call the [Tab Rotate Server][tab-rotate-server-project] to get a playlist of contents
3) The [Tab Rotate Server][tab-rotate-server-project] detect the IP of the screen that requested the playlist and if a playlist exists for this screen, it send it or uses the default one
4) The [Tab Rotate extension][tab-rotate-project] will create a tab for each content (website, image, etc.) and start rotating between the tabs
5) After a configurable time, the [Tab Rotate extension][tab-rotate-project] will request a new version of the playlist and reload each tab if the playlist changed

## What do you need

This project is running on the RaspberryPi hardware only. For now :)

You will need per screen:

* A Raspberry Pi board: from RPi2 to RPi3 (need to test RPi4 when available)
* A TV or monitor with HDMI
* An HDMI cable
* An AC power that can deliver 2.5Amp minimum with micro-USB connector (USB-C for RPi4)

## How to start

The following information will help you to create the first player. This will be your master image.

If you have multiple screens, you will be able to clone this master image to avoid to redo this manual steps on the other players.

1) Download the [latest version of Chilipie kiosk][chilipie-kiosk-download]
2) Follow the [Getting started][chilipie-kiosk-getting-started]

## Other useful Chrome extensions

* [Requestly][requestly-extension] can be uses to inject HTTP headers like Auth token for Grafana dashboards or other websites that require authentication
* [Ignore X-Frame headers][ignore-x-frame-headers-extension] can help you if you need to `<iframe>` a site that doesn't want to be framed
* [Tampermonkey][tampermonkey-extension] can be useful for injecting custom JS or CSS to a page you're displaying

## Howto

Sometimes, the content (dashboards, websites, etc.) are not accessible without authentication.

When possible, you can use Basic Auth, API Token (Bearer, etc.) and inject them in the HTTP headers, using the Chrome Extension [Requestly][requestly-extension] for example.

Be careful to create users that have limited access (read only) to your accounts and save your credentials/api keys securely.

### Grafana

Grafana can use an API key to authenticates. You can create an API token on `Configuration` > `API Keys`.

Give a `Key name` (screens for ex.) and role `Viewer` and set the `Time to live` between one month and one year, depending of your company policy.

When it's done, save your `Key` into a safe place (1Password, etc.) and launch the Google profile created for your screens.

Click on `New Rule` > `Modify Headers`.

Set a `Rule Name` (Grafana) and in the `Header` field, add `Authorization`. On the `Value` field, set:

``` text
Bearer {put your API token here}
```

Set the last field with the URL of your Grafana instance to put this HTTP header only when the screens call Grafana.

## TODO

* Finish the "How to start"
* Create an Ansible role to configure and maintain the RPi automatically instead of doing manual process

[chilipie-kiosk-project]: https://github.com/futurice/chilipie-kiosk
[chilipie-kiosk-download]: https://github.com/futurice/chilipie-kiosk/releases
[chilipie-kiosk-getting-started]: https://github.com/futurice/chilipie-kiosk#getting-started
[chromium-project]: https://www.chromium.org/
[tab-rotate-project]: https://github.com/KevinSheedy/chrome-tab-rotate
[tab-rotate-server-project]: https://github.com/timoa/chrome-tab-rotate-server
[requestly-extension]: https://chrome.google.com/webstore/detail/requestly-redirect-url-mo/mdnleldcmiljblolnjhpnblkcekpdkpa
[ignore-x-frame-headers-extension]: https://chrome.google.com/webstore/detail/ignore-x-frame-headers/gleekbfjekiniecknbkamfmkohkpodhe
[tampermonkey-extension]: https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo
