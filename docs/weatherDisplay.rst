.. _weather_display_project:

Weather Display
===============

.. image:: images/weatherImage.jpg
   :alt: vPlayer Weather Display

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

1) Get a WeatherAPI key
~~~~~~~~~~~~~~~~~~~~~~~

Create a free account at `WeatherAPI <https://www.weatherapi.com/>`_ and copy your API key from your dashboard.

2) Prepare SD card settings file
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

Keep your API key private and do not commit it to GitHub.

Screen Views
------------

The display cycles through:

1. Current temp
2. Today high/low
3. Today rain %
4. Tomorrow high/low
5. Tomorrow rain %

Firmware Update (from main vPlayer firmware)
---------------------------------------------

1. Download weather firmware from `vPlayer Weather Releases <https://github.com/krdarrah/vPlayer_Weather/releases>`_
2. Or use direct latest asset: `Latest firmware.bin <https://github.com/krdarrah/vPlayer_Weather/releases/latest/download/firmware.bin>`_
3. Save the file to SD root as ``/firmware.bin``
4. Reboot board (or reboot into weather firmware)
5. Weather firmware detects ``/firmware.bin``, flashes it, removes it, and reboots

If successful, serial output includes::

   Firmware update completed successfully!
