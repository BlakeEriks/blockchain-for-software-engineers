# What is a Blockchain
A blockchain is a ledger of facts replicated across several computers in a p2p network. Members of the network are called nodes. All communication inside the network takes advantage of cryptography to add a fact to the ledger. When a node wants to add data to the ledger, the network must form a consensus on where the fact should appear. This consensus is called a block.

## Other P2P Networks

* Napster
* BitTorrent

## Big Problem in P2P is Reconciliation

If two contradicting facts arrive at the same time, the system must have a protocol to determine which fact is considered valid.

### The Double Spend Problem

If a node tries to insert multiple transactions spending more tokens than they currently have, the system must prevent this from being added to the blockchain.

## The Solution is a Consensus System

The blockchain implements a consensus system using the proof-of-work method, using blocks.

# Blocks

Blocks are a work-around to order facts in a network of non-trusted peers. 
 
## Core Concept

* Facts are grouped in blocks
* There is only a single chain of blocks, replicated across the entire network
* Each block references the previous one.
* Before being added to a block, facts are *pending*, as in unconfirmed

## Example

If fact F is in block 21, and fact E is in block 22, then fact E is considered by the entire network to be posterior to fact F. 

![0da66a0f56c83ba79c03196ca2fae2c1.png](https://marmelab.com/images/blog/blocks_facts.png)

# Mining

Mining nodes locally try to make the next block with pending facts. They compete to create the next block in the node by hashing the list of facts with a string and trying to get a result with a given number of leading 0's. If the hash meets the difficulty requirement, then the miner earns the ability to publish their local block, and all facts in this block become confirmed. This block is sent out to the network and confirmed by the other nodes, and then added to their chains. New blocks are published every 10 minutes on average.

![9c214da78dd098a5a20b46ceb2e2a4ce.png](https://marmelab.com/images/blog/rolling_dice.png)

Finding the key to validate a block is very unlikely, by design. This prevents fraud and keeps the system safe. A malicious attacker would have to own more than half of the nodes in the network. 

## The Mining Challenge

The challenge consists of a double SHA-256 (double meaning applies hash function twice) hash of a string made from the pending facts. A node wins if their hash contains at least n leading zeroes. The number **b** is called the difficulty. Other blockchain implementations use special hashing techniques that discourage the usage of GPU's (e.g. by requiring large memeory transfers)

Whichever miner is able to create the newest block is rewarded with BitCoins (thus incentivizing mining at all). 

# Money and Cryptocurrencies

Miner nodes test thousands of random strings every second to try and form a new block, thus running a miner requires a huge amount of power and computing resources (storage and CPU). That's why **you must pay to store facts** in a blockchain. Reading facts is free. 

* Reading data is free
* Adding facts costs a small fee
* Mining a block brings in the money of all the fees of the facts included in the block

The money we discuss isn't dollars. Each blockchain has its own (crypto-)currency. It's called Bitcoin (BTC) in the Bitcoin network, Ether (ETH) on the Ethereum network. To make a payment in the Bitcoin network, you make a small fee in Bitcoins. 

Miners also receive a **gratification** for keeping the network working and safe. At the start, mining a successful block rewarded a miner with 25 BTC. Ethereum miners are rewarded with 5 ETH per block. In this sense, **the blockchain generates its own money**.

# Contracts

A blockchain can also **execute programs.** Some blockchains allow each fact to contain a mini program. Such programs are replicated together with facts, and every node executes them when receiving the facts. In Bitcoin, this can be used to make a transaction **conditional.** 

For Example: **Bob will receive 100 BTC from Alive if and only if today is November 5th**

## Other Blockchain Contracts

In Ethereum, each contract carries a **mini-database,** and exposes methods to modify the data. As contracts are replicated across all the nodes, so are their database. Each timer a user calls a method on the contract (and therefore the underlying data), this command is replicated and replayed by the entire network. This allows for a **distributed consensus on the execution of a promise.**

## Smart Contracts

The concept of **pre-programmed conditions, interfaced with the real world, and broadcasted to everyone** is called a **smart contract.** A **contract** is a promise that signing parties agree to make legally-enforceable. A **smart contract** is the same, except enforced technically instead of legally. This removes the need for any judiciary enforcing the rules of the contract.

### Example

>Imagine that you want to rent your house for a week and 1,000, with a 50% upfront payment. You and the loaner sign a contract, probably written by a lawyer. You also need a bank to receive the payment. At the beginning of the week, you ask for a5,000 deposit; the loaner writes a check for it. At the end of the week, the loaner refuses to pay the remaining 50%. You also realize that they broke a window, and that the deposit check refers to an empty account. You'll need a lawyer to help you enforce the rental contract in a court.

>Smart contracts in a blockchain allow you to get rid of the bank, the lawyer, and the court. Just write a program that defines how much money should be transferred in response to certain conditions:

>* Two weeks before beginning of rental: transfer $500 from loaner to owner
>* Cancellation by the owner: transfer $500 from owner to loaner
>* End of the rental period: transfer $500 from loaner to owner
>* Proof of physical degradation after the rental period: transfer $5,000 from loaner to owner

>Upload this smart contract to the blockchain, and you're all set. At the time defined in the contract, the money transfers will occur. And if the owner can bring a predefined proof of physical degradation, they get the $5,000 automatically (without any need for a deposit).

Applications relying on smart contracts are called **Decentralized Apps,** or **DApps**. In this sense, **smart** means **no intermediaries** or **technically-enforced**.

# Blockchains looked at again

## What it does

A blockchain allows the secure sharing and/or the process of data between multiple parties over a network of non-trusted peers. Data can be **anything**, but most revolutionary cases concern cases where a trusted third party is normally involved.

Examples

* Money (requires a bank)
* Proof of property (requires a lawyer)
* Loan certificate (requires a lawyer)

## How it works

A blockchain is an innovation relying on three concepts:

* **Peer to peer networks**
* **Public-key cryptography**
* **Distributed consensus**

None of these are new, however their combination requires a breakthrough in computing. 

## What is compares to

The blockchain can be viewed as a database loosely synchronized and replicated across every node in the network, OR as a supercomputer formed by the combination of the CPU's/GPU's of all of its nodes. This supercomputer can be used to store and process data, just how it can be done with a remote API - except you can be sure the data is safe and processed properly by the network.

## Why It's a Big deal

>The Blockchain is the most disruptive technology I have ever seen.» Salim Ismail

>The most interesting intellectual development on the Internet in the last five years.» Julian Assange

>I think the fact that within the Bitcoin universe an algorithm replaces the functions of [the government] ... is actually pretty cool.» Al Gore

![569a986d53d1f4afc435b2a6286c1c57.png](https://marmelab.com/images/blog/blockchain_infographic.png)