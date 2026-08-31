shared-data
===========

Purpose
-------

``shared-data`` is an installable Python distribution containing common
spectrograph reference files. It exists so that each scientific repository can
declare a dependency on one authoritative data package instead of carrying a
private copy of the same curves.

Package layout
--------------

The current distribution contains two top-level data directories:

.. code-block:: text

   shared-data/
   ├── __init__.py
   ├── csv_files/
   │   └── *.csv
   ├── reference_spectra/
   │   └── ...
   └── pyproject.toml

The distribution name is ``shared-data`` and the import package is
``shared_data``.

The packaging metadata includes ``csv_files/*.csv`` and all files immediately
under ``reference_spectra`` as package data.

Accessing packaged files
------------------------

Use ``importlib.resources`` rather than constructing a filesystem path from
``__file__``. This works with normal installations and avoids making callers
know the package's installation layout.

.. code-block:: python

   from importlib.resources import files

   import shared_data

   qe_file = files(shared_data) / "csv_files" / "KL400BI_qe.csv"

   with qe_file.open("rb") as handle:
       payload = handle.read()

For libraries that require a real path, use ``importlib.resources.as_file`` so
the resource remains compatible with different import/package loaders.

What belongs here?
------------------

Put data here when multiple spectrograph packages need the same authoritative
file: detector QE curves, grating-efficiency curves, fiber attenuation,
atmospheric extinction, and common reference spectra are typical examples.

Do not put generated observation products or user-specific calibration data in
this package.
