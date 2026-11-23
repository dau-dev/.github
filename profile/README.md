<p align="center">
  <a href="https://dau.dev">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://github.com/dau-dev/.github/raw/main/profile/lockup-on-shadow.svg" />
      <source media="(prefers-color-scheme: light)" srcset="https://github.com/dau-dev/.github/raw/main/profile/lockup-on-lit.svg" />
      <img width="280" src="https://github.com/dau-dev/.github/raw/main/profile/lockup-on-lit.svg" alt="dau" />
    </picture>
  </a>
</p>
<p align="center">
  <code>Data. Accelerated.</code>
  <br />
  <code>by <a href="https://1kbgz.com">1kbgz</a>.</code>
</p>

<p align="center">
  <a href="https://dau.dev"><b>dau.dev</b></a> ·
  <a href="https://github.com/dau-dev/dau-core">Core IP</a> ·
  <a href="https://github.com/dau-dev/dau-driver">Driver</a> ·
  <a href="https://github.com/dau-dev/dau-scheduler">Scheduler</a> ·
  <a href="https://github.com/dau-dev/dau-build">Build tools</a> ·
  <a href="https://github.com/dau-dev/dau-sim">Simulation</a>
</p>

---

[**dau**](https://dau.dev) is a framework for building and running calculations
on an FPGA accelerator composed of expression-backed hardware tiles.
It takes a lazy Polars query, offloads whatever it can to the FPGA,
and runs the rest on the CPU.
It can also design a slate of hardware tiles based on the query itself, so you
can build custom hardware specific to your operation.

```text
Polars lazy plan
    → capture and type the operation graph
    → compile the supported parts onto tiles from the catalog
    → compare the required design with what the device holds
    → run now | build a configuration for the workload | run on the CPU and report why
```

Data crosses PCIe as fixed-width streams derived from Arrow. A capability contract describes what
the configuration on the device can run. One declarative build spec drives simulation, synthesis,
packaging, flashing and smoke testing for a design.

### Design principles

- **Selective offload.** Accelerate the operations that gain from streaming hardware, and keep an
  explicit CPU fallback for everything else.
- **Tiles and cores.** A tile is an operation to which a Polars expression maps. Each tile is built
  from cores, the reusable hardware blocks for operators, storage and routing.
- **A configuration per workload.** Observed plans and measurements choose what goes into the next
  device configuration. No single bitstream is expected to cover every workload.
- **Artifacts first.** Package generated HDL, constraints, bitstreams, reports and capability
  metadata as typed, traceable artifacts.
- **Validate in simulation, then on silicon.** Test golden semantics and composed workflows in
  simulation before measuring the same contracts on an FPGA.

### Developer projects

- [**dau-build**](https://github.com/dau-dev/dau-build): declarative FPGA build specs, generated
  SystemVerilog, artifact bundles, Vivado and yosys handoff, and task orchestration.
- [**dau-sim**](https://github.com/dau-dev/dau-sim): cycle-accurate simulation for Amaranth,
  SystemVerilog and hand-constructed hardware IR.
- [**dau-utils**](https://github.com/dau-dev/dau-utils): host utilities for FPGA bench machines.
- [**artlink**](https://github.com/dau-dev/artlink): domain-neutral artifact manifests, validation
  templates, composition and registry discovery.

### Platform components

These make up the accelerator itself. dau-core, dau-scheduler and dau-driver are public, and dau
and dau-polars will be public soon.

- [**dau-core**](https://github.com/dau-dev/dau-core): the HDL cores and their golden models, the
  tile catalog, capability contracts and stream protocols.
- [**dau-scheduler**](https://github.com/dau-dev/dau-scheduler): work splitting between host and
  device, and the measured profiles it uses.
- [**dau-driver**](https://github.com/dau-dev/dau-driver): device discovery, register access, DMA,
  codecs and execution helpers.
- **dau**: end-user Python API, and the designs and board definitions the other packages build.
- **dau-polars**: Polars plan capture, compilation onto tiles, the host and device split, and CPU
  fallback.

Public `dau` projects are released under the Apache 2.0 License unless a repository states
otherwise.
