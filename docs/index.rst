MLO Spectrograph Software
========================

This site is the unified user and developer documentation for the software
supporting the MLO fiber-fed spectrograph. The software is intentionally split
into focused repositories, but users should be able to approach the instrument
as one system rather than learning each repository in isolation.

The normal path through the software is:

.. code-block:: text

   target or template spectrum
            |
            v
       Exposure-time calculator
            |
            v
      observing plan / SNR target
            |
       +----+-------------------+
       |                        |
       v                        v
   Simulator               Instrument control
       |                        |
       v                        v
   synthetic FITS          acquired FITS frames
       \                        /
        +----------+-----------+
                   |
                   v
             Reduction pipeline
                   |
                   v
            extracted spectra

Reference throughput curves, detector-response data, atmospheric-extinction
data, and template spectra are shared across packages through the
``shared-data`` distribution where practical.

.. note::

   The documentation distinguishes physical instrument assumptions from
   software defaults. In particular, the current design uses a multi-fiber
   linear bundle and the simulator supports the seven-fiber geometry developed
   for the instrument, but fiber count should not be treated as a permanent
   software invariant.

Start here
----------

* :doc:`getting-started` -- install the software and understand the repository split.
* :doc:`user-guide/index` -- end-to-end guide from planning through extracted spectra.
* :doc:`packages/index` -- package-by-package documentation.
* :doc:`reference/conventions` -- units, coordinate, detector, and spectrum conventions.
* :doc:`development` -- how the repositories fit together and how to update these docs.

.. toctree::
   :maxdepth: 2
   :hidden:

   getting-started
   user-guide/index
   packages/index
   reference/index
   development
