Planning an observation
=======================

The exposure-time calculator is the first scientific tool in the normal
workflow. It predicts the signal-to-noise ratio in user-selected wavelength bins
for a source spectrum and instrument configuration.

Inputs
------

The core calculation accepts a reference or target spectrum together with:

* exposure time;
* redshift;
* wavelength-bin centers and bin size;
* sky surface brightness;
* detector/camera model;
* grating choice;
* numerical airmass;
* fiber length;
* detector temperature; and
* optional target AB magnitude plus LSST magnitude band for flux scaling.

The ETC currently supports scaling a template spectrum to LSST ``g``, ``r``,
or ``i`` photometry in the AB system. This is useful when the spectral
shape is known or assumed but only broadband target photometry is available.

Detector sampling, projected fiber width, read noise, telescope collecting
area, and the component throughput model are derived from the selected camera
and the shared ``spectrograph-sim`` instrument model rather than entered as
independent GUI parameters.

Throughput accounting
---------------------

The calculation keeps the major throughput terms separate before multiplying
them into the total response. This makes it possible to inspect detector,
grating, fiber, atmosphere, and lens contributions individually and to disable a
term for diagnostic comparisons.

The reported result for each wavelength bin includes source counts, sky counts,
S/N, and mean component throughputs. Detector read noise and dark current are
included in the noise budget.

Recommended workflow
--------------------

#. Choose a representative template spectrum covering the wavelength region of
   interest.
#. Redshift it as required and, if needed, scale it to the target's measured
   LSST ``g``, ``r``, or ``i`` AB magnitude.
#. Select the expected camera/grating configuration and airmass.
#. Evaluate several wavelength bins, especially the region containing the
   diagnostic spectral feature that drives the observation.
#. Adjust exposure time until the limiting bin reaches the desired S/N.
#. Check the component-throughput plot if the result is unexpectedly poor.

The ETC answer is a planning estimate, not a substitute for the simulator when
pixel-level effects, trace overlap, saturation morphology, or extraction
behavior matter.
