---
layout: post
title: Kafka leader broker down with hard drive failure while secondary broker leave the ISR, how to not lose all your Kafka messages.
---

By default Apache Kafka brokers’ configuration have the unclean leader election disabled, field **unclean.leader.election.enable=false**. [Kafka documentation](https://kafka.apache.org/documentation/#brokerconfigs).

If you haven’t change it, let’s say the following scenario occurs:

* MyPartition is led by BrokerA and followed by BrokerB.
* BrokerA is on offset 1000
* BrokerB is on offset 980
* BrokerB falls out of the In Sync Replica list (that I’ll name later ISR), leaving only BrokerA in the ISR.
* BrokerA has a hard drive failure and goes down. Which means _all messages held by this broker are now permanently lost._

If we bring back BrokerA online all these messages are lost. Which is the worst scenario possible.

### What can we do to get out of this situation by not losing everything?

First, Apache Kafka’s [documentation](https://kafka.apache.org/documentation/#design_uncleanleader) says:

**Kafka's guarantee with respect to data loss is predicated on at least one replica remaining in sync. If all the nodes replicating a partition die, this guarantee no longer holds.**

Two choices stand in front of us:
- Wait for a replica in the ISR to come back to life and choose this replica as the leader (hopefully it still has all its data).
- Choose a replica (not necessarily in the ISR) that comes back to life as the leader.

To be able to use the solution 2 you need to change the configuration of your BrokerB, which is out of the ISR:

```
unclean.leader.election.enable=true
```

Restart BrokerB and it will become the leader with its 980 messages. Therefore, you’ll lose only 20 messages.

**Other recommendations:**

In order to prevent these situations, it could also be good to use the equivalent of AWS EBS, in case of your infrastructure being on AWS services, or to use JBOD or RAID to prevent infrastructure component failure.

Another good practice wold be to not consider messages committed if they are not replicated to all followers. [Documentation](https://kafka.apache.org/documentation.html#replication)