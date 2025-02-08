# MongoDB Guidelines

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [MongoDB Compass](#mongodb-compass)
- [Setting Up .env File](#setting-up-env-file)
- [Starting MongoDB](#starting-mongodb)
- [Basic Commands](#basic-commands)
- [CRUD Operations](#crud-operations)
- [Indexes](#indexes)
- [Backup & Restore](#backup--restore)
- [Security Best Practices](#security-best-practices)
- [Performance Tuning](#performance-tuning)
- [Resources](#resources)

## Introduction
MongoDB is a NoSQL database that provides high performance, high availability, and easy scalability. It stores data in flexible, JSON-like documents.

## Installation

### Install MongoDB on Linux (Ubuntu/Debian)
```sh
sudo apt update
sudo apt install -y mongodb
```

### Install MongoDB on macOS (Homebrew)
```sh
brew tap mongodb/brew
brew install mongodb-community@6.0
```

### Install MongoDB on Windows
1. Download MongoDB from [MongoDB Download Center](https://www.mongodb.com/try/download/community)
2. Run the installer and follow the installation wizard
3. Select "Complete" setup type
4. Ensure "Install MongoDB as a Service" is checked
5. Finish installation and restart the system if required
6. Add MongoDB bin directory (`C:\Program Files\MongoDB\Server\6.0\bin`) to the system PATH

### Verify Installation on Windows
```sh
mongo --version
```

## MongoDB Compass
MongoDB Compass is a GUI tool for visualizing and managing MongoDB databases.

### Install MongoDB Compass
1. Download MongoDB Compass from [MongoDB Compass Download](https://www.mongodb.com/products/compass)
2. Run the installer and follow the setup instructions

### Connect to MongoDB
1. Open MongoDB Compass
2. Enter the connection string (e.g., `mongodb://localhost:27017`)
3. Click "Connect"

### Basic Usage
- View and manage databases and collections
- Run queries with the built-in query builder
- Visualize schema and analyze data

## Setting Up .env File
Using an `.env` file allows you to manage MongoDB connection details securely without hardcoding them into your application.

### Create an `.env` File
In your project root directory, create a `.env` file and add the following:
```sh
MONGO_URI=mongodb://localhost:27017/myDatabase
```

### Load the `.env` File in Your Application
In a Node.js project, install `dotenv`:
```sh
npm install dotenv
```
Then, load the environment variables in your application:
```javascript
require('dotenv').config();
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGO_URI, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
})
.then(() => console.log('MongoDB connected'))
.catch(err => console.error('MongoDB connection error:', err));
```

## Starting MongoDB

### Start MongoDB Service
```sh
sudo systemctl start mongod  # Linux
brew services start mongodb-community@6.0  # macOS
net start MongoDB  # Windows
```

### Stop MongoDB Service
```sh
sudo systemctl stop mongod  # Linux
brew services stop mongodb-community@6.0  # macOS
net stop MongoDB  # Windows
```

### Verify MongoDB is Running
```sh
mongo --eval 'db.runCommand({ connectionStatus: 1 })'
```

## Basic Commands

### Connect to MongoDB
```sh
mongo
```

### Show Databases
```sh
show dbs
```

### Switch/Create Database
```sh
use myDatabase
```

### Show Collections
```sh
show collections
```

## CRUD Operations

### Insert Data
```sh
db.users.insertOne({ name: "John", age: 30, city: "New York" })
```

### Read Data
```sh
db.users.find()
```

### Update Data
```sh
db.users.updateOne({ name: "John" }, { $set: { age: 31 } })
```

### Delete Data
```sh
db.users.deleteOne({ name: "John" })
```

## Indexes
Indexes improve query performance. Example:
```sh
db.users.createIndex({ name: 1 })
```

## Backup & Restore

### Backup Database
```sh
mongodump --db=myDatabase --out=/backup/
```

### Restore Database
```sh
mongorestore --db=myDatabase /backup/myDatabase
```

## Security Best Practices
- **Enable Authentication:**
  ```sh
  use admin
  db.createUser({ user: "admin", pwd: "securepassword", roles: ["root"] })
  ```
- **Bind MongoDB to a Specific IP:**
  Modify `mongod.conf`:
  ```yaml
  bindIp: 127.0.0.1
  ```
- **Use TLS/SSL for Encryption**
- **Regularly Update MongoDB**

## Performance Tuning
- Use **Indexes** for faster queries
- Optimize **Schema Design**
- Use **Replication & Sharding** for scalability
- Monitor queries using `explain()`

## Resources
- [MongoDB Documentation](https://www.mongodb.com/docs/manual/)
- [MongoDB University](https://university.mongodb.com/)
- [MongoDB Community Forum](https://www.mongodb.com/community/forums/)
