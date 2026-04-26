# Black Hat Rust - Companion Code Repository

This is the companion code repository for the "Black Hat Rust" book by Sylvain Kerkour. It contains educational implementations of offensive security tools written in Rust.

## Repository Structure

- **ch_01/**: SHA1 hash cracker - introductory Rust example
- **ch_02/** to **ch_05/**: Reconnaissance tools building a multi-threaded/async scanner (tricoder)
- **ch_06/**: Fuzzing examples
- **ch_07/**: Exploit development (CVE-2021-3156, CVE-2019-89242, CVE-2019-11229)
- **ch_08/**: Shellcode development (reverse_tcp, exec shellcodes)
- **ch_09/**: Phishing toolkit with WebAssembly
- **ch_10/** to **ch_13/**: RAT (Remote Access Tool) development with end-to-end encryption
- **extra/**: Backdoor examples for supply chain attack research

## Working with Individual Projects

Each chapter contains standalone Cargo projects. Navigate to the specific chapter directory before running commands:

```bash
# Chapter 01 - SHA1 cracker
cd ch_01/sha1_cracker
cargo run -- wordlist.txt <hash>

# Chapter 04 - Scanner with modules
cd ch_04/tricoder
cargo run -- scan example.com
```

## Workspace Projects

Chapters 10-13 use Cargo workspaces with multiple crates:

```bash
# Build entire workspace
cd ch_10 && cargo build --release

# Build only the agent (optimized for size)
cd ch_10 && cargo build --release -p agent
```

## Build Profiles

Release builds for RAT agents use aggressive optimization:
- `opt-level = 'z'` (optimize for size)
- `lto = true` (link-time optimization)
- `codegen-units = 1` (single codegen unit for better optimization)

These settings produce minimal binary sizes suitable for implants.

## Shellcode Development

Chapter 8 shellcode targets Linux x86_64 with `no_std`. Build with:

```bash
cd ch_08/hello_world
cargo build --target x86_64-unknown-linux-gnu
```

## Cross-Compilation (ch_12)

The RAT supports cross-compilation for multiple platforms. Refer to ch_12 for target setup.

## Dependencies to Note

- **tokio**: Async runtime (ch_03+)
- **reqwest**: HTTP client with rustls-tls
- **clap**: CLI argument parsing (ch_04+)
- **serde**: Serialization
- **sha-1/hex**: Cryptographic utilities (ch_01)
- **trust-dns-resolver**: DNS resolution
- **rayon**: Data parallelism (ch_02)

## Safety Considerations

This repository contains educational offensive security code. All code is for learning purposes as described in the book. Review code carefully before execution and only use in authorized environments.
