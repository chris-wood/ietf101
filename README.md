# ietf101

## MAMI traffic management workshop

TODO

## dinrg 

### Stellar Consensus Protocol (SCP)
- Nick Johnson: description of quorum slices is opaque in the draft, though clear in the slides
- Nick: not clear how quorum slices are encoded? 
  - Use XDR (?) which supports recursive data structures.
- Paul: assume that nodes trust eachother?
  - Nodes depend on one another. Assumes that transitive closure of trust dependencies yields overlap in trust relationship, and those common nodes emerge as trusted.
  - Trust is placed in conjunction in parties, even though dependency is placed in individual nodes. 
  - Each participant must configure participant to have one or more quorum slice.
- Paul Mendes: Did you look into more efficient multicast protocols?
  - Would be willing to adopt one being discussed in IETF and IRTF.

### Distributed Authenticated Messaging

- Nick: What is the model for adding new mappings? Are they defined at deployment time, during upgrades, etc?
  - Anyone can add a new mapping -- working on a form of versioning 
  - This is a general framework for adding new mappings
  
### Applying distributed ledger to IoT app

- David: Why do you need a blockchain or append only log for this application? What is the threat?
  - We use blockchains to log all events.
- David: is this for billing or forensics?
  - There are definitely record errors that we try to prevent or mitigate
- Wes Hardaker: Have you looked at power consumption, and who is paying for the system?
  - System does not depend on solar generation to operate
  - Have not done any assessment, though signature verification should be cheaper than other proof of work schemes
  - Another benefit of is the slimness of the stack (see slides) in comparison to a more traditional one
  
### Decentralized mapping system for LISP

- David: What prevents malicious node from sending a bad registers (e.g. RLOCs)?
  - All mapping registrations are signed
  - Map register looks up public verification keys to validate each message
- David: Do you assume EIDs are public keys?
  - You can create crypto EIDs for the sole purpose of registering mappings
  - To join a multicast group, you need to send RLOC to the group, which is signed
- Stéphane Bortzmeyer: What happens if unicast messages are lost?
  - Use TCP, set reliability bit and keep retrying, or (third option)
- Look at https://www.lispers.net

### Chainspace: A Shared Smart Contract Platform

- David Mazieres: Seem to claim that PBFT is a scalability bottleneck for throughput not latency
  - PBFT has complexity O(n^2), and we use it for inter-shard consensus
- David: Can amortize cost over arbitrarily many transactions, which has latency, but still low throughput. You could batch transactions to increase throughput.
  - Maybe increase block size too?
- How can you develop this going forward? (Or how do you address your future work items, especially w.r.t. dishonest shards?)
  - We could fork, though it's not the best solution. This is still an open question.
- (missed)
- ???: Can you scale up to thousands or tens of thousands of transactions per second?
  - Do not focus on absolute number of transactions per second (bad metric) -- focus on scalability, and aim for linear
  
### Discussion

- Dino: Does anyone have a desire to interoperate between different chains/ledgers?
  - Ripple folks have done some work here
- Nick: Look at Polkadot (?)
- DINRG is not meant to be a blockchain group -- one primary element is consensus
- Nick: Hope RG works on formalizing consensus systems so that they may be better and more quickly deployed
- Dino: Assume RG cares about interoperability, even if not focused on blockchains. Today, wallets try to support all chains. Could we standardize a protocol between wallets?
  - We're doing research here -- not standards.
- Faye: Group is good on the consensus front -- current PoW schemes are economically not viable. Growth curve for purchase of ASIC miners has been exponential since the beginning of 2017.
- Lixia: The group is *D*INRG, not *B*INRG (blockchain), so we should focus on decentralized work.
- Marie-Jose: There are people who thinkt that the only way networks can be efficient is through centralization. Will we focus on other problems that come from decentralization such as management, performance, etc?
  - Yes.
- Eve Schooler: Agree that consensus is important, though motivating factors for me are (1) we should focus on applications, systems, etc. that are not always connected, and (2) address trust issues at the IoT data production scale. 
- David: Blockchains cannot attest to authenticity of data, only immutability of data.
- Allison Mankin: Let's focus on things we can talk about and address together as a group. 
