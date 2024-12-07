# 0x03. Queuing System in JS

## Back-end | JavaScript | ES6 | Redis | NodeJS | ExpressJS | Kue

---

## Resources
### Read or Watch:
- [Redis Quick Start](https://redis.io/docs/getting-started/)
- [Redis Client Interface](https://redis.io/docs/clients/)
- [Redis Client for Node JS](https://github.com/redis/node-redis)
- [Kue (Deprecated but Used in the Industry)](https://github.com/Automattic/kue)

---

## Learning Objectives
By the end of this project, you should be able to explain:
1. How to run a Redis server on your machine.
2. How to perform basic operations using the Redis client.
3. How to use a Redis client with Node.js for basic operations.
4. How to store hash values in Redis.
5. How to handle asynchronous operations with Redis.
6. How to implement Kue as a queue system.
7. How to build a basic Express app interacting with a Redis server.
8. How to build a basic Express app interacting with both a Redis server and a queue.

---

## Requirements
- **Environment**: Ubuntu 18.04, Node 12.x, Redis 5.0.7
- **Coding Style**: Files must end with a new line.
- **Extensions**: JavaScript files should use `.js`.
- **Project Structure**:
  - A `README.md` file at the root of the project is mandatory.
  - Ensure a proper `package.json` is included.

### Required Files:
- **`package.json`**: Contains project dependencies and scripts.
- **`.babelrc`**: Babel configuration file.

Run the following to install the dependencies:
```bash
npm install
```

---

## Tasks

### 0. Install a Redis Instance
1. Download, extract, and compile Redis:
   ```bash
   wget http://download.redis.io/releases/redis-6.0.10.tar.gz
   tar xzf redis-6.0.10.tar.gz
   cd redis-6.0.10
   make
   ```
2. Start the Redis server:
   ```bash
   src/redis-server &
   ```
3. Confirm the server is running:
   ```bash
   src/redis-cli ping
   ```
   Expected output:
   ```
   PONG
   ```

4. Use the Redis client to set and get a value:
   ```bash
   set ALX School
   get ALX
   ```
   Expected output:
   ```
   "School"
   ```

5. Kill the server:
   ```bash
   ps aux | grep redis
   kill <PID_OF_Redis_Server>
   ```

6. Copy the `dump.rdb` file to the root of the project.

**Repository**:  
- **Directory**: `0x03-queuing_system_in_js`  
- **Files**: `README.md`, `dump.rdb`

---

### 1. Node Redis Client
- Install `node_redis` using npm:
  ```bash
  npm install redis
  ```
- **File**: `0-redis_client.js`

### Requirements:
- Log connection success or failure:
  - **Success**: `Redis client connected to the server`
  - **Failure**: `Redis client not connected to the server: ERROR_MESSAGE`

**Repository**:  
- **Directory**: `0x03-queuing_system_in_js`  
- **File**: `0-redis_client.js`

---

### 2. Node Redis Client and Basic Operations
- **File**: `1-redis_op.js`
- Add:
  - `setNewSchool(schoolName, value)`: Sets a key-value pair in Redis.
  - `displaySchoolValue(schoolName)`: Logs the value of a key.

---

### 3. Node Redis Client and Async Operations
- **File**: `2-redis_op_async.js`
- Use `util.promisify` to refactor `displaySchoolValue` for async/await operations.

---

### 4. Node Redis Client and Advanced Operations
- **File**: `4-redis_advanced_op.js`
- Use `hset` to store a hash and `hgetall` to display it.

---

### 5. Node Redis Client Publisher and Subscriber
- **Files**: `5-publisher.js`, `5-subscriber.js`
- Set up Redis pub/sub to handle messages across processes.

---

### 6. Create the Job Creator
- **File**: `6-job_creator.js`
- Use Kue to create a job and log its status.

---

### 7. Create the Job Processor
- **File**: `6-job_processor.js`
- Set up a queue processor using Kue to handle jobs.

---

### 8. Track Progress and Errors with Kue
- **File**: `7-job_creator.js`
- Loop through an array of jobs, create jobs in the queue, and track their status.

---

## Author
**Martin Nyemba**  
Part of the **ALX Backend** curriculum.  
