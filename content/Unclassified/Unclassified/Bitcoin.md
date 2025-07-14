
### Early Bitcoin Development


### Satoshi Nakamoto


### White Paper

![[bitcoin-white-paper.pdf]]

### Bitcoin: A Peer-to-Peer Electronic Cash System

**Satoshi Nakamoto**  
satoshin@gmx.com  
[www.bitcoin.org](http://www.bitcoin.org)

---

#### Abstract

A purely peer-to-peer version of electronic cash would allow online payments to be sent directly from one party to another without going through a financial institution. Digital signatures provide part of the solution, but the main benefits are lost if a trusted third party is still required to prevent double-spending. We propose a solution to the double-spending problem using a peer-to-peer network. The network timestamps transactions by hashing them into an ongoing chain of hash-based proof-of-work, forming a record that cannot be changed without redoing the proof-of-work. The longest chain not only serves as proof of the sequence of events witnessed, but proof that it came from the largest pool of CPU power. As long as a majority of CPU power is controlled by nodes that are not cooperating to attack the network, they'll generate the longest chain and outpace attackers. The network itself requires minimal structure. Messages are broadcast on a best effort basis, and nodes can leave and rejoin the network at will, accepting the longest proof-of-work chain as proof of what happened while they were gone.

---

#### 1. Introduction

Commerce on the Internet has come to rely almost exclusively on financial institutions serving as trusted third parties to process electronic payments. While the system works well enough for most transactions, it still suffers from the inherent weaknesses of the trust based model. Completely non-reversible transactions are not really possible, since financial institutions cannot avoid mediating disputes. The cost of mediation increases transaction costs, limiting the minimum practical transaction size and cutting off the possibility for small casual transactions, and there is a broader cost in the loss of ability to make non-reversible payments for non-reversible services.

What is needed is an electronic payment system based on cryptographic proof instead of trust, allowing any two willing parties to transact directly with each other without the need for a trusted third party. Transactions that are computationally impractical to reverse would protect sellers from fraud, and routine escrow mechanisms could easily be implemented to protect buyers.

In this paper, we propose a solution to the double-spending problem using a peer-to-peer distributed timestamp server to generate computational proof of the chronological order of transactions. The system is secure as long as honest nodes collectively control more CPU power than any cooperating group of attacker nodes.

---

#### 2. Transactions

We define an electronic coin as a chain of digital signatures. Each owner transfers the coin to the next by digitally signing a hash of the previous transaction and the public key of the next owner and adding these to the end of the coin. A payee can verify the signatures to verify the chain of ownership.

> The problem of course is the payee can't verify that one of the owners did not double-spend the coin.

A common solution is to introduce a trusted central authority, or mint, that checks every transaction for double spending. After each transaction, the coin must be returned to the mint to issue a new coin, and only coins issued directly from the mint are trusted not to be double-spent.

We need a way for the payee to know that the previous owners did not sign any earlier transactions. The only way to confirm the absence of a transaction is to be aware of all transactions. To accomplish this without a trusted party, transactions must be publicly announced, and we need a system for participants to agree on a single history of the order in which they were received. The payee needs proof that at the time of each transaction, the majority of nodes agreed it was the first received.

---

#### 3. Timestamp Server

The solution we propose begins with a timestamp server. A timestamp server works by taking a hash of a block of items to be timestamped and widely publishing the hash, such as in a newspaper or Usenet post. The timestamp proves that the data must have existed at the time in order to get into the hash. Each timestamp includes the previous timestamp in its hash, forming a chain, with each additional timestamp reinforcing the ones before it.

Hash(Block)

↓

Block

[Item1, Item2, Item3…]

---

#### 4. Proof-of-Work

To implement a distributed timestamp server on a peer-to-peer basis, we will need to use a proof-of-work system similar to Adam Back's Hashcash. The proof-of-work involves scanning for a value that when hashed, such as with SHA-256, the hash begins with a number of zero bits. The average work required is exponential in the number of zero bits required and can be verified by executing a single hash.

For our timestamp network, we implement the proof-of-work by incrementing a nonce in the block until a value is found that gives the block's hash the required zero bits. Once the CPU effort has been expended to make it satisfy the proof-of-work, the block cannot be changed without redoing the work. As later blocks are chained after it, the work to change the block would include redoing all the blocks after it.

Block:

├── Prev Hash

├── Nonce

└── Transaction

The proof-of-work also solves the problem of determining representation in majority decision making. If the majority were based on one-IP-address-one-vote, it could be subverted by anyone able to allocate many IPs. Proof-of-work is essentially one-CPU-one-vote.

---

#### 5. Network

The steps to run the network are as follows:

1. New transactions are broadcast to all nodes.
2. Each node collects new transactions into a block.
3. Each node works on finding a difficult proof-of-work for its block.
4. When a node finds a proof-of-work, it broadcasts the block to all nodes.
5. Nodes accept the block only if all transactions in it are valid and not already spent.
6. Nodes express their acceptance by working on the next block in the chain.

Nodes always consider the longest chain to be the correct one and will keep working on extending it.

---

#### 6. Incentive

By convention, the first transaction in a block is a special transaction that starts a new coin owned by the creator of the block. This adds an incentive for nodes to support the network, and provides a way to initially distribute coins into circulation. The incentive may also be funded with transaction fees. Once a predetermined number of coins have entered circulation, the incentive can transition entirely to transaction fees and be completely inflation free.

The incentive may help encourage nodes to stay honest. If a greedy attacker assembles more CPU power than all the honest nodes, he must choose between defrauding people or generating new coins. He ought to find it more profitable to play by the rules.

---

#### 7. Reclaiming Disk Space

To save disk space, spent transactions can be discarded once they are sufficiently deep in the chain. This is done by hashing transactions in a Merkle Tree, with only the root included in the block’s hash.

Block Header:

├── Prev Hash

├── Nonce

└── Root Hash (Merkle Tree)

├── Hash01

├── Hash23

└── …

A block header with no transactions would be ~80 bytes. With blocks every 10 minutes, this amounts to ~4.2MB/year, which is easily manageable.

---

#### 8. Simplified Payment Verification

It is possible to verify payments without running a full network node. A user only needs to keep a copy of the block headers and obtain the Merkle branch linking the transaction to the block it's in.

> As such, verification is reliable as long as honest nodes control the network.

However, it is more vulnerable if the network is overpowered by an attacker. A strategy to protect against this is to accept alerts from full nodes when they detect an invalid block.

---

#### 9. Combining and Splitting Value

To allow value to be split and combined, transactions contain multiple inputs and outputs. Typically there will be either a single input or multiple inputs combining smaller amounts, and at most two outputs: one for the payment, one for change.

Transaction:

Inputs:  [TxIn1, TxIn2]

Outputs: [TxOut1 (payment), TxOut2 (change)]

Fan-out is not a problem—there is no need to extract the full transaction history for a coin.

---

#### 10. Privacy

The traditional banking model achieves privacy by limiting information access to trusted parties. Bitcoin proposes a model where privacy is maintained by **anonymizing public keys**.

> A new key pair should be used for each transaction to avoid linking them to a common owner.

New Privacy Model:

Public Key 1 ⟶ Tx 1

Public Key 2 ⟶ Tx 2

This approach is similar to stock exchanges publishing trade data without identities.

---

#### References

[1] W. Dai, "b-money", http://www.weidai.com/bmoney.txt  
[2] H. Massias, X.S. Avila, and J.J. Quisquater, "Design of a Secure Timestamping Service with Minimal Trust Requirements," 1999  
[3] S. Haber, W.S. Stornetta, "How to Time-Stamp a Digital Document," 1991  
[4] D. Bayer, S. Haber, W.S. Stornetta, "Improving the Efficiency and Reliability of Digital Time-Stamping," 1993  
[5] M. Jakobsson, M. K. Reiter, "Secure and Efficient Logging of Audit Logs," 1998  
[6] A. Back, "Hashcash - A Denial of Service Counter-Measure," http://www.hashcash.org  
[7] R.C. Merkle, "Protocols for Public Key Cryptosystems," 1980

---

**End of White Paper**

### Modern Bitcoin
