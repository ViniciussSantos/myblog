+++
title = "Becoming the engineer i want to be"
description = "My project-driven learning plan to become the engineer I always wanted to be"
date = 2026-07-25
[taxonomies]
tags = ["planning", "engineering", "learning"]
+++

A common frustration with most software engineers in the same moment in their careers as me is the fact you know enough to be useful every day, but also know how much you don't understand. You rely on databases whose internals are a black box, you push data through pipelines that you couldn't build from scratch, you use distributed systems, but you have no idea how to implement the primitives they use. 
 
That's a feeling that has been bothering me for a while. I have a computer science degree, I've read the books, the Kleppmans, The Tanenbaums, the Cormen. I'm a software engineer for a living, I spend a big chunk of my day programming. But reading about a thing and building a thing are different kinds of knowledge, and I've decided I want the second kind. So I decided to create a plan.
 
The approach is simple: implement everything from scratch, in the language that best matches what each project is actually teaching, with no scaffolding beyond the papers and books that describe the original ideas. My goal isn't to produce amazing production-level software/code, it's to develop the kind of deep knowledge that changes how you reason about systems even when you're not building them from scratch. 
 
I don't want to use AI for anything beyond asking simple questions, no AI agents writing code for me, I want to do everything by hand. AI would be more an assistant than an agent writing code, because anything else would defeat the purpose of this plan. To learn, I need to do it myself and fail, not make an AI do it for me.
 
# Getting warmed up 
These are ideas or projects that I wanted to do for a long time, but I never did for a myriad of reasons. Most of them are challenges or tutorials.
 
- **Fly.io Distributed Systems Challenges**: A few years ago, I discovered Jon Gjengset's youtube channel and I watched a lot of his videos. He had so many interesting ideas and projects that he worked on during his livestreams. [One of these videos](https://www.youtube.com/watch?v=gboGyccRVXI) was him solving the fly.io distributed systems challenges in rust, so I decided to take a stab at it. My plan here is to do the challenge in the language they were planned for, which is go. Even though I love programming in rust, I kinda want to branch out and use go because it has been such a long time since I used this language. The challenges go from pretty simple to complex, and my plan is to solve all of them. Let's see how it goes. 
- **MIT 6.5840 labs**: In my distributed systems class in college, I had to implement two things (in Java of all things), a peer-to-peer file sharing application very similar to a simplified version of napster and a simple distributed key-value store with leader based replication. All of them were pretty simple and the main issue was more adhering to the professor's nebulous specs than implementing it. My implementation for both of them wasn't very challenging, for the kv store, it was basically a bunch of java processes communicating with each other through TCP and key and values were saved in a concurrent hash map, and the napster one was just a bunch of processes that had a folder with a file watcher attached, and they would share the files through TCP. There weren't any automatic testing, you just had to record a video showing the thing working, and the professor would look through your code if necessary. I decided that I want something more challenging, something that actually made me implement the stuff I was reading about in the books, so I did some research during that time and found the MIT 6.5840 labs. The labs have you build a complete distributed key-value store from the ground up, a MapReduce framework, a fault-tolerant Raft consensus library, a replicated key-value service on top of Raft, and finally a sharded KV store with cross-shard configuration management. These things are far more complex and difficult to implement than what I did in my dis-sys class, and I welcome the challenge. The only thing here is that I might do this thing in rust, instead of the language they use for the class, which is go. Even though I will lose all the helper code built by the professors to make the students lives easier, I also want to implement the testing harnesses and helper code they implemented myself to learn even more. Doing it in another language forces me to understand the code instead of simply copying and pasting it. I also don't have the time limitations students have when doing these labs, which gives me more leeway to make choices that benefit my learning at the expense of not finishing this in a semester. There might be an overlap with the fly.io challenges, but let's see how it goes.
- **Mini-LSM**: My undergraduate thesis was about adaptive compaction scheduling for RocksDB on Intel Optane persistent memory, so I'm aware of how a LSM tree works on paper, but during the coding, I noticed even though I had this knowledge, I was having a really hard time reasoning about the code and the different parts I needed to modify to achieve my objectives. So I decided to go through the amazing [mini-lsm](https://skyzh.github.io/mini-lsm) tutorial. This tutorial will help me know the LSM internals at the implementation level. The gap between reading RocksDB source code and writing your own compaction logic is enormous, I hope that this project will help me close this gap.
# Systems programming and my desire to use rust
 
I have used rust in my job for some tasks, and I've done very small stuff in rust in my free time, and I loved it. So I decided to create a systems programming plan that uses rust to help me understand how something actually works at the hardware boundary. I've also added a dis-sys project because why not? 
 
- **A slab and buddy memory allocator**: I have no idea how memory allocation works, what `malloc` is actually doing, why there are different memory allocators, like `jemalloc`, and a lot of more questions. I picked rust for this one because I found out that rust lets you hook your memory allocator into the Rust's `GlobalAlloc` trait, which lets me benchmark my code against the system allocator and observe the difference. The plan here is to just learn how memory allocation works, nothing too fancy, I believe.
- **A on-disk B+ tree with a buffer pool**: If I implement a lsm tree, I also need to implement a B tree, right? Traditional relational databases are more ubiquitous than lsm-tree based databases, and understanding both of them at the implementation level would make me literate in storage engine design trade-offs.
- **A vectorized expression evaluator**: This is the core of how analytical databases like ClickHouse execute queries. Building this would give me an intuition for why columnar execution dominates for analytics. I thought of this one because I have been using ClickHouse at my job, but I might drop it because I don't get the visceral reaction to code this when I read it. Who knows.

and now the dis-sys projects: 
 
- **Leaderless replication with anti-entropy**: Basically the dynamo model. Building this would teach me what "eventual consistency" actually means at the code level, not just the concept level.
- **Byzantine fault tolerant consensus**: Maybe the hardest project of the entire plan. Things get much more complicated when you assume that nodes in the system can lie, equivocate, and actively try to corrupt the protocol. I might leave this to be the last one.
# Infrastructure Patterns 
 
These projects are chosen to cover the distributed systems primitives that most tools are built from. I picked Go for all these projects because most of the time this kind of stuff (Kubernetes, etcd, Prometheus, Consul, etc) are all written in go, so there might be a reason, maybe I'll figure it out when I'm writing the code.
 
- **SWIM failure detector**: I know that Consul uses it internally, and also know that it works a little bit differently than raft. It looks cool enough for me to try to implement. 
- **two-phase commit coordinator**: I read recently about distributed transactions, and one of the ways of implementing them is through the 2PC protocol, and to implement it you need a coordinator. Super interesting stuff that I have no idea how it works, so it qualifies as good project. 
- **Chandy-Lamport distributed snapshot**: Lamport himself said in his website that he considers this algorithm to be a straightforward application of the basic ideas from the "Time, Clocks and the Ordering of Events in a Distributed System", which is a foundational paper for distributed systems. Implementing something like this might be amazing and an incredible learning opportunity.
- **CRDT library**: The Fly.io dis-sys challenges have a CRDT challenge, but it's just two CRDTs. Depending on my mood, I might try to also implement more of those.
- **log-structured message broker**: Kafka is cool, everyone loves to use it in their system design answers, so why not try to implement it. I might drop this if I implement it for the Kafka style-log challenge from fly.io.

# More distributed systems, but with a twist 
 
I always heard about the erlang/otp runtime, and how their approach makes failure recovery a first class design concern, how they treat different processes and how they communicate. So why not learn about elixir while also learning about distributed systems? 
 
- **saga orchestrator**: The other way of solving the issue of distributed transactions. If I do one, I have to do the other, right? It's only fair.
- **distributed lock manager**: Martin Kleppmann has an essay called [How to do distributed locking](https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html) where he talks at length about it. The problem is interesting, and it might be fun to use the supposedly amazing failure recovery system that elixir (its runtime actually) has to try to insert network partitions and see how things work. 
- **consistent hash ring router**: Every intro dis-sys book talks about this at least once, and I don't get why it's so prevalent on all the textbooks. Maybe implementing it might show me what's so important about it. 
- **Chain replication**: Interesting solution to replication. Most systems nowadays use raft or paxos for this kind of stuff, but there are still some cool systems that use it, like the Azure Storage. If I'm feeling motivated, I can extend it with CRAQ. 
- **Total order Broadcast**: As far as I know, this is the primitive used by the Zookeeper protocol. I always wanted to know how Zookeeper works, so this is a good project.
# Building data structures and trying clojure
 
I always wanted to try a lisp dialect, and clojure has been the only one with good LSP support, and easy to setup on neovim. It's also maybe the most used lisp dialect out there, so I'm going to stick to it. The projects I have in mind for this section/language aren't only distributed systems anymore, so a change of pace.
 
- **Hash Array Mapped Trie**: This is a very interesting data structure that I know is used internally by scala and clojure, and it has a persistent variant too. It seems fun to implement, so I added it to my plan
- **property graph database**: I know that graph databases are supposedly inefficient and all, but I have no idea how they work internally, and most social media companies have implemented some kind of graph database, be it an actual database, or graph model on top of another database, so I really want to know how they did it. 
- **Percolator cross-shard transactions**: Google's (relatively) new approach to distributed transactions. I find it interesting, so I added to the project list 

# Having fun with Haskell 
 
I started programming in Haskell back in 2023, but I stopped because, please don't laugh, I was looking for a job and I needed to go back to the normie languages to implement the leetcode solutions. Well, let's try it again, shall we? 
 
- **linearizability checker**: I remember reading about porcupine when I found out the MIT dis-sys labs and I still have no idea of how they built it. Well, so let's add it to the list.

# What now?
 
This a really good list of ideas for personal projects with the only intention of improving my understanding of these systems. Most of them are distributed systems projects because that's what I currently find interesting, but the important thing when building this kind of plan is to take into account your opinion about what you want to do. I'm going to probably spend months of my spare time on this, why not do something I enjoy, you know? Also, I have had this plan for a few months now, but I decided to post it now because usually announcing you are going to do something usually forces you to do that thing.
 
I also know that the plan is ambitious and might take years to do all of this. That's completely fine, the point here isn't to finish all of them, it's to learn, to keep moving, to build that life-long knowledge. Only time can tell if I'll stick to this plan, or how many projects I'll implement, but I hope that I gain some knowledge along the way.
