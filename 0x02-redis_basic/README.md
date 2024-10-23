# Redis basic
## Resources

**Read or watch:**

-   [Redis Crash Course Tutorial](https://intranet.alxswe.com/rltoken/hJVo3XwMMFFoApyX8zPXvA "Redis Crash Course Tutorial")
-   [Redis commands](https://intranet.alxswe.com/rltoken/oauvbRmxM12SxvimzqhrOg "Redis commands")
-   [Redis python client](https://intranet.alxswe.com/rltoken/imfgFhAZPlg7YMZ_tHvFZw "Redis python client")
-   [How to Use Redis With Python](https://intranet.alxswe.com/rltoken/7SluvFvgckwVgsvrfOf1CQ "How to Use Redis With Python")

## Learning Objectives

-   Learn how to use redis for basic operations
-   Learn how to use redis as a simple cache

### Overview of Redis

**Redis** (Remote Dictionary Server) is an open-source, in-memory key-value data store that can be used as a database, cache, message broker, and queue. Unlike traditional databases, Redis is designed for extremely fast operations due to its in-memory nature, meaning that data is stored in the system's RAM rather than on disk. It supports a variety of data structures such as strings, hashes, lists, sets, and sorted sets.

### Key Features of Redis:

1.  **In-Memory Data Store**: Redis keeps the entire dataset in memory, ensuring very low-latency data access. This makes it ideal for caching and real-time analytics.
2.  **Persistence Options**: Although it operates primarily in memory, Redis can persist data to disk using two mechanisms: **RDB (Redis Database Backup)** snapshots and **AOF (Append-Only File)** logs.
3.  **Data Structures**: Redis supports various data types:
    -   **Strings**: Simple key-value pairs.
    -   **Lists**: Ordered lists of strings.
    -   **Hashes**: Key-value pairs where values are mapped to keys within a key.
    -   **Sets**: Unordered collections of unique elements.
    -   **Sorted Sets**: Sets ordered by a score associated with each element.
4.  **Atomic Operations**: All Redis operations are atomic, ensuring that simultaneous operations won’t interfere with each other.
5.  **Replication and Clustering**: Redis supports master-slave replication and can be used in a distributed manner with Redis Cluster.
6.  **Pub/Sub Messaging**: Redis allows the implementation of publish/subscribe messaging, making it a good fit for real-time systems.
### Learning Objectives:

#### 1. How to Use Redis for Basic Operations

##### Installing Redis

Before you start using Redis, you need to install it on your system. You can install Redis on Linux or macOS using the following commands:
```
# On Linux (Ubuntu)
sudo apt update
sudo apt install redis-server

# On macOS (with Homebrew)
brew install redis
```
Start the Redis server:
```
redis-server
```
You can then interact with Redis using the Redis CLI:
```
redis-cli
```
##### Basic Redis Operations

In Redis, you perform basic CRUD (Create, Read, Update, Delete) operations using key-value pairs. Below are examples of how to use Redis for basic operations.

###### **1. Storing and Retrieving Strings (SET/GET)**

-   **SET**: Store a value associated with a key.
-   **GET**: Retrieve the value associated with a key.

Example:
```
# Set a value
SET name "George"
# Retrieve a value
GET name
```
###### **2. Incrementing Values**

Redis provides atomic operations like `INCR` to increment a value.

Example:
```
# Set an initial value
SET counter 1
# Increment the value by 1
INCR counter
# Output: 2
```

###### **3. Working with Lists**

-   **LPUSH**: Adds an element to the left (start) of a list.
-   **RPUSH**: Adds an element to the right (end) of a list.
-   **LPOP**: Removes and returns the first element of a list.
-   **LRANGE**: Retrieves elements from a list.

Example:
```
# Push values to the list
LPUSH tasks "Task 1"
LPUSH tasks "Task 2"
RPUSH tasks "Task 3"

# Retrieve all elements from the list
LRANGE tasks 0 -1
# Output: ["Task 2", "Task 1", "Task 3"]

# Pop the first element
LPOP tasks
# Output: "Task 2"
```
###### **4. Working with Hashes**

Redis hashes are perfect for representing objects.

-   **HSET**: Sets a field in a hash.
-   **HGET**: Retrieves a field from a hash.
-   **HGETALL**: Retrieves all fields and values of a hash.

Example:
```
# Set multiple fields in a hash
HSET user:1000 name "John" age 25 city "London"

# Retrieve a specific field
HGET user:1000 name

# Retrieve all fields and values in a hash
HGETALL user:1000
```
###### **5. Working with Sets**

Redis sets store unique elements and are useful when you want to ensure that a collection has no duplicates.

-   **SADD**: Adds one or more elements to a set.
-   **SMEMBERS**: Retrieves all the members of a set.
-   **SISMEMBER**: Checks if a specific value is in a set.

Example:
```
# Add values to a set
SADD languages "Python" "Java" "C++"

# Retrieve all members of the set
SMEMBERS languages
# Output: ["Python", "Java", "C++"]

# Check if a value exists in the set
SISMEMBER languages "Python"
# Output: 1 (True)
```
###### **6. Setting Expiration Times for Keys**

You can set a timeout for how long a key should exist before it is automatically deleted.

-   **EXPIRE**: Set the expiration time of a key in seconds.
-   **TTL**: Check how many seconds are left before a key expires.

Example:
```
# Set a key with a 60-second expiration
SET session_id "abc123"
EXPIRE session_id 60

# Check remaining time to live
TTL session_id
```
#### 2. How to Use Redis as a Simple Cache

Redis is often used as a cache layer in front of databases to reduce read times for frequently accessed data.

##### Why Use Redis for Caching?

-   **Fast access**: Since Redis stores data in-memory, it’s much faster than retrieving data from a traditional disk-based database.
-   **TTL (Time-to-Live)**: Redis allows you to set expiration times for cached entries, automatically removing them when they expire.
-   **Data integrity**: Redis ensures atomic operations, preventing race conditions and ensuring data consistency.

##### Simple Caching Example in Python with Redis

In this example, we will simulate using Redis as a cache to store user profile information that is normally retrieved from a database.

###### **Step 1: Install Redis-Py**

First, you need to install the Redis Python client:
```
pip install redis

```
###### **Step 2: Using Redis as a Cache**

Here’s an example of using Redis to cache user profiles:
```
import redis
import time

# Connect to Redis
cache = redis.Redis(host='localhost', port=6379, db=0)

# Simulate a function to retrieve data from a database
def get_user_profile(user_id):
    # Simulated delay for fetching from a database
    time.sleep(2)
    return {"user_id": user_id, "name": "John Doe", "age": 30}

# Define a function to fetch a user profile, with caching
def get_cached_user_profile(user_id):
    # Check if user profile is in cache
    cached_profile = cache.get(f"user_profile:{user_id}")
    if cached_profile:
        print("Cache hit!")
        return eval(cached_profile)
    
    print("Cache miss! Fetching from database...")
    # Fetch user profile from the database (or other sources)
    profile = get_user_profile(user_id)
    
    # Cache the profile with a TTL of 60 seconds
    cache.setex(f"user_profile:{user_id}", 60, str(profile))
    
    return profile

# Fetch the user profile
profile = get_cached_user_profile(1000)
print(profile)

# Fetch the user profile again (this time it should come from the cache)
profile = get_cached_user_profile(1000)
print(profile)
```
##### Explanation:

-   **Cache Miss**: The first time the user profile is requested, it will be fetched from the "database" (in this case, simulated by the `get_user_profile()` function), and then cached for 60 seconds.
-   **Cache Hit**: The second time the same user profile is requested within the TTL, Redis will serve the data from the cache, avoiding a trip to the database.
### Summary

**Basic Redis Operations**:

-   Redis allows you to perform fast CRUD operations with key-value pairs and supports a variety of data structures.
-   Basic operations include `SET`, `GET`, `LPUSH`, `HSET`, `SADD`, and `EXPIRE`.

**Redis as a Cache**:

-   Redis is commonly used as a caching layer for frequently accessed data due to its speed.
-   You can cache data with TTL (time-to-live) to automatically expire keys when needed.

Redis is an excellent choice for applications requiring fast access to data, low latency, and flexible data structures, making it widely used in real-time systems, caching, and distributed environments.

## Install Redis on Ubuntu 18.04
```
$ sudo apt-get -y install redis-server
$ pip3 install redis
$ sed -i "s/bind .*/bind 127.0.0.1/g" /etc/redis/redis.conf
```
**Use Redis in a container**

Redis server is stopped by default - when you are starting a container, you should start it with:  `service redis-server start`
