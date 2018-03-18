https://github.com/ethereum/wiki/wiki/White-Paper

1. previous block is valid
2. timestamp > now - 2 hours
3. pow nonce
4. state 0 -> previous block
5. all signatures are valid

SPV (Simplified Payment Verification) only download block header hash (200 byte) -> merkle tree

ether account
- nonce
- ether balance
- contract code
- storage
- two type
  * externally account, no contract
  * contract account, activate when receive msg, update state or create new contract

transaction
- recipient
- sender
- ether amount

gas
- at least 1 gas per op
- 1 byte cost 5 gas

contract can send msg to other contract
- recipient
- sender
- msg
- ether amount

transaction fee: start gas * gas price
- deduct transaction fee from sender balance
- increase sender nonce
- gas = start gas
- if recipient does not exit, create one. If recipient is a contract, run this contract until contract end or gas used up
- revert state change if gas used up or balance not enough

ether blockchain v.s. bitcoin blockchain
- ether has transaction list and state copy
- block number and mining difficulty are saved in blockchain

EVM full computational state can be defined by the tuple (block_state, transaction, message, code, memory, stack, pc, gas)
- block_state is the global state containing all accounts and includes balances and storage

validate an ether block
- check if pre block is valid
- check if block height is larger than index and within 15 minutes
- check pow result
- check merkle root S_FINAL is equal to the final state root provided in the block header
