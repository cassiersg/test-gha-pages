# Framework

We provide a comprehensive python-based framework to develop and evaluate
attacks, available [on github](TODO).
This chapter is an overview of the framework, see its and in-code
documentation for more details.
In this overview, we assume that the attack is written in python, but the
framework [will also work with other languages](not_python.md).

## Contents

The framework is split in two parts:

- The code running the attack, given as a demonstration attack.
    This includes:
    * Loading the datasets.
    * Running a profiling step (optional).
    * Executing the attack itself.
    * Running a simplified evaluation for testing purpose.
- The scripts for building a submission package and evaluating it.

## Dependencies

The framework runs with `python >= 3.8`. We suggest using python's standard
library virtual environment module `venv`. On some python installations, this
is not included by default (e.g., you have to `apt install python3-venv` to get
it).

Additionally, the demonstration attack depends on
- [`Yosys`](https://yosyshq.net/yosys/)Yosys 0.25 (git sha1 e02b7f64b, gcc 9.4.0-1ubuntu1~20.04.1 -fPIC -Os) tested,
- [`verilator`](https://www.veripool.org/verilator/) Verilator 5.004 2022-12-14 rev v5.004-30-g8468af1a2 tested,
- [`Verime`](TODO) (TODO version / git commit)

## Getting started
We provide an example submission package that implements a simple profiled
attack in our evaluation framework.  The later has been designed to limit a
candidate's work to the implementation of two functions (one being optional,
the other being mandatory) from a single file ([attack.py](), see
[Profiling](profiling.md) and [Attack](attack.md)).  Next, we summarize the
steps that are required to run the demo attack in the evaluation framework. We
strongly encourage to develop your submission by tweaking this demo attack, as
it significantly reduces the work required to integrate your submission in our
evaluation framework.

1. Download the datasets. We next assume that `DS_DIR_PATH` is the path to the directory storing the different datasets (for a single target).
1. Clone the [challenge repository](TODO) (be sure to have the **submodules** with the `--recursive` option).
1. From the challenge repository, perform the following steps:
    1. Create a virtual environment for developing the attack:
        ```
        python3 -m venv demo_venv
        ```
        and **activate it**.
    2. Go in the demo attack directory
        ```
        cd example_submission_package
        ```
    2. Install the required dependencies.
        ```
        pip install --upgrade pip
        pip install -r requirements.txt
        ```
    3. Build the simulation library and install it (for more details, see [Target Simulation](target_simulation.md)):
        ```
        make -C ./simulations 
        pip install simulations/aeshpc_new_32bit_d2_lib/*.whl
        ```
    4. Run the profiling phase (for more details, see [Profiling](profiling.md)):
        ```
        mkdir workspace
        python3 quick_eval.py profile --profile-dataset DS_DIR_PATH/vk0/manifest --attack-case A_d2 --save-profile ./workspace
        ```
    5. Run the attack phase (for more details, see [Attack](attack.md)):
        ```
        python3 quick_eval.py attack --attack-dataset DS_DIR_PATH/fk0/manifest --n-attack-traces 1000000 --attack-case A_d2 --load-profile ./workspace --save-guess workspace/kg1e6_fk0
        ```
    6. Evaluate the attack (for more details, see [Evaluation](evaluation.md)):
        ```
        TODO
        ```
1. Start tweaking the demo into your own super effective attack!
1. Once your happy with your attack performance, see [Submission](submission.md) for packaging your submission.

