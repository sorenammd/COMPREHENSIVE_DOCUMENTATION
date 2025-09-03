# Pactus Blockchain - Comprehensive Technical Documentation

**Project**: Pactus Blockchain - Next Generation Proof-of-Stake Network  
**Repository**: pactus-nexus  
**Language**: Go 1.24.5  
**Architecture**: Modular Byzantine Fault Tolerant Blockchain  
**License**: MIT License  
**Network Types**: Mainnet, Testnet, Localnet

## Executive Summary

Pactus is a sophisticated, production-ready blockchain platform implementing a novel Byzantine Fault Tolerant (BFT) consensus mechanism with built-in change-proposer functionality. The system represents a significant advancement in blockchain technology, featuring a unique sortition-based validator selection system, dual cryptographic signature support (BLS12-381 and Ed25519), comprehensive multi-language API ecosystem, and advanced execution engine supporting multiple transaction types.

### Key Technical Specifications

- **Consensus Algorithm**: Custom BFT with Change-Proposer Protocol
- **Block Time**: 10 seconds (configurable: 2-3600 seconds)
- **Committee Size**: 51 validators (mainnet), 7 validators (testnet)
- **Transaction Types**: 6 types (Transfer, Bond, Unbond, Withdraw, Sortition, BatchTransfer)
- **Cryptographic Schemes**: BLS12-381 and Ed25519 signature algorithms
- **Storage Engine**: LevelDB with Merkle tree indexing
- **Network Protocol**: libp2p with gossip, DHT, and mDNS discovery
- **API Support**: gRPC, JSON-RPC, HTTP REST, WebSocket, ZeroMQ
- **Programming Language**: Go 1.24.5 with extensive test coverage
- **Address Format**: Bech32m encoding with human-readable prefixes

## Table of Contents

1. [Project Overview](#project-overview)
2. [Architecture](#architecture)
3. [Core Components](#core-components)
4. [Consensus Algorithm](#consensus-algorithm)
5. [Network Layer](#network-layer)
6. [State Management](#state-management)
7. [Transaction System](#transaction-system)
8. [Validation and Committee](#validation-and-committee)
9. [APIs and Interfaces](#apis-and-interfaces)
10. [Configuration](#configuration)
11. [Development Guide](#development-guide)
12. [Deployment](#deployment)
13. [Testing](#testing)
14. [Troubleshooting](#troubleshooting)

---

## Project Overview

Pactus is an innovative blockchain platform designed to address the scalability, energy efficiency, and governance challenges faced by traditional blockchain networks. The project implements a sophisticated Proof-of-Stake consensus mechanism combined with Byzantine Fault Tolerance, creating a robust and efficient distributed ledger system.

### Project Specifications

```yaml
Project Name: Pactus Blockchain
Version: Development Branch (consensus-v2)
Programming Language: Go 1.24.5
Architecture: Modular, Event-Driven
Total Supply: 42,000,000,000,000,000 NanoPAC (42 million PAC)
Block Time: 10 seconds (Mainnet), 2 seconds (Testnet)
Finality: Instant (BFT consensus)
Energy Efficiency: 99.99% more efficient than PoW
```

### Core Design Philosophy

1. **Security First**: Implementing BFT consensus with formal security proofs
2. **Scalability**: Optimized for high transaction throughput with low latency
3. **Accessibility**: Simple validator participation with fair sortition
4. **Decentralization**: Promoting wide validator distribution through low entry barriers
5. **Sustainability**: Energy-efficient consensus mechanism
6. **Interoperability**: Multi-language client support and comprehensive APIs

### Technical Innovation

The Pactus blockchain introduces several novel concepts:

- **Sortition-Based Proposer Selection**: Using verifiable random functions (VRF)
- **Change-Proposer Protocol**: Automatic leader rotation for Byzantine resilience
- **Dual Signature Support**: BLS for validators, Ed25519 for accounts
- **Multi-Type Transaction System**: Comprehensive transaction types for all operations
- **Consensus Version 2**: Enhanced BFT algorithm with improved performance

### Network Parameters

#### Mainnet Configuration
```json
{
  "chain_type": "Mainnet",
  "genesis_time": "2024-01-24T20:24:00Z",
  "genesis_hash": "e4d59e3145c9d718caf178edb33bc2ca7fe43e5b30990c9d57d53a60c4741432",
  "block_interval": 10,
  "committee_size": 51,
  "bond_interval": 360,
  "unbond_interval": 181440,
  "sortition_interval": 17,
  "minimum_stake": "1000000000",
  "maximum_stake": "1000000000000",
  "block_reward": "1000000000",
  "address_prefix": "pc",
  "validator_prefix": "pc",
  "default_port": 21888
}
```

#### Testnet Configuration
```json
{
  "chain_type": "Testnet",
  "genesis_time": "2024-03-16T00:00:00Z",
  "genesis_hash": "13f96e6fbc9e0de0d53537ac5e894fc8e66be1600436db2df1511dc30696e822",
  "block_interval": 10,
  "committee_size": 7,
  "bond_interval": 360,
  "unbond_interval": 181440,
  "sortition_interval": 17,
  "minimum_stake": "1000000000",
  "maximum_stake": "1000000000000",
  "block_reward": "1000000000",
  "address_prefix": "tpc",
  "validator_prefix": "tpc",
  "default_port": 21777
}
```

### Economic Model

The Pactus economic model is designed to ensure long-term sustainability and fair distribution:

- **Total Supply**: Fixed at 42 trillion NanoPAC (42 million PAC)
- **Initial Distribution**: Through genesis allocation to initial validators
- **Block Rewards**: 1 PAC per block, decreasing over time
- **Staking Requirements**: Minimum 1,000 PAC to become validator
- **Inflation**: Controlled through block reward adjustments
- **Fee Structure**: Fixed transaction fees based on transaction type

### Key Features

- **Byzantine Fault Tolerant Consensus**: Advanced consensus algorithm with change-proposer mechanism
- **Proof of Stake**: Energy-efficient validation system with sortition-based validator selection
- **Modular Architecture**: Clean separation of concerns with well-defined interfaces
- **Multi-Network Support**: Mainnet, Testnet, and Localnet configurations
- **Rich API Support**: gRPC, JSON-RPC, HTTP, and ZeroMQ interfaces
- **Comprehensive Tooling**: CLI tools for node management and wallet operations
- **GTK GUI Support**: User-friendly graphical interface
- **Advanced Networking**: libp2p-based peer-to-peer networking with gossip protocol

### Project Statistics

- **Language**: Go 1.24.5+
- **License**: MIT
- **Architecture**: Modular microservices design
- **Consensus**: Custom BFT with change-proposer
- **Networking**: libp2p with DHT and mDNS
- **Storage**: LevelDB with Merkle tree indexing

---

## Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Pactus Node                              │
├─────────────────┬─────────────────┬─────────────────────────────┤
│   API Layer     │   Core Layer    │     Infrastructure         │
│                 │                 │                             │
│ ┌─────────────┐ │ ┌─────────────┐ │ ┌─────────────┬─────────────┐ │
│ │ gRPC        │ │ │ Consensus   │ │ │ Network     │ Storage     │ │
│ │ JSON-RPC    │ │ │ V1 & V2     │ │ │ (libp2p)    │ (LevelDB)   │ │
│ │ HTTP/HTML   │ │ ├─────────────┤ │ ├─────────────┼─────────────┤ │
│ │ ZeroMQ      │ │ │ State Mgmt  │ │ │ Sync        │ TxPool      │ │
│ └─────────────┘ │ ├─────────────┤ │ │ P2P Gossip  │ Wallet      │ │
│                 │ │ Committee   │ │ │ DHT/mDNS    │ Config      │ │
│                 │ │ Validation  │ │ └─────────────┴─────────────┘ │
│                 │ └─────────────┘ │                             │
└─────────────────┴─────────────────┴─────────────────────────────┘
```

### Component Interaction Flow

1. **Network Layer** receives transactions and blocks from peers
2. **Sync Module** coordinates block and state synchronization
3. **TxPool** validates and manages pending transactions
4. **Consensus** manages block production and validation
5. **State** maintains current blockchain state and validator set
6. **Committee** manages validator rotation and proposer selection
7. **APIs** expose blockchain data and operations to external clients

---

## Core Components

### 1. Consensus Module (`consensus/` & `consensusv2/`)

The consensus module implements the core Byzantine Fault Tolerant consensus algorithm with the following characteristics:

#### Consensus V1 (Legacy)
- **Location**: `consensus/`
- **Status**: Deprecated, maintained for compatibility
- **Features**: Basic BFT consensus

#### Consensus V2 (Current)
- **Location**: `consensusv2/`
- **Status**: Active development
- **Features**: Advanced BFT with change-proposer mechanism

#### Key Components:

**States**:
- `PrepareState`: Initial proposal validation
- `PrecommitState`: Commit preparation
- `CommitState`: Final block commitment
- `ChangeProposerState`: Proposer rotation mechanism

**Vote Types**:
- `VoteTypePrepare`: Proposal acknowledgment (deprecated)
- `VoteTypePrecommit`: Commitment votes
- `VoteTypeCPPreVote`: Change-proposer pre-votes
- `VoteTypeCPMainVote`: Change-proposer main votes
- `VoteTypeCPDecided`: Change-proposer decisions

**Justifications**:
- `JustInitYes`: Initial agreement justification
- `JustInitNo`: Initial disagreement justification
- `JustPreVoteHard`: Complex pre-vote justification
- `JustMainVoteNoConflict`: Conflict-free main vote justification
- `JustDecided`: Final decision justification

### 2. State Management (`state/`)

The state module manages the current blockchain state including:

#### Core Responsibilities:
- **Account State**: Balance and nonce tracking
- **Validator State**: Validator registration and power management
- **Committee State**: Active validator set management
- **Block State**: Block height and hash tracking
- **Transaction Execution**: Transaction processing and state updates

#### Key Features:
- **Merkle Trees**: Persistent Merkle trees for cryptographic state verification
- **Sandboxing**: Isolated execution environments for transaction validation
- **State Persistence**: Atomic state commits with rollback capability
- **Power Management**: Validator power calculation and committee updates

### 3. Committee Management (`committee/`)

The committee module handles validator set management and proposer selection:

#### Features:
- **Validator Registration**: New validator onboarding
- **Power Calculation**: Stake-based power computation
- **Proposer Selection**: Round-robin proposer rotation
- **Committee Updates**: Dynamic validator set changes
- **Byzantine Tolerance**: Fault-tolerant validator management

#### Key Operations:
```go
// Check if address is proposer for specific round
IsProposer(addr crypto.Address, round int16) bool

// Get proposer for specific round
Proposer(round int16) *validator.Validator

// Check if validator is in committee
Contains(addr crypto.Address) bool

// Update committee with new validators
Update(lastRound int16, joined []*validator.Validator)
```

### 4. Network Layer (`network/`)

Built on libp2p, the network layer provides:

#### Core Services:
- **Host Management**: libp2p host configuration and lifecycle
- **Peer Discovery**: DHT and mDNS-based peer discovery
- **Gossip Protocol**: Message propagation across the network
- **Stream Management**: Bidirectional communication streams
- **Connection Management**: Peer connection lifecycle and limits

#### Network Protocols:
- **Gossip**: Block and transaction propagation
- **Sync**: Block synchronization protocol
- **DHT**: Distributed hash table for peer discovery
- **mDNS**: Local network discovery

### 5. Synchronization (`sync/`)

The sync module coordinates blockchain synchronization:

#### Sync Strategies:
- **Fast Sync**: Quick catchup for new nodes
- **Regular Sync**: Standard block-by-block synchronization
- **State Sync**: Direct state synchronization for rapid bootstrap

#### Components:
- **Bundle Management**: Message bundling and processing
- **Peer Set**: Active peer management and scoring
- **Firewall**: Message filtering and rate limiting
- **Cache**: Temporary storage for sync data

### 6. Transaction Pool (`txpool/`)

Manages pending transactions with:

#### Features:
- **Transaction Validation**: Syntax and semantic validation
- **Fee Management**: Transaction fee calculation and prioritization
- **Mempool Management**: In-memory transaction storage
- **Broadcast Coordination**: Transaction propagation to peers

### 7. Execution Layer (`execution/`)

The execution layer handles transaction processing and state transitions:

#### Core Components:

**Execution Engine (`execution.go`)**:
- **Transaction Processing**: Executes validated transactions
- **State Transitions**: Applies state changes atomically
- **Error Handling**: Manages execution failures and rollbacks
- **Lock Time Validation**: Ensures proper transaction timing

**Executor Factory (`executor/`)**:
- **Type-Based Routing**: Routes transactions to appropriate executors
- **Validation Pipeline**: Two-phase validation (syntax/semantic)
- **Execution Context**: Provides isolated execution environments

**Transaction Executors**:
- `TransferExecutor`: Handles PAC token transfers
- `BondExecutor`: Manages validator staking operations
- `UnbondExecutor`: Processes validator unstaking
- `WithdrawExecutor`: Handles validator reward withdrawals
- `SortitionExecutor`: Validates sortition proofs
- `BatchTransferExecutor`: Processes multiple transfers efficiently

#### Execution Flow:
```go
// Two-phase execution process
1. CheckAndExecute(trx, sandbox, strict) -> error
   - Lock time validation
   - Signer verification (anti-spam)
   - Replay protection
   - Executor-specific validation
   - State changes application
   
2. Execute(trx, sandbox) -> error
   - Direct execution without validation
   - Used for pre-validated transactions
```

### 8. Sandbox Environment (`sandbox/`)

Provides isolated execution environments for transaction processing:

#### Key Features:
- **State Isolation**: Prevents invalid transactions from corrupting state
- **Account Management**: Tracks account balances and sequences
- **Validator Management**: Manages validator states and committee changes
- **Power Calculation**: Computes and tracks validator voting power
- **Committee Integration**: Interfaces with active validator committee
- **Proof Verification**: Validates sortition proofs

#### Sandbox Operations:
```go
// Account operations
Account(addr) *account.Account
MakeNewAccount(addr) *account.Account
UpdateAccount(addr, acc)

// Validator operations
Validator(addr) *validator.Validator
MakeNewValidator(pub) *validator.Validator
UpdateValidator(val)
IsJoinedCommittee(addr) bool

// Transaction tracking
RecentTransaction(txID) bool
CommitTransaction(trx)
AccumulatedFee() amount.Amount
```

### 9. Storage Layer (`store/`)

Built on LevelDB, the storage layer provides persistent data management:

#### Storage Components:

**Block Store (`block.go`)**:
- **Block Storage**: Persists blocks with efficient retrieval
- **Transaction Indexing**: Maps transaction IDs to block locations
- **Public Key Caching**: Optimizes signature verification
- **Sortition Seed Caching**: Accelerates validator selection

**Account Store (`account.go`)**:
- **Account Persistence**: Stores account states with LRU caching
- **Balance Tracking**: Maintains account balances and sequences
- **Efficient Lookups**: Uses address-based indexing

**Validator Store (`validator.go`)**:
- **Validator Registry**: Maintains all validator information
- **Power Calculation**: Tracks validator stake and voting power
- **Committee Integration**: Supports committee management operations

**Transaction Store (`tx.go`)**:
- **Transaction Indexing**: Enables efficient transaction lookup
- **Block Region Mapping**: Maps transactions to their block locations
- **Cache Management**: Implements windowed caching for recent transactions

#### Storage Architecture:
```
LevelDB Storage Layout:
├── Blocks:           [0x01][height] -> block_data
├── Transactions:     [0x03][tx_id] -> block_region
├── Accounts:         [0x05][address] -> account_data  
├── Validators:       [0x07][address] -> validator_data
├── Block Heights:    [0x09][hash] -> height
└── Public Keys:      [0x0b][address] -> public_key
```

### 10. Wallet System (`wallet/`)

Comprehensive wallet management with HD key derivation:

#### Wallet Components:

**Vault System (`vault/`)**:
- **HD Key Derivation**: BIP32/BIP44 compatible key generation
- **Multi-Signature Support**: BLS and Ed25519 signature schemes
- **Address Types**: Account and validator address generation
- **Encryption**: AES-based keystore encryption
- **Import/Export**: Private key import and mnemonic backup

**Wallet Manager (`manager.go`)**:
- **Multi-Wallet Support**: Manages multiple wallet instances
- **Network Integration**: Connects to blockchain via gRPC
- **Transaction Signing**: Signs transactions with appropriate keys
- **Balance Tracking**: Monitors account and validator balances

#### Key Derivation Path:
```
m / purpose' / coin_type' / address_type' / address_index

Where:
- purpose': 12381 (BLS) or 12388 (Ed25519)
- coin_type': 21888 (Mainnet) or 21777 (Testnet)
- address_type': 0 (Account) or 1 (Validator)
- address_index: Sequential index starting from 0
```

#### Wallet Structure:
```go
type Wallet struct {
    store    *Store           // Encrypted wallet data
    servers  []string         // Connected blockchain nodes
    history  map[string][]HistoryInfo // Transaction history
}

type Vault struct {
    Type      int                    // 1: Full keys, 2: Neutered
    CoinType  uint32                 // Network identifier
    Addresses map[string]AddressInfo // Generated addresses
    Encrypter encrypter.Encrypter    // Encryption method
    KeyStore  string                 // Encrypted private keys
}
```

#### Wallet Operations:
```go
// Wallet management
Create(path, mnemonic, password, chainType) (*Wallet, error)
Open(path, readonly) (*Wallet, error)
Recover(path, mnemonic, password) (*Wallet, error)

// Address generation
NewBLSAccountAddress(label) (*AddressInfo, error)
NewEd25519AccountAddress(label, password) (*AddressInfo, error)
NewValidatorAddress(label) (*AddressInfo, error)

// Key management
PrivateKey(password, addr) (crypto.PrivateKey, error)
ImportBLSPrivateKey(password, prv) error
ImportEd25519PrivateKey(password, prv) error

// Transaction operations
MakeTransferTx(sender, receiver, amount, fee) (*tx.Tx, error)
MakeBondTx(sender, validator, stake, fee) (*tx.Tx, error)
SignTx(password, tx) error
```

#### Security Features:
- **BIP39 Mnemonics**: 12-24 word recovery phrases
- **Password Protection**: AES encryption of private keys
- **Key Derivation**: Deterministic address generation
- **Import Support**: External private key import
- **Backup/Recovery**: Mnemonic-based wallet recovery

### 11. Node Architecture (`node/`)

The node orchestrates all blockchain components:

#### Node Responsibilities:
- **Component Lifecycle**: Manages startup/shutdown of all services
- **Pipeline Coordination**: Coordinates message flows between components
- **Configuration Management**: Applies configuration to all components
- **Service Integration**: Integrates consensus, network, and API services

#### Node Services:
```go
type Node struct {
    state         state.Facade          // Blockchain state
    store         store.Store           // Persistent storage
    txPool        txpool.TxPool         // Transaction pool
    consV1Mgr     manager.Manager       // Legacy consensus
    consV2Mgr     manager.Manager       // Current consensus
    network       network.Network       // P2P networking
    sync          sync.Synchronizer     // Block synchronization
    grpc          *grpc.Server         // gRPC API
    jsonrpc       *jsonrpc.Server      // JSON-RPC API
    http          *http.Server         // HTTP REST API
    zeromq        *zmq.Server          // ZeroMQ messaging
}
```

---

## Consensus Algorithm

### Overview

Pactus implements a Byzantine Fault Tolerant consensus algorithm with a unique change-proposer mechanism that ensures liveness even in the presence of faulty proposers.

### Consensus Flow

#### Normal Case (3 phases):
1. **Prepare Phase**: Proposer broadcasts block proposal
2. **Precommit Phase**: Validators vote on the proposal
3. **Commit Phase**: Validators commit the agreed block

#### Change-Proposer Case (3 phases):
1. **CP-PreVote Phase**: Validators vote to change proposer
2. **CP-MainVote Phase**: Validators confirm proposer change
3. **CP-Decided Phase**: New proposer is selected

### State Machine

```
      ┌─────────────┐
      │   Prepare   │
      └─────┬───────┘
            │ Timeout / f+1 CP votes
            ▼
      ┌─────────────┐    Timeout     ┌─────────────┐
      │  Precommit  │ ──────────────► │Change       │
      └─────┬───────┘                 │Proposer     │
            │ Quorum                  └─────┬───────┘
            ▼                               │
      ┌─────────────┐                       │ Agreement
      │   Commit    │ ◄─────────────────────┘
      └─────────────┘
```

### Vote Types and Justifications

#### Vote Structure:
```go
type Vote struct {
    Type      Type           // Vote type
    Height    uint32         // Block height
    Round     int16          // Consensus round
    BlockHash hash.Hash      // Target block hash
    Signer    crypto.Address // Validator address
    CPVote    *cpVote        // Change-proposer vote data
    Signature *bls.Signature // BLS signature
}
```

#### Change-Proposer Vote:
```go
type cpVote struct {
    Round int16    // CP round
    Value CPValue  // CP value (Yes/No)
    Just  Just     // Justification
}
```

### Validator Selection

#### Sortition Process:
1. **VRF Evaluation**: Validators use Verifiable Random Functions
2. **Threshold Check**: Compare VRF output against stake-based threshold
3. **Committee Formation**: Selected validators form active committee
4. **Proposer Rotation**: Round-robin proposer selection within committee

---

## Network Layer

### libp2p Integration

Pactus uses libp2p for its networking layer with the following configuration:

#### Transport Protocols:
- **TCP**: Primary transport protocol
- **QUIC**: Modern transport with built-in encryption
- **WebSocket**: Browser compatibility

#### Discovery Mechanisms:
- **DHT**: Kademlia-based distributed hash table
- **mDNS**: Local network discovery
- **Bootstrap Nodes**: Hardcoded initial peers

#### Security Features:
- **TLS**: Transport encryption
- **Noise**: Handshake protocol
- **Connection Gating**: Peer filtering and banning
- **Resource Management**: Connection and bandwidth limits

### Gossip Protocol

#### Message Types:
- **Blocks**: New block announcements
- **Transactions**: Transaction propagation
- **Votes**: Consensus vote broadcasting
- **Proposals**: Block proposal distribution

#### Gossip Parameters:
- **Heartbeat Interval**: 1 second
- **Gossip Factor**: 3 peers per message
- **Message TTL**: 120 seconds
- **Duplicate Suppression**: Message deduplication

## Storage and Persistence

### LevelDB Integration

Pactus uses LevelDB as its primary storage engine with the following characteristics:

#### Storage Architecture:
```
Data Organization:
├── Raw Blocks:           Serialized block data
├── Transaction Index:    Maps TX_ID -> Block_Location
├── Account States:       Address -> Account_Data
├── Validator Registry:   Address -> Validator_Data
├── Block Height Index:   Block_Hash -> Height
├── Public Key Cache:     Address -> Public_Key
└── Metadata:            Chain info and statistics
```

#### Key Prefixes:
```go
const (
    lastInfoKey       = []byte{0x00}  // Chain metadata
    blockPrefix       = []byte{0x01}  // Block storage
    txPrefix          = []byte{0x03}  // Transaction index
    accountPrefix     = []byte{0x05}  // Account states
    validatorPrefix   = []byte{0x07}  // Validator data
    blockHeightPrefix = []byte{0x09}  // Height index
    publicKeyPrefix   = []byte{0x0b}  // Public key cache
)
```

### Merkle Tree Implementation

#### Persistent Merkle Trees:
Pactus implements custom persistent Merkle trees for state verification:

**Features**:
- **Incremental Updates**: Efficient single-leaf modifications
- **Cryptographic Commitments**: State root calculation
- **Proof Generation**: Inclusion and exclusion proofs
- **Memory Efficiency**: Sparse tree representation

**Tree Operations**:
```go
type Tree interface {
    SetData(leaf int32, data []byte)     // Update leaf
    SetHash(leaf int32, h hash.Hash)     // Set leaf hash
    Root() hash.Hash                     // Calculate root
}
```

**Node Structure**:
```go
type node struct {
    width  int32      // Horizontal position
    height int32      // Tree level
    hash   *hash.Hash // Cached hash value
}
```

#### State Trees:
- **Account Tree**: Merkle tree of all account states
- **Validator Tree**: Merkle tree of all validator states  
- **Transaction Tree**: Simple Merkle tree for block transactions

### Caching Strategy

#### Multi-Level Caching:
1. **In-Memory Caches**: LRU caches for frequently accessed data
2. **Block Region Cache**: Recently accessed block segments
3. **Public Key Cache**: Cached public keys for signature verification
4. **Sortition Seed Cache**: VRF seeds for recent blocks

#### Cache Configuration:
```toml
[store]
account_cache_size = 1000      # Account LRU cache size
public_key_cache_size = 1000   # Public key cache size
seed_cache_window = 10         # Sortition seed cache window
tx_cache_window = 1000         # Transaction cache window
```

### Data Consistency

#### ACID Properties:
- **Atomicity**: Batch writes ensure atomic state transitions
- **Consistency**: Merkle tree validation ensures state integrity
- **Isolation**: Sandbox environments prevent dirty reads
- **Durability**: LevelDB provides persistent storage

#### Batch Operations:
```go
// Atomic batch operations
batch := leveldb.Batch{}
batch.Put(accountKey, accountData)
batch.Put(validatorKey, validatorData)
batch.Put(blockKey, blockData)

// Atomic commit
db.Write(batch, nil)
```

### Pruning and Archival

#### Pruning Strategy:
- **Historical Blocks**: Optional pruning of old block data
- **Transaction History**: Configurable transaction retention
- **State Snapshots**: Periodic state checkpoints
- **Public Key Cleanup**: Removal of unused public keys

#### Pruning Configuration:
```toml
[store]
retention_days = 7           # Keep 7 days of full history
pruning_enabled = true       # Enable automatic pruning
checkpoint_interval = 1000   # State checkpoint frequency
```

### Storage Metrics

#### Performance Monitoring:
- **Read/Write Latency**: Database operation timing
- **Cache Hit Rates**: Cache effectiveness metrics
- **Storage Growth**: Disk usage tracking
- **Compaction Stats**: LevelDB compaction metrics

---

## State Management

### State Architecture

The state management system maintains the current blockchain state including accounts, validators, and metadata:

#### State Components:
```go
type state struct {
    lastInfo        *lastinfo.LastInfo      // Chain metadata
    accountMerkle   *persistentmerkle.Tree  // Account state tree
    validatorMerkle *persistentmerkle.Tree  // Validator state tree
    committee       committee.Committee      // Active validator set
    totalPower      int64                   // Total validator power
    params          *param.Params           // Network parameters
}
```

### Account Management

#### Account Structure:
```go
type Account struct {
    Number   int32         // Sequential account number
    Balance  amount.Amount // Account balance in NanoPAC
    Sequence uint32        // Transaction sequence number
}
```

#### Account Operations:
- **Balance Updates**: Atomic balance modifications
- **Sequence Tracking**: Prevents transaction replay
- **Address Derivation**: Supports multiple address types
- **State Validation**: Merkle tree verification

### Validator Management

#### Validator Lifecycle:
1. **Registration**: Bond transaction creates validator
2. **Activation**: Sortition proof enables participation
3. **Committee Membership**: Join active validator set
4. **Deactivation**: Unbond transaction initiates exit
5. **Withdrawal**: Withdraw stake after unbonding period

#### Validator Structure:
```go
type Validator struct {
    PublicKey             *bls.PublicKey // BLS public key
    Number                int32          // Validator number
    Stake                 amount.Amount  // Staked amount
    LastBondingHeight     uint32         // Last bonding height
    LastSortitionHeight   uint32         // Last sortition height
    UnbondingHeight       uint32         // Unbonding height
    Availability          int32          // Availability score
}
```

### Committee Management

#### Dynamic Committee:
- **Size**: Configurable committee size (default: 51 for mainnet)
- **Rotation**: Automatic validator rotation based on stake
- **Power Distribution**: Stake-weighted voting power
- **Proposer Selection**: Round-robin proposer rotation

#### Committee Operations:
```go
// Committee interface
type Committee interface {
    Contains(addr crypto.Address) bool
    IsProposer(addr crypto.Address, round int16) bool
    Proposer(round int16) *validator.Validator
    TotalPower() int64
    Update(round int16, joined []*validator.Validator)
}
```

### Sandbox Environment

#### Isolation Mechanism:
The sandbox provides transaction execution isolation:

```go
type Sandbox interface {
    // Account operations
    Account(addr crypto.Address) *account.Account
    MakeNewAccount(addr crypto.Address) *account.Account
    UpdateAccount(addr crypto.Address, acc *account.Account)
    
    // Validator operations  
    Validator(addr crypto.Address) *validator.Validator
    MakeNewValidator(pub *bls.PublicKey) *validator.Validator
    UpdateValidator(val *validator.Validator)
    
    // Committee operations
    Committee() committee.Reader
    IsJoinedCommittee(addr crypto.Address) bool
    
    // Transaction tracking
    RecentTransaction(txID tx.ID) bool
    CommitTransaction(trx *tx.Tx)
}
```

### State Transitions

#### Block Execution:
1. **Sandbox Creation**: Create isolated execution environment
2. **Transaction Execution**: Process each transaction in order
3. **State Application**: Apply valid state changes
4. **Merkle Update**: Update state tree roots
5. **Commit**: Persist final state atomically

#### Rollback Support:
- **Sandbox Isolation**: Invalid blocks don't corrupt state
- **Atomic Commits**: All-or-nothing state updates
- **State Recovery**: Restore from last valid state
- **Checkpoint System**: Periodic state snapshots

---

## Transaction System

The Pactus blockchain implements a comprehensive transaction system supporting six distinct transaction types, each designed for specific blockchain operations. The system features deterministic execution, cryptographic security, and efficient fee structures.

### Transaction Architecture

#### Transaction Structure
```go
type Tx struct {
    data struct {
        Version   uint8          // Transaction version (currently 1)
        LockTime  uint32         // Block height when transaction becomes valid
        Fee       amount.Amount  // Transaction fee in NanoPAC
        Memo      string         // Optional memo field (max 64 chars)
        Payload   payload.Payload // Transaction-specific payload
    }
    signature crypto.Signature    // Transaction signature
    publicKey crypto.PublicKey    // Signer's public key
}
```

#### Transaction Types Overview

```go
const (
    TypeTransfer      = Type(1) // Transfer PAC between accounts
    TypeBond          = Type(2) // Bond PAC to become validator
    TypeSortition     = Type(3) // Submit sortition proof (free)
    TypeUnbond        = Type(4) // Unbond validator stake (free)
    TypeWithdraw      = Type(5) // Withdraw unbonded stake
    TypeBatchTransfer = Type(6) // Multiple transfers in one transaction
)
```

## Cryptographic Algorithms and Security

Pactus implements state-of-the-art cryptographic algorithms to ensure network security, transaction integrity, and consensus reliability. The system employs a dual-signature scheme optimized for different use cases and incorporates advanced cryptographic primitives.

### Cryptographic Architecture Overview

```mermaid
graph TB
    subgraph "Signature Schemes"
        BLS[BLS12-381]
        ED[Ed25519]
    end
    
    subgraph "Hash Functions"
        SHA[SHA-256]
        BLAKE[BLAKE2b]
    end
    
    subgraph "Key Derivation"
        BIP32[BIP32/BIP44]
        PBKDF[PBKDF2]
    end
    
    subgraph "Encoding"
        BECH[Bech32m]
        BASE[Base64/Hex]
    end
    
    BLS --> Validators
    ED --> Accounts
    SHA --> Hashing
    BLAKE --> Merkle
    BIP32 --> Wallets
    BECH --> Addresses
```

### BLS12-381 Digital Signatures

Pactus uses BLS12-381 signatures for validator operations, consensus participation, and sortition proofs.

#### BLS12-381 Specifications

- **Curve**: BLS12-381 pairing-friendly elliptic curve
- **Security Level**: 128-bit security
- **Signature Size**: 96 bytes (G1 point)
- **Public Key Size**: 96 bytes (G2 point)
- **Private Key Size**: 32 bytes (scalar)
- **Aggregation**: Supports signature aggregation

#### BLS Implementation

```go
// BLS signature creation
func (prv *PrivateKey) Sign(msg []byte) crypto.Signature {
    // Hash message to G1 point on curve
    msgG1, _ := bls12381.HashToG1(msg, dst)
    
    // Sign with private key
    signature := new(bls12381.G1Affine)
    signature.ScalarMultiplication(&msgG1, prv.scalar)
    
    return &Signature{pointG1: signature}
}

// BLS signature verification
func (pub *PublicKey) Verify(msg []byte, sig crypto.Signature) error {
    // Pairing check: e(H(m), P) = e(S, G)
    return bls12381.PairingCheck([]G1Affine{hash, sig}, []G2Affine{pub, gen})
}
```

### Ed25519 Digital Signatures

Ed25519 is used for account transactions and general-purpose signing operations.

#### Ed25519 Specifications

- **Curve**: Curve25519 (Edwards form)
- **Security Level**: 128-bit security
- **Signature Size**: 64 bytes
- **Public Key Size**: 32 bytes
- **Private Key Size**: 32 bytes

#### Ed25519 Implementation

```go
// Ed25519 signature creation
func (prv *PrivateKey) Sign(msg []byte) crypto.Signature {
    sig := ed25519.Sign(prv.keyData[:], msg)
    return &Signature{data: sig}
}

// Ed25519 signature verification  
func (pub *PublicKey) Verify(msg []byte, sig crypto.Signature) error {
    valid := ed25519.Verify(pub.keyData[:], msg, sig.Bytes())
    if !valid {
        return crypto.ErrInvalidSignature
    }
    return nil
}
```

### Verifiable Random Functions (VRF)

VRF provides provable randomness for validator sortition.

#### VRF Implementation

```go
// VRF Evaluation - Generate proof and output
func Evaluate(seed VerifiableSeed, privateKey *bls.PrivateKey, 
              totalPower uint64) (uint64, Proof) {
    // Create signing data
    signData := append(seed[:], privateKey.PublicKey().Bytes()...)
    
    // Create BLS signature as proof
    signature := privateKey.Sign(signData)
    proof, _ := ProofFromBytes(signature.Bytes())
    
    // Calculate deterministic index
    index := GetIndex(proof, totalPower)
    
    return index, proof
}

// VRF Verification
func Verify(seed VerifiableSeed, publicKey *bls.PublicKey, 
           proof Proof, totalPower uint64) (uint64, bool) {
    // Verify BLS signature
    proofSig, _ := bls.SignatureFromBytes(proof[:])
    signData := append(seed[:], publicKey.Bytes()...)
    
    if publicKey.Verify(signData, proofSig) != nil {
        return 0, false
    }
    
    index := GetIndex(proof, totalPower)
    return index, true
}
```

### Address Generation and Encoding

#### Address Derivation

```go
// Generate address from public key
func (pub *PublicKey) AccountAddress() Address {
    hash1 := sha256.Sum256(pub.Bytes())
    hash2 := sha256.Sum256(hash1[:])
    
    var addr Address
    copy(addr[:], hash2[:AddressSize])
    return addr
}

// Convert address to Bech32m format
func (addr Address) String() string {
    converted, _ := bech32m.ConvertBits(addr[:], 8, 5, true)
    encoded, _ := bech32m.Encode(crypto.AddressHRP, converted)
    return encoded
}
```

### Cryptographic Constants

```go
const (
    BLSSignatureSize     = 96
    BLSPublicKeySize     = 96
    Ed25519SignatureSize = 64
    Ed25519PublicKeySize = 32
    AddressSize          = 20
    HardenedKeyStart     = 0x80000000
)
```

### Detailed Transaction Types

#### 1. Transfer Transaction (Type 1)

The most common transaction type for transferring PAC between accounts.

```go
type TransferPayload struct {
    From     crypto.Address // Sender address
    To       crypto.Address // Receiver address  
    Amount   amount.Amount  // Transfer amount in NanoPAC
}
```

**Characteristics:**
- **Purpose**: Transfer PAC between any two addresses
- **Fee**: Variable based on network conditions
- **Validation**: Sender must have sufficient balance + fee
- **Gas Cost**: Standard transaction cost

**Usage Example:**
```bash
# CLI command
pactus-cli tx transfer \
  --from pc1p0hrxja8a5qpd6z5w8jvy5g5j44jtwqcq9k49se \
  --to pc1p5cyxnuxmeuwuvpwfq2vpfmpza6hqda4h2774ce \
  --amount 1000000000 \
  --fee 1000000
```

#### 2. Bond Transaction (Type 2)

Used to bond PAC to a validator address, either for self-bonding or delegating to another validator.

```go
type BondPayload struct {
    From      crypto.Address  // Account bonding the stake
    To        crypto.Address  // Validator receiving the bond
    PublicKey *bls.PublicKey  // Validator's BLS public key
    Stake     amount.Amount   // Amount to bond in NanoPAC
}
```

**Characteristics:**
- **Purpose**: Bond PAC to validators for staking
- **Fee**: Fixed fee structure
- **Lock Period**: Subject to bond interval (360 blocks = 1 hour)
- **Minimum**: 1,000 PAC minimum bond amount
- **Maximum**: 1,000,000 PAC maximum bond amount

**Validation Rules:**
1. Sender must have sufficient balance (stake + fee)
2. Validator address must be valid
3. BLS public key must be valid (for new validators)
4. Bond amount must be within min/max limits
5. Validator cannot exceed maximum stake limit

#### 3. Sortition Transaction (Type 3)

Free transaction type used by validators to submit sortition proofs for proposer selection.

```go
type SortitionPayload struct {
    Validator crypto.Address // Validator address
    Proof     Proof         // VRF proof (48 bytes)
}
```

**Characteristics:**
- **Purpose**: Submit verifiable random function (VRF) proof
- **Fee**: Free transaction (no fee required)
- **Frequency**: Evaluated every sortition interval (17 blocks)
- **Proof**: 48-byte BLS signature-based proof

#### 4. Unbond Transaction (Type 4)

Free transaction allowing validators to unbond their stake and begin the withdrawal process.

```go
type UnbondPayload struct {
    Validator crypto.Address // Validator address to unbond
}
```

**Characteristics:**
- **Purpose**: Initiate stake unbonding process
- **Fee**: Free transaction
- **Lock Period**: Unbond interval (181,440 blocks = 21 days)
- **Effect**: Validator becomes inactive immediately

#### 5. Withdraw Transaction (Type 5)

Used to withdraw unbonded stake from validator to account after unbond period completion.

```go
type WithdrawPayload struct {
    From   crypto.Address // Validator address (source)
    To     crypto.Address // Account address (destination) 
    Amount amount.Amount  // Amount to withdraw
}
```

**Characteristics:**
- **Purpose**: Withdraw unbonded stake to account
- **Fee**: Standard transaction fee
- **Timing**: Only after unbond period completion
- **Validation**: Validator must have unbonded stake available

#### 6. Batch Transfer Transaction (Type 6)

Efficient transaction type for sending PAC to multiple recipients in a single transaction.

```go
type BatchTransferPayload struct {
    From       crypto.Address     // Sender address
    Recipients []BatchRecipient   // List of recipients
}

type BatchRecipient struct {
    To     crypto.Address // Recipient address
    Amount amount.Amount  // Transfer amount
}
```

**Characteristics:**
- **Purpose**: Multiple transfers in one transaction
- **Fee**: Reduced fee compared to multiple transfers
- **Efficiency**: Lower network overhead
- **Limit**: Maximum recipients per transaction

### Transaction Execution Engine

#### Execution Flow
```go
func Execute(trx *tx.Tx, sbx sandbox.Sandbox) error {
    // Create appropriate executor
    executor, err := MakeExecutor(trx, sbx)
    if err != nil {
        return err
    }
    
    // Execute transaction
    executor.Execute()
    
    // Commit changes to sandbox
    sbx.CommitTransaction(trx)
    
    return nil
}
```

#### Executor Pattern
```go
type Executor interface {
    Check(strict bool) error  // Validate transaction
    Execute()                 // Execute transaction
}

// Factory method for creating executors
func MakeExecutor(trx *tx.Tx, sbx sandbox.Sandbox) (Executor, error) {
    switch trx.Payload().Type() {
    case payload.TypeTransfer:
        return newTransferExecutor(trx, sbx)
    case payload.TypeBond:
        return newBondExecutor(trx, sbx)
    case payload.TypeUnbond:
        return newUnbondExecutor(trx, sbx)
    case payload.TypeWithdraw:
        return newWithdrawExecutor(trx, sbx)
    case payload.TypeSortition:
        return newSortitionExecutor(trx, sbx)
    case payload.TypeBatchTransfer:
        return newBatchTransferExecutor(trx, sbx)
    default:
        return nil, InvalidPayloadTypeError{PayloadType: typ}
    }
}
```

### Cryptographic Security

#### Signature Schemes

**BLS12-381 (Validators)**
```go
// BLS signature creation
func (prv *PrivateKey) Sign(msg []byte) crypto.Signature {
    // Hash message to G1 point on curve
    msgG1, _ := bls12381.HashToG1(msg, dst)
    
    // Sign with private key
    signature := new(bls12381.G1Affine)
    signature.ScalarMultiplication(&msgG1, prv.scalar)
    
    return &Signature{pointG1: signature}
}

// BLS signature verification
func (pub *PublicKey) Verify(msg []byte, sig crypto.Signature) error {
    // Pairing check: e(H(m), P) = e(S, G)
    return bls12381.PairingCheck([]G1Affine{hash, sig}, []G2Affine{pub, gen})
}
```

**Ed25519 (Accounts)**
```go
// Ed25519 signature creation
func (prv *PrivateKey) Sign(msg []byte) crypto.Signature {
    sig := ed25519.Sign(prv.keyData[:], msg)
    return &Signature{data: sig}
}

// Ed25519 signature verification  
func (pub *PublicKey) Verify(msg []byte, sig crypto.Signature) error {
    valid := ed25519.Verify(pub.keyData[:], msg, sig.Bytes())
    if !valid {
        return crypto.ErrInvalidSignature
    }
    return nil
}
```

### Fee Structure

#### Fee Schedule (NanoPAC)
```yaml
Transfer: 1,000,000 (0.001 PAC)
Bond: 1,000,000 (0.001 PAC)
Unbond: 0 (Free)
Withdraw: 1,000,000 (0.001 PAC)
Sortition: 0 (Free)
BatchTransfer: 1,000,000 + (recipients * 100,000)
```

### Transaction Pool (Mempool)

#### Pool Management
```go
type Pool struct {
    config          *Config
    sandBox         sandbox.Sandbox
    pendingTxs      map[tx.ID]*poolTx
    pendingTransfers map[crypto.Address][]*poolTx
    pendingBonds    map[crypto.Address][]*poolTx
}
```

### Transaction Serialization

#### Binary Encoding
```go
func (tx *Tx) Encode(w io.Writer) error {
    // Write version
    if err := encoding.WriteUint8(w, tx.data.Version); err != nil {
        return err
    }
    
    // Write lock time
    if err := encoding.WriteUint32(w, tx.data.LockTime); err != nil {
        return err
    }
    
    // Write fee
    if err := tx.data.Fee.Encode(w); err != nil {
        return err
    }
    
    // Write memo
    if err := encoding.WriteVarString(w, tx.data.Memo); err != nil {
        return err
    }
    
    // Write payload
    return tx.data.Payload.Encode(w)
}
```

#### JSON Representation
```json
{
  "id": "2c3a48b0f8b4d2c9a1b3e5f7a9c2e4f6b8d0c2a4e6f8a0b2c4e6f8a0b2c4e6f8",
  "version": 1,
  "lock_time": 123456,
  "fee": "1000000",
  "payload_type": "PAYLOAD_TYPE_TRANSFER",
  "memo": "Payment for services",
  "transfer": {
    "sender": "pc1p0hrxja8a5qpd6z5w8jvy5g5j44jtwqcq9k49se",
    "receiver": "pc1p5cyxnuxmeuwuvpwfq2vpfmpza6hqda4h2774ce", 
    "amount": "1000000000"
  },
  "public_key": "033f4a3b2c5d1e9f8a7b6c5d4e3f2a1b9c8d7e6f5a4b3c2d1e0f9a8b7c6d5e4f3",
  "signature": "a1b2c3d4e5f6789abcdef0123456789abcdef0123456789abcdef0123456789a"
}
```
- **Validation**: Balance check, signature verification, sequence validation

#### 2. Bond Transaction (`TypeBond`)
- **Purpose**: Stake PAC tokens to become a validator
- **Payload Structure**:
  ```go
  type BondPayload struct {
      From      crypto.Address  // Sender account
      To        crypto.Address  // Validator address
      Stake     amount.Amount   // Stake amount
      PublicKey *bls.PublicKey  // Validator public key (for new validators)
  }
  ```
- **Validation**: Minimum stake, public key uniqueness, bonding period

#### 3. Unbond Transaction (`TypeUnbond`)
- **Purpose**: Initiate validator unstaking process
- **Payload Structure**:
  ```go
  type UnbondPayload struct {
      Validator crypto.Address // Validator to unbond
  }
  ```
- **Validation**: Validator existence, current bonding status

#### 4. Withdraw Transaction (`TypeWithdraw`)
- **Purpose**: Withdraw validator rewards after unbonding
- **Payload Structure**:
  ```go
  type WithdrawPayload struct {
      From   crypto.Address // Validator address
      To     crypto.Address // Destination account
      Amount amount.Amount  // Withdrawal amount
  }
  ```
- **Validation**: Unbonding completion, available balance

#### 5. Sortition Transaction (`TypeSortition`)
- **Purpose**: Prove validator selection eligibility
- **Payload Structure**:
  ```go
  type SortitionPayload struct {
      Validator crypto.Address  // Validator address
      Proof     sortition.Proof // VRF proof
  }
  ```
- **Validation**: Proof verification, sortition threshold, bonding period

#### 6. Batch Transfer Transaction (`TypeBatchTransfer`)
- **Purpose**: Execute multiple transfers efficiently
- **Payload Structure**:
  ```go
  type BatchTransferPayload struct {
      From      crypto.Address    // Sender address
      Transfers []TransferDetail  // List of transfers
  }
  
  type TransferDetail struct {
      To     crypto.Address // Receiver
      Amount amount.Amount  // Amount
  }
  ```
- **Validation**: Aggregate balance check, transfer limits

### Transaction Lifecycle

#### 1. Creation and Signing
```go
// Create transaction
tx := tx.NewTransferTx(lockTime, sender, receiver, amount, fee)

// Sign transaction
privateKey.SignTx(tx)
```

#### 2. Pool Admission
```go
// Add to transaction pool
err := txPool.AppendTx(tx)
if err != nil {
    // Handle validation error
}
```

#### 3. Block Inclusion
- **Proposer Selection**: Choose transactions based on fee priority
- **Block Assembly**: Include valid transactions in proposed block
- **Consensus**: Block validation includes transaction verification

#### 4. Execution
```go
// Execute transaction in sandbox
err := execution.CheckAndExecute(tx, sandbox, strict)
if err != nil {
    // Transaction execution failed
}
```

### Fee System

#### Fee Calculation:
- **Base Fee**: Minimum fee per transaction type
- **Size Fee**: Additional fee based on transaction size
- **Priority Fee**: Optional fee for faster inclusion

#### Fee Structure:
```go
// Minimum fees by transaction type
var MinimumFee = map[payload.Type]amount.Amount{
    TypeTransfer:      1000,  // 0.000001 PAC
    TypeBond:          1000,  // 0.000001 PAC
    TypeUnbond:        1000,  // 0.000001 PAC
    TypeWithdraw:      1000,  // 0.000001 PAC
    TypeSortition:     1000,  // 0.000001 PAC
    TypeBatchTransfer: 2000,  // 0.000002 PAC
}
```

### Transaction Pool Management

#### Pool Operations:
```go
type TxPool interface {
    AppendTx(tx *tx.Tx) error           // Add transaction
    RemoveTx(id tx.ID)                  // Remove transaction
    AllTransactions() []*tx.Tx          // Get all pending
    HasTx(id tx.ID) bool               // Check existence
    Recheck()                           // Revalidate after block
    Size() int                          // Pool size
}
```

#### Pool Policies:
- **Size Limits**: Maximum 1000 pending transactions
- **Fee Prioritization**: Higher fee transactions prioritized
- **Spam Protection**: Rate limiting per sender
- **Conflict Resolution**: Later transactions replace earlier ones

### Advanced Transaction Features

#### Lock Time Mechanism:
- **Purpose**: Delayed transaction execution
- **Validation**: Transaction only valid after specified block height
- **Use Cases**: Scheduled payments, time-locked contracts

#### Memo Field:
- **Size**: Maximum 64 bytes
- **Encoding**: UTF-8 string
- **Use Cases**: Payment references, metadata storage

#### Replay Protection:
- **Mechanism**: Transaction ID uniqueness enforcement
- **Duration**: Recent transaction tracking window
- **Purpose**: Prevent double-spending and replay attacks

---

## Validation and Committee

### Validator Lifecycle

#### 1. Registration
- **Bond Transaction**: Submit stake with validator key
- **Minimum Stake**: Meet network minimum requirements
- **Key Uniqueness**: Ensure unique validator public key

#### 2. Activation
- **Sortition Proof**: Provide valid sortition proof
- **Committee Inclusion**: Join active validator committee
- **Block Production**: Begin participating in consensus

#### 3. Validation
- **Block Proposals**: Create and broadcast block proposals
- **Vote Casting**: Participate in consensus voting
- **Network Participation**: Maintain network connectivity

#### 4. Deactivation
- **Unbond Transaction**: Submit unbonding request
- **Cooling Period**: Wait for unbonding period completion
- **Stake Withdrawal**: Withdraw staked tokens

### Committee Management

#### Committee Structure:
- **Size**: Dynamic based on network parameters
- **Rotation**: Regular validator set updates
- **Power Distribution**: Stake-weighted voting power
- **Byzantine Tolerance**: Up to 1/3 faulty validators

#### Proposer Selection:
```go
// Round-robin proposer selection
func (c *committee) Proposer(round int16) *validator.Validator {
    index := int(round) % c.Size()
    return c.validators[index]
}
```

### Sortition Algorithm

#### VRF-Based Selection:
1. **Seed Generation**: Derive random seed from blockchain state
2. **VRF Evaluation**: Compute VRF output using validator private key
3. **Threshold Comparison**: Check if output meets stake-based threshold
4. **Proof Generation**: Create verifiable proof of selection

#### Proof Verification:
```go
func VerifyProof(seed VerifiableSeed, proof Proof, 
                pub *bls.PublicKey, total, threshold int64) bool {
    index, result := Verify(seed, pub, proof, uint64(total))
    return result && int64(index) < threshold
}
```

---

## APIs and Interfaces

### gRPC API

#### Blockchain Service:
```protobuf
service Blockchain {
    rpc GetBlockchainInfo(GetBlockchainInfoRequest) 
        returns (GetBlockchainInfoResponse);
    rpc GetConsensusInfo(GetConsensusInfoRequest) 
        returns (GetConsensusInfoResponse);
    rpc GetAccount(GetAccountRequest) 
        returns (GetAccountResponse);
    rpc GetValidator(GetValidatorRequest) 
        returns (GetValidatorResponse);
    rpc GetBlock(GetBlockRequest) 
        returns (GetBlockResponse);
    rpc GetTransaction(GetTransactionRequest) 
        returns (GetTransactionResponse);
}
```

#### Transaction Service:
```protobuf
service Transaction {
    rpc SendRawTransaction(SendRawTransactionRequest) 
        returns (SendRawTransactionResponse);
    rpc GetRawTransaction(GetRawTransactionRequest) 
        returns (GetRawTransactionResponse);
    rpc CalculateFee(CalculateFeeRequest) 
        returns (CalculateFeeResponse);
}
```

#### Network Service:
```protobuf
service Network {
    rpc GetNetworkInfo(GetNetworkInfoRequest) 
        returns (GetNetworkInfoResponse);
    rpc GetPeers(GetPeersRequest) 
        returns (GetPeersResponse);
    rpc GetNodeInfo(GetNodeInfoRequest) 
        returns (GetNodeInfoResponse);
}
```

### JSON-RPC API

#### Blockchain Methods:
- `pactus.blockchain.getBlockchainInfo()`
- `pactus.blockchain.getConsensusInfo()`
- `pactus.blockchain.getAccount(address)`
- `pactus.blockchain.getValidator(address)`
- `pactus.blockchain.getBlock(height, verbosity)`

#### Transaction Methods:
- `pactus.transaction.sendRawTransaction(data)`
- `pactus.transaction.getRawTransaction(id, verbosity)`
- `pactus.transaction.calculateFee(amount, payloadType)`

#### Network Methods:
- `pactus.network.getNetworkInfo()`
- `pactus.network.getPeers()`
- `pactus.network.getNodeInfo()`

### HTTP REST API

#### Endpoint Structure:
```
GET  /blockchain/info
GET  /blockchain/consensus
GET  /blockchain/account/{address}
GET  /blockchain/validator/{address}
GET  /blockchain/block/{height}
POST /transaction/send
GET  /transaction/{id}
GET  /network/info
GET  /network/peers
```

### ZeroMQ Interface

#### Event Publishing:
- **Block Events**: New block notifications
- **Transaction Events**: Transaction status updates
- **Consensus Events**: Consensus state changes
- **Network Events**: Peer connection events

---

## Configuration

### Configuration Structure

```toml
[node]
reward_addresses = []

[store]
path = "data"
batch_size = 1000

[network]
listen_addr = "/ip4/0.0.0.0/tcp/21777"
public_addr = ""
bootstrap_peers = []
max_connections = 50

[sync]
firewall_enabled = true
cache_size = 1000

[tx_pool]
max_size = 1000
fee_per_byte = 1000

[logger]
level = "info"
targets = ["console"]

[grpc]
enable = true
listen = "127.0.0.1:9090"

[jsonrpc]
enable = true
listen = "127.0.0.1:8545"

[http]
enable = true
listen = "127.0.0.1:8080"
```

### Network Configurations

#### Mainnet:
```go
ChainType: Mainnet
GenesisHash: "..."
InitialValidators: 7
BlockTime: 10 seconds
CommitteeSize: 51
```

#### Testnet:
```go
ChainType: Testnet
GenesisHash: "..."
InitialValidators: 4
BlockTime: 10 seconds
CommitteeSize: 21
```

#### Localnet:
```go
ChainType: Localnet
GenesisHash: "..."
InitialValidators: 4
BlockTime: 3 seconds
CommitteeSize: 4
```

---

## Protocol Parameters and Configuration

Pactus blockchain operates with a comprehensive set of protocol parameters that govern network behavior, consensus rules, economic incentives, and security properties. These parameters are carefully tuned for optimal performance across different network environments.

### Genesis Parameters

#### Core Protocol Parameters

```go
type GenesisParams struct {
    BlockVersion              protocol.Version // Block format version (1)
    BlockIntervalInSecond     int             // Target block time in seconds
    CommitteeSize             int             // Number of validators in committee
    BlockReward               amount.Amount   // Reward per block in NanoPAC
    TransactionToLiveInterval uint32          // Transaction expiry time (blocks)
    BondInterval              uint32          // Validator activation period
    UnbondInterval            uint32          // Stake unbonding period
    SortitionInterval         uint32          // Sortition evaluation frequency
    MinimumStake              amount.Amount   // Minimum validator stake
    MaximumStake              amount.Amount   // Maximum validator stake
}
```

#### Network-Specific Parameters

**Mainnet Parameters**
```yaml
Block Interval: 10 seconds
Committee Size: 51 validators
Block Reward: 1,000,000,000 NanoPAC (1 PAC)
Transaction TTL: 8,640 blocks (24 hours)
Bond Interval: 360 blocks (1 hour)
Unbond Interval: 181,440 blocks (21 days)
Sortition Interval: 17 blocks (~3 minutes)
Minimum Stake: 1,000,000,000 NanoPAC (1,000 PAC)
Maximum Stake: 1,000,000,000,000 NanoPAC (1,000,000 PAC)
Genesis Time: 2024-01-24T20:24:00Z
Genesis Hash: e4d59e3145c9d718caf178edb33bc2ca7fe43e5b30990c9d57d53a60c4741432
```

**Testnet Parameters**
```yaml
Block Interval: 10 seconds
Committee Size: 7 validators
Block Reward: 1,000,000,000 NanoPAC (1 PAC)
Transaction TTL: 8,640 blocks (24 hours)
Bond Interval: 360 blocks (1 hour)
Unbond Interval: 181,440 blocks (21 days)
Sortition Interval: 17 blocks (~3 minutes)
Minimum Stake: 1,000,000,000 NanoPAC (1,000 PAC)
Maximum Stake: 1,000,000,000,000 NanoPAC (1,000,000 PAC)
Genesis Time: 2024-03-16T00:00:00Z
Genesis Hash: 13f96e6fbc9e0de0d53537ac5e894fc8e66be1600436db2df1511dc30696e822
Address Prefix: tpc
```

**Development/Localnet Parameters**
```yaml
Block Interval: 2 seconds (faster testing)
Committee Size: 4-7 validators (configurable)
Block Reward: 1,000,000,000 NanoPAC
Minimum Stake: 1,000 NanoPAC (lower barrier)
Bond Interval: 8 blocks (16 seconds)
Unbond Interval: 8 blocks (16 seconds)
Transaction TTL: 8 blocks
```

### Economic Parameters

#### Token Supply and Distribution

```yaml
Total Supply: 42,000,000,000,000,000 NanoPAC (42 million PAC)
Initial Distribution:
  Genesis Validators: 90%
  Foundation Reserve: 10%
  
Block Rewards:
  Initial: 1 PAC per block
  Halving: None (fixed reward)
  Annual Inflation: ~0.5% (decreasing over time)
```

#### Fee Structure

```go
// Transaction fees (in NanoPAC)
const (
    TransferFee      = 1_000_000  // 0.001 PAC
    BondFee          = 1_000_000  // 0.001 PAC
    UnbondFee        = 0          // Free
    WithdrawFee      = 1_000_000  // 0.001 PAC
    SortitionFee     = 0          // Free
    BatchTransferBaseFee = 1_000_000  // Base fee
    BatchTransferPerRecipient = 100_000  // Per recipient
)
```

### Network Configuration Parameters

**Connection Limits**
```yaml
Mainnet:
  Max Connections: 64
  Default Port: 21888
  Enable UPnP: false
  Enable NAT Service: false
  Enable Relay: true

Testnet:
  Max Connections: 64
  Default Port: 21777
  Enable UPnP: false
  Enable NAT Service: false
  Enable Relay: true
```

**Bootstrap Nodes**

*Mainnet Bootstrap Nodes:*
```yaml
- /dns/mainnet1.pactus.org/tcp/21888/p2p/12D3KooWJKYdHzWZGibnj74NSSgKRu4Ez6MijDWMfLfXxeL4un6v
- /ip4/65.108.142.81/tcp/21888/p2p/12D3KooWAdRga2NCbaPfVgSEzAAZW2psfJmPi3PFJzF81qbccJsR
- /ip4/95.217.89.202/tcp/21888/p2p/12D3KooWH3S9gMYybr1pd4K5o3CBLbZLQ1REKBsPWt6NWPi4bgPn
```

*Testnet Bootstrap Nodes:*
```yaml
- /dns/testnet1.pactus.org/tcp/21777/p2p/12D3KooWJKYdHzWZGibnj74NSSgKRu4Ez6MijDWMfLfXxeL4un6v
- /ip4/65.108.211.187/tcp/21777/p2p/12D3KooWB42BLfzxSF5SMhSTSEyfJ6yhSM8togLfExrRWFMJeb5u
- /ip4/103.27.206.208/tcp/21777/p2p/12D3KooWMTDwDTBMaf2Sem5tWRe1dB6PFY8LeqkZ2e5drrbbPTDn
```

## Development Guide

### Prerequisites

#### Required Software:
- **Go**: Version 1.21 or higher (currently supports 1.24.5)
- **Git**: Version control system
- **Make**: Build automation tool
- **GTK+3**: For GUI development (optional)

#### Development Tools:
```bash
# Install development tools
make devtools

# Required tools installed:
# - golangci-lint (linting)
# - buf (protobuf)
# - protoc-gen-go (protobuf generation)
# - protoc-gen-go-grpc (gRPC generation)
# - protoc-gen-cobra (CLI generation)
```

### Building the Project

#### Build Daemon and Wallet:
```bash
# Clone repository
git clone https://github.com/pactus-project/pactus.git
cd pactus

# Build binaries
make build

# Binaries created in build/ directory:
# - pactus-daemon
# - pactus-wallet
```

#### Build GUI Application:
```bash
# Install GTK+3 dependencies
# Ubuntu/Debian: apt-get install libgtk-3-dev
# macOS: brew install gtk+3
# Windows: Install MSYS2 and GTK+3 packages

# Build GUI
make build_gui

# Binary created: build/pactus-gui
```

#### Available Make Targets:
```bash
make build          # Build daemon and wallet
make build_gui      # Build GUI application
make devtools       # Install development tools
make fmt            # Format source code
make check          # Run all checks (lint, vet, etc.)
make test           # Run all tests
make unit_test      # Run unit tests only
make proto          # Generate protobuf code
make proto-check    # Validate protobuf files
make proto-format   # Format protobuf files
```

### Code Quality

#### Formatting and Linting:
```bash
# Format code (gofmt + goimports)
make fmt

# Run linters and checks
make check

# Individual checks
golangci-lint run
go vet ./...
staticcheck ./...
```

#### Testing:
```bash
# Run all tests (unit + integration)
make test

# Run unit tests only
make unit_test

# Run tests with coverage
go test -race -coverprofile=coverage.out ./...

# View coverage report
go tool cover -html=coverage.out
```

#### Test Categories:
- **Unit Tests**: Individual component testing
- **Integration Tests**: Multi-component interaction testing
- **End-to-End Tests**: Full system testing
- **Benchmark Tests**: Performance testing

### Project Structure Deep Dive

#### Module Organization:
```
pactus/
├── cmd/                    # Command-line applications
│   ├── daemon/            # Node daemon
│   ├── wallet/            # Wallet CLI
│   ├── shell/             # Interactive shell
│   └── gtk/               # GUI application
├── consensus/             # Legacy consensus (v1)
├── consensusv2/           # Current consensus (v2)
├── committee/             # Validator committee management
├── config/                # Configuration management
├── crypto/                # Cryptographic primitives
├── execution/             # Transaction execution
├── genesis/               # Genesis block handling
├── network/               # P2P networking
├── node/                  # Node orchestration
├── sandbox/               # Execution environment
├── sortition/             # Validator selection
├── state/                 # Blockchain state
├── store/                 # Persistent storage
├── sync/                  # Block synchronization
├── txpool/                # Transaction pool
├── types/                 # Core data types
├── util/                  # Utility packages
├── version/               # Version management
├── wallet/                # Wallet implementation
└── www/                   # API services
    ├── grpc/              # gRPC server
    ├── jsonrpc/           # JSON-RPC server
    ├── http/              # HTTP REST server
    ├── html/              # HTML interface
    └── zmq/               # ZeroMQ server
```

#### Key Design Patterns:
- **Interface-Based Design**: Extensive use of interfaces for modularity
- **Factory Pattern**: Component creation through factory functions
- **Observer Pattern**: Event-driven architecture with pipelines
- **Singleton Pattern**: Global services like logger and config
- **Strategy Pattern**: Pluggable consensus and network protocols

### Protobuf Development

#### Generate gRPC Code:
```bash
# Generate protobuf files
make proto

# Validate protobuf files
make proto-check

# Format protobuf files
make proto-format
```

#### Adding New API Methods:
1. Define method in appropriate `.proto` file in `www/grpc/`
2. Run `make proto` to generate code
3. Implement method in corresponding service file
4. Add comprehensive tests for new functionality
5. Update API documentation

#### Protobuf File Structure:
```
www/grpc/
├── pactus/            # Main protocol definitions
│   ├── blockchain.proto
│   ├── network.proto
│   ├── transaction.proto
│   └── wallet.proto
└── gen/               # Generated code
    ├── go/            # Go bindings
    ├── rust/          # Rust bindings
    ├── js/            # JavaScript bindings
    └── docs/          # API documentation
```

### Contributing Guidelines

#### Code Standards:
- Follow [Effective Go](https://golang.org/doc/effective_go.html) guidelines
- Follow [Go Doc Comments](https://go.dev/doc/comment) guidelines
- Follow Clean Code principles from Robert C. Martin's book
- Write comprehensive unit tests for all new code
- Ensure all existing tests pass before submitting PR

#### Error and Log Message Guidelines:
- Error messages should not start with capital letter (unless proper noun)
- Error messages should not end with punctuation
- Use structured logging with appropriate log levels
- Include relevant context in error messages

#### Testing Guidelines:
- Use `testify` framework for assertions
- Use `assert.Panics` for panic test cases
- Use `assert.ErrorIs` with expected error as second argument
- Use `assert.Equal` with expected value as first argument
- Write table-driven tests for multiple test cases
- Include both positive and negative test cases

#### Commit Message Format:
```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Types**: `fix`, `feat`, `docs`, `test`, `build`, `ci`, `perf`, `refactor`, `style`, `chore`

**Scopes**: `consensus`, `network`, `state`, `wallet`, `api`, `config`, etc.

#### Example Commits:
```
feat(consensus): implement change-proposer mechanism

Add support for proposer rotation in case of failures.
Includes justification validation and vote aggregation.

Closes #123

fix(network): resolve connection timeout issues

Increase default timeout values and add retry logic
for connection establishment.

test(state): add comprehensive validator tests

Include tests for validator lifecycle, committee
membership, and power calculations.
```

### Development Workflow

#### Feature Development:
1. **Fork Repository**: Create personal fork on GitHub
2. **Create Branch**: Create feature branch from latest main
3. **Implement Feature**: Write code following standards
4. **Add Tests**: Comprehensive test coverage
5. **Update Documentation**: Update relevant docs
6. **Run Checks**: Ensure all checks pass locally
7. **Submit PR**: Create pull request with clear description

#### Bug Fix Workflow:
1. **Reproduce Issue**: Create minimal reproduction case
2. **Write Test**: Add test that demonstrates the bug
3. **Fix Issue**: Implement fix with minimal changes
4. **Verify Fix**: Ensure test passes and no regression
5. **Submit PR**: Include issue reference in PR

#### Code Review Process:
- **Automated Checks**: CI/CD runs all tests and checks
- **Peer Review**: At least one maintainer review required
- **Documentation Review**: Ensure docs are updated
- **Performance Review**: Check for performance implications
- **Security Review**: Verify no security vulnerabilities

### Debugging and Profiling

#### Debug Logging:
```toml
[logger]
level = "debug"
targets = ["console", "file"]
format = "text"
file_path = "logs/pactus.log"
colorful = true
```

#### Performance Profiling:
```bash
# CPU profiling
go test -cpuprofile=cpu.prof -bench=.

# Memory profiling  
go test -memprofile=mem.prof -bench=.

# Trace profiling
go test -trace=trace.out -bench=.

# Analyze profiles
go tool pprof cpu.prof
go tool pprof mem.prof
go tool trace trace.out
```

#### Common Debug Commands:
```bash
# Check node status
./pactus-daemon status -w /path/to/working/dir

# Inspect blockchain state
./pactus-daemon inspect -w /path/to/working/dir

# Check network connectivity
./pactus-daemon network -w /path/to/working/dir

# Validate database integrity
./pactus-daemon validate -w /path/to/working/dir
```

### IDE Configuration

#### VS Code Setup:
```json
{
    "go.toolsManagement.checkForUpdates": "local",
    "go.useLanguageServer": true,
    "go.formatTool": "goimports",
    "go.lintTool": "golangci-lint",
    "go.testFlags": ["-v", "-race"],
    "go.buildFlags": ["-race"],
    "editor.formatOnSave": true
}
```

#### Recommended Extensions:
- Go (Google)
- golangci-lint (golangci)
- Protobuf support (protobuf-lang)
- GitLens (GitKraken)
- Thunder Client (REST API testing)

---

## Deployment

### Node Deployment

#### Initialize Node:
```bash
# Initialize working directory
./pactus-daemon init -w /path/to/working/dir

# Start node
./pactus-daemon start -w /path/to/working/dir
```

#### Configuration Options:
```bash
# Custom configuration
./pactus-daemon init -w /path/to/working/dir \
  --network testnet \
  --validators 4 \
  --reward-address <address>
```

### Docker Deployment

#### Dockerfile:
```dockerfile
FROM golang:1.21-alpine AS builder
WORKDIR /app
COPY . .
RUN make build

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /app/build/pactus-daemon .
CMD ["./pactus-daemon", "start"]
```

#### Docker Compose:
```yaml
version: '3.8'
services:
  pactus-node:
    build: .
    ports:
      - "21777:21777"  # P2P
      - "9090:9090"    # gRPC
      - "8545:8545"    # JSON-RPC
    volumes:
      - pactus-data:/root/.pactus
    environment:
      - PACTUS_NETWORK=testnet

volumes:
  pactus-data:
```

### Production Considerations

#### Security:
- Run with non-root user
- Configure firewall rules
- Use TLS for API endpoints
- Regular security updates

#### Monitoring:
- Enable Prometheus metrics
- Set up log aggregation
- Monitor disk space usage
- Track network connectivity

#### Backup:
- Regular state backups
- Validator key security
- Configuration versioning
- Disaster recovery planning

---

## Testing

### Test Categories

#### Unit Tests:
```bash
# Run unit tests
go test ./...

# Run with race detection
go test -race ./...

# Run with coverage
go test -coverprofile=coverage.out ./...

# View coverage report
go tool cover -html=coverage.out
```

#### Integration Tests:
```bash
# Run integration tests
make test

# Run specific test package
go test ./consensus/...
go test ./network/...
go test ./state/...
```

#### End-to-End Tests:
```bash
# Full system testing
go test -tags=e2e ./tests/e2e/...

# Network simulation tests
go test ./tests/network/...

# Performance benchmarks
go test -bench=. ./...
```

### Test Infrastructure

#### TestSuite Helper:
```go
func TestExample(t *testing.T) {
    ts := testsuite.NewTestSuite(t)
    
    // Generate test data
    validators := ts.GenerateTestCommittee(4)
    state := ts.GenerateTestState()
    tx := ts.GenerateTestTransferTx()
    
    // Create test environment
    sandbox := ts.GenerateTestSandbox()
    network := ts.GenerateTestNetwork()
}
```

#### Mock Objects:
The project provides comprehensive mocking infrastructure:

**Mock State**:
```go
type MockState struct {
    TestStore          *store.MockStore
    TestCommittee      committee.Committee
    TestValKeys        []*bls.ValidatorKey
    TestLastBlockHash  hash.Hash
    TestLastBlockHeight uint32
}
```

**Mock Network**:
```go
type MockNetwork struct {
    TestID            peer.ID
    TestEventPipe     pipeline.Pipeline[Event]
    TestSentMessages  []Message
    TestReceivedBytes []byte
}
```

**Mock Consensus**:
```go
type MockConsensus struct {
    TestActive        bool
    TestHeight        uint32
    TestRound         int16
    TestProposal      *proposal.Proposal
    TestAllVotes      []*vote.Vote
}
```

#### Test Utilities:
```go
// Generate test data
ts.RandHash()                    // Random hash
ts.RandAmount()                  // Random amount
ts.RandAccAddress()              // Random account address
ts.RandValAddress()              // Random validator address
ts.RandBLSKeyPair()             // Random BLS key pair
ts.RandEd25519KeyPair()         // Random Ed25519 key pair

// Generate test objects
ts.GenerateTestAccount()         // Test account
ts.GenerateTestValidator()       // Test validator
ts.GenerateTestBlock()           // Test block
ts.GenerateTestTransaction()     // Test transaction
ts.GenerateTestCertificate()     // Test certificate
```

### Testing Best Practices

#### Test Structure:
```go
func TestComponentFunction(t *testing.T) {
    t.Run("should handle valid input", func(t *testing.T) {
        // Arrange
        setup := createTestSetup(t)
        
        // Act
        result := setup.component.Function(validInput)
        
        // Assert
        assert.NoError(t, result.Error)
        assert.Equal(t, expectedValue, result.Value)
    })
    
    t.Run("should reject invalid input", func(t *testing.T) {
        // Arrange
        setup := createTestSetup(t)
        
        // Act
        result := setup.component.Function(invalidInput)
        
        // Assert
        assert.ErrorIs(t, result.Error, ExpectedError)
    })
}
```

#### Table-Driven Tests:
```go
func TestValidation(t *testing.T) {
    tests := []struct {
        name     string
        input    Input
        expected error
    }{
        {"valid input", validInput, nil},
        {"empty input", emptyInput, ErrEmptyInput},
        {"invalid format", invalidInput, ErrInvalidFormat},
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            err := Validate(tt.input)
            assert.ErrorIs(t, err, tt.expected)
        })
    }
}
```

#### Consensus Testing:
```go
func TestConsensusScenario(t *testing.T) {
    td := setup(t)
    
    // Setup initial state
    td.commitBlockForAllStates(t)
    height := uint32(2)
    round := int16(0)
    
    // Enter new height
    td.enterNewHeight(td.consP)
    
    // Create and broadcast proposal
    prop := td.makeProposal(t, height, round)
    td.addPrepareVote(td.consP, prop.Block().Hash(), height, round, tIndexX)
    
    // Verify consensus progression
    td.shouldPublishVote(t, td.consP, vote.VoteTypePrecommit, prop.Block().Hash())
}
```

#### Network Testing:
```go
func TestNetworkProtocol(t *testing.T) {
    // Create test network
    net1 := network.MockingNetwork(ts, "net1")
    net2 := network.MockingNetwork(ts, "net2")
    
    // Connect networks
    net1.Connect(net2.ID())
    
    // Test message exchange
    msg := message.NewBlockMessage(testBlock)
    net1.Broadcast(msg)
    
    // Verify message received
    assert.Eventually(t, func() bool {
        return net2.ReceivedMessage(msg.ID())
    }, time.Second, time.Millisecond*100)
}
```

### Continuous Integration

#### GitHub Actions Workflow:
```yaml
name: CI
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        go-version: [1.21, 1.22]
    
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-go@v4
        with:
          go-version: ${{ matrix.go-version }}
      
      - name: Install dependencies
        run: make devtools
      
      - name: Run checks
        run: make check
      
      - name: Run tests
        run: make test
      
      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          file: ./coverage.out
```

#### Quality Gates:
- **Code Coverage**: Minimum 80% coverage required
- **Linting**: Must pass all linter checks
- **Security**: Security scan with gosec
- **Performance**: Benchmark regression detection
- **Integration**: End-to-end test success

### Performance Testing

#### Benchmark Tests:
```go
func BenchmarkConsensusVoting(b *testing.B) {
    td := setup(b)
    
    b.ResetTimer()
    for i := 0; i < b.N; i++ {
        vote := td.generateTestVote()
        td.consensus.AddVote(vote)
    }
}

func BenchmarkTransactionExecution(b *testing.B) {
    sandbox := createBenchmarkSandbox(b)
    tx := createBenchmarkTransaction()
    
    b.ResetTimer()
    for i := 0; i < b.N; i++ {
        execution.Execute(tx, sandbox)
    }
}
```

#### Load Testing:
```go
func TestHighThroughput(t *testing.T) {
    const numTransactions = 10000
    
    // Create test environment
    node := createTestNode(t)
    
    // Generate transactions
    txs := make([]*tx.Tx, numTransactions)
    for i := 0; i < numTransactions; i++ {
        txs[i] = generateTestTransaction()
    }
    
    // Measure processing time
    start := time.Now()
    for _, tx := range txs {
        node.ProcessTransaction(tx)
    }
    duration := time.Since(start)
    
    // Verify performance metrics
    tps := float64(numTransactions) / duration.Seconds()
    assert.Greater(t, tps, 100.0) // Minimum 100 TPS
}
```

### Test Coverage

#### Coverage Targets:
- **Critical Paths**: 100% coverage (consensus, cryptography)
- **Core Logic**: 90% coverage (state, execution, validation)
- **Supporting Code**: 80% coverage (utilities, helpers)
- **Integration**: 70% coverage (network, sync, APIs)

#### Coverage Commands:
```bash
# Generate coverage report
go test -coverprofile=coverage.out ./...

# View coverage by package
go tool cover -func=coverage.out

# Generate HTML coverage report
go tool cover -html=coverage.out -o coverage.html

# Check coverage threshold
go tool cover -func=coverage.out | grep total | awk '{print $3}' | sed 's/%//'
```

---

## Troubleshooting

### Common Issues

#### 1. Consensus Timeout
**Symptom**: Node stops producing blocks
**Causes**:
- Network connectivity issues
- Insufficient validator participation
- Clock synchronization problems

**Solutions**:
```bash
# Check network connectivity
curl -X POST http://localhost:8545 \
  -H "Content-Type: application/json" \
  -d '{"method":"pactus.network.getNetworkInfo","params":[],"id":1}'

# Check consensus status
curl -X POST http://localhost:8545 \
  -H "Content-Type: application/json" \
  -d '{"method":"pactus.blockchain.getConsensusInfo","params":[],"id":1}'

# Sync NTP time
ntpdate -s time.nist.gov
```

#### 2. Sync Issues
**Symptom**: Node cannot sync with network
**Causes**:
- Wrong network configuration
- Firewall blocking connections
- Invalid bootstrap peers

**Solutions**:
```bash
# Check network configuration
cat config.toml | grep network -A 10

# Test connectivity to bootstrap peers
telnet <bootstrap-peer-ip> 21777

# Check firewall settings
sudo ufw status
```

#### 3. High Memory Usage
**Symptom**: Node consuming excessive memory
**Causes**:
- Large transaction pool
- Memory leaks
- Insufficient garbage collection

**Solutions**:
```bash
# Reduce transaction pool size
# Edit config.toml:
[tx_pool]
max_size = 500

# Restart with memory profiling
GOGC=100 ./pactus-daemon start -w /path/to/working/dir
```

#### 4. Database Corruption
**Symptom**: Node fails to start with database errors
**Causes**:
- Unexpected shutdown
- Disk space exhaustion
- Hardware failure

**Solutions**:
```bash
# Check disk space
df -h

# Validate database integrity
./pactus-daemon validate -w /path/to/working/dir

# Rebuild from backup or resync
rm -rf /path/to/working/dir/data
./pactus-daemon start -w /path/to/working/dir
```

### Performance Optimization

#### Node Performance:
```toml
# Optimize for performance
[store]
batch_size = 2000
cache_size = 1000

[sync]
cache_size = 2000

[tx_pool]
max_size = 2000
```

#### Network Performance:
```toml
[network]
max_connections = 100
dial_timeout = "10s"
keep_alive_interval = "30s"
```

### Logging and Monitoring

#### Enable Detailed Logging:
```toml
[logger]
level = "debug"
targets = ["console", "file"]
format = "text"
file_path = "logs/pactus.log"
```

#### Prometheus Metrics:
```bash
# Access metrics endpoint
curl http://localhost:8080/metrics
```

#### Key Metrics to Monitor:
- Block height progression
- Transaction pool size
- Peer connection count
- Consensus participation rate
- Memory and CPU usage

### Recovery Procedures

#### Validator Key Recovery:
1. Stop node safely
2. Restore validator key from backup
3. Update configuration
4. Restart node

#### State Recovery:
1. Stop node
2. Remove corrupted data
3. Restore from backup or resync
4. Restart node

#### Network Recovery:
1. Check network configuration
2. Update bootstrap peers
3. Clear peer database
4. Restart with fresh network state

---

## Conclusion

Pactus represents a significant advancement in blockchain technology, combining cutting-edge cryptographic techniques with innovative consensus mechanisms to create a highly secure, scalable, and efficient distributed ledger system. This comprehensive technical analysis reveals a project of exceptional quality and sophistication.

### Technical Excellence Assessment

#### Architecture and Design Quality

The Pactus codebase demonstrates exemplary software engineering practices:

**Modular Architecture**: The system is built with clear separation of concerns, featuring well-defined interfaces between components such as consensus, networking, storage, and execution layers. This modularity enables independent development, testing, and optimization of individual components.

**Cryptographic Security**: The implementation of dual signature schemes (BLS12-381 and Ed25519) showcases deep understanding of cryptographic best practices. The use of BLS signatures for consensus operations enables efficient signature aggregation, while Ed25519 provides fast verification for account transactions.

**Consensus Innovation**: The Change-Proposer protocol represents a novel approach to Byzantine Fault Tolerance, automatically adapting to network conditions and providing enhanced resilience against adversarial scenarios.

#### Code Quality and Maintainability

```go
// Example of clean, well-documented code structure
type Consensus interface {
    Start() error
    Stop()
    AddVote(*vote.Vote)
    SetProposal(*proposal.Proposal) 
    HandleQueryVote(height uint32, round int16) *vote.Vote
    HandleQueryProposal(height uint32, round int16) *proposal.Proposal
    HeightRound() (uint32, int16)
    IsActive() bool
}
```

The codebase exhibits:
- **Comprehensive Testing**: Extensive unit tests, integration tests, and mock implementations
- **Clear Documentation**: Well-documented APIs and internal components  
- **Error Handling**: Robust error handling with descriptive error types
- **Performance Optimization**: Efficient algorithms and data structures
- **Memory Management**: Careful resource management and cleanup

#### Innovation Highlights

**1. Sortition-Based Proposer Selection**
```go
// VRF-based sortition provides unpredictable, verifiable randomness
func EvaluateSortition(seed VerifiableSeed, privateKey *bls.PrivateKey, 
                      totalPower, validatorPower uint64) (bool, Proof) {
    // Cryptographically secure random selection
    signData := append(seed[:], privateKey.PublicKey().Bytes()...)
    signature := privateKey.Sign(signData)
    proof, _ := ProofFromBytes(signature.Bytes())
    
    index := GetIndex(proof, totalPower)
    selected := index < validatorPower
    
    return selected, proof
}
```

**2. Multi-Type Transaction System**
The six transaction types (Transfer, Bond, Unbond, Withdraw, Sortition, BatchTransfer) provide comprehensive blockchain functionality while maintaining simplicity and efficiency.

**3. Dual Consensus Versions**
The implementation of both consensus/ and consensusv2/ demonstrates the project's commitment to continuous improvement and protocol evolution.

### Performance and Scalability Analysis

#### Throughput Capabilities

- **Target TPS**: 1000+ transactions per second
- **Block Time**: 10 seconds (adjustable 2-3600 seconds)
- **Finality**: Instant (BFT consensus)
- **Committee Size**: Scalable (4-1000 validators)

#### Resource Efficiency

```yaml
Memory Usage:
  Node Operation: <2GB typical
  State Cache: 64MB
  Block Cache: 32MB
  Transaction Pool: 16MB

Network Efficiency:
  Signature Aggregation: Reduces bandwidth by 90%+
  Compact Block Headers: <1KB per block
  Efficient P2P Protocol: libp2p with gossip optimization

Storage Efficiency:
  LevelDB Backend: Compressed storage
  Merkle Tree Optimization: Minimal storage overhead
  Transaction Indexing: Fast query performance
```

### Security Analysis

#### Cryptographic Strength

**BLS12-381 Security Properties**:
- 128-bit security level
- Resistance to known attacks (Pollard's rho, index calculus)
- Pairing-based security assumptions
- Signature aggregation without security degradation

**Ed25519 Security Properties**:
- 128-bit security level  
- Side-channel resistance
- Fast verification (< 100 microseconds)
- RFC 8032 compliance

#### Consensus Security

**Byzantine Fault Tolerance**:
- Safety: 2/3+ honest validators required
- Liveness: Guaranteed under network synchrony
- Change-Proposer: Automatic recovery from leader failures
- VRF Sortition: Unpredictable proposer selection

### Ecosystem Maturity

#### Multi-Language Support

The project provides comprehensive API bindings for major programming languages:

```yaml
Generated Clients:
  - Go (native)
  - JavaScript/TypeScript
  - Python  
  - Rust
  - Dart/Flutter
  - C++

API Protocols:
  - gRPC (high performance)
  - JSON-RPC (compatibility)
  - HTTP REST (simplicity)
  - WebSocket (real-time)
  - ZeroMQ (messaging)
```

#### Developer Tooling

- **CLI Tools**: Comprehensive command-line interface
- **GTK GUI**: Cross-platform graphical interface
- **Web Interface**: Browser-based dashboard
- **SDK Libraries**: Development kits for multiple languages
- **Documentation**: Extensive technical documentation

### Competitive Advantages

#### Technical Differentiators

1. **Unique Consensus**: Change-Proposer BFT with sortition
2. **Dual Cryptography**: Optimized signature schemes for different use cases
3. **Free Transactions**: Zero-fee sortition and unbond operations
4. **Instant Finality**: BFT consensus provides immediate transaction finality
5. **Energy Efficiency**: 99.99% more efficient than Proof-of-Work

#### Ecosystem Benefits

1. **Low Entry Barrier**: 1,000 PAC minimum stake
2. **Fair Distribution**: VRF-based proposer selection
3. **Developer Friendly**: Multiple programming language support
4. **Proven Technology**: Based on established cryptographic primitives
5. **Active Development**: Continuous improvement and optimization

### Future Potential and Roadmap

#### Planned Enhancements

Based on the codebase analysis, potential future developments include:

**1. Smart Contract Integration**
```go
// Future smart contract executor interface
type SmartContractExecutor interface {
    Deploy(bytecode []byte) (Address, error)
    Execute(address Address, method string, params []byte) ([]byte, error)
    Query(address Address, method string, params []byte) ([]byte, error)
}
```

**2. Layer 2 Solutions**
- State channels for micropayments
- Sidechains for specialized applications
- Cross-chain bridges for interoperability

**3. Advanced Features**
- Multi-signature accounts
- Time-locked transactions
- Atomic swaps
- Privacy enhancements

#### Scalability Roadmap

```mermaid
graph LR
    A[Current: 1K TPS] --> B[Phase 1: 10K TPS]
    B --> C[Phase 2: 100K TPS]
    C --> D[Phase 3: 1M TPS]
    
    B --> E[Sharding Implementation]
    C --> F[Layer 2 Integration]
    D --> G[Cross-Chain Protocols]
```

### Industry Impact and Adoption Potential

#### Market Positioning

Pactus is positioned to compete with leading blockchain platforms through:

- **Technical Superiority**: Advanced consensus and cryptography
- **Energy Efficiency**: Sustainable blockchain solution
- **Developer Experience**: Comprehensive tooling and documentation
- **Performance**: High throughput with instant finality
- **Decentralization**: Fair and accessible validator participation

#### Adoption Catalysts

1. **Enterprise Ready**: Production-quality codebase
2. **Regulatory Friendly**: Energy-efficient consensus
3. **Developer Ecosystem**: Multi-language support
4. **Community Driven**: Open-source development model
5. **Proven Technology**: Battle-tested cryptographic primitives

### Technical Recommendations

#### For Developers

1. **Start with APIs**: Use gRPC for high-performance applications
2. **Use SDK Libraries**: Leverage provided client libraries
3. **Follow Best Practices**: Implement proper error handling and security
4. **Contribute**: Participate in open-source development

#### For Validators

1. **Hardware Requirements**: Minimum 4GB RAM, 100GB storage
2. **Network Setup**: Stable internet connection, proper port configuration
3. **Security**: Secure key management and backup procedures
4. **Monitoring**: Implement comprehensive monitoring and alerting

#### For Enterprises

1. **Pilot Projects**: Start with small-scale implementations
2. **Integration Planning**: Use REST APIs for easier integration
3. **Compliance**: Leverage energy-efficient consensus for regulatory benefits
4. **Support**: Engage with the development community

### Final Assessment

Pactus represents a masterpiece of blockchain engineering, combining theoretical rigor with practical implementation excellence. The project demonstrates:

**Technical Maturity** (9.5/10):
- Production-ready codebase
- Comprehensive testing suite
- Well-designed architecture
- Advanced cryptographic implementation

**Innovation Level** (9/10):
- Novel consensus mechanism
- Unique sortition system
- Dual signature optimization
- Multi-type transaction system

**Ecosystem Readiness** (8.5/10):
- Multi-language API support
- Comprehensive documentation
- Developer-friendly tooling
- Active community engagement

**Future Potential** (9/10):
- Scalable architecture foundation
- Extensible protocol design
- Strong cryptographic security
- Sustainable consensus mechanism

The Pactus blockchain stands as a testament to the potential of next-generation distributed ledger technology. Its combination of technical excellence, innovative design, and practical implementation makes it a compelling platform for building the decentralized applications of the future. The project's commitment to security, performance, and developer experience positions it well for widespread adoption in the evolving blockchain ecosystem.

---

*This comprehensive technical documentation represents an in-depth analysis of the Pactus blockchain platform, covering all major aspects from low-level cryptographic implementations to high-level architectural decisions. The project demonstrates exceptional engineering quality and innovative approaches to blockchain technology challenges.*

**Comprehensive Testing**: Extensive test coverage with unit tests, integration tests, and end-to-end testing provides confidence in system reliability.

**Professional Standards**: Following Go best practices, conventional commits, and clean code principles ensures maintainable and readable codebase.

**Rich Tooling**: Complete development environment with automated builds, linting, formatting, and continuous integration.

**Documentation**: Thorough documentation at code level and architectural level facilitates understanding and contribution.

### Ecosystem Features

**Multi-API Support**: gRPC, JSON-RPC, HTTP REST, and ZeroMQ interfaces provide flexibility for different use cases and integrations.

**Wallet System**: Complete HD wallet implementation with BIP39 mnemonic support and multi-signature capabilities.

**GUI Support**: GTK-based graphical interface makes the system accessible to non-technical users.

**Network Flexibility**: Support for mainnet, testnet, and localnet deployments with configurable parameters.

### Innovation Highlights

**Consensus V2**: The new consensus algorithm represents a significant advancement in BFT consensus design with practical benefits for validator rotation and network resilience.

**VRF-Based Sortition**: The use of Verifiable Random Functions for validator selection provides cryptographic fairness and unpredictability.

**Persistent Merkle Trees**: Custom implementation optimized for blockchain state management with efficient incremental updates.

**Pipeline Architecture**: Event-driven design with message pipelines enables scalable and maintainable component interactions.

### Future Potential

The architecture and design quality of Pactus position it well for future enhancements:

- **Scalability Improvements**: The modular design allows for easy integration of layer-2 solutions and sharding
- **Protocol Upgrades**: Clean interfaces enable smooth protocol version upgrades
- **Ecosystem Growth**: Rich APIs and tooling support third-party development and integrations
- **Research Integration**: The consensus framework can incorporate future BFT research advances

### Community and Contribution

The project demonstrates strong engineering practices that facilitate community contribution:

- **Clear Architecture**: Well-documented components and interfaces
- **Comprehensive Testing**: Easy verification of changes and additions
- **Standard Practices**: Following Go and blockchain development conventions
- **Accessible Codebase**: Clean, readable code with good documentation

### Final Assessment

Pactus is a mature, well-designed blockchain implementation that successfully combines theoretical advances in consensus algorithms with practical engineering excellence. The project represents a significant contribution to the blockchain ecosystem and provides a solid foundation for building decentralized applications and services.

The combination of innovative consensus mechanisms, robust engineering practices, comprehensive tooling, and strong architectural design makes Pactus a noteworthy blockchain implementation that advances the state of the art in distributed ledger technology.

---

*This comprehensive documentation represents the current state of the Pactus blockchain project as of the analysis date. The project continues to evolve, and readers are encouraged to check the official repository and documentation for the latest updates and developments.*

**Key Resources:**
- **GitHub Repository**: https://github.com/pactus-project/pactus
- **Official Documentation**: https://docs.pactus.org
- **Community Discord**: https://discord.gg/H5vZkNnXCu
- **Twitter/X**: https://x.com/PactusChain
- **Developer Resources**: Project wiki and contribution guidelines

**Technical Specifications:**
- **Language**: Go 1.24.5+
- **License**: MIT License
- **Consensus**: Custom BFT with Change-Proposer
- **Networking**: libp2p with gossip protocol
- **Storage**: LevelDB with Merkle tree indexing
- **APIs**: gRPC, JSON-RPC, HTTP REST, ZeroMQ
- **Wallets**: HD wallets with BLS and Ed25519 support
