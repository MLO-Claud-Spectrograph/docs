ETC
===

Purpose
-------

The exposure-time calculator estimates detected source counts, sky counts, and
signal-to-noise in wavelength bins for the spectrograph. It contains a reusable
calculation layer and a Tk-based desktop interface.

Primary interface
-----------------

``ETCCalculator`` is the scientific core. The most important methods and
properties are:

``get_SNR_from_spectrum(...)``
   Calculate counts and S/N for one or more wavelength bins.

``load_spectrum(spectrum_file, z)``
   Load a two-column reference spectrum and place its wavelength grid in the
   frame expected by the current calculator.

``scale_spectrum_to_magnitude(...)``
   Scale a template spectrum to a target Johnson ``B`` or ``V`` magnitude in
   the Vega or AB system.

``get_throughput_components(...)``
   Return detector, grating, fiber, atmosphere, lens, and total throughput
   arrays on a supplied wavelength grid.

``available_camera_models`` / ``available_gratings``
   Enumerate the configurations represented by the installed reference data.

Result structure
----------------

``get_SNR_from_spectrum`` returns a mapping containing:

``bins``
   A sequence of ``SNRBinResult`` objects with wavelength center, source counts,
   sky counts, S/N, and mean component throughputs.

``meta``
   Resolved detector/instrument inputs such as read noise, pixel scale, grating,
   atmosphere model, and any spectrum-scaling factor.

``throughput_plot``
   Wavelength and component arrays suitable for plotting the response used in
   the calculation.

Example
-------

.. code-block:: python

   from etc_core import ETCCalculator

   calc = ETCCalculator(fiber_length_m=10.0)
   result = calc.get_SNR_from_spectrum(
       exp_time=1800.0,
       spectrum_file="target_template.txt",
       z=0.03,
       wave_centers=[500.0, 600.0, 700.0],
       binsize=5.0,
       target_magnitude=17.5,
       magnitude_band="V",
       magnitude_system="AB",
   )

   for bin_result in result["bins"]:
       print(bin_result.wave_center_nm, bin_result.snr)

Data dependency
---------------

Instrument throughput/reference files should come from ``shared-data`` rather
than being maintained independently in the ETC repository. This makes changes
to detector QE, grating efficiency, atmospheric extinction, or reference
spectra explicit shared-data version changes.
