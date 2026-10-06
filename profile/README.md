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

[**dau**](https://dau.dev) is a hardware and software platform for speeding up analytical work. It
captures dataframe plans, runs the parts an FPGA can take on composable operator tiles, and leaves
the rest in ordinary host software.

The device never runs everything, and you always see what it runs:

```text
Polars lazy plan
    → capture and type the operation graph
    → compile the supported fragments against the tile palette
    → compare the required design with what the device holds
    → run now | build a right-sized configuration | hand back typed CPU residue
```

Data crosses PCIe as fixed-width streams derived from Arrow. A capability contract describes what
the configuration on the device can run. One declarative build spec drives simulation, synthesis,
packaging, flashing and smoke testing for a design.

### Design principles

- **Selective offload.** Accelerate the operations that gain from streaming hardware, and keep an
  explicit CPU fallback for everything else.
- **Tile-aware compilation.** Compile dataframe and domain expressions onto reusable operator,
  storage and routing tiles.
- **Workload-shaped configurations.** Use observed plans and measurements to size the next device
  configuration, rather than treating one bitstream as universal.
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

These make up the accelerator itself. They are private today and are being prepared for public
release; the plan is for all of the code to be open, with the boards as the product.

- **dau**: end-user Python API and the integration home for designs and platforms.
- **dau-polars**: Polars plan capture, tile compilation, selective execution and CPU fallback.
- **dau-core**: capability contracts, golden semantics, stream protocols and reusable HDL tiles.
- **dau-driver**: device discovery, register access, DMA, codecs and execution helpers.
- **dau-scheduler**: work splitting between host and device, and the measured profiles it uses.

Public `dau` projects are released under the Apache 2.0 License unless a repository states
otherwise.

**Current status:** TPC-H and market-data aggregation workloads have run end to end on FPGA and
matched their CPU results bit for bit. A query can run on the device, on the CPU, or split between
the two, and the split is chosen from measured costs. Current work is on operator coverage, the cost
model, and the next board.
