## Aerospike Observability Demo Workshop

### Pre-requisites

1. Docker & docker-compose - you probably already have this. 
1. [Aerolab 6.2+](https://github.com/aerospike/aerolab/releases/tag/6.2.0-0dc1bb4) - the draft release latest version has some additional dashboards you'll want for this demo.

### Clone aerospike-monitoring repo

```
git clone 
cd aerospike-monitoring
```

### Try the docker-compose example (2 minutes)
Run the following and click the link to open.
```
cd examples/docker/ && \
docker compose up -d && \
echo "http://localhost:4000" 
```
Once you're done go ahead and tear it back down

```
docker compose down
```

### Try the aerolab example (5 minutes)
```
cd ../aerolab/ 
```
I recommend configuring your backend to docker for the workshop

```
aerolab config backend -t docker
```

```
./01-create.sh && \
echo "http://localhost:3000"
```

### Multi-cluster view and editing dashboards. 
Before we start exploring the dashboards, let's put some load on the cluster so something 
interesting is happening.

```
./02-load.sh
```

1. The geomap view is powered by the lat/long details specified in `ape1.toml`, and `ape2.toml`
1. The panels below require selecting a datacenter (tho I thought they used to repeat)
1. Let's edit a query in depth and explore the labels.
1. If you want to make a change, let us know about it. Let me show you how to export a dashboard

### Triggering stop writes
Let's use asadm and set quotas (new feature) to set of an alert.

```
aerolab attach shell -n dc1
```
1. run `asadm` and enable management mode
1. use the `manage config` command to set the stop-write size on the set `testset` to something very low
1. navigate back to the overview dashboard





