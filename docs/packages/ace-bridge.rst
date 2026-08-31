ACE read-only bridge
====================

Purpose
-------

The ACE read-only bridge is a compatibility service for deployments where the
vendor ACE Connector Python modules are only usable on the observatory x86 host.
It exposes selected state over a small HTTP API so another machine can consume
telemetry without loading the vendor extension modules.

Security model
--------------

The bridge is intentionally not a generic RPC server. Requests cannot provide a
Python expression, arbitrary ACE attribute name, or arbitrary method name.
Only fixed, allow-listed reads are exposed.

Only ``GET``, ``HEAD``, and ``OPTIONS`` are accepted. State-changing HTTP verbs
are rejected before device lookup.

HTTP resources
--------------

The service provides an unauthenticated health endpoint plus authenticated
resource/snapshot endpoints:

.. code-block:: text

   GET /healthz
   GET /v1
   GET /v1/health
   GET /v1/devices
   GET /v1/devices/<id>
   GET /v1/snapshot

A partial ACE read failure is reported for the affected field rather than
causing the service to guess another call or invoke a state-changing method.

Deployment note
---------------

The first-cut service uses ordinary HTTP. Restrict it to the observatory/private
network and use an appropriate protected transport or tunnel if traffic crosses
an untrusted network. The bearer token is not encryption.
