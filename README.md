# nagios-plugin-ekg

This package provides `check_ekg`, a generic plugin for Nagios (and
compatible) monitoring systems which translates metrics exposed by
[ekg](https://hackage.haskell.org/package/ekg) into perfdata suitable
for use with pnp4nagios and similar tools.

There is currently no support for threshold checks; the plugin will
always return an `OK` result if it can obtain and parse output from
the EKG endpoint. Its primary function is to allow gathering
performance data over time from EKG-enabled Haskell applications;
there are no current plans to add support for thresholds/alerting,
though I'd consider it in the future if there was demand.

# Usage

The plugin can either be executed directly on the Nagios host or
invoked via NRPE.

Example invocation:

```
$ check_ekg -e http://haskell-app.example.com:8000
OK: perfdata only | iterations=60614c;;;; rts_gc_bytes_allocated=0c;;;; rts_gc_bytes_copied=0c;;;; rts_gc_cpu_ms=0c;;;; rts_gc_cumulative_bytes_used=0c;;;; rts_gc_current_bytes_slop=0.0;;;; rts_gc_current_bytes_used=0.0;;;; rts_gc_gc_cpu_ms=0c;;;; rts_gc_gc_wall_ms=0c;;;; rts_gc_max_bytes_slop=0.0;;;; rts_gc_max_bytes_used=0.0;;;; rts_gc_mutator_cpu_ms=0c;;;; rts_gc_mutator_wall_ms=0c;;;; rts_gc_num_bytes_usage_samples=0c;;;; rts_gc_num_gcs=0c;;;; rts_gc_par_avg_bytes_copied=0.0;;;; rts_gc_par_max_bytes_copied=0.0;;;; rts_gc_par_tot_bytes_copied=0.0;;;; rts_gc_peak_megabytes_allocated=0.0;;;; rts_gc_wall_ms=0c;;;; ekg_server_timestamp_ms=1435214338224c;;;;
$ echo $?
0
```
