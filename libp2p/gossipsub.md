# Deep dive into gossipsub

## Motivation
The first implementation of the pubsub interface that libp2p has done was the [`floodsub`](https://github.com/libp2p/js-libp2p-floodsub). It simply "floods" the network by having every peer broadcast to every other peer what they know about in a given topic. Although it's straight forward to implement the `floodsub` and robust, however, it is bandwidth efficiently and hard to scale.

Gossipsub is introduced to solve this existing problem.

## The gossiping mesh 
There are two type of peering in gossipsub network: `full-message` and `metadata` peerings.

Full-message peerings are used to transmit the full contents of messages throughout the network. Each peer only forwards full message to a few other peers, rather than all of them. The peering degree (or network degree or D) is configured so that each peer knows how many other peers it needs to communication with full messages. There are few parameters about the peering degree could be found at [the specs](https://github.com/libp2p/specs/blob/master/pubsub/gossipsub/gossipsub-v1.0.md#parameters).
