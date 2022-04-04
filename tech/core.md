---
title: Network API
description: This doc offers a high-level overview of the networking APIs.
published: true
date: 2022-03-29T03:45:54.059Z
tags: 
editor: markdown
dateCreated: 2021-11-10T06:12:36.195Z
---

# Network APIs

Nodes connect with each other primarily via websockets. Messages are sent with an 8-byte header that indicates the type of message being sent, followed by a binary stream the contents of the message. Communications are broadcast-oriented and do not require a response.

In addition to connecting with other nodes via websocket, nodes are also expected to run a server which provides HTTP/S access to FULL and LITE blocks. Block distribution is currently handled this way for the convenience of the browsers on the network, some of which have difficulty with large-data downloads via websockets. 


# API Commands

All messages are sent with an 8-byte header which indicates the type of data being sent along the chain. The data that follows is specific to the type of request.

SHAKINIT: initialize handshake
SHAKCOMP: complete handshake
SNDTRANS: send transaction
REQBLOCK: request block
REQCHAIN: request blockchain
SNDCHAIN: send blockchain
REQBLKHD: request block_header
SNDBLKHD: send block_header
SNDKYLST: send keylist

## Initialize Handshake (SHAKINIT)

Does a handshake which authorizes each party as their public key. This is the first thing which should be done after opening the websocket connection. Unless a peer is aware of your publickey and you have cryptographically proved your ownership of it, that peer will not route transactions to you.

### SENDS: 

- Sender's Publickey as hex-encoded byte array

### RETURNS:
RESULT__: 
- HandshakeChallenge
  - Receiver's IP(as 4-bytes) - i.e. their own IP
  - Sender's IP(as 4-bytes) - read from the source of the http request
  - Receiver's Publickey(hex-encoded by array) - i.e. their own PublicKey
  - Sender's PublicKey(hex-encoded by array) - received from request
- Signature
	- The structure above is serialized, signed, and then the signature is appended to the binary blob
ERROR___: Message describing any error encountered


## Handshake Complete(SHAKCOMP)

After the IP and signature of the SHAKINIT response(RESULT__) have been verified by the peer which sent the SHAKINIT request, they will send this command.

After this point the Sender would consider that the Receiver has completed the handshake and might set a flag accordingly. For example in the Rust implementation this is called has_completed_handshake.

The data package is simply the entire SHAKINIT response signed again by the Sender of SHAKINIT and SHAKCOMP.

### SENDS: 

- The reply from SHAKINIT but with another signature attached(the sender's signature)

### RETURNS:
RESULT__: OK
ERROR___: Message describing any error encountered

## Send transaction(SNDTRANS)

validates transaction and adds it to mempool

### SENDS:

 - transaction object

### RETURNS:
RESULT__: OK
ERROR___: Message describing reason transaction is not valid or Description of any other error

## request block

### SENDS:

 - block_id OR block_hash(both optional but at least one is needed)
 - synctype(optional)

### RETURNS: 

 - full-block
 - lite-block

## Request blockchain(REQCHAIN)

This is for requesting meta-data about the blockchain which will be sent via “send blockchain”.

For version 1, we will assume that only one node is producing blocks and all other nodes will simply read from there. Therefore, a node should only send it’s latest block id/hash when requesting blockchain.

The node being asked for blocks will simply check if the block hash is known and send data from that block to it’s latest block.

After receiving the metadata, the requesting node can then request blocks one at a time via “send block”

### SENDS:

 - block_id(starts with latest)
 - block_hash(starts with latest)
 - fork_id
 - synctype(optional)

### RETURNS:
RESULT__: OK
ERROR___: NOTFOUND or Description of any error

Future Work:
Here we will eventually use fork_id(or some other means) to figure out what is a decent common ancestor.

request block_header could be used for this purpose if it accepted block id.

Clayton Rabenda, [12.08.21 13:58]
we could add an API that let's B discover the common ancestor, but i think this is what fork_id is for...?

David Lancashire, [12.08.21 13:58]
that is a good idea

the reason it is all packed together in that one request is to speed up lite-client connection

but we can do that better with the functionality separated


## Send blockchain(SNDCHAIN)

After request blockchain, the peer pushes blockchain data at the requesting peer.

For version 1 we do not need pre_hash since this is only used by lite clients for payment verification. Additionally, we wouldn’t need the number of transactions.

pre_hash is a hash of everything in the block except for the merkle root. By including this hash in the block header or allowing a lite client to compute it from the block hash, it can be coupled with the merkle root to produce lite-blocks with properties similar to Bitcoin’s SPV.

See “request blockchain” for more details.


### SENDS:
Blocktype/synctype
Starting_hash
array of block data with each entry containing:
block_id: the id of the block
block_hash: the hash of the block
timestamp: the timestamp of the block
pre_hash: the hash which is hashed with the previous block_hash to generate the hash of the current block.
number of transactions: the number of transactions in the block for the recipient

### RETURNS:

RESULT__: OK
ERROR___: Description of any error

Future Work:
Since we are not yet validating payments with lite-blocks/merkle tree, it’s not necessary to send pre_hash or number of transactions. This could be sent now, but we won’t be doing anything with the data until the future when we add lite blocks.

## Request block_header(REQBLKHD)

This is only called in case a node falls behind and receives a block or block header that has a gap between it and it’s latest block. In this case, this API can be called using the prev_hash of the new block and this process can be repeated until an ancestor of the new block/blockheader is found.

Current implementation only

### SENDS:

block_id (optional)
Block_hash
synctype(optional)

triggers remote server to send block_header

### RETURNS:

RESULT__: OK
ERROR___: NOTFOUND or Description of any error

### Future considerations:

For now we can only request blockheader by hash, but it may be useful for performance or conveniences in the future to also be able to request headers by block id.

## Send block_header(SNDBLKHD)

This is used to send block meta data to a peer which may be interested in a block that the node has. There are two cases, when a node produces a block or when a node receives a block from a 3rd peer.

In either case, a SNDBLKHD request is made and the receiving node can then decide whether to issue a  REQBLOCK request for the full block or ignore the header.

### SENDS:

- SendBlockHeadMessage
  - Block Hash

### RETURNS:

RESULT__: OK
ERROR___: ALREADYKNOWN or Description of any error

### Current Implementation:

Currently only the block hash is included in the SendBlockHeadMessage, but this will be expanded to the entire block header in the future perhaps as features are added.

### Future considerations:

We will need to access the blockchain and peers in the future here to implement “congestion policy”.
E.g.  has peer has forwarded 2 blocks at the same depth from the same block producer? blacklist them
E.g. this block didn’t validate. did the sending peer say that it did and sign that?

In the future this will also send routing sigs.
“we have routing sigs when sending TXS and will need to have them for blocks in the near future”
David mentioned that this should include routing sigs, but it’s not clear why and they are currently unimplemented so I’m leaving it off the spec.

## send keylist(SNDKYLST)

This will not be implemented at all for version 1. This is only needed for lite-blocks and the design is not yet finalized.

updates keylist for peer and set’s peer synctype to “lite”.

### SENDS:

 - array of addresses to track

### RETURNS:

???

