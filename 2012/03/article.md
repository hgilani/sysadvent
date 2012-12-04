# Zero-Downtime Deployments with Active-Passive MySQL

This was written by [Bob Feldbauer](http://twitter.com/bobfeldbauer).

It's time to deploy a new version of our awesome application, but this time
we're changing database stuff. Can we do it without an outage?

Schema changes can often lock your database, stall your application, and cause
an outage, so you'll want to be careful in how you design the infrastructure
to permit database changes.

Achieving a zero-downtime schema deployment can be done with load balancer and
a technique called [Blue-Green](http://martinfowler.com/bliki/BlueGreenDeployment.html
*Blue-Green Deployment*) deployment.

"Blue-Green deployment" is a fancy term that basically means you have two sets
of an application stack. You start with Blue (version N) and Green (N-1),
deploy version N+1 to the Green stack, and then cutover to the Green stack.

Traffic for a high-availability architecture for an application might look like
this:

![](https://lh5.googleusercontent.com/-lh0WFxOXlac/ULwyLBXg5BI/AAAAAAAAAHo/0OckggXE7Cs/s419/zero-downtime-mysql1.jpg)

Summarizing the above image: 

* Incoming requests hit the main loadbalancers
* That traffic is routed to a pair of caching proxies
* Then shipped to another set of loadbalancers
* Before hitting the application servers themselves, which have Blue-Green
  versions (N and N-1 respectively).
* The application servers read and write to a database.

Changing the load balancers to point to different web or application servers
with new versions to implement Blue-Green is generally trivial; however,
deployments with database schema changes aren't always trivial. Schema changes
often lock the database which means an outage for your application during the
change.

You can implement blue-green deployments for mysql using Master-Master. Many
people have tried Master-Master MySQL over the years and found it to be a
painful experience. The traditional Master-Master MySQL setup involves two
active database servers (we'll call this "Active-Active"). The problem is that
both servers can accept reads and writes, and conflicting writes will cause
replication to break.

Instead of the traditional Active-Active approach, we can use an Active-Passive
MySQL setup to achieve many of the same benefits while avoiding the danger of
conflicting writes breaking replication, *and* it will still allow us to do
zero downtime deployments with database schema changes.

In an Active-Passive setup, there are two database servers, but only one can
accept writes at any given time. (The one that can accept writes is the
"Active" server, while the read-only server is "Passive".) To achieve this, we
simply add an additional load balancer layer between the application and
database tiers.

Traffic in our new example architecture would swap the last step ("The
application servers talk to a database") for these two new steps:

* The application servers connect to a pair of high-availability load balancers
  for their database queries
* The load balancer sends database connections to the Active MySQL server

![](https://lh4.googleusercontent.com/-liRHbdWsWsY/ULwyLCZz_GI/AAAAAAAAAHs/VA80Zduaovg/s400/zero-downtime-mysql2.jpg)

## MySQL Replication Details

Each server (both Active and Passive) has a MySQL Master and Slave running on
it, just like a Master-Master (Active-Active) setup. Changes occur as follow:
  
* Changes get written to the active server's binary log and flow through
  replication to the passive server's relay log
* The passive server executes the query and writes the event to its own binary
  log
* The active server retrieves the same change via replication into its relay
  log, but ignores it because the server ID in the event matches its own 

## Active-Passive MySQL Server Configuration

Just make sure to set server-id to unique values for both servers (i.e. 1 for
server X, 2 for server Y), and this is all you realy need: 

    server-id=1
    log_bin=/var/lib/mysql/mysql-bin.log
    sync_binlog=1
    log_slave_updates=1
    log_bin_index=/var/lib/mysql/mysql-bin.index
    relay_log=/var/lib/mysql/slave-relay.log
    relay_log-index=/var/lib/mysql/slave-relay-log.index
    binlog_do_db=Your Database Name

## Zero Downtime Database Schema Changes

Let's get down to the nitty-gritty details of how zero downtime database schema
changes actually work:

* Run STOP SLAVE on both the Active and Passive servers
* Run SQL for the schema change on the Passive server
* Run START SLAVE on the Active server
* Wait for replication lag on the Active server to become small enough (ideally
  about a second). You can check replication lag with SHOW SLAVE STATUS
  "Seconds_Behind_Master", although that isn't 100% reliable and you are better
  off with something like Percona's MySQL Toolkit's
  [pt-heartbeat](http://www.percona.com/doc/percona-toolkit/pt-heartbeat.html).
* Run LOCK TABLES on the Active server for the final replication catchup
* Ensure replication lag is zero on the Active server
* Modify your proxy configuration to change the Active/Passive designations
* Unlock the new Passive server
* Run START Slave on the new Active server

## Required Rules for Schema Changes

One small caveat to the whole process is that you must be able to
follow/enforce two basic rules for schema changes to work:

1. The new schema must be backwards compatible with the previous schema:
 * Add new columns with triggers rather than modifying in place
 * New columns cannot be required immediately, or old writes will not replicate appropriately
 * No use of server-generated data functions (UUID, NOW, RAND, etc)
2. It cannot conflict with pending writes:
 * No auto-increment INSERT unless the application doesn't insert to that table
 * No DROP COLUMN nor DELETE rows if they are used in the previous schema version

## Conclusion

Don't forget about your databases!

Using an Active-Passive MySQL setup allows zero downtime deployments to become
a reality. Active-Passive is much less scary than the traditional
Active-Active, Master-Master MySQL setup you may have tried in the past.

## Further Reading
  
* [Etsy's deployments using on Master-Master MySQL](http://codeascraft.etsy.com/2012/04/20/two-sides-for-salvation/)
* [High Performance MySQL](http://shop.oreilly.com/product/0636920022343.do), "Replication" (Ch. 10 in 3rd edition, Ch. 8 in 2nd edition)
* [MySQL Load Balancing with HAProxy](http://blogs.reliablepenguin.com/2011/03/31/mysql-load-balancing-with-haproxy)

