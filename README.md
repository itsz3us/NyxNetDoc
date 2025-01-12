People often get really interested in P2P decentralized distributed systems, but they tend to overlook an important detail. Just because a system is decentralized doesn’t mean the participants are anonymous or that their actions can’t be traced. In fact, activities on decentralized systems *can* still be traced, especially when privacy measures aren’t used. For example, the IP addresses of peers in a P2P network can be tracked across the network. Even using solutions like TOR doesn’t fully protect against this. Activities can still be traced by using pattern recognition and advanced analysis methods, which TOR and similar tools can’t always block.

We need to create a P2P network that eliminates the use of IP addresses altogether and can withstand advanced tracking techniques. The first thing to do is create a system where users can interact without revealing their IP addresses. Nym Mixnet offers a potential solution to this problem.

By using Nym Mixnet, we can set up a P2P network that protects privacy and security for all users, going beyond what current solutions offer. The first step involves creating a P2P network of nodes where anyone running a local Nym client can participate. Unlike traditional P2P networks that expose node IP addresses, this system keeps things private by having nodes use Nym client addresses instead. This way, no node’s IP address is exposed.

The basic message structure between P2P nodes looks like this:

- **Version**: Sent when a node connects to another node, announcing its version. If the node is not in maximum anonymity mode, it also shares its Nym client address. Otherwise, it uses a Surb (Single Use Reply Block) for privacy.
- **Verack**: Sent as a response to the version message, confirming that the node is ready to continue the connection.
- **Ping/Pong**: Used to check if the connection is active. A ping is sent by one node, and the other node responds with a pong.
- **Addr/Getaddr**: Helps with peer discovery and sharing addresses within the network.
   - **Addr**: A node sends a getaddr message to request a list of peer addresses from another node.
   - **GetAddr**: The other node replies with an addr message containing known peer addresses (Nym client addresses), helping the requesting node expand its peer list.

All messages in this system are passed through the Nym Mixnet, making them resistant to pattern recognition and advanced tracking techniques.

Here’s an example of how this works:

1. **AliceNode** sends a version message to **BobNode**. 
   - Start Mixing → Mixnode → Mixnode → Mixnode → Mixnode → Mixnode → End Mixing → BobNode.
2. **BobNode** replies with a verack message to **AliceNode**.
   - Start Mixing → Mixnode → Mixnode → Mixnode → Mixnode → Mixnode → End Mixing → AliceNode.

This process happens with every protocol message exchanged between nodes, ensuring that each stage of the communication remains anonymous and private.

In addition to the core message types (version, verack, ping/pong, addr/getaddr), the systemcan be designed to support custom objects seamlessly. Any object that implements the serialize and deserialize methods can be transmitted between nodes. This flexibility allows developers to extend the protocol for a variety of use cases..
