# netkit (NetKit visualization app)

Installed on the Splunk Cloud search head. Provides four Dashboard Studio views
(Ping Trends, Speedtest Trends, Availability, App Health) plus search-time JSON
extraction and the `netkit_index` macro. The field extractions and the macro are
exported globally so ad-hoc searches work from any app; the views stay scoped to
this app.

## Requires the NetKit Add-on

This app only visualizes data; it does not collect it. Install the companion
collection add-on, [TA_netkit](https://github.com/jewnix/TA_netkit), on a Heavy
Forwarder to run the probes and produce the `netkit:ping` and `netkit:speedtest`
events these dashboards read, then point `netkit_index` at the index it writes to.

## CIM (Common Information Model)

NetKit's probe events are members of the CIM **Network Traffic** data model
(`All_Traffic`). Two things are required for the data model to return them:

1. Install the **Splunk CIM Add-on** (`Splunk_SA_CIM`) on the same search head.
2. Add NetKit's index (default `index=main`) to `cim_Network_Traffic_indexes` via
   the CIM Setup UI, otherwise the data model stays empty.

Filter NetKit's synthetic traffic with `vendor_product=NetKit`.

## Install (Cloud search head)

1. Install this app via ACS / Splunk Web.
2. Create (or identify) the destination index that
   [TA_netkit](https://github.com/jewnix/TA_netkit) writes to.
3. Point the `netkit_index` macro at that index: create
   `netkit/local/macros.conf` with:

       [netkit_index]
       definition = index=<your_index>

   The shipped default is `index=main`.

## Dashboards

- Ping Trends - connect-latency and jitter by target.
- Speedtest Trends - download/upload/latency over time.
- Availability - complete-outage KPIs, outage timeline, and per-target status.
- App Health - NetKit's own logs (index=_internal sourcetype=netkit_log).
