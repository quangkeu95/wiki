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

## Give me an identity address
So every user using the chat app have an unique address, since `libp2p` is designed to work across a wide variety of networks, there should be a way to work with a lot of different addressing schemes in a consistent way. So `libp2p` using `multiaddress` (often abbreviated `multiaddr`) as a convention for encoding multiple layers of addressing info into a single "future-proof" path structure.
An example of `multiaddr` is `/ip4/198.51.100.0/tcp/4242/p2p/QmYyQSo1c1Ym7orWxLYvCrM2EmxFTANf8wXmmE7DWjhx5N` where:
- The client is using IPv4 protocol.
- The client has an IPv4 address `198.51.100.0`.
- The chat app uses TCP at port `4242`.
- The chat app uses libp2p's registered protocol id `/p2p/`.
- The multihash of the client public key is `QmYyQSo1c1Ym7orWxLYvCrM2EmxFTANf8wXmmE7DWjhx5N`.

The `multihash` document could be found at [here](https://docs.libp2p.io/concepts/appendix/glossary/#multihash). 

So a quick way to create a new network identity for the user is to use [`SwarmBuilder::with_new_identity` method](https://docs.rs/libp2p/0.52.4/libp2p/struct.SwarmBuilder.html#method.with_new_identity), or with existing keypair [`SwarmBuilder::with_existing_identity` method](https://docs.rs/libp2p/0.52.4/libp2p/struct.SwarmBuilder.html#method.with_existing_identity) to create the `SwarmBuilder` instance. Note that we have to call `build` method on `SwarmBuilder` instance in order to get the `Swarm` instance.

Our code for now looks something like below:
```rust
use libp2p::SwarmBuilder;

use tracing_error::ErrorLayer;
use tracing_subscriber::filter::LevelFilter;
use tracing_subscriber::prelude::*;

/// Initializes a tracing Subscriber for logging
#[allow(dead_code)]
pub fn init_tracing_subscriber() {
    tracing_subscriber::Registry::default()
        .with(
            tracing_subscriber::EnvFilter::builder()
                .with_default_directive(LevelFilter::INFO.into())
                .from_env_lossy(),
        )
        .with(ErrorLayer::default())
        .with(tracing_subscriber::fmt::layer())
        .init()
}

#[tokio::main]
async fn main() -> anyhow::Result<()> {
    init_tracing_subscriber();

    let mut swarm = SwarmBuilder::with_new_identity();
    Ok(())
}```


