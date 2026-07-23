<p align="center">
  <a href="https://dau.dev">
    <img width="160" src="https://github.com/dau-dev.png?size=320" alt="dau logo" />
  </a>
</p>
<p align="center">
  <code>Data. Accelerated.</code>
  <br />
  <code>by <a href="https://1kbgz.com">1kbgz</a>.</code>
</p>

<p align="center">
  <a href="https://dau.dev"><b>dau.dev</b></a> ·
  <a href="https://github.com/dau-dev/dau-build">Build tools</a> ·
  <a href="https://github.com/dau-dev/dau-sim">Simulation</a> ·
  <a href="https://github.com/dau-dev/artlink">Artifacts</a>
</p>

---

[**dau**](https://dau.dev) is a modular hardware/software platform for accelerating analytical
workflows. It captures dataframe plans, maps supported work onto composable FPGA operator tiles, and
keeps unsupported work in familiar host software.

The execution model is selective and explicit:

```text
Polars lazy plan
    → capture and type the operation graph
    → compile supported fragments against the tile palette
    → compare the required design with the resident device
    → run now | build a right-sized configuration | return typed CPU residue
```

Fixed-width Arrow-derived streams carry data across PCIe. Capability contracts describe what a
resident configuration can execute. Declarative build specs connect the same design description to
simulation, synthesis, packaging, flashing, and smoke testing.

### Design principles

- **Selective offload:** accelerate operations that benefit from streaming hardware; preserve
  explicit CPU fallback for everything else.
- **Tile-aware compilation:** compile dataframe and domain expressions onto reusable operator,
  storage, and routing tiles.
- **Workload-shaped configurations:** use observed plans and measurements to right-size future
  device configurations instead of treating one bitstream as universal.
- **Artifact-first workflows:** package generated HDL, constraints, bitstreams, reports, and
  capability metadata as typed, traceable artifacts.
- **In-silica validation:** test golden semantics and composed workflows in simulation before
  measuring the same contracts on physical FPGA hardware.

### Public developer projects

- [**dau-build**](https://github.com/dau-dev/dau-build) — declarative FPGA build specs, generated
  SystemVerilog, artifact bundles, Vivado/yosys handoff, and task orchestration.
- [**dau-sim**](https://github.com/dau-dev/dau-sim) — cycle-accurate simulation for Amaranth,
  SystemVerilog, and hand-constructed hardware IR.
- [**artlink**](https://github.com/dau-dev/artlink) — domain-neutral artifact manifests, validation
  templates, composition, and registry discovery.

### Private platform components

- **dau** — end-user Python API.
- **dau-polars** — Polars plan capture, tile compilation, selective execution, and CPU fallback.
- **dau-core** — capability contracts, golden semantics, stream protocols, and reusable HDL tiles.
- **dau-driver** — device discovery, register access, DMA, codecs, and execution helpers.
- **dau-utils** — shared host utilities.

The accelerator implementation, hardware-lab integration, datasets, and some validation evidence
remain private while the platform develops. Public `dau` projects are released under the Apache 2.0
License unless a repository states otherwise.

**Current status:** end-to-end market-data aggregation workflows have run on FPGA and matched CPU
goldens. Current work expands operator coverage, runtime scheduling, result streaming, and throughput.
