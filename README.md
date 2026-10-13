<p align="center">
  <img src="https://raw.githubusercontent.com/yabanana/yabanana/main/assets/header.svg" alt="Daniele Giovane — Systems, graphics, and the software in between." width="100%" />
</p>

<p align="center">
  <a href="#open-source-contributions">Open source</a> &nbsp; / &nbsp;
  <a href="#personal-projects">Personal projects</a> &nbsp; / &nbsp;
  <a href="#beyond-public-repositories">Private work</a> &nbsp; / &nbsp;
  <a href="#how-i-work">How I work</a>
</p>

## Close to the machine. Connected to the whole system.

I'm **Daniele**, a systems and backend developer in Italy. I work on the boundaries where software gets interesting: between an instruction set and a compiler, a VPN and the operating system, a renderer and the GPU, or a service and the data it must keep consistent.

I like understanding a system deeply enough to **build it, explain its failures, and make it behave predictably**. My work spans native platform integration, compiler/runtime experiments, real-time graphics, parallel simulation, and backend products.

**C · C++ · Rust · Go · Java** &nbsp; / &nbsp; Python · TypeScript  
Apple silicon & Linux · Concurrency · Graphics · Distributed systems · Artificial life

## Open source contributions

### snx-rs · Bringing a VPN client to macOS

**Merged upstream.** I contributed the macOS platform backend, then followed it through hardening, desktop integration, and packaging. The work reaches from native networking APIs to the app people install:

- **Networking:** utun interfaces, routing sockets, split DNS through SystemConfiguration, and Keychain integration.
- **Reliability and security:** local command-socket peer authorization, crash recovery for network state, and parser tests.
- **Desktop and delivery:** menu-bar GUI, WebKit login, native notifications, launchd service, and DMG/PKG release tooling.

[Platform port #227](https://github.com/ancwrd1/snx-rs/pull/227) · [Hardening #229](https://github.com/ancwrd1/snx-rs/pull/229) · [GUI #230](https://github.com/ancwrd1/snx-rs/pull/230) · [Packaging #231](https://github.com/ancwrd1/snx-rs/pull/231)

### rust-lang/libc · Filling a gap in Apple's platform bindings

**Merged upstream.** I added missing socket and network-interface `ioctl` constants for Apple targets, with checks against the native SDK headers and coverage of the crate's public API. Small surface area; careful attention to the OS interface underneath it.

[Read the patch → libc #5263](https://github.com/rust-lang/libc/pull/5263)

### AnyPS5 · Exploring native ARM64 ahead-of-time compilation

**Open PR series / experimental.** I'm developing an offline path from x86-64 ELF programs to native ARM64 code: instruction semantics, LLVM lowering, ABI boundaries, native providers, and the runtime needed to execute the result. Generated programs run without an x86 interpreter, JIT, or Rosetta dependency.

<details>
<summary><b>Explore the compiler, runtime, and validation work ↗</b></summary>

<br>

| Layer | Work in the PR series |
| :--- | :--- |
| **Binary recovery** | ELF metadata, relocations, sectionless images, unwind information, and explicit limits on recovered facts. |
| **Code generation** | A signature-qualified path and a whole-program path that preserves guest registers and stack; integer and SIMD instruction semantics lowered through LLVM. |
| **Runtime** | Native import providers, checked indirect transfers, module lifecycle, static TLS, C++ exception paths, and joinable guest workers. |
| **Memory ordering** | A bounded concurrent-memory profile, checked native atomics, and reference comparisons before performance changes. |
| **Graphics** | A source-built cube executed through the native ARM64 runtime, compared with an independently compiled reference using exact RGB frames. |

The series documents comparisons using **zstd**, **yaml-cpp**, instruction-level reference cases, and native graphics consumers. These are bounded compiler/runtime results; **commercial-game compatibility remains unproven**.

[Compiler foundation #1835](https://github.com/boykopovar/AnyPS5/pull/1835) · [Graphics #3891](https://github.com/boykopovar/AnyPS5/pull/3891) · [Whole-program lowering #4599](https://github.com/boykopovar/AnyPS5/pull/4599) · [C++ / TLS #4718](https://github.com/boykopovar/AnyPS5/pull/4718) · [Concurrency #4740](https://github.com/boykopovar/AnyPS5/pull/4740) · [Atomics #4813](https://github.com/boykopovar/AnyPS5/pull/4813)

Separate, merged contributions include [macOS unwind register contexts #1499](https://github.com/boykopovar/AnyPS5/pull/1499) and [graphics descriptor-array snapshots #1831](https://github.com/boykopovar/AnyPS5/pull/1831).

</details>

## Personal projects

| Project | What I'm exploring |
| :--- | :--- |
| **[Phosphor](https://github.com/yabanana/phosphor)** | A C++20 renderer built around **Metal 4 and Apple silicon**: GPU-driven geometry, explicit resource lifetimes, ray tracing, and MetalFX. An experimental renderer with documented measurements and open quality/performance gates. |
| **[LENIA-3D](https://github.com/yabanana/LENIA-3D)** | **Artificial life through continuous cellular automata.** 2D/3D simulation, FFT convolution, OpenMP, interactive isosurfaces, and parameter searches for emergent behavior. |
| **[ParallelWatorCA](https://github.com/yabanana/ParallelWatorCA)** | Predator–prey simulation using **hybrid MPI + OpenMP**, exploring how work is divided across processes and threads. |
| **[Fildem](https://github.com/yabanana/Fildem)** | My fork and rewrite of the GNOME global-menu project: a **C/GObject core**, session daemon, versioned D-Bus interfaces, Shell extension, and GTK4 HUD. |

<details>
<summary><b>Earlier experiments ↗</b></summary>

<br>

**[VulkanTorus](https://github.com/yabanana/VulkanTorus)** explores explicit GPU setup, swapchains, command buffers, and synchronization in C++/Vulkan on Linux. **[FlappyD](https://github.com/yabanana/FlappyD)** is an earlier Java game project around real-time loops, input, and state.

</details>

## Beyond public repositories

My private projects extend the same interests into software people interact with:

- **Sim-racing operations:** a booking and event platform built with Go, PostgreSQL, and web/mobile clients; tenant isolation, background jobs, and rules enforced on the backend.
- **Live race telemetry:** a Go desktop application and UDP-to-WebSocket relay, with concurrent race streams, synchronized state, and deterministic replay for testing.
- **AI-assisted compliance workflows, in development:** connecting source material, domain rules, permissions, and traceable actions. I'm interested in making AI useful inside systems with explicit authority and verifiable results.

## How I work

**Correctness first. Measure next. Optimize what matters.**

I follow problems across layers: from an API symptom to a database transaction, from a broken tunnel to routing state, from a rendered frame to GPU resource ownership. I value small reproducible cases, independent reference results, explicit failure paths, and clear boundaries between what is implemented and what is verified.

The questions that keep pulling me back: **How does this execute? Where does the time go? What happens under concurrency or failure? What complex behavior can emerge from simple rules?**

---

<p align="center">
  <b>Building things I want to understand — and making that understanding useful.</b><br><br>
  <a href="https://github.com/yabanana?tab=repositories">Browse repositories</a> &nbsp; · &nbsp;
  <a href="https://github.com/pulls?q=is%3Apr+author%3Ayabanana+-user%3Ayabanana">Explore upstream contributions</a>
</p>
