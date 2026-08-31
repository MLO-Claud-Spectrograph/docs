Simulating detector data
========================

The simulator converts one or more input spectra into a synthetic detector
image. Its current model is unit-aware through Astropy quantities and computes
important detector-space quantities from the physical spectrograph geometry.

Inputs and units
----------------

Wavelength and flux-density arrays should carry Astropy units. The simulator
internally converts wavelength to Angstrom and flux density to
``erg / (s cm2 Angstrom)`` before computing photon/electron counts.

For a multi-fiber simulation, supply a two-dimensional flux array with shape
``(fiber_count, n_wavelength)``. All fibers share the same wavelength grid, but
each row can contain a different spectrum.

Detector sampling
-----------------

Input spectra can be more coarsely sampled than the detector dispersion. Before
rendering, the simulator inserts a sufficiently fine wavelength grid and
linearly interpolates each spectrum onto it while preserving the original
samples as interpolation breakpoints. This prevents gaps in traces that would
otherwise appear when sparse spectral samples are deposited directly on the
detector.

Optical geometry
----------------

The spectrograph model derives the central wavelength from

.. math::

   m\lambda = d(\sin\alpha + \sin\beta),

where ``m`` is the diffraction order, ``d`` the groove spacing, ``alpha`` the
incidence angle, and ``beta`` the diffraction angle.

The detector dispersion is derived from groove spacing, diffraction angle,
camera focal length, and detector pixel size. Fiber pitch and fiber image width
are likewise projected from physical dimensions through the
camera/collimator magnification.

Image formation
---------------

For each wavelength sample and fiber, the simulator:

#. multiplies the source flux by collecting area and the combined throughput;
#. converts energy flux to expected photoelectrons;
#. maps wavelength to detector ``x`` through the grating geometry;
#. maps the fiber to the appropriate detector ``y`` trace;
#. deposits the counts with a two-dimensional Gaussian kernel; and
#. optionally applies a vignetting map.

The detector model can then add Poisson noise, dark current, read noise, full
well clipping, gain conversion, and bias to return an ADU image.

Use a fixed random seed when producing regression fixtures for the pipeline.
