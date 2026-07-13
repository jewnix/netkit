# Changelog

All notable changes to the NetKit App are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-07-13

### Added

- Ping Trends dashboard for connect latency and jitter by target.
- Speedtest Trends dashboard for download, upload, and latency trends.
- Availability dashboard for complete-outage KPIs, an outage timeline, and per-target status.
- App Health dashboard for NetKit's probe logs.
- Search-time JSON field extraction for netkit:ping and netkit:speedtest events.
- CIM-friendly field aliases: latency, dest_port, bytes_in, bytes_out, duration.
- netkit_index macro for targeting the destination index.
