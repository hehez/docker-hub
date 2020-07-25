# The ViennaRNA (RNAfold)

## This is an optimized docker image for The ViennaRNA (RNAfold)

  - Alpine Linux:3.12
  - ViennaRNA-2.4.14

## Images
  - The image from Dockerfile-whole is ***~700MB*** (deprecated)
  - The image from Dockerfile is ***~116MB***
    > Multi-stage builds are a new feature requiring Docker 17.05 or higher on the daemon and client.

## How to use it
Run `make` to see more details

#### Build an image
```shell
make build
```

#### Run RNAfold with fasta format file (i.e. test.fasta) in **input** directory, check screen and **output** directory to see the result 
```shell
make rnafold name=test.fasta
```

### FQA
It works on MacOS 10.14.6 (Mojave).  
Compile failed at line `19258` in original configure file. One line change will work on Alpine Linux.

```shell
osx_arch_array=( ${enable_universal_binary} )
```
&#8595;&#8595;&#8595;&#8595;&#8595;
```shell
osx_arch_array= ${enable_universal_binary}
```