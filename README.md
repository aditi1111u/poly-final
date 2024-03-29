# poly-final

Below is an example of a simple circuit implementation in Circom, along with instructions for compiling the circuit, generating a proof, deploying a solidity verifier, and testing the proof.

### 1. Circuit Implementation (circuit.circom)

```circom
template Multiplier() {
    signal private input a, b;
    signal output c;
    c <== a * b;
}

component main = Multiplier();
```

### 2. Compile Circuit

Compile the circuit using Circom:

```bash
circom circuit.circom -o circuit.json
```

### 3. Generate Proof

Generate a proof using the compiled circuit:

```bash
snarkjs wtns calculate circuit.wasm input.json witness.wtns
```

### 4. Deploy Solidity Verifier

Deploy a Solidity verifier contract to the Sepolia or Mumbai Testnet. Below is a simple example:

```solidity
pragma solidity ^0.8.0;

contract Verifier {
    function verifyProof(uint[2] memory a, uint[2][2] memory b, uint[2] memory c, uint[2] memory input) public view returns (bool) {
        // Verification logic
        // Return true if proof is valid, false otherwise
    }
}
```

### 5. Test Proof

Call the `verifyProof()` method on the deployed verifier contract and assert the output is true:

```solidity
// Assuming you have deployed the verifier contract and have its address stored in verifierAddress

bool proofIsValid = Verifier(verifierAddress).verifyProof(a, b, c, input);
require(proofIsValid, "Proof is invalid");
```

### README File

#### Project Overview
This project demonstrates how to create and verify a simple circuit using Circom and Solidity.

#### Instructions
1. **Compile Circuit**: Use Circom to compile the circuit.
2. **Generate Proof**: Generate a proof using the compiled circuit and input values.
3. **Deploy Verifier**: Deploy a Solidity verifier contract to Sepolia or Mumbai Testnet.
4. **Test Proof**: Call the `verifyProof()` method on the deployed verifier contract and assert the output is true.

#### Notes
- Ensure you have the necessary tools installed (Circom, snarkjs, Solidity compiler).
- Modify the verifier contract as needed to match your specific circuit and proof format.

By following these steps and guidelines, you can successfully create, compile, and verify a circuit using Circom and Solidity.
- - -
