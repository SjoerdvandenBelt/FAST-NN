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
- `-m train` for training a model, `-m predict` for inference
- `-p cpu` for CPU, `-p cuda` for GPU use (requires Pytorch CUDA support)
- `-t` number of threads Pytorch is allowed to use
- `-a` filename for logging training information (training / validation accuracies, etc)
- `-r` if loading binary DAF data, set to 1, otherwise set to 0
- `-e` number of epochs to train
- `-i` path to dataset
- `-o` for training, output path to save model, for inference, output path to save inference results
- `-d` only for inference, path to directory where model is saved
- `-h` number of samples on input data
- `-w` number of SNPs per input image/binary
- `-c` set to `-c FAST-NN` to select FAST-NN model for trainin and inference
- `-f` set to 1 if loading binary SNP data, if using images, set to 0
- `-x` set 1 to use SNP distance data in inference and training, note this data should be included in the binary/image data
- `-b` batch size to use
- `y` set to 0 (currently not supported)

## Example datasets
Three datasets are provided, which contain SNP and derived allele frequency data, based on the OutOfAfrica-3G09 model by Gutenkunst et al. (2009) [1].
The BINFRQPOS datasets contain derived allele frequency data with SNP position data, in binary format. The BINSNPPOS datasets contain SNP matrix data with SNP positions, in binary format. The 2DSNP datasets contain SNP matrix data without SNP positions, in image format.

## Example commands
We provide example commands to use with the provided datasets.

Training using derived allele frequency data (with SNP distance data):
`python main.py -m train -p "cpu" -t 1 -a "train.log" -r 1 -e 20 -i "TrainingDataBINFRQPOS" -o "models/BINFRQPOS/" -h 128 -w 128 -c "FAST-NN" -f 1 -x 1
 -b 8 -y 0`

Training using binary SNP data (with SNP distance data):
`python main.py -m train -p "cpu" -t 1 -a "train.log" -r 0 -e 20 -i "TrainingDataBINSNPPOS" -o "models/BINSNPPOS/" -h 128 -w 128 -c "FAST-NN" -f 1 -x 1
 -b 8 -y 0`

Training using image SNP data (without SNP distance data):
`python main.py -m train -p "cpu" -t 1 -a "train.log" -r 0 -e 20 -i "TrainingData2DSNP" -o "models/2DSNP/" -h 128 -w 128 -c "FAST-NN" -f 0 -x 0 -b 8 -y
 0`


Inference using derived allele frequency data (with SNP distance data):
`python main.py -m predict -p "cpu" -t 1 -r 0 -i "TestData2DSNP" -d "models/2DSNP/" -o "results/2DSNP/" -h 128 -w 128 -c "FAST-NN" -f 0 -x 0 -b 8 -y 0

Inference using binary SNP data (with SNP distance data):
`python main.py -m predict -p "cpu" -t 1 -r 0 -i "TestDataBINSNPPOS" -d "models/BINSNPPOS/" -o "results/BINSNPPOS/" -h 128 -w 128 -c "FAST-NN" -f 1 -x
1 -b 8 -y 0`

Inference using image SNP data (without SNP distance data):
`python main.py -m predict -p "cpu" -t 1 -r 1 -i "TestDataBINFRQPOS" -d "models/BINFRQPOS/" -o "results/BINFRQPOS/" -h 128 -w 128 -c "FAST-NN" -f 1 -x 1 -b 8 -y 0`

[^1]: Gutenkunst, R. N., Hernandez, R. D., Williamson, S. H., & Bustamante, C. D. (2009).
Inferring the joint demographic history of multiple populations from multidimensional SNP frequency data.
PLoS genetics, 5(10), e1000695. https://doi.org/10.1371/journal.pgen.1000695

