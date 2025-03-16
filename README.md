# Simple Redis in Go

This project is a simplified, educational implementation of an in-memory database inspired by Redis, built using Go. It demonstrates core database concepts like network communication, data parsing, command handling, and persistence.

![image](https://github.com/user-attachments/assets/99c0ebac-e87e-45b5-a1a3-0ae8071cf48d)


## Features

- **Basic Redis Command Support:**
  - Implements `PING`, `SET`, `GET`, `HSET`, and `HGET`.
  - `PING`: Responds with "PONG" or echoes the provided argument. Implemented in `handler.go` within the `ping` function.
  - `SET` and `GET`: Stores and retrieves key-value pairs using a Go map. Thread safety is ensured with `sync.RWMutex`. Implemented in `handler.go` within the `set` and `get` functions.
  - `HSET` and `HGET`: Stores and retrieves key-value pairs within hashes, using a nested Go map. Thread safety is also provided by `sync.RWMutex`. Implemented in `handler.go` within the `hset` and `hget` functions.
- **RESP Protocol:**
  - Parses and serializes data using the Redis Serialization Protocol (RESP).
  - The `resp.go` file contains the `Resp` struct and its methods for parsing RESP data from client connections.
  - It also contains the `Value` struct, and its methods for marshalling data to RESP format for sending responses.
- **Concurrency:**
  - Handles multiple client connections using Go routines.
  - The `main.go` file spawns a new goroutine for each incoming client connection, allowing the server to handle multiple clients concurrently.
- **AOF Persistence:**
![image](https://github.com/user-attachments/assets/d1230b38-8855-44b5-a0be-4d4b8739ffd0)

  - Implements Append Only File (AOF) persistence for data durability.
  - The `aof.go` file manages the AOF file, writing `SET` and `HSET` commands to the file.
  - On server startup, it reads the AOF file and replays the commands to restore the database state.
  - A goroutine is used to sync the file to disk every second.

## Getting Started

### Prerequisites

- Go 1.16 or later

### Installation

1.  Clone the repository:

    ```bash
    git clone https://github.com/harshita9104/Redis_Golang.git
    ```

2.  Build the server:

    ```bash
    go build
    ```

### Running the Server

1.  Run the executable:

    ```bash
    go run main.go
    ```

2.  Connect using `redis-cli`:

    ```bash
    redis-cli
    ```

3.  Use the implemented Redis commands.

## Project Structure

- `main.go`: Contains the main server logic, including connection handling and command dispatch.
- `resp.go`: Handles RESP parsing and serialization, defining the `Resp` and `Value` structs.
- `handler.go`: Implements Redis command handlers, using Go maps for data storage.
- `aof.go`: Manages AOF persistence, providing methods for writing and reading commands.
