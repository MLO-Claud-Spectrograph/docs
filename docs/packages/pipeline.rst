Pipeline
========

Purpose
-------

The pipeline reduces raw or calibrated spectrograms into extracted spectra while
preserving detector masks, uncertainties, and per-fiber identity.

Processing levels
-----------------

The current code separates detector/image handling from the Level-1 spectral
extraction. A typical instrument-specific script reads a FITS frame into a
CCD-style object, locates or supplies the trace centers, and calls the generic
Level-1 processing routines.

Primary extraction interface
----------------------------

``process_l1(...)`` is the main entry point used by instrument-specific
extraction scripts. Its extraction configuration includes trace centers,
extraction half-width, detector gain, and read noise. The function delegates to
optimal extraction of the requested traces and returns one spectrum per trace.

A representative pattern is:

.. code-block:: python

   spectra = process_l1(
       ccd,
       centers=trace_centers,
       half_width=8,
       gain=detector_gain,
       read_noise=detector_read_noise,
   )

Keep detector-specific constants in the instrument adapter or configuration
layer rather than baking them into the reusable extraction algorithm.

Masks and variance
------------------

The pipeline should treat saturation and other invalid detector pixels as masks.
A mask is not the same thing as replacing a value with ``NaN``: the underlying
value can remain available while the extraction/combination logic knows that it
must not contribute as a valid measurement.

Variance used by optimal extraction should include the appropriate detector
noise terms and should remain consistent with the CCD data unit.

Per-fiber outputs
-----------------

Return every extracted fiber independently. Higher-level processing can label
fibers as science, sky, or calibration based on the observing configuration,
but the low-level extraction code should not assume a permanent semantic role
for a fixed fiber number.
