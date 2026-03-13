AI (Dalle) Image Generator
===================================

Overview
--------
The AI (Dalle) Image Generator is a project designed to fetch AI-generated images using OpenAI's DALL-E model and display them on the vPlayer board. The system retrieves images from the internet via WiFi and stores them on an SD card for display. The user can configure the settings, including WiFi credentials, API key, and refresh interval, through a ``settings.txt`` file stored on the SD card.

Features
--------
- Runs on the vPlayer board without requiring additional hardware.
- Connects to WiFi to download AI-generated images.
- Uses OpenAI's DALL-E API to fetch images based on a prompt.
- Saves images as PNG files on an SD card.
- Displays images on the screen.
- Configurable settings via ``settings.txt``.
- Auto-refresh feature to periodically update the displayed image. Can be $$$, so keep this in mind.  Once an hour would be a good start

Software Requirements
----------------------
- OpenAI API key
- Libraries:
  - ``Arduino_GFX_Library.h`` for display control 
  - ``PNGdec.h`` for PNG decoding (v1.0.3)
  - ``AIChatbot.h`` for OpenAI API communication (modified included with source) `Original Source <https://github.com/bayeggex/Arduino-AI-Chat-Library>`_

Setup Instructions
------------------
1. **Prepare the SD Card:**
   - Format an SD card (FAT32 recommended).
   - Place a ``settings.txt`` file in the root directory of the SD card.

2. **Configure ``settings.txt``:**
   The settings file should contain the following:
   ::

      YOUR_SSID
      YOUR_PASSWORD
      YOUR_API_KEY
      YOUR_PROMPT
      YOUR_UPDATE_RATE (SECONDS)

   - **YOUR_SSID**: WiFi network name
   - **YOUR_PASSWORD**: WiFi password
   - **YOUR_API_KEY**: OpenAI API key
   - **YOUR_PROMPT**: Text prompt for generating images "paint me a picture in stylel of Monet"
   - **YOUR_UPDATE_RATE (SECONDS)**: Interval for refreshing images (API usage costs may apply)

3. **Run the System:**
   - Insert the SD card into the vPlayer board.
   - Power on the board.
   - The system will load settings from the SD card, connect to WiFi, fetch an AI-generated image, and display it on the screen.
   - The image will be updated based on the defined refresh interval.

Obtaining an API Key
--------------------
To use OpenAI’s image generation API, you need an API key:
1. Visit `OpenAI's API page <https://platform.openai.com/login>`_.
2. Sign up or log in.
3. Navigate to the API section and generate an API key.
4. Copy the key and paste it into the ``settings.txt`` file on the SD card.

Functionality Breakdown
-----------------------
WiFi Connection Handling
^^^^^^^^^^^^^^^^^^^^^^^^
- Ensures the device stays connected to WiFi.
- Reconnects if the connection is lost.

Image Download and Storage
^^^^^^^^^^^^^^^^^^^^^^^^^^
- Fetches a PNG image URL using OpenAI’s API.
- Downloads and saves the image on the SD card.

Image Display
^^^^^^^^^^^^^
- Loads the saved PNG from the SD card.
- Decodes and renders it onto the screen.

Auto-Refresh
^^^^^^^^^^^^
- Periodically fetches a new image based on the configured update interval.

Troubleshooting
---------------
WiFi Connection Issues
^^^^^^^^^^^^^^^^^^^^^^
- Ensure the SSID and password are correctly set in ``settings.txt``.
- Check if the router allows connections from new devices.

API Key Errors
^^^^^^^^^^^^^^
- Verify that the API key is valid and has sufficient quota.
- Ensure there are no extra spaces or newline characters in ``settings.txt``.

SD Card Not Detected
^^^^^^^^^^^^^^^^^^^^
- Ensure the SD card is properly inserted.
- Try formatting the card as FAT32.

No Image Displayed
^^^^^^^^^^^^^^^^^^
- Check if the image file exists on the SD card (``/image.png``).
- Ensure the vPlayer board is properly powered.
- Verify that the power supply is sufficient for the board.

Source Code
--------------
`Github page <https://github.com/krdarrah/vPlayer_Dalle>`_  You can also drop that firmware.bin file on your sd card and the vPlayer will automatically update to this firmware

