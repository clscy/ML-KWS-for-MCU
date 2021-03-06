# Keyword spotting for Microcontrollers 

This repository consists of the tensorflow models and training scripts used 
in the paper: 
[Hello Edge: Keyword spotting Microcontrollers](https://arxiv.org/pdf/1711.07128.pdf). 
The scripts are adapted from [Tensorflow examples](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/speech_commands) 
and some are repeated here for the sake of making these scripts self-contained.

To train a DNN with 3 fully-connected layers with 128 neurons in each layer, run:

```
python train.py --model_architecture dnn --model_size_info 128 128 128 
```
The command line argument *--model_size_info* is used to pass the neural network layer
dimensions such as number of layers, convolution filter size/stride as a list to models.py, 
which builds the tensorflow graph based on the provided model architecture 
and layer dimensions. 
For more info on *model_size_info* for each network architecture see 
[models.py](models.py).
The training commands with all the hyperparameters to reproduce the models shown in the 
[paper](https://arxiv.org/pdf/1711.07128.pdf) are given [here](train_commands.txt).

To run inference on the trained model from a checkpoint on train/val/test set, run:
```
python test.py --model_architecture dnn --model_size_info 128 128 128 --checkpoint 
<checkpoint path>
```

To freeze the trained model checkpoint into a .pb file, run:
```
python freeze.py --model_architecture dnn --model_size_info 128 128 128 --checkpoint 
<checkpoint path> --output_file dnn.pb
```

## Pretrained models

Trained models (.pb files) for different neural network architectures such as DNN,
CNN, Basic LSTM, LSTM, GRU, CRNN and DS-CNN shown in 
this [arXiv paper](https://arxiv.org/pdf/1711.07128.pdf) are added in 
[Pretrained_models](Pretrained_models).
To run an audio file through the trained model (e.g. a DNN) and get top prediction, 
run:
```
python label_wav.py --wav <audio file> --graph Pretrained_models/DNN/DNN_S.pb 
--labels Pretrained_models/labels.txt --how_many_labels 1
```
