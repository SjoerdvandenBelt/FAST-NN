# FAST-NN
This is the repository to use the FAST-NN CNN-based selective sweep classification method.

## Dependencies
To use FAST-NN, we recommend installing Python 3.10.11, with the following packages:
- Pytorch
- Torchvision
- Numpy

## Command line interface
To run FAST-NN, run:
`python main.py` with the following command line options:
`-m train` for training a model, `-m predict` for inference
`-p CPU` for CPU, `-p CUDA` for GPU use (requires Pytorch CUDA support)
`-t` number of threads Pytorch is allowed to use
`-a` filename for logging training information (training / validation accuracies, etc)
`-r` if loading binary DAF data, set to 1, otherwise set to 0
`-e` number of epochs to train
`-i` path to dataset
`-o` for training, output path to save model, for inference, output path to save inference results
`-d` only for inference, path to directory where model is saved
`-h` number of samples on input data
`-w` number of SNPs per input image/binary
`-c` set to `-c FAST-NN` to select FAST-NN model for trainin and inference
`-f` set to 1 if loading binary SNP data, if using images, set to 0
`-x` set 1 to use SNP distance data in inference and training, note this data should be included in the binary/image data
`-b` batch size to use
`y` set to 0 (currently not supported)
