Data products
=============

Raw detector frames
-------------------

Raw FITS files from the ICS are the authoritative acquisition products. Keep
all original headers and do not overwrite the raw files during reduction.

Calibrated detector frames
--------------------------

Pipeline calibration products should preserve data, unit, mask, and uncertainty
information together. The exact serialization can evolve, but the scientific
meaning of those components should remain explicit.

Extracted spectra
-----------------

The pipeline should retain one product per extracted fiber through the low-level
processing stages. A final science product can then associate fiber spectra with
roles or spatial positions according to the observation metadata.

Simulation products
-------------------

Synthetic detector frames should record enough simulator configuration to be
reproduced: physical spectrograph parameters, detector model, throughput data
versions, exposure time, random seed, and input-spectrum provenance.
