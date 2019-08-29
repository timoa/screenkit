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
2) Follow the [Getting started][chilipie-kiok-getting-started]

## TODO

* Finish the "How to start"
* Add the Chrome extension that helps to load iframes
* Add the Chrome extension that inject the HTTP headers (Grafana auth token for ex.)
* Create an Ansible role to configure and maintain the RPi automatically instead of doing manual process

[chilipie-kiosk-project]: https://github.com/futurice/chilipie-kiosk
[chilipie-kiosk-download]: https://github.com/futurice/chilipie-kiosk/releases
[chilipie-kiok-getting-started]: https://github.com/futurice/chilipie-kiosk#getting-started
[chromium-project]: https://www.chromium.org/
[tab-rotate-project]: https://github.com/KevinSheedy/chrome-tab-rotate
[tab-rotate-server-project]: https://github.com/timoa/chrome-tab-rotate-server
