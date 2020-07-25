# mfold

## This is a docker image for mfold

  - Alpine Linux:3.12
  - mfold-3.6

## Images
The lite version is ***~15.9MB***, no pdf output \
The regular version is ***~118MB***

## How to use it
Run `make` to see more details

#### Build an image
```shell
make build
```

#### Run RNAfold with fasta format file (i.e. test.fasta) in **input** directory, check screen and **output** directory to see the result 
```shell
make mfold name=test.fasta
```