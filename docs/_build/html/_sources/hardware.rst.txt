Knowledgebase
===================================

.. image:: images/blownUp.jpg

Schematic
-------------

.. image:: images/videoPlayer_v1.0_SCH.pdf

Power
-------------

- The default power source is from the USB-C at 5V [VUSB]
- The onboard 5V-3.3V Regulator supplies power to all of the circuitry [3V3]
- Power consumption [TBD]
- If you want to supply power at the connectors, you can do this, just be careful to not plug in the USB-C cable, since there would be a conflict.  Like if you want to make this battery powered, you could apply a 4.2V cell to the VUSB connection.  Again, just be careful to not connect the USB-C.  Same goes for the 3.3V conenction, you could just apply 3.3V here, but same thing as before, do not connect to the USB-C port.

Programming
-------------

- Arduino IDE 2.3.3
- ESP32 Core Version 2.0.14  (newer will work, but my code was developed with this version)

**Flash Settings**

.. image:: images/flashsettings.png


**Forcing download mode**

You can do this easily by shorting the BOOT IO0 pin on the connector to GND.  Then just power cycle (plug in with the USB-C) then it will be in download mode.  Sometimes when you have some code that's crashing, it is dificult for the auto-download function to work.  

Expansion
-------------

.. image:: images/pinout.png

These connections here can be used for anything you want.  They are JST SH/SR 1mm connectors.  I just use one of these `kits from Amazon to make my own cables <https://www.amazon.com/gp/product/B07PDQKHJ2/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1>`_


.. image:: images/SHSR.png

All spare IO pins on the ESP32 are broken out on the backside of the board:

.. image:: images/backside.png

Mechanical
-------------

`Link to the 3D Model <https://a360.co/3ZtBuwH>`_

.. image:: images/3dmodel.png

The case I came up with is made up in 3 pieces

`Link to the case 3D Model <https://a360.co/3ZpAjNd>`_

.. image:: images/case3D.png







