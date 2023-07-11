
## Aerospike Observability

### Using the Metric Reference
When your working on observability projects it's incredibly 
important to know what your looking at. The Aerospike 
[metric-reference]() should be open up in a tab. There's a few things to note
about how to use the guide.

* Metric Location - determins what API the metric is from and will determine what
is prepended to the metric. e.g. namespace metrics will be pre-pended with 
`aerospike_namespace` when exported. 

* Type - cummulative, instantaneous, integer is wha the metric reference uses. 
This is typically referred to as counter and guage. 

* Hidden Metrics - metrics from older versions are not shown by default.

* Labels - metrics have labels which allow you to filter, and sort them in
Grafana. 

### Alerting is everything
Alerting is the backbone of the observability experience. When working with
customers start by establishing Service Level Objectives, and work backwards
from there to a set of alerts around latency targets, tenant behavior, and other
app specific details. The alert rules included in our Observability Stack
provide a starting point and expand on the [Key Metrics to Monitor guide]().

###  Use Case Dashboards
When customers are operating Aerospike, they are not worried about particular
metrics, or alerts they wan't to "see what's going on". We organize our dashboards
towards specific use cases, such as.

* Managing mult-tenant users
* Cross Data Center Replication (XDR)
* Rolling Restarts & Upgrades (NEW)
* All Flash (coming soon!)
* Client Metrics (planned)

### Corresponding Cli Use Cases
We have been working to align our CLI experience with the dashboards included.
Unlike the Observability Stack no additional steps or installation is required
to include these new commands. 

Find and show stop writes in your cluster
```
show stop-writes
```
(coming next month in Tools 9.0 asadm will warn you automatically when you approach stop-writes)

Get multi-tenant user information across nodes
```
show user stat
```

### Start managing aerepspike config in YAML!
You can now convert, validate, and compare YAML files to one another. Here's a quick
example walk through. 

1. Start by getting the latest tools package.

2. Change into the `/config/` directory

3. Convert the `aerospike.conf` file to `aerospike.yaml`

```
asconfig convert -f aerospike.conf -a 6.3.0.1 > aerospike.yaml
```

4. Make a change - e.g. remove security section

5. Convert back to a conf file

```
asconfig convert -f aerospike.yaml -a 6.3.0.1 > aerospike-new.conf
```

6. Compare the two conf files

```

```



