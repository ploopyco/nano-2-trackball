# Appendix E: Using VIA

The Nano 2's button can be customized using a web application called "VIA". Currently, a bit of additional work is necessary to get VIA to work, but it should only take about thirty seconds.

Begin by copying and pasting the following into a text file, saving it as *nano2.json*:

    {
      "name": "Ploopy Nano 2 Trackball",
      "vendorId": "0x5043",
      "productId": "0x4CE5",
      "matrix": {
        "rows": 1,
        "cols": 1
      },
      "customKeycodes": [
        {
          "name": "DPI Config",
          "title": "DPI Config",
          "shortName": "DPI"
        },
        {
          "name": "Drag Scroll",
          "title": "Drag Scroll",
          "shortName": "DragScl"
        }
      ],
      "layouts": {
        "keymap": [
          [
            {
              "h": 2
            },
            "0,0"
          ]
        ]
      }
    }

- Next, navigate to [the VIA web app](https://usevia.app), using **Microsoft Edge, Chrome, or Opera**. Any other browser that supports WebHID will work, too.
- Look at the top toolbar of the web application, and click the tab called *DESIGN*.
- Uncheck *Use V2 definitions (deprecated)*.
- Click *Load* and upload the *nano2.json* file that you saved on your computer.
- Plug in the Nano 2 if it wasn't plugged in already.
- Look at the top toolbar of the web application, and click the tab called *CONFIGURE*.
- Click *Authorize Device*. A modal window should pop up, and you should see the *Ploopy Nano 2 Trackball* as an option to connect. Do so now.

You should now see a representation of the buttons of the Nano 2 in the web app. You are now free to modify the button's functionality.


## Using VIA and VIAL on Linux

By default, Ploopy devices are compatible with VIA, but not VIAL. However, in both cases, using VIA or VIAL with Ploopy devices on Linux requires modifying a few `udev` rules. If you have `sudo` access on your box, the following command will export the necessary `udev` rules and reload `udev`:

> export USER_GID=`id -g`; sudo --preserve-env=USER_GID sh -c 'echo "KERNEL==\"hidraw*\", SUBSYSTEM==\"hidraw\", ATTRS{idVendor}==\"5043\", MODE=\"0660\", GROUP=\"$USER_GID\", TAG+=\"uaccess\"" > /etc/udev/rules.d/50-qmk-ploopy.rules && udevadm control --reload && udevadm trigger'

As an alternative, you can use `qmk_udev` [here](https://github.com/qmk/qmk_udev) to perform automated `udev` access updates whenever compatible devices are plugged in.

If you're looking for more specific advice on configuring `udev` with VIA and VIAL, see [VIAL's documentation on udev here](https://get.vial.today/manual/linux-udev.html#generalized-via-udev-rule). If you're using VIA, make sure that you follow the instructions allowing VIA devices, as the instructions for VIAL devices are more specific and will not work with VIA.
