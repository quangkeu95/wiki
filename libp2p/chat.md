# Using libp2p-rs to build a simple p2p chat app

## Motivation
In order to get familiar with `libp2p` protocol, I decide to build a p2p chat app with `libp2p-rs`. Some goals the app should able to achieve:
- [ ] Each user enters the network with unique-id, derive from crytographic key pairs.
- [ ] Allow users to connect to the public network.
- [ ] Allow users to send private message.
- [ ] The connection between users should be encrypted.
- [ ] Discovering peers.
- [ ] Finding peers with the DHT

## Init the repository
I want a simple architecture at first so I create the `chat` binary module inside the `examples` directory.

The repository is initialized [here](https://github.com/quangkeu95/libp2p-learner/commit/bddf28e28a5ecba39e4209e1311efd763643035c)




