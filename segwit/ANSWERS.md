# Some Responses to the Discussion Questions

Q: How can new script versions remain backwards compatible?

A: TX version field for example is checked by `op_checksequenceverify`, a script op_code. The witness version is not checked by a script operator, but pushed onto the stack and evaluated at the end of the script run, when the witness script pattern is detected. I suppose it would entirely be possible to encode the witness version in the version field as well.


Q: What is the quadratic sighash problem prior to Segwit? How does [BIP 143](https://github.com/bitcoin/bips/blob/master/bip-0143.mediawiki) solve this?

A: Explanation by [Sipa](https://youtu.be/NOYNZB5BCHM?t=1625)


Q: Where are the locking script operations in P2WPKH/P2WSH?

A: Non-witness nodes never receive any witness data or witness blocks (BIP144), and only validate the spending of [0 20/32b-hash] witness script (no witness data is available and is not evaluated). The correctness of a witness spend therefore differs between old/new nodes. If the strong-chain is a witness chain, it is safe to assume old nodes will follow this chain, and the correctness of witness transactions is implied by POW for these older nodes. If the strong-chain is not a witness chain, new nodes will fork off (weak-chain), but old nodes will continue to follow it. It is not safe to conduct witness transactions on this non-witness strong-chain. This is why miner-support for SegWit is relevant during activation.
