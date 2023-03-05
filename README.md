# Gift List - A Merkle Tree Implementation

This is a client-server connection with Zero Knowledge Architecture implementation to verify data.

Zero Knowledge Proof is a way for a prover to prove a thing to a verifier without showing the secret. Example: A verifier will verify if a prover has access to an email and the prover login into the email and shows it to the verifier but doesn't reveal the credentials, i.e. the prover gives zero information to the validator and shows that the information is correct.

Zero Knowledge Architecture is a pattern that allow to build applications where all data is stored and exchanged in an encrypted way. It enforces end-to-end encryption and client-side (prover) operations only.

What is the connection between a Merkle Tree and the Zero Knowledge Proof?

Merkle tree algorithm creates the ability to prove certain data is valid without sharing all the data. This makes it zero-knowledge proof.

When verifying data using a Merkle tree, there is a **Prover** and a **Verifier**:

- A Prover: Do all the calculations to create the Merkle root (just a hash!)
- A Verifier: Does not need to know all the values to know *for certain* one value is in the tree

Merkle trees are a huge benefit to the **Verifier**. You either produce a proof successfully, meaning data verification passes, or you don't, meaning your piece of data was not present when the Merkle root hash was calculated (or you performed the calculation wrong!).

## Install and run the project 

To get started with the repository, clone it and then run `npm install` in the top-level directory to install the depedencies.

There are three folders in this repository:

### Server

You can run the server from the top-level directory with `node server/index`. This file is an express server which will be hosted on port 1225 and respond to the client's request.

Think of the server as the _verifier_ here. It needs to verify that the `name` passed by the client is in the `MERKLE_ROOT`. If it is, then we can send the gift!

### Client

You can run the client from the top-level directory with `node client/index {name}`. This file is a script which will send an HTTP request to the server.

Think of the client as the _prover_ here. It needs to prove to the server that some `name` is in the `MERKLE_ROOT` on the server.  

### Utils

There are a few files in utils:

- The `niceList.json` which contains all the names of the people who deserve a gift this year (this is randomly generated, feel free to add yourself and others to this list!)
- The `example.js` script shows how we can generate a root, generate a proof and verify that some value is in the root using the proof. Try it out from the top-level folder with `node/example.js`
- The `MerkleTree.js` should look familiar from the Merkle Tree module! This one has been modified so you should not have to deal with any crypto type conversion. You can import this in your client/server
- The `verifyProof.js` should also look familiar. This was the last stage in the module. You can use this function to prove a name is in the merkle root, as show in the example.
