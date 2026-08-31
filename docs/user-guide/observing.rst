Operating the instrument
========================

The instrument-control system provides the observing interface while keeping
hardware-specific details behind backend classes.

Development versus deployment
------------------------------

Use mock backends for UI and workflow development. Hardware deployment can use
INDI for instrument-side devices such as the science camera and camera-lens
focus controller, while telescope and guide-side devices can be reached through
ACE Connector interfaces.

This split lets most of the web application and acquisition logic be tested
without physical hardware.

Science exposures
-----------------

The ICS stores completed exposures under its configured data root and exposes
the most recent science FITS image to the web interface for display. The UI can
use JS9 to inspect the current frame without converting the scientific FITS file
to a lossy preview format.

For science operations, preserve the raw FITS files and their metadata. Treat
browser display state as a convenience layer only.

ACE compatibility bridge
------------------------

Where the ACE vendor Python modules are restricted to the x86 observatory host,
a small HTTP service can expose a fixed read-only subset of instrument state.
The bridge is deliberately allow-listed: clients request known resources rather
than arbitrary object names or Python expressions.

The bridge is suitable for status and telemetry. Any control path should remain
explicit and narrowly scoped; do not turn the read-only service into a generic
RPC interface.

Operational caution
-------------------

Hardware configuration, device names, ports, and credentials are deployment
configuration, not library defaults. Keep credentials out of the repository and
use environment files or the deployment system's secret management.
