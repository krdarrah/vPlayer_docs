.. _weather_display_project:

Weather Display
================

.. image:: images/weatherImage.jpg

This project turns the vPlayer into a compact weather dashboard using WeatherAPI data over Wi-Fi.

What This Firmware Does
-----------------------

- Shows current temperature + weather icon
- Shows today and tomorrow forecast:

  - high/low temperatures
  - rain chance
  - condition icons

- Rotates through 5 views automatically (every 3 seconds)
- Reads Wi-Fi + API settings from SD card
- Supports boot-time self-update from ``/firmware.bin`` on SD card

First-Time Setup
----------------

Prepare SD card settings file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create ``/settings.txt`` in SD card root with exactly 4 lines::

   YOUR_WIFI_SSID
   YOUR_WIFI_PASSWORD
   YOUR_WEATHERAPI_KEY
   YOUR_ZIP_CODE

Example::

   MyWiFi
   mySecretPass
   abc123weatherapikey
   90210


Screen Views
------------

The display cycles through:

1. Current temp
2. Today high/low
3. Today rain %
4. Tomorrow high/low
5. Tomorrow rain %

----------------------------------------------------------------

The main vPlayer firmware can update this weather firmware automatically:


1. Download weather image from GitHub Releases  `vPlayer Weather Releases <https://github.com/krdarrah/vPlayer_Weather/releases>`_

2. Save it to SD root as ``/firmware.bin``
3. Reboot board (or reboot into weather firmware)
4. Weather firmware detects ``/firmware.bin``, flashes it, removes file, and reboots

If successful, serial output includes::

   Firmware update completed successfully!
