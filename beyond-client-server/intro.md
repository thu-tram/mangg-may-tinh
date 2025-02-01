---
title: Multicast
parent: Beyond Client-Server
nav_order: 1
layout: page-with-toc
---

# Multicast

## Motivation: Multicast

In every topic we've seen so far, we've said that the goal of the Internet is to deliver data between hosts. In particular, we've assumed unicast delivery, which means that there is a single source, sending data to a single destination.

Many protocols we've seen (e.g. HTTP, DNS, TCP, TLS) rely on a client-server model, which relies on the unicast delivery model. In the client-server model, there is one client and one server exchanging data, which implies that they are sending unicast data between each other.

Most of the traffic on the Internet is indeed unicast, but there are some exceptions. In particular, some applications involve groups of hosts communicating. For example, consider a multi-player game, or a live content delivery app (e.g. Zoom meeting, live-streaming a sports game), or a collaborative document (e.g. Google Docs). More exotic uses of group communication also exist, such as discovery (e.g. send a message to all Apple devices so that you can find the nearest speaker), or AI training (we'll study this later in these notes).

The client-server paradigm is not the most natural way to think about these situations. In a multi-player game or a video-conferencing app, there isn't a single client or a single server. How should the network support these applications, to make it easier for developers to write these types of applications?

One possible answer to this question is: The network should offer no support at all. Group communication can be implemented with unicast. For example, when you make an update to the collaborative document, you can send a separate unicast packet to everyone else in the group, so that they all know about your update.

<img width="500px" src="/assets/beyond-client-server/7-001-unicast-model.png">

However, this unicast-only approach can be inefficient. Consider this network topology, where you are in the USA and all other group members are in Europe. If you send separate unicast packets to each group member, you're sending duplicate copies of the data across the expensive undersea cable. Also, this forces the sender to send many duplicate unicast packets, which scales poorly (e.g. imagine a single server streaming a sports game to millions of users).

Intuitively, a more natural approach would be to send just a single packet across the undersea cable, and then let someone in Europe (e.g. a router or a host) distribute copies of the packet to the group members. Ideally, we would like to avoid sending duplicate copies of a packet along a link. In other words, each link should only carry the packet once (or possibly zero times, if there are no group members along that link).

<img width="500px" src="/assets/beyond-client-server/7-002-multicast-model.png">

This approach requires extra support from the network, and requires developing some new protocols.


## Multicast Definitions

Recall that we have seen four packet delivery models so far:

Unicast: Send a packet to exactly one destination.

Anycast: Send a packet to anyone in a set of possible destinations. Only one member of the set needs to receive the packet.

Broadcast: Send a packet to all destinations. The definition of "all" depends on the context of the problem, but you can think of it as all hosts in a local network.

Multicast: Send a packet to all members in a group. Hosts can choose to join/leave groups at any time. Note that you can send a packet to a group, even if you yourself are not a member of that group.

<img width="900px" src="/assets/beyond-client-server/7-003-uni-any-multi-broadcast.png">

The multicast paradigm can be used to think about the group communication problems from earlier. For example, all hosts interested in receiving the live-streamed sports game can join a multicast group. Then, the streaming service can multicast packets to the entire group.

As another example, if we wanted to use multicast for discovery, we could have all printers in the building join a multicast group. Then, users can multicast packets to the entire group to find the printers that they can use.


## IP vs. Overlay Multicast

A perennial debate throughout the history of multicast is an architectural question: At what layer should we implement multicast?

One option is to implement multicast in Layer 3, sometimes called **IP multicast**. In this approach, we add specialized support to routers so that they understand how to multicast packets. This option gives better performance, but is harder to implement.

The other option is implement multicast in Layer 7, sometimes called **overlay multicast**. In this approach, applications handle any multicast functionality. This approach leaves Layer 3 untouched, so routers only need to understand unicast. This option gives worse performance, but is simpler to implement.

Neither option is strictly better. We'll study both options and analyze the trade-offs between them.

<img width="500px" src="/assets/beyond-client-server/7-004-multicast-taxonomy.png">