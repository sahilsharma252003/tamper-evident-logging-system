# 🛡️ Blockchain-Based Tamper-Evident Logging System with Proof-of-Work

This project simulates a decentralized and tamper-evident logging system using blockchain principles and proof-of-work (PoW). It ensures secure, verifiable log entries through cryptographic hashing and a custom server-client architecture built in Python and C.

---

## 🧠 Core Idea

The system logs messages with a computational proof-of-work (PoW) that guarantees tamper resistance. Messages are chained using hashes, and verification ensures historical integrity—similar to blockchain logging but in a lighter, file-based form.

---

## 🔧 Components

### 🔹 `log`
- Python client that:
  - Sanitizes the log message
  - Performs a double SHA-256 PoW to find a valid nonce (22-bit difficulty)
  - Sends the final message (`nonce:message`) to the logging server

### 🔹 `logserver`
- C-based TCP server that:
  - Receives messages and appends them to the log file
  - Validates message structure and PoW before acceptance
  - Maintains integrity by chaining log entries via hashes

### 🔹 `checklog`
- C program that:
  - Validates the integrity of the log chain by re-computing hashes
  - Detects if any message was altered or deleted

---

## 🔐 Security Features

- **Double SHA-256** for proof-of-work
- **22-bit PoW difficulty**, enforced via leading-zero bit threshold
- **Log chain verification** via chained hash structure
- **Message sanitization** to ensure format consistency and prevent injection

---

## 📂 File Structure

| File         | Language | Role                                  |
|--------------|----------|----------------------------------------|
| `log`        | Python   | Client: message sanitization + PoW     |
| `logserver`  | C        | Server: message reception + hash chain |
| `checklog`   | C        | Verifier: re-hashes log chain          |
| `Makefile`   | Shell    | Compiles C binaries (`logserver`, `checklog`) |

---

## 🚀 How to Run

### 🛠 Compile the server and verifier

```bash
make
```

### 🔐 Start the log server

```bash
./logserver <port>
```

### 📝 Submit a log message (must be ≥ 64 bytes)

```bash
./log <port> "This is a secure message that is at least sixty-four bytes long..."
```

### 🔍 Verify the entire log chain

```bash
./checklog
```

---

## 📊 Example Log Format

```
1: <nonce>:<message>
2: <nonce>:<message>
...
Hash Chaining: Each message includes the SHA-256 hash of the previous entry
```

---

## 🧠 Concepts Demonstrated

- Blockchain-inspired logging architecture
- Cryptographic hash chaining
- Proof-of-work difficulty validation
- TCP socket communication
- Tamper detection in log chains

---

## 🙌 Authors

Sahil Sharma — CS440 Assignment, April 2025

---

## 📜 License

For academic and educational demonstration purposes.
