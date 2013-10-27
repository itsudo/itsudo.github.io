---
layout: post
title:  "Mongodb cluster config"
date:   2013-10-27 12:28:31
categories: mongodb
---

I assume that you have mongodb installed. 

	mongod [other options] --replSet replica_set_name # each member must be started with the same repSet name

so to keep things simple here, on each server run mongod like this:

	mongod --fork --dbpath data --logpath mongodb.log --replSet myreplicaset

Now connect to the node that you wolud like to be a master ('primary' in mongodb terminology)

	mongo mongo0.example.com:27001

and initiate config for the cluster (replica set). NOTE: If there is no data, it doesn't matter which one is master, but if you have data, make that one a master, otherwise you will loose data

	replSetCfg = 
	{
		"_id" : "myreplicaset", // it is the same as our replSet argument passed to mongod on startup
		"members" : [
			{
				"_id" : 0,
				"host" : "mongo0.example.com:27001"
			},
			{
				"_id" : 1,
				"host" : "mongo1.example.com:27001"
			},
			{
				"_id" : 2,
				"host" : "mongo2.example.com:27001"
			}
		]
	}

	rs.initiate(replSetCfg)

Note on host names: use names that are dns resolvable with short ttl (1-5min). This is important so IPs can be switched quickly if you need to replace a machine in the replicaset.

Check status of the replicaset with
	
	rs.status()

At this stage, we can only read and write from/to master. If you try reading from slaves you get an error, as mongo slave can be behind the master. To declare, that we are fine with this slight lag in data consistency, and we are happy to read from slaves, on each slave we need to issue
	
	rs.slaveOk()