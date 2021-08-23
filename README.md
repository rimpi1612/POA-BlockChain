# POA-BlockChain

The Proof of Authority (PoA) algorithm is typically used for private blockchain networks as it requires pre-approval of, or voting in of, the account addresses that can approve transactions.

Because the accounts must be approved, we will generate two new nodes with new account addresses that will serve as our pre-approved sealer addresses.

1. Create accounts for two nodes for the network with a separate datadir for each using geth.
./geth --datadir node1 account new
./geth --datadir node2 account new


2. Next, generate genesis block.

   - Run puppeth, name the network, and select the option to configure a new genesis block.

   - Choose the Clique (Proof of Authority) consensus algorithm.

   -  Paste both account addresses from the first step one at a time into the list of accounts to seal.

   - Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so we will need to pre-fund.

    - We can choose no for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.

    - Complete the rest of the prompts, and when we are back at the main menu, choose the "Manage existing genesis" option.

    - Export genesis configurations. This will fail to create two of the files, but we only need networkname.json.

3. With the genesis block creation completed, we will now initialize the nodes with the genesis' json file.

    - Using geth, initialize each node with the new networkname.json.
        ./geth --datadir node1 init networkname.json
        ./geth --datadir node2 init networkname.json

4. Now the nodes can be used to begin mining blocks.

    - Run the nodes in separate terminal windows with the commands:
./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
NOTE: Type your password and hit enter - even if you can't see it visually!
Your private PoA blockchain should now be running!

With both nodes up and running, the blockchain can be added to MyCrypto for testing.

Open the MyCrypto app, then click Change Network at the bottom left: