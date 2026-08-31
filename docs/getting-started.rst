Getting started
===============

Software layout
---------------

The software stack is organized as several repositories with distinct
responsibilities. Keeping these concerns separate makes the scientific
packages usable without requiring observatory-control dependencies and keeps
shared calibration/reference files from being copied into every repository.

.. list-table:: Main repositories
   :header-rows: 1
   :widths: 20 80

   * - Repository/package
     - Role
   * - ``etc``
     - Predict source and sky counts and signal-to-noise for a supplied spectrum,
       instrument configuration, exposure time, and optional photometric scaling.
   * - ``simulator``
     - Forward-model spectra through the optical geometry and detector to produce
       realistic synthetic data products.
   * - ``pipeline``
     - Reduce detector frames and extract one-dimensional spectra from the fiber
       traces, carrying masks and uncertainties through the reduction.
   * - ``shared-data``
     - Installable package containing common CSV calibration/reference curves and
       reference spectra.
   * - instrument-control system (ICS)
     - Operate and monitor the science camera, camera-lens focus, telescope-side
       guide hardware, and related observatory interfaces.

Environment strategy
--------------------

For development, clone the repositories side-by-side and use editable installs.
A typical checkout can look like this:

.. code-block:: text

   spectrograph/
   ├── etc/
   ├── simulator/
   ├── pipeline/
   ├── shared-data/
   ├── ics/
   └── docs/

Create a virtual environment and install the packages you need. Package metadata
should declare ``shared-data`` as a dependency rather than asking users to copy
its files manually.

.. code-block:: bash

   python -m venv .venv
   source .venv/bin/activate
   python -m pip install -U pip
   python -m pip install -e ./shared-data
   python -m pip install -e ./etc
   python -m pip install -e ./simulator
   python -m pip install -e ./pipeline

The ICS can be kept in a separate environment because hardware-control stacks can
have tighter platform and version constraints than the analysis software.

Which package do I need?
------------------------

Use the ETC when you are deciding whether an observation is practical or how
long to expose. Use the simulator when you need a detector-level prediction,
want to exercise the pipeline without real data, or want to study how geometry
changes the recorded traces. Use the pipeline for real or simulated FITS data.
Use the ICS only when controlling the instrument or developing against its mock
backends.

Continue with :doc:`user-guide/index` for the complete observing workflow.
