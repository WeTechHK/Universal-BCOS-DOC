# Nodes

Universal BCOS is a distributed network of computers (known as nodes) running software that can verify blocks and transaction data. The software must be run on your computer or server to turn it into an Universal BCOS node.

## Node types

There are three types of nodes:

- Consensus Node:
- Observer Node:
- Light Node:

### Consensus node

Consensus nodes are responsible for validating transactions and producing new blocks. Also, consensus nodes do a block-by-block validation of the blockchain, including downloading and verifying the block body and state data for each block.

- Stores full blockchain data (although this is periodically pruned so a full node does not store all state data back to genesis)
- Participates in block validation, verifies all blocks and states.
- Serves the network and provides data on request.

### Observer node

Observer nodes are full nodes that verify every block from genesis but do not have to participate producing new blocks.

- Stores full blockchain data as Consensus node
- Sync blocks from Consensus node and verifies all blocks and states.
- Serves the network and provides data on request.

### Light node

Instead of downloading every block, light nodes only download block headers. These headers contain summary information about the contents of the blocks. Any other information the light node requires gets requested from a full node. The light node can then independently verify the data they receive against the state roots in the block headers. Light nodes enable users to participate in the Universal BCOS network without the powerful hardware or high bandwidth required to run full nodes. Eventually, light nodes might run on mobile phones or embedded devices. The light nodes do not participate in consensus (i.e. they cannot be miners/validators), but they can access the Universal BCOS blockchain with the same functionality and security guarantees as a full node.

## Running your own node

Interested in running your own Universal BCOS client?

For a beginner-friendly introduction visit our [run a node](/run-a-node) page to learn more.

If you're more of a technical user, dive into more details and options on how to [spin up your own node](/developers/docs/nodes-and-clients/run-a-node/).
