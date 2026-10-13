<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/masthead-dark.svg" />
  <img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/masthead-light.svg" alt="Daniele Giovane — Systems &amp; backend developer. Native platforms, compilers, graphics, and simulation." width="100%" />
</picture>

[How I work](#how-i-work) · [Open source](#open-source-contributions) · [Personal projects](#personal-projects) · [Private work](#beyond-public-repositories)

<img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/dot-blue.svg" width="8" height="8" alt="" /> I'm **Daniele**, a systems and backend developer in Italy. I build native software and backend platforms, with a particular interest in **compilers, real-time graphics, concurrency, and simulation**.

I want to understand what happens underneath the code I write: how instructions execute, how memory is shared, how data moves between services, and where time is spent. That's what draws me to porting software, building renderers, and working on runtimes. With simulation, there's another question I enjoy: how much complexity can come from a few simple rules?

I also like taking a project through the less visible work that makes it usable: handling failures, testing it against real constraints, packaging it, and following what happens after deployment.

**C · C++ · Rust · Go · Java** &nbsp; / &nbsp; Python · TypeScript

## <img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/section-method.svg" width="24" height="24" alt="" /> How I work

<img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/dot-blue.svg" width="8" height="8" alt="" /> **Understand the problem. Build a correct version. Measure it. Then improve it.**

I start with the behavior I need and the constraints I actually have. I prefer a straightforward implementation I can explain and test. When performance becomes a problem, I want a measurement, a hypothesis, and a comparison that tells me whether the change helped.

When something breaks, I follow it across the stack: from the request to the database, from the tunnel to the routing table, from the frame to the lifetime of a GPU resource. I try to reduce it to a case I can reproduce, fix the cause, and check the original case again.

**I keep implementation and verification separate.** A passing build, a working example, and a deployed system answer different questions. I want the result to be clear about what works, under which conditions, and what still needs work.

## <img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/section-oss.svg" width="24" height="24" alt="" /> Open source contributions

### snx-rs · macOS support, from networking to packaging

<img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/dot-green.svg" width="8" height="8" alt="" /> **Merged upstream.** I added the macOS backend and followed it through hardening, GUI integration, and release tooling. The port uses native macOS APIs and follows the existing Linux/Windows platform abstraction:

- **Networking:** utun, routing sockets, split DNS through SystemConfiguration, and Keychain.
- **Reliability and security:** command-socket peer authorization, network-state crash recovery, and parser tests.
- **Desktop and delivery:** menu-bar GUI, WebKit login, notifications, launchd, and DMG/PKG packaging.

[Port #227](https://github.com/ancwrd1/snx-rs/pull/227) · [Hardening #229](https://github.com/ancwrd1/snx-rs/pull/229) · [GUI #230](https://github.com/ancwrd1/snx-rs/pull/230) · [Packaging #231](https://github.com/ancwrd1/snx-rs/pull/231)

### rust-lang/libc · Apple platform bindings

<img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/dot-green.svg" width="8" height="8" alt="" /> **Merged upstream.** I added missing socket and network-interface `ioctl` constants for Apple targets, checked against native SDK headers, with public API coverage.

[libc #5263 →](https://github.com/rust-lang/libc/pull/5263)

### AnyPS5 · Native ARM64 ahead-of-time compilation

<img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/dot-amber.svg" width="8" height="8" alt="" /> **Open PR series / experimental.** I'm developing offline x86-64 ELF → ARM64 compilation: instruction semantics, LLVM lowering, ABI boundaries, and native runtime providers. Generated programs run without an x86 interpreter, JIT, or Rosetta dependency.

<details>
<summary><b>Compiler, runtime, and validation ↗</b></summary>

<br>

| Layer | Work in the PR series |
| :--- | :--- |
| **Binary recovery** | ELF metadata, relocations, sectionless images, unwind information, and explicit recovery limits. |
| **Code generation** | Signature-qualified and whole-program paths; guest registers/stack and integer/SIMD semantics lowered through LLVM. |
| **Runtime** | Native providers, checked indirect transfers, module lifecycle, static TLS, C++ exceptions, and joinable workers. |
| **Memory ordering** | Bounded concurrency support, checked atomics, and reference comparisons. |
| **Graphics** | A source-built cube compared with an independently compiled ARM64 reference using exact RGB frames, checking completed frames and teardown as part of acceptance. |

Validation includes **zstd**, **yaml-cpp**, instruction-level comparisons, and graphics consumers. Results cover specific execution profiles; **commercial-game compatibility remains unproven**.

[Foundation #1835](https://github.com/boykopovar/AnyPS5/pull/1835) · [Graphics #3891](https://github.com/boykopovar/AnyPS5/pull/3891) · [Whole-program #4599](https://github.com/boykopovar/AnyPS5/pull/4599) · [C++ / TLS #4718](https://github.com/boykopovar/AnyPS5/pull/4718) · [Concurrency #4740](https://github.com/boykopovar/AnyPS5/pull/4740) · [Atomics #4813](https://github.com/boykopovar/AnyPS5/pull/4813)

Merged separately: [macOS unwind contexts #1499](https://github.com/boykopovar/AnyPS5/pull/1499) and [graphics descriptor-array snapshots #1831](https://github.com/boykopovar/AnyPS5/pull/1831).

</details>

## <img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/section-projects.svg" width="24" height="24" alt="" /> Personal projects

| Project | Focus |
| :--- | :--- |
| **[Phosphor](https://github.com/yabanana/phosphor)** | Experimental C++20 / **Metal 4** renderer for Apple silicon: GPU-driven geometry, resource lifetimes, ray tracing, and MetalFX. Measurements and reproducible test benches guide the work; quality and performance qualification remain ongoing. |
| **[LENIA-3D](https://github.com/yabanana/LENIA-3D)** | **Continuous cellular automata** in 2D/3D: FFT convolution, OpenMP, interactive isosurfaces, and parameter searches for emergent behavior. |
| **[ParallelWatorCA](https://github.com/yabanana/ParallelWatorCA)** | Predator–prey simulation with **MPI + OpenMP**, dividing work across processes and threads. |
| **[Fildem](https://github.com/yabanana/Fildem)** | My GNOME global-menu fork/rewrite: **C/GObject core**, session daemon, versioned D-Bus contracts, Shell extension, and GTK4 HUD. |

<details>
<summary><b>Earlier experiments ↗</b></summary>

<br>

**[VulkanTorus](https://github.com/yabanana/VulkanTorus):** C++/Vulkan on Linux, covering swapchains, command buffers, and synchronization. **[FlappyD](https://github.com/yabanana/FlappyD):** a Java game exploring real-time loops, input, and state.

</details>

## <img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/section-private.svg" width="24" height="24" alt="" /> Beyond public repositories

<img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/dot-blue.svg" width="8" height="8" alt="" /> My private projects include:

- **Sim-racing operations:** Go/PostgreSQL booking and events, web/mobile clients, tenant isolation, backend rules, background jobs, and a shared backend for independently branded clients.
- **Live telemetry:** a Go desktop app and UDP-to-WebSocket relay, concurrent race streams, synchronized state, and deterministic test replay.
- **AI-assisted compliance, in development:** source material, domain rules, permissions, and traceable actions, with explicit authority and verifiable results. The aim is to connect proposed actions to their sources and permissions.

---

[Browse repositories](https://github.com/yabanana?tab=repositories) · [Upstream contributions](https://github.com/pulls?q=is%3Apr+author%3Ayabanana+-user%3Ayabanana)
