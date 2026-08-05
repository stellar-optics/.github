# Stellar Optics

**Go tooling that makes Stellar and Soroban legible.**

Working with Stellar means working with XDR — opaque base64 blobs for transactions, results, ledger entries, and contract events. Reading one usually means pasting it into a web tool and losing your context. Testing against one usually means comparing base64 strings and getting a useless failure message when they differ.

Stellar Optics is a family of small, focused Go tools that fix that. Each does a single job well, and they share a core so the output looks the same everywhere.

## The instruments

### 🔍 [stellar-xdr-lens](https://github.com/stellar-optics/stellar-xdr-lens)

*Magnifies one thing.* Decode, explain, and diff a single XDR value from the terminal. Auto-detects the type, prints a readable tree, and tells you in plain English why a transaction failed. Fully offline and deterministic.

```console
$ lens explain --file tx.xdr
```

### 🌈 [stellar-prism](https://github.com/stellar-optics/stellar-prism)

*Splits a live stream.* `tail -f` for Soroban. Stream contract events and ledger data from RPC, decoded and filtered as they arrive, with NDJSON output that pipes straight into `jq`.

```console
$ prism events --contract <CONTRACT_ID>
```

### 🎯 [stellar-focus](https://github.com/stellar-optics/stellar-focus)

*Sharpens tests.* A Go testing toolkit for Stellar and Soroban. Assert on decoded XDR with failure output that shows a real structural diff, manage golden fixtures, and capture live chain data as test data.

```console
$ go get github.com/stellar-optics/stellar-focus
```

## How they fit together

```
        stellar-xdr-lens
         (core decoding)
          ↑           ↑
   stellar-prism   stellar-focus
   (live streams)  (test tooling)
```

Prism and Focus both build on Lens, so decoded output looks the same whether you're inspecting a blob by hand, watching a live stream, or reading a test failure. Learn one tool and the others are already familiar.

## Principles

- **Go only.** No polyglot build steps, no npm in your Go project.
- **Offline where possible.** Core functionality that doesn't need a network is easier to test, faster to run, and works on a plane.
- **Readable failures.** An error message that doesn't tell you what went wrong is a bug.
- **Small and composable.** Unix-friendly output, sensible exit codes, no framework lock-in.

## Status

Early and actively developed. APIs may shift before `v1`. Issues and feedback are welcome on any of the repos.

## Contributing

All three repos welcome contributions. Each has a `CONTRIBUTING.md` with setup instructions and conventions. Questions and ideas are best raised in the relevant repo's Discussions. Security issues should be reported privately through GitHub's security advisory flow rather than as public issues.

Licensed under Apache-2.0.
