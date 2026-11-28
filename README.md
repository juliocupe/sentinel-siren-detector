# Sentinel: an always-on siren detector chip

**Status: work in progress. Step 1 of 7 (Verilog basics: a counter and its testbench). No results yet.**

Sentinel is a small digital chip, written in SystemVerilog, that listens to audio and raises a flag when it hears a siren. I am building it from zero HDL experience and plan to submit it to Tiny Tapeout.

## Why I'm building it
Last summer I worked on classifying urban sounds (including sirens) with a CNN in Python. Python on a laptop is not something that can run all day on a tiny battery. I want to learn what it takes to do a small version of that job in hardware: a few simple filters and a tiny classifier that use very little area and power.

See my software project: [urban-sound-stability-cnn](https://github.com/juliocupe/urban-sound-stability-cnn)

## What I did vs. what I built on
- This is an individual project.
- Ideas and tools I build on will be credited in the Credits section as I use them.

## Planned design (nothing below is built yet)
1. Serial audio input and a small async FIFO that crosses clock domains safely.
2. A bank of Goertzel filters (4 bins to start, up to 8) that share one multiplier over time. The number of bins is a setting in the code.
3. A cheap log2 using a leading-one detector.
4. Clock gating: the classifier's clock stops when the room is quiet. I plan to measure the saving in simulation against a version without gating.
5. A tiny 8-bit classifier (one neuron to start).
6. Smoothing: raise the flag only if k of the last n decisions say siren.
7. Check the hardware bit for bit against a fixed-point Python model, using UrbanSound8K clips.
8. A tradeoff study: accuracy against number of bins, bit width and chip area.

The size target is one Tiny Tapeout tile on SkyWater 130 nm (about 1000 cells). TO CONFIRM against the current Tiny Tapeout docs before I design to it. Cell count and timing will be logged at every step.

## Roadmap
| Step | What | Status |
|---|---|---|
| 1 | Verilog basics: counter and testbench | Ongoing |
| 2 | Async FIFO, with assertions, cocotb tests and a formal proof | Planned |
| 3 | Goertzel filter bank, bit-exact against the Python model, with coverage | Planned |
| 4 | Classifier, clock gating, smoothing, top level and the tradeoff study | Planned |
| 5 | Tiny Tapeout submission (estimated May 2027, TO CONFIRM) | Planned |
| 6 | Second project: single-cycle RISC-V core | Planned |
| 7 | RISC-V core: 5-stage pipeline on an FPGA | Planned |

Steps 6 and 7 will be in their own repo.

## Results
None yet. Simulation output, waveforms, synthesis and timing numbers will be added here as I measure them, with what they were measured on.

## Tools
Installed (Ubuntu on WSL, Windows 11): Icarus Verilog 12.0, GTKWave 3.3.126.
Planned for later steps: cocotb, Yosys, SymbiYosys, Verilator, Python.

## How to build and run
Not ready yet. Step 1 instructions will be added when the first simulation works.

## Layout
```
src/    SystemVerilog design files
test/   testbenches
docs/   waveforms and notes
model/  Python fixed-point model (added at step 3)
```

## What I'm learning and what's next
Simulator installed. Next: write a counter myself and test it with a testbench.

## License
MIT. See [LICENSE](LICENSE).
