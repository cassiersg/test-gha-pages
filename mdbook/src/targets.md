# Targets

The target for this challenges are all instantiations of
[AES-HPC](https://github.com/simple-crypto/aes_hpc) on FPGAs.
AES-HPC is a masked implementation of the AES-128 encrypt function.
For the challenge, we instantiate it at the first and second-order security (\\(d=2,3\\)).
For more details, see the [AES-HPC documentation](TODO).

We have two FPGA targets: the [Chipwhisperer CW305]() with an Artix-7 Xilinx
FPGA and the [Sakura-G]() with a Spartan-6 FPGA.

The challenge for the Artix-7 target is in a fully white-box profiled setting:
the full implementation is open-source, including the bitstream.
The profiling datasets for this target include the full seed randomness,
therefore the complete state of the FPGA is known for the profiling traces.
Refer to [Artix-7](./artix7.md) for detailled explanations.

For the Spartan-6, the profiling setting is more constrained: only the AES-HPC
core is open-source, and the remaining part of the design is kept secret.
The profiling datasets for this target only contain the value of the key and
the plaintext.
Of course challenge participants can run their own instance of AES-HPC on a
Sakura-G, or use the Artix-7 dataset as a starting point for a Spartan-6
attack. Refer to [Spartan-6](./spartan6.md) for detailled explanations.
