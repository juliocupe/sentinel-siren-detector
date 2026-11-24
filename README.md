# Sentinel: an always-on siren detector chip

**Status: work in progress. Step 1 of 7 (Verilog basics: a counter and its testbench). No results yet.**

Sentinel is a small digital chip, written in SystemVerilog, that listens to audio and raises a flag when it hears a siren. I am building it from zero HDL experience and plan to submit it to Tiny Tapeout.

## Why I'm building it
Last summer I worked on classifying urban sounds (including sirens) with a CNN in Python. Python on a laptop is not something that can run all day on a tiny battery. I want to learn what it takes to do a small version of that job in hardware: a few simple filters and a tiny classifier that use very little area and power.

See my software project: [urban-sound-stability-cnn](https://github.com/juliocupe/urban-sound-stability-cnn)

## What I did vs. what I built on
- This is an individual project.
- I am learning with Claude (Anthropic) as a tutor and reviewer. I write the code myself. If any file contains AI-written code, the file will say so.
- Ideas and tools I build on will be credited in the Credits section as I use them.

## Planned design (nothing below is built yet)
1. Serial audio input and a small async FIFO that crosses clock domains safely.
2. A bank of Goertzel filters (4 to 8 frequency bins) that share one multiplier over time.
3. A cheap log2 using a leading-one detector.
4. An energy gate, so the chip stays quiet when the room is quiet.
5. A tiny 8-bit classifier (one neuron to start).
6. Smoothing: raise the flag only if k of the last n decisions say siren.
7. Check the hardware bit for bit against a fixed-point Python model, using UrbanSound8K clips.

The size target is one Tiny Tapeout tile on SkyWater 130 nm (about 1000 cells). TO CONFIRM against the current Tiny Tapeout docs before I design to it.

## Roadmap
| Step | What | Status |
|---|---|---|
| 1 | Verilog basics: counter and testbench | Ongoing |
| 2 | Async FIFO, with assertions, cocotb tests and a formal proof | Planned |
| 3 | Goertzel filter bank, bit-exact against the Python model, with coverage | Planned |
| 4 | Classifier, smoothing and top level | Planned |
| 5 | Tiny Tapeout submission (estimated May 2027, TO CONFIRM) | Planned |
| 6 | Second project: single-cycle RISC-V core | Planned |
| 7 | RISC-V core: 5-stage pipeline on an FPGA | Planned |

Steps 6 and 7 may move to their own repo.

## Results
None yet. Simulation output, waveforms, synthesis and timing numbers will be added here as I measure them, with what they were measured on.

## Tools
Planned: Icarus Verilog, GTKWave, cocotb, Yosys, SymbiYosys, Verilator, Python. Versions will be listed once installed.

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
I am at the very start. Next: get the simulator working, write a counter myself, and test it with a testbench.

## License
MIT. See [LICENSE](LICENSE).
