

# Blockchain-Python  

This is a Python-based blockchain implementation designed for educational purposes.  

The project demonstrates the fundamentals of blockchain, including block mining, transaction management, inter-node communication, and data persistence. Currently, it supports mining, simple transaction mechanisms, and inter-node communication through an HTTP-based RPC model instead of a peer-to-peer network. Advanced cryptographic verifications and validations for blocks and transactions between nodes are not yet implemented.  

---

## **Installation**  

### **1. Prerequisites**  
Ensure that [Python 3.2+](https://www.python.org/downloads/) is installed on your system.  

### **2. Clone the Repository**  
```bash
git clone https://github.com/chaithupro/blockchain-_final_year_project.git
cd blockchain
```

---

## **Usage**  

### **Creating an Account**  
```bash
python console account create
```  

### **Starting a Miner**  
```bash
python console miner start 3008
```  

### **Performing a Transaction**  
```bash
python console tx transfer from_address to_address amount
```  

### **Viewing Transactions**  
```bash
python console tx list
```  

### **Displaying Blockchain Data**  
```bash
python console blockchain list
```  

### **Setting Up Nodes**  
To simulate a network, duplicate the project directory and follow these steps:  

1. Start the miner on the first node:  
   ```bash
   python console miner start 3008
   ```  

2. In the new directory, add the first node:  
   ```bash
   python console node add 3008
   ```  

3. Start the new node:  
   ```bash
   python console node run 3009
   ```  

When a block is mined, it and its transactions will be broadcast to all connected nodes.  

---

## **Command Overview**  

Commands are structured as follows:  
```bash
python console [module] [action] [params...]
```  

For example:  
```bash
python console tx list
```  

| Module   | Action      | Parameters                        | Description                                   |
|----------|-------------|------------------------------------|-----------------------------------------------|
| `account` | `create`   | None                              | Create a new account.                         |
| `account` | `get`      | None                              | Display all accounts.                         |
| `account` | `current`  | None                              | Show the current mining reward account.       |
| `miner`   | `start`    | ip:port/port                      | Start the miner at the specified port.        |
| `node`    | `run`      | ip:port/port                      | Start a node at the specified port.           |
| `node`    | `list`     | None                              | List all nodes broadcasting transactions.     |
| `node`    | `add`      | ip:port                           | Add a node to broadcast transactions to.      |
| `tx`      | `transfer` | from_address to_address amount    | Transfer coins between addresses.             |
| `tx`      | `list`     | None                              | Display all transactions.                     |  

---

## **Project Details**  

### **Blockchain Structure**  

The blockchain consists of sequentially linked blocks, each containing transaction details. Each block is hashed using SHA256 to maintain its integrity. For example, a block may resemble the following:  
```json
{
  "index": 7,
  "timestamp": 1528972070,
  "tx": [
    "transaction_hash_1",
    "transaction_hash_2",
    "transaction_hash_3"
  ],
  "previous_block": "previous_block_hash",
  "nonce": 11063,
  "hash": "current_block_hash"
}
```  

Mining involves solving a cryptographic puzzle where the generated hash must meet a specific difficulty target (e.g., starting with a certain number of zeros).  

### **Simplifications**  
- The difficulty is low to make mining faster and more comprehensible.
- Transactions are stored directly as an array of hashes in blocks instead of using a Merkle tree structure.  

---

### **Mining Process**  

Mining rewards the miner with coins recorded as the first transaction in the new block.  
- Rewards are automatically credited to the miner's current account.  
- To start mining, create an account if you don’t already have one:  
  ```bash
  python console account create
  ```  

---

### **Networking**  

The blockchain network uses Python's RPC framework for communication between nodes instead of a peer-to-peer protocol.  
- Nodes can share transaction and block data.  
- New nodes can synchronize with existing ones to retrieve the full blockchain.  
- When a block is mined, nodes broadcast the new data to others for synchronization.  

---

### **Transactions**  

This implementation follows a simplified version of Bitcoin's UTXO (Unspent Transaction Output) model.  
- A balance is derived by summing unspent outputs.  
- Transactions consist of multiple inputs and outputs.  
- Pending transactions are broadcast to nodes and added to the blockchain after being mined into a block.  

---

## **Contributing**  

Contributions are welcome! Feel free to submit a pull request or open an issue for discussion.  

