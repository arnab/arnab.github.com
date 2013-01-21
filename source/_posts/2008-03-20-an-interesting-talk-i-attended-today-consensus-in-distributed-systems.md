---
author: Arnab
title: 'An interesting talk I attended today - Consensus in distributed systems'
excerpt:
layout: post
category: programming
tags:
  - amazon
  - architecture
  - design
post_format: [ ]
---
Went to an incredible talk today and was so damn impressed with the presentation and the concepts behind. So wanted to share it with you…<o:p></o:p>

Basically the talk was on Consensus among Distributed Systems. So if you have a Master DB and two Slaves – and if the master dies, how do you choose which Slave to promote, automatically?<o:p></o:p>

Or consider you have some sort of a pool of managers who decide what to do and a bigger pool of workers who do what the managers say. Let’s say a manager dies – how do you choose which worker to promote to a manager? Because all of them might be equally eligible to get promoted (we are talking about systems here not humans).<o:p></o:p>

The simple way is – go for the majority. So every worker votes and one of them is elected. But then take in some factors such as message losses, network disturbance and partial network failure – now your vote might not have been so accurate after all ha?<o:p></o:p>

Good Robust systems built to be successful must be fault-tolerant and self-healing. It has to take care of its own – if some process fails, it has to figure out a way to fix it by itself – no human intervention – coz that takes time and money – which is not always easy or affordable. Now if it’s just one system you could somehow make it think of these situations. But make a distributed system where each worker has its own mind! The group (distributed system) has to come to \_correct\_ decision somehow right?<o:p></o:p>

<o:p> </o:p>To build such (distributed) systems we need to be able to solve this problem of consensus. A few people have started or already have implemented this (including Google Chubby, Microsoft Autopilot, Amazon S3 etc.)<o:p></o:p>

<o:p> </o:p>
So this talk was about all this – must say it was done in a very lively manner – with a skit showing the different parts of the system, the network (where volunteers passed messages and took parts of the system – some \_crashed\_ too ). Was fun!<o:p></o:p>

<o:p> </o:p>
The idea stems from ancient ages and has been modeled to meet the requirements we have today. It’s called Paxos Protocol. Do read up on it – very interesting… You will definitely have nothing but appreciation for the great minds that created the mathematical model in those ancient times and the other great minds who translated it to modern day distributed systems and the other minds who have/are implementing these ideas!<o:p></o:p>

<o:p> </o:p>Here are some links:<o:p></o:p>

*   <o:p> </o:p>The Consensus problem: [http://en.wikipedia.org/wiki/Consensus\_%28computer\_science%29][1] <o:p></o:p>
*   <o:p> </o:p>The algorithm: <http://en.wikipedia.org/wiki/Paxos_algorithm> <o:p></o:p>
*   <o:p> Pa</o:p>rt-Time Parliament by Leslie Lamport: <http://research.microsoft.com/users/lamport/pubs/lamport-paxos.pdf> <o:p></o:p> (I highly recommend this one – very interesting read – and begins in an interesting manner)<o:p></o:p>
*   Leslie Lamport: <http://en.wikipedia.org/wiki/Leslie_Lamport> <o:p></o:p>

 [1]: http://en.wikipedia.org/wiki/Consensus_%28computer_science%29