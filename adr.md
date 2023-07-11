
## Aerospike Database Recovery

### Backup, replication, and archiving
We have a variety of tooling to help with various disaster scenarios
and considering what to choose means understanding your customers needs.

1. Multi-site cluster w/strong consistency (stretch cluster) - This
provides guaranteed writes across multiple sites but comes with a 
performance penalty for writes.

1. XDR Passive cluster - This provides the ability to failover to a 
fully replicated dataset in seconds or less. This is for true disaster recovery 
scenarios and ADR does not replace this, but is built ontop of some
of the underlying technologies.

1. ADR - This is expected to be layered into the above data protections
with the ability to go "back in time" to a specified time range. 

1. asbackup/asrestore - This still has a role operationally, and will continue to
be supported for the forseeable future. It's lightweight and leaves the 
policy, and restore details up to the user.

### How ADR works

1. Requires a backup Aerospike cluster, s3 storage, and kubernetes microservices
1. Changes in records are shipped into the backup cluster, and asynchronously worked off into the s3 storage.
1. The backup cluster has a namespace mapped for each backup policy enabled, and 1 for storing meta data for
looking up records in s3. This limits the number of total backup policies to 31. 
1. Everything is periodically backed up to s3 so that you can bootstrap a cluster just from s3.

### Layering ADR into an environment
It's likely that your customers will be bringing ADR to a Aerospike environment
that is already significantly complex, so a few thoughts and pointers.

1. Start with the docker-compose example we're walking through and build them up to AWS
1. For passive clusters plan to deploy ADR at the primary site, and use [s3 cross region replication]()
to ship backups to a secondary site.

### Why isn't this called PITR
The differences in the behavior of the ADR system is best explained by the following
specifics.

1. A point-in-time system allows the user to specify a particular (single) timestamp when request a record.
1. Our system takes a time-range input to find and returns all available versions of that record.

### Installing user docker-compose
Let's hop over to the [Aerospike Database Recovery getting started guide]()