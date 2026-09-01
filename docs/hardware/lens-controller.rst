Lens controller: Pinefeat CEF
=============================

The Pinefeat ``CEF135`` M42 adapter mechanically couples the Canon EF lens to
the instrument camera and provides electronic focus and aperture control. It
connects over USB as a serial device; the instrument control software operates
the controller through its instrument-side focus backend.

Operational notes
-----------------

* Disconnect USB power before connecting or disconnecting the lens.
* Ensure the mechanical switch on the lens body is set to ``AF`` to enable
  electronic focus control.
* Calibrate the focus travel for the attached lens before adjusting the focus
  position or aperture setting.
* Canon EF lenses do not report their current aperture, so aperture commands are
  effectively write-only.


Vendor resources
----------------

* `Product brief (PDF) <https://docs.pinefeat.co.uk/cef135-product-brief-M42-astro.pdf>`_
* `Pinefeat CEF135 driver (GitHub) <https://github.com/pinefeat/cef135>`_
* `Troubleshooting guide <https://github.com/pinefeat/cef135/blob/main/troubleshooting.md>`_
