# Changelog

All notable changes to the NetKit App are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-07-21

### Added

- Ping Trends dashboard for connect latency and jitter by target.
- Speedtest Trends dashboard for download, upload, and latency trends.
- Availability dashboard for complete-outage KPIs, an outage timeline, and per-target status.
- App Health dashboard for NetKit's probe logs.
- Search-time JSON field extraction for netkit:ping and netkit:speedtest events.
- Field aliases (latency, dest_port, bytes_in, bytes_out, duration) for the metric sourcetypes.
- CIM Network Traffic (All_Traffic) data model membership via eventtypes.conf, tags.conf, and search-time field normalization.
- commonInformationModels declaration (Network_Traffic) in app.manifest.
- netkit_index macro for targeting the destination index.
- Certificate Monitoring dashboard for certificate expiry, validation status, and chain trust by target.
- Search-time JSON field extraction and CIM Certificates data model normalization for netkit:tls events.
- Search-time naming for netkit:tls certificate fields (eku, key usage, signature algorithm) via lookups, plus pubkey and key-usage fields.
- commonInformationModels declaration (Certificates) in app.manifest.
- Alert: NetKit - Certificate expiring soon.
- Alert: NetKit - Certificate validation failed.
- Alert: NetKit - Certificate changed.

