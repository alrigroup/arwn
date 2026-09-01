# ARWN — ALRI Web Native Framework (.arweb)

**Next-Generation Multi-Language High-Performance Web & Microservices Framework for ALRIOS.**

Developed by **[ALRIGROUP](https://alrigroup.com/)**.

---

## 🚀 Overview

**ARWN (ALRI Web Native)** is an ultra-fast, multi-language binary container format (`.arweb`) and multi-threaded embedded web server designed to package, protect, and execute high-performance frontend and backend services within the **ALRIOS** operating environment.

Unlike traditional web runtimes that read static files sequentially from disk, **ARWN** operates entirely out of in-memory, CRC32-verified binary archives with zero runtime file system access, sub-millisecond response times, and multi-core thread pooling.

---

## 🏗️ Architecture & Binary Layout

```
┌────────────────────────────────────────────────────────┐
│               .arweb Binary Container                  │
├────────────────────────────────────────────────────────┤
│ Header: Magic 'ARWN' (0x4E575241) | Version | Sections │
├────────────────────────────────────────────────────────┤
│ Section 0: app.html      (Entrypoint HTML / No-Cache)  │
│ Section 1: main.js       (Base64 VM Crypt / Immutable) │
│ Section 2: main.css      (Tailored CSS / Immutable)    │
│ Section 3: mod/*.wasm    (Direct Memory / WASM Engine) │
│ Section 4: *.arweb       (Nested Multi-Language Units) │
└────────────────────────────────────────────────────────┘
```

---

## 🌟 Key Features

### 1. Multi-Language Native WASM Engine
- Compile and execute modules written in **C**, **C++**, **Rust**, **Go**, and **JavaScript JIT** under unified linear memory buffers.
- Direct pointer manipulation and `i32.load`/`store` execution without garbage collection pauses or bounds-check overhead.

### 2. Multi-Threaded Worker Pool Concurrency
- Integrated **Multi-Worker Thread Pool** with circular queue dispatcher (`ARWN_SERVER_QUEUE_SIZE = 4096`).
- Capable of sustaining **2,500+ requests/sec** with zero drops and sub-millisecond latency.
- Anti-DoS Load Shedding (`HTTP 503` under queue exhaustion).

### 3. IP Protection & Military-Grade Obfuscation
- **Dual-Pass Security Layer**:
  1. Whitespace minification and complete internal comment stripping.
  2. Byte-level **Base64 binary encapsulation**.
  3. Self-executing **VM Bootstrapper** evaluating dynamically into global browser memory without file traces.
- **Mandatory Licensing Headers**: Official ALRI GROUP License Header + Custom Developer Licensing automatically appended to all distributed web units.

### 4. Standard Unit Naming Convention
All ARWN units enforce a clean, standard file naming hierarchy:
- `main.arhtml` (HTML Entrypoint)
- `main.js` (JavaScript logic & bridge)
- `main.css` (Stylesheets & design tokens)
- `[unit_name].arweb` (Compiled binary container)

---

## ⚙️ Configuration (`config.arwn`) Reference

```ini
[app]
name=ecosystem-demo
port=3055
bind=127.0.0.1
copyright=Copyright (c) 2026 ALRIGROUP. All rights reserved.

[arws]
gateway=127.0.0.1:9500
route.host=ecosystem.localhost
route.path=/*
route.mode=production

[unit:main]
source=web/
entry=main.arhtml
compile=main.js
compile.lang=js
obfuscate=yes
copyright=Custom Frontend Module - Unauthorized copying prohibited.

[unit:c_engine]
source=units/c
compile=c_calc.wasm
compile.lang=c
obfuscate=yes

[unit:rust_engine]
source=units/rust
compile=rust_calc.wasm
compile.lang=rust
obfuscate=yes
```

---

## 🛠️ CLI & Build Tooling

### 1. Compiling & Packing Containers
```bash
# Compile and package .arweb units from config.arwn
./arcore/programfiles/arwn/arwn_build /path/to/app/config.arwn /path/to/app/build/

# Extract and inspect an .arweb archive
./arcore/programfiles/arwn/arwn_build inspect main.arweb
```

### 2. Packaging `.arapp` Application
```bash
./arcore/armake pack /path/to/app /mnt/HD/ALRIGROUP/local/alrios/arcore/apps/app_name.arapp
```

### 3. Deploying in ALRIOS Daemon
```bash
./arcore/alrios power reload
./arcore/alrios status
```

---

## 📊 Security & Compliance Standards

| Feature | Standard | Compliance |
| :--- | :--- | :--- |
| **Data Integrity** | IEEE 802.3 CRC32 Section Table | ✅ Active |
| **HTTP Security Headers** | `nosniff`, `DENY`, Strict CSP | ✅ Active |
| **Anti-Tamper Packaging** | Base64 Dynamic VM Loader | ✅ Active |
| **Multi-Core Concurrency** | Dedicated Thread Worker Pool | ✅ Active |
| **Zero-Disk Streaming** | In-Memory Route Dispatch | ✅ Active |
