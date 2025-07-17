# QuickDB With Go

QuickDB is a lightweight, in-memory key-value database written in Go with basic data persistence. It provides both a server component exposing a simple Redis-like protocol over TCP/HTTP and a command-line interface (CLI) client for managing data.

## Features

* **In-memory storage** for fast read/write operations
* **Persistent snapshot** to disk to recover data on restart
* **Redis-inspired CLI** and server commands (e.g., `SET`, `GET`, `DEL`)
* **RESTful HTTP API** for easy integration
* **Modular architecture** with separate client and server submodules

## Repository Structure

```
quickdb-WithGo/
├── client/           # CLI client implementation (submodule)
├── quickdbServer/    # Server implementation (submodule)
├── .gitmodules       # Defines submodules
└── README.md         # Project overview and instructions
```

## Getting Started

### Prerequisites

* Go 1.18 or higher
* Git

### Clone the Repository

```bash
# Clone with submodules
git clone --recursive https://github.com/yagyagoel1/quickdb-WithGo.git
cd quickdb-WithGo
```

If you forgot `--recursive`, initialize submodules manually:

```bash
git submodule update --init --recursive
```

## Building

### Build the Server

```bash
cd quickdbServer
go build -o quickdbServer ./cmd/quickdb
```

### Build the CLI Client

```bash
cd ../client
go build -o quickdb-cli ./cmd
```

## Usage

### Start the Server

Run the server on the default port (6379) with persistence file `dump.db`:

```bash
./quickdbServer --port 6379 --dbpath dump.db
```

Or specify a custom port and database path:

```bash
./quickdbServer --port 8080 --dbpath /path/to/data.db
```

### CLI Client Commands

Use the CLI client to interact with the server:

```bash
# Set a key
./quickdb-cli set mykey "Hello, QuickDB!" --addr localhost:6379

# Get a key
./quickdb-cli get mykey --addr localhost:6379

# Delete a key
./quickdb-cli del mykey --addr localhost:6379
```

### HTTP API

The server also exposes a RESTful API:

```bash
# Set via HTTP
curl -X POST http://localhost:6379/set \   
  -d '{"key":"mykey","value":"value123"}'

# Get via HTTP
curl http://localhost:6379/get?key=mykey
```

## Configuration

The server supports the following flags:

* `--port` (int): Port on which the server listens (default: 6379)
* `--dbpath` (string): Path to the persistence file (default: `dump.db`)

The CLI client supports:

* `--addr` (string): Address of the QuickDB server (default: `localhost:6379`)

## Contributing

Contributions are welcome! Please open an issue for bugs or feature requests, or submit a pull request:

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -m "Add feature"`)
4. Push to the branch (`git push origin feature/my-feature`)
5. Open a pull request

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.

## Contact

Maintainer: Yagya Goel Email: [yagya](mailto:yagya.goel@example.com)[goel87@gmail.com](mailto:goel87@gmail.com)
Blog: [https://blogs.yagyagoel.dev/how-to-achieve-persistent-and-fast-in-memory-databases](https://blogs.yagyagoel.dev/how-to-achieve-persistent-and-fast-in-memory-databases)
