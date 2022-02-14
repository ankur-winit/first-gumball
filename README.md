# first-gumball
Proof of Concept: Candy Machine

1. Create Solana Account
	
a. Verify the folllowing tools availability
>> node --version
v17.5.0

>> ts-node --version
v10.5.0

>> yarn --version
1.22.17

>> solana --version
solana-cli 1.9.6

b. Create a wallet
>> solana-keygen new --outfile ./keypair.json
Generating a new keypair

For added security, enter a BIP39 passphrase

NOTE! This passphrase improves security of the recovery seed phrase NOT the
keypair file itself, which is stored as insecure plain text

BIP39 Passphrase (empty for none): 

Wrote new keypair to ./keypair.json
============================================================================
pubkey: CM4VRQEdfW6ttsd2jvXbA3cMarLZM4gMHfMAW8uTyGtQ
============================================================================
Save this seed phrase and your BIP39 passphrase to recover your new keypair:
develop silly dragon talent cram receive crew worth truth two defense obtain
============================================================================

2. Create Metaplex Candy Machine v2

a. Clone the metaplex library from the github

>> git clone https://github.com/metaplex-foundation/metaplex.git

>> cd metaplex/js

>> yarn install

>> solana config set --url https://api.devnet.solana.com
Config File: /home/ankur/.config/solana/cli/config.yml
RPC URL: https://api.devnet.solana.com 
WebSocket URL: wss://api.devnet.solana.com/ (computed)
Keypair Path: /home/ankur/.config/solana/devnet.json 
Commitment: confirmed

>> solana config set --keypair keypair.json
Config File: /home/ankur/.config/solana/cli/config.yml
RPC URL: https://api.devnet.solana.com 
WebSocket URL: wss://api.devnet.solana.com/ (computed)
Keypair Path: keypair.json 
Commitment: confirmed

>> solana address
CM4VRQEdfW6ttsd2jvXbA3cMarLZM4gMHfMAW8uTyGtQ

>> solana balance
0 SOL

>> solana airdrop 4
Requesting airdrop of 4 SOL

Signature: 3HTpSu5Bgbaejqh7C7EvWjPyC3Mg6YPuRzMJC2vfBXXgPzMZ83Npm1mApdHwKsjGdhWtnX53MRmdpuLjs5kdLTi2

4 SOL

3. Upload Metadata to Arweave

>> npx ts-node ~/Documents/WinIT/first-gumball/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts upload \
    -e devnet \
    -k keypair.json \
    -cp config.json \
    ./assets

wallet public key: CM4VRQEdfW6ttsd2jvXbA3cMarLZM4gMHfMAW8uTyGtQ
WARNING: The "arweave" storage option will be going away soon. Please migrate to arweave-bundle or arweave-sol for mainnet.

Beginning the upload for 10 (img+json) pairs
started at: 1644859553130
initializing candy machine
initialized config for a candy machine with publickey: AahydrBY7rfqSBNyWfdtwzkAKuudLEfViTLjfBFHduab
Uploading Size 10 { mediaExt: '.png', index: '0' }
Processing asset: 0
Processing asset: 1
Processing asset: 2
Processing asset: 3
Processing asset: 4
Processing asset: 5
Processing asset: 6
Processing asset: 7
Processing asset: 8
Processing asset: 9
Writing indices 0-9
Done. Successful = true.
ended at: 2022-02-14T17:27:52.195Z. time taken: 00:01:59

4. Verify Upload

>> npx ts-node ~/Documents/WinIT/first-gumball/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts verify_upload \
    -e devnet \
    -k keypair.json

wallet public key: CM4VRQEdfW6ttsd2jvXbA3cMarLZM4gMHfMAW8uTyGtQ
Key size 10
Looking at key  0
Looking at key  1
Looking at key  2
Looking at key  3
Looking at key  4
Looking at key  5
Looking at key  6
Looking at key  7
Looking at key  8
Looking at key  9
uploaded (10) out of (10)
ready to deploy!

5. Mint tokens

// One token
>> npx ts-node ~/Documents/WinIT/first-gumball/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts mint_one_token \
    -e devnet \
    -k keypair.json

//Mutliple token
>> npx ts-node ~/Documents/WinIT/first-gumball/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts mint_one_token \
    -e devnet \
    -k keypair.json
    -- number 2

6. Start UI

>> cd metaplex/js/packages/candy-machine-ui
>> npm start