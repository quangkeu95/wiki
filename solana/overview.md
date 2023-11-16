# Basic terminology
1 SOL = 10^9 Lamports

# Accounts
- Everything is an account.
- Store some SOL (with unit in lamports).
- Held in validator memory, have to pay rent to stay.
- Represented by 256 bits address.
- Contains a `owner` field to indicate who has the write access to the account.
- Contains a `executable` field to indicate whether the account is a program.
- Can store arbitrary data.
- Maximum size of an account data is 10MB.

# Transactions
- Contains an array of signatures.
- Contains an message.
- Transactions are atomic.
- A filed `message` will contains an array of account_keys that the transaction with interact with (read/write), and an array of instructions that will be executed sequentially.
- Transactions are limited to 1232 bytes.
- Contains recent blockhash to prevent duplications and eliminate stale transactions.
- Max age of transaction's blockhash is 150 blocks (~1min19sec).

# References
- Cookbook: https://solanacookbook.com/
- Anchor: https://book.anchor-lang.com/
