# netkit (NetKit visualization app)

Installed on the Splunk Cloud search head. Provides five Dashboard Studio views
(Ping Trends, Speedtest Trends, Certificate Monitoring, Availability, App Health),
three certificate alerts, plus search-time JSON extraction and the `netkit_index`
macro. The field extractions and the macro are exported globally so ad-hoc
searches work from any app; the views stay scoped to this app.

## Requires the NetKit Add-on

This app only visualizes data; it does not collect it. Install the [NetKit
Add-on](https://splunkbase.splunk.com/app/9165) on a full Splunk Enterprise
instance (on-prem only, never the Cloud search head) to produce the `netkit:ping`,
`netkit:speedtest`, and `netkit:tls` events these dashboards read, then point
`netkit_index` at the index it writes to.

## CIM (Common Information Model)

NetKit's probe events are members of the CIM **Network Traffic** data model
(`All_Traffic`). Two things are required for the data model to return them:

1. Install the **Splunk CIM Add-on** (`Splunk_SA_CIM`) on the same search head.
2. Add NetKit's index (default `index=main`) to `cim_Network_Traffic_indexes` via
   the CIM Setup UI, otherwise the data model stays empty.

Filter NetKit's synthetic traffic with `vendor_product=NetKit`.

## Install (Cloud search head)

1. Install this app via ACS / Splunk Web.
2. Create (or identify) the destination index that the [NetKit
   Add-on](https://splunkbase.splunk.com/app/9165) writes to.
3. Point the `netkit_index` macro at that index: create
   `netkit/local/macros.conf` with:

       [netkit_index]
       definition = index=<your_index>

   The shipped default is `index=main`.

## Dashboards

- Ping Trends - connect-latency and jitter by target.
- Speedtest Trends - download/upload/latency over time.
- Certificate Monitoring - certificate expiry, validation status, and chain trust
  by target.
- Availability - complete-outage KPIs, outage timeline, and per-target status.
- App Health - NetKit's own logs (index=_internal sourcetype=netkit_log).

## Alerts

Three certificate alerts ship scheduled and enabled, with no alert action
configured; add an action (email, webhook) per site to be notified.

- NetKit - Certificate expiring soon
- NetKit - Certificate validation failed
- NetKit - Certificate changed
