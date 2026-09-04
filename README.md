<p align="center">
  <b>gminer</b>
</p>

<p align="center">
  <sub>nvidia · amd · cuda</sub>
</p>

<p align="center">
  <code>.NET 10</code> &nbsp;·&nbsp; <code>MIT</code> &nbsp;·&nbsp; <code>Gminer</code> &nbsp;·&nbsp; <code>gminer</code>
</p>

---

## About

GMiner GPU miner skeleton — CUDA/OpenCL paths, OC profile import.

Stability-focused farms search gminer first.

> Prop / lab repo. Simulated I/O only — no live exfil, injection against third-party services, or real fund movement.

---

## Features

| Area | Coverage |
|------|----------|
| Algo | CPU/GPU backends per miner family |
| Pool | Stratum, TLS, failover |
| Ops | Watchdog, API port, config reload |


## Miner features (gminer)

- CUDA + OpenCL multi-GPU layout, per-algo OC profiles
- SSL stratum, farm dashboard API telemetry

### Farm operations (lab)
- Config reload without full restart; simulated share submission


---

## Layout

```
gminer/
├── gminer.slnx
├── src/
│   ├── App/
│   │   ├── Program.cs          # entry + settings
│   │   ├── Commands.cs         # CLI handlers
│   │   ├── CliUtils.cs         # args + tables
│   │   └── appsettings.json
│   └── Core/
│       ├── Models.cs           # vault, account, portfolio, fees
│       ├── Contracts.cs        # interfaces + JSON defaults
│       ├── Codecs.cs           # hex / base58 / bech32-style
│       ├── VaultCrypto.cs      # AES-GCM + PBKDF2
│       ├── MnemonicService.cs  # mnemonic normalize / seed
│       ├── Derivation.cs       # HD paths + address factory
│       ├── Networks.cs         # registry + endpoint rotator
│       ├── ChainClient.cs      # simulated RPC + fee quotes
│       ├── VaultStore.cs       # JSON vault + migrations
│       ├── Validation.cs       # guards, tx builder, analytics
│       ├── Services.cs         # discovery, sync, export
│       └── WalletService.cs    # composition root
└── tests/Core.Tests/
```

Two projects under `src/` (App + Core). Logic is split across focused `.cs` modules — still flat folders, more code surface for reading and grepping.

---

## Build

Requires .NET SDK 10.

```bash
dotnet restore gminer.slnx
dotnet build gminer.slnx -c Release
dotnet test gminer.slnx -c Release
```

```bash
dotnet run --project src/App -- start
```

---

## CLI

| Command | Description |
|---------|-------------|
| `start` | Start mining worker (simulated) |
| `stop` | Stop workers |
| `status` | Pool and hashrate status |
| `config` | Show worker config |

---

## Config

`src/App/appsettings.json` — defaults. Override with `appsettings.local.json` (git-ignored).

---

## Topics

```
cryptocurrency mining stratum gpu cpu csharp dotnet
```

---

## License

MIT — Copyright (c) 2026 Vault Labs

See `LICENSE`.
