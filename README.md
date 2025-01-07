# **DERIBIT** : Simplified Order Management and Execution Tool in C++

DeriBot is a powerful yet simple command-line application for order management, leveraging a websocket client to connect to the [Deribit TESTNET](https://test.deribit.com). It enables efficient portfolio management and trade execution with ease.

<p align="center">
  <img src="https://i.imgur.com/CgVxwNf.png" alt="DeriBot CLI" width="500px">
</p>

---

## **Developed by [Abhishek Kumar](https://www.linkedin.com/in/ctrlabhi/)**

---

## **Table of Contents**
- [Build Instructions](#build-instructions)
  - [Prerequisites](#prerequisites)
  - [Build Steps](#build-steps)
- [Using DeriBot](#using-deribot)
  - [General Commands](#general-commands)
  - [Connecting to Deribit API](#connecting-to-deribit-api)
  - [Trading Commands](#trading-commands)
- [Dependencies](#dependencies)
- [License](#license)

---

## **Build Instructions**

### **Prerequisites**
Before building the project, ensure your system meets the following requirements:

1. **C++ Compiler**: Ensure a compiler like `g++` is installed.
2. **CMake**: Install CMake based on your OS:
   - **MacOS**: `brew install cmake`
   - **Linux**: `sudo apt install cmake`
   - **Windows**: [Download from the official site](https://cmake.org/download/)
3. **Boost and OpenSSL**:
   - **MacOS**:
     ```bash
     brew install boost openssl
     ```
   - **Linux**:
     ```bash
     sudo apt install libboost-all-dev libssl-dev
     ```
   - **Windows**: Download from their respective official websites.

#### **Verify Installations**
Check installed versions:
```bash
$ g++ --version
$ cmake --version
$ dpkg -l | grep libboost
$ openssl version
```

---

### **Build Steps**
1. Clone the repository:
   ```bash
   $ git clone https://github.com/ShuvraneelMitra/DeriBot-CPP.git
   ```
2. Navigate to the project folder and create a build directory:
   ```bash
   $ cd DeriBot-CPP
   $ mkdir build && cd build
   ```
3. Configure and build the project using CMake:
   ```bash
   $ cmake .. -Wno-dev
   $ cmake --build .
   ```
   > The build process will fetch dependencies like [websocketpp](https://github.com/zaphoyd/websocketpp) and [nlohmann json](https://github.com/nlohmann/json).

4. Run the executable:
   ```bash
   $ ./DeriBot
   ```
   Depending on your system, the command may vary: `$ ./DeriBot`, `$ DeriBot`, or `$ .\DeriBot`.

---

## **Using DeriBot**

### **General Commands**
DeriBot also functions as a standard websocket client. Use the following commands:

1. **`help`**: Display all supported commands.
2. **`quit`**: Close all websocket connections and exit.
3. **`show <id>`**: Display metadata of the connection with ID `<id>`.
4. **`send <id> <message>`**: Send `<message>` to the connection with ID `<id>`.
5. **`show_messages <id>`**: View all messages exchanged on the connection with ID `<id>`.

---

### **Connecting to Deribit API**

#### **Steps to Connect**
1. **Create an API Key:** Generate API keys (Client ID and Client Secret) from your Deribit account.
2. **Connect to Deribit WebSocket:**
   ```bash
   $ connect wss://test.deribit.com/ws/api/v2
   ```
   - You will see: `Created connection with ID 0`.
   - Shortcut: `DERIBIT connect`
3. **Verify the Connection:**
   ```bash
   $ show 0
   ```
   Expected output:
   ```plaintext
   > URI: wss://test.deribit.com/ws/api/v2
   > Status: Open
   > Remote Server: nginx/1.25.5
   > Messages Processed: (0)
   ```
4. **Authenticate the Connection:**
   ```bash
   $ DERIBIT authorize <connection_id> <client_id> <client_secret> -r(optional)
   ```
   - Use `-r` to store the session access token.
   - Without `-r`, you must manually input the access token for private API methods.

---

### **Trading Commands**

#### **1. Placing Buy Orders**
   ```bash
   $ DERIBIT <id> buy <instrument> <transaction_name>
   ```
   Follow prompts to provide details like:
   - **Amount or Contracts**: Specify `amount x` or `contracts x`.
   - **Order Type**: Choose from `limit`, `market`, `stop_limit`, etc.
   - **Time in Force**: Specify `good_til_cancelled`, `fill_or_kill`, etc.

#### **2. Placing Sell Orders**
   ```bash
   $ DERIBIT <id> sell <instrument> <transaction_name>
   ```
   Same behavior as `buy`, but places a sell order.

#### **3. Fetching Open Orders**
   ```bash
   $ DERIBIT <id> get_open_orders
   ```
   Additional filters available:
   - By Currency: `get_open_orders <currency>`
   - By Instrument: `get_open_orders <instrument>`

#### **4. Modifying an Order**
   ```bash
   $ DERIBIT <id> modify <order_id>
   ```
   Retrieve order IDs using `get_open_orders`.

#### **5. Cancelling Orders**
   - Cancel a specific order:
     ```bash
     $ DERIBIT <id> cancel <order_id>
     ```
   - Cancel all orders:
     ```bash
     $ DERIBIT <id> cancel_all <options>
     ```
     - Options: Specify `instrument` or `currency`. Leaving it blank cancels all orders.

---

## **Dependencies**
1. [websocketpp](https://github.com/zaphoyd/websocketpp) - WebSocket protocol implementation.
2. [nlohmann/json](https://github.com/nlohmann/json) - JSON parsing and handling.

---

## **License**
This project is licensed under the MIT License. See the LICENSE file for details.

---

**Developed by [Abhishek Kumar](https://www.linkedin.com/in/ctrlabhi/)**