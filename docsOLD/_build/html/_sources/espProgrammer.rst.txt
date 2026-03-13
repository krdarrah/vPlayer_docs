.. _espProgrammer:

ESP32 Programmer
================

This guide explains how to use vPlayer as a **standalone flasher** for any ESP32-based board. Since different ESP32 variants (ESP32, ESP32-S2, ESP32-S3, ESP32-C3, etc.) may have unique partition layouts, you can specify **memory offsets** for the bootloader, partition table, firmware, and SPIFFS (or other file systems) in a simple ``config.txt`` file. vPlayer reads these offsets at startup, ensuring compatibility across multiple boards without recompilation.

To maintain different firmware sets, create **unique folders** on the SD card—one folder per firmware variant—placing the associated `.bin` files and a matching ``config.txt`` into each folder.

Source Code and bin file
-------------------------

`GitHub <https://github.com/krdarrah/vPlayer_ESPprogrammer>`_


Configuration File
------------------

1. **Create** a file named ``config.txt`` in your firmware folder.
2. **Define** offsets for each component (bootloader, partitions, firmware, etc.):

   .. code-block:: text

      bootloaderNameOffset=0x0
      partitionsNameOffset=0x8000
      bootNameOffset=0xe000
      firmwareNameOffset=0x10000
      spiffsNameOffset=0x10000

   - These values are **example offsets** commonly used for an ESP32-C3.

   **Example for a Standard ESP32**

   .. code-block:: text

      bootNameOffset=0xe000
      bootloaderNameOffset=0x1000
      partitionsNameOffset=0x8000
      firmwareNameOffset=0x10000
      spiffsNameOffset=0x3D0000

Locating the Offsets
--------------------

If you’re compiling and uploading with the Arduino IDE, you can retrieve the exact offsets by **enabling verbose output** (in ``File -> Preferences``, check “Verbose Output” for both compile and upload). During the upload process, look for a line similar to:

.. code-block:: bash

   "/Users/YourName/Library/Arduino15/packages/esp32/tools/esptool_py/4.9.dev3/esptool" 
     --chip esp32s3 --port "/dev/cu.usbmodem1412201" --baud 921600 
     --before default_reset --after hard_reset write_flash -z --flash_mode keep --flash_freq keep --flash_size keep 
     0x0 "/Users/YourName/Library/Caches/arduino/sketches/.../myProject.ino.bootloader.bin" 
     0x8000 "/Users/YourName/Library/Caches/arduino/sketches/.../myProject.ino.partitions.bin" 
     0xe000 "/Users/YourName/Library/Arduino15/packages/esp32/hardware/esp32/.../boot_app0.bin" 
     0x10000 "/Users/YourName/Library/Caches/arduino/sketches/.../myProject.ino.bin"

Here, each **offset** is followed by the corresponding `.bin` file:

- ``0x0`` – Bootloader (``.bootloader.bin``)  
- ``0x8000`` – Partition table (``.partitions.bin``)  
- ``0xe000`` – Boot App (``boot_app0.bin``)  
- ``0x10000`` – Main application firmware (``myProject.ino.bin``)

You can also copy these `.bin` files from their listed paths to your SD card folder, making sure they follow the naming rules below.

File Naming Requirements
-------------------------

When you select a folder on the SD card, the code checks for specific **keywords** in the filenames to identify each file type. This is how it knows which files to flash and their intended purpose.

Required Files
--------------

1. **Bootloader**  
   - Must contain the substring ``bootloader`` in its filename.
   - Examples: ``bootloader_s3.bin``, ``mybootloader.bin``.

2. **Partition Table**  
   - Must contain the substring ``partitions`` in its filename.
   - Examples: ``partitions.bin``, ``partitions_custom.bin``.

3. **Main Firmware**  
   - Must contain either ``.ino.bin`` (e.g., ``mySketch.ino.bin``) **or** ``esp32.bin`` (e.g., ``myFirmware_esp32.bin``) in its name.  
   - If either substring is detected, it’s assumed to be the **main application**.

4. **Boot App**  
   - Must contain the substring ``boot_app`` in its filename.
   - Example: ``boot_app0.bin``.

5. **SPIFFS (Optional)**  
   - Must contain the substring ``spiffs.bin`` (e.g., ``myData_spiffs.bin``).
   - If present, SPIFFS will be flashed using the offset in ``config.txt``.  
   - If missing, SPIFFS flashing is skipped.

6. **Configuration File**  
   - Must be named exactly ``config.txt``.
   - Includes key-value pairs for each file’s flash offset (e.g., ``bootloaderNameOffset=0x0``).
   - If this is missing, the flasher will not proceed.

Example Folder Layout
---------------------

A typical folder might look like this:

.. code-block:: none

   /MyFirmwareFolder
   ├─ config.txt
   ├─ boot_app0.bin
   ├─ bootloader_s3.bin
   ├─ partitions_custom.bin
   ├─ mySketch.ino.bin
   ├─ myData_spiffs.bin

Where:

- **boot_app0.bin** has ``boot_app``  
- **bootloader_s3.bin** has ``bootloader``  
- **partitions_custom.bin** has ``partitions``  
- **mySketch.ino.bin** has ``.ino.bin``  
- **myData_spiffs.bin** has ``spiffs.bin``  
- **config.txt** defines the offsets.


.. image:: images/programmerFolders.png


Connection Basics
-----------------

For minimal hookup, simply connect the vPlayer device to your target ESP32’s TX and RX pins.  
If you want automated programming (i.e., toggling the ESP32 into bootloader mode without manual intervention),  
you can add code to drive the BOOT and RESET lines directly—vPlayer has extra I/O pins available for this purpose.  
However, for a basic setup, you only need:

1. TX (vPlayer) -> RX (ESP32)
2. RX (vPlayer) -> TX (ESP32)
3. GND (shared between vPlayer and ESP32)

To enter the bootloader manually:

- Hold the **BOOT** pin low,
- Then toggle **RESET** or power cycle the ESP32 while BOOT is held low.

.. image:: images/ProgrammerWiring.png



