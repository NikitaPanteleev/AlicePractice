# Lecture 1
## Hash functions
Crypto-secure
- Collision-free: No one can find x and y such that H(x) = H(y)
- Hiding: Given H(x), it's infeasible to find x. x is taken from
  distribution with high min-entropy = "very spread out"

Commitement
(com, key) = (H(key|msg), key)
We provide only com and then lately show com and key so everyone can
verify that we really sealed msg using verify(com, key, msg) =
(H(key|msg) == com).
And it's impossible give `com` guess `msg`. Infeasible to fin `msg'`
such that generate the same `com`
- Puzzle friendly. For every positive output value y if k is chosen
  from high min-entropy it's infeasible to find x such that H(k|x) =
  y.

*sha-256*

256 bits -> c (with 512 msg block) -> c(with another 512 block) ->...
 -> Hash(of 256 bit)

## Hash Pointers
Point to location where info stored and hash info.
Merkle tree - binary tree with hash pointers.

## Signatures.
ECDSA - Elliptic Curve Digital Signature Algorithm. Relies on good
randomness both in genKeys() and in sign() methods.

## Public keys as identities.

## Cryptocurrencies
Double-spend attack

# Lecture 2
## Centralization vs decentralization
Consensus. A lot of impossibility theorems. Some working protocols
(Proxos). Introduces incentives, embraces randomness.

## Identities
Sybil attack (creation of a lot of identites)
0 confirmation, 1 and 3 confirmation (wait 6 confirmations). The
longest valid path is extended. Proof-of-work systems.

Puzzle problem to create block.

# Lecture 3: Bitcoin scripts.

Not turing complete, finite time, stack-based lang
99.9% of scripts if verification
0.01 - multiSig
0.01 - pay-to-script-hash

Reminders are errors, proof of burn scripts.

## Escrow transaction.

Alice do not wanna pay until something is shipped, Bob dont wann ship
until payment.

Alice sent x to 2-of-3 alice, bob, judy. 2 of 3 can release money.

## Green addresses

Another third party called bank. Alice pays to bank, bank pays from
green address to Bob.

## Efficient micro-payments
 - multiplayer lotteries
 - hash pre-image challenges
 - coin swapping protocols

Bitcoin blocks.

20Gb the whole story. 44mb in ram of all unspent transaction outputs.

## Limitations and improvements
 - 10 min average creation time per block.
 - 1 m bytes in a block.

7 transaction /sec

compare visa 2,000 - 10,000 transaction/sec
paypal: 50 - 100

Cryptographic attack. Changes must hard-fork.
hard-forks. soft fork only limit the set of valid transactions.

#Lecture 4: How to Store and Use Bitcoins
Storing keys.


