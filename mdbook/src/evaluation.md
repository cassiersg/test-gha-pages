# Evaluation
In order to assess the quality of the implemented attack, the framework provides an evaluation tool. In particular, based on the `KeyGuess` instance produced, it computes an estimation of the 
rank of the correct key. In the context of the challenge, a successful attack is an attack that results in an estimated rank that is below \\( 2 ^ {64} \\) (see [Challenge rules](./rules.md)). The validation dataset is provided 
in order to make it possible for a user to verify that its attack is working properly. In particular, the following command 
```
python3 quick_eval.py eval --load-guess KGUESS_FILE_PATH --attack-case A_d2 --attack-dataset DS_DIR_PATH/fk0/manifest
```
allows to evaluate the `KeyGuess` instance saved in the file `KGUESS_FILE_PATH` based on the correct fixed key from the evaluation dataset.
The outcome of this command is that the rank estimated for the correct is key plotted on the standard output. 
It has to be noted that the exact same methodology will be used to evaluate the different submissions!  

As for the attack phase, it is possible to perform the evaluation step together with the other steps in a single command. One may 
consider the following command in order to execute the full flow
```
python quick_eval.py profile attack eval --profile-dataset DS_DIR_PATH/vk0/manifest --attack-case A_d2 --attack-dataset DS_DIR_PATH/fk0/manifest --n-attack-traces NT_ATCK
```
Please refer the the helper and the code of [quick_eval.py](TODO) to get more
information about the parameters that can be used in the framework. 
