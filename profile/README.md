<p align="center">
  <a href="https://dau.dev">
    <img width="160" src="https://dau.dev/img/dau-dark.png" alt="DAU logo" />
  </a>
</p>
<p align="center">
  <code>Data. Accelerated.</code>
  <br />
  <code>by <a href="https://1kbgz.com">1kbgz</a>.</code>
</p>

<p align="center">
  <a href="https://dau.dev"><b>dau.dev</b></a> ·
  <a href="https://github.com/dau-dev/dau">Python API</a> ·
  <a href="https://github.com/dau-dev/dau-polars">Polars frontend</a> ·
  <a href="https://github.com/dau-dev/dau-build">Build tools</a> ·
  <a href="https://github.com/dau-dev/dau-sim">Simulation</a>
</p>

---

[**DAU**](https://dau.dev) is a hardware/software stack for accelerating analytical queries.
It maps SQL-style operators onto a reconfigurable, tile-based FPGA dataflow engine, moves
fixed-width Arrow record batches over PCIe, and drives execution from Python dataframe workflows.

The long-term shape is a database processing unit: host-analyzed query plans, composable operator
tiles, a host-configured on-chip network, explicit CPU fallback for unsupported plan fragments, and
repeatable build/simulation flows for FPGA targets.

- **Frontend:** lazy Polars integration for selective pushdown of supported operators.
- **Runtime:** Python APIs, device discovery, register access, DMA helpers, Arrow-derived stream codecs, and result rematerialization.
- **Hardware:** reusable SystemVerilog operator tiles with golden software models, cocotb benches, and Verilator benches.
- **Build flow:** declarative specs, artifact manifests, Vivado/XDMA handoff, simulation, synthesis, flash, and smoke-test task surfaces.
- **Current status:** internal end-to-end market-data aggregation workloads have run on FPGA and matched CPU goldens.
- **Current focus:** broader operator coverage, runtime scheduling, result streaming, and throughput work.

### Public repos

- [**dau**](https://github.com/dau-dev/dau) - thin end-user Python API over stable DAU primitives.
- [**dau-polars**](https://github.com/dau-dev/dau-polars) - Polars frontend for selective FPGA pushdown with CPU fallback.
- [**dau-core**](https://github.com/dau-dev/dau-core) - hardware-facing contracts, golden semantics, stream protocols, and reusable HDL.
- [**dau-driver**](https://github.com/dau-dev/dau-driver) - DAU-compatible device discovery, registers, DMA, codecs, and execution helpers.
- [**dau-build**](https://github.com/dau-dev/dau-build) - build specs, artifact bundles, generated hardware handoff, and task orchestration.
- [**dau-sim**](https://github.com/dau-dev/dau-sim) - simulation infrastructure for digital hardware designs, including cocotb and Verilator integration.
- [**dau-utils**](https://github.com/dau-dev/dau-utils) - shared host utilities used by the stack.
- [**artlink**](https://github.com/dau-dev/artlink) - domain-neutral artifact manifests, validation templates, and registry/discovery helpers.
- [**website**](https://github.com/dau-dev/website) - source for [dau.dev](https://dau.dev).

### Public/private boundary

Some DAU development is proprietary or hardware-lab specific, including portions of the accelerator
implementation, bring-up evidence, datasets, and internal integration notes. Public repositories are
the stable surface for shared tooling, interfaces, examples, and open-source components. Open-source
DAU code is released under the Apache 2.0 License unless a repository states otherwise.
