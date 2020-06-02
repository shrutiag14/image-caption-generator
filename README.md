

__Note__: This project is under active development. 
To generate a caption for any image in natural language, English. The architecture for the model is inspired from [1] by Vinyals et al. The module is built using [keras](https://keras.io/), the deep learning library. 

This repository serves two purposes:
- present/ discuss my model and results I obtained
- provide a simple architecture for image captioning to the community

## Model 

The Image captioning model has been implemented using the Sequential API of keras. It consists of three components:
1. __An encoder CNN model__: A pre-trained CNN is used to encode an image to its features. In this implementation VGG16 model[d] is used as encoder and with its pretrained weights loaded. The last softmax layer of VGG16 is removed and the vector of dimention (4096,) is obtained from the second last layer. 

	_To speed up my training, I pre-encoded each image to its feature set. This is done in the `prepare_dataset.py` file to form a resultant pickle file `encoded_images.p`. In the current version, the image model takes the (4096,) dimension encoded image vector as input. This can be overrided by uncommenting the VGG model lines in `caption_generator.py`. There is no fine tuning in the current version but can be implemented._

2. __A word embedding model__: Since the number of unique words can be large, a one hot encoding of the words is not a good idea. An embedding model is trained that takes a word and outputs an embedding vector of dimension (1, 128).

	_Pre-trained word embeddings can also be used._

3. __A decoder RNN model__: A LSTM network has been employed for the task of generating captions. It takes the image vector and partial captions at the current timestep and input and generated the next most probable word as output. 

The overall architecture of the model is described by the following picture. It also shows the input and output dimension of each layer in the model. 

<div align="center">
  <img src="vis/model.png"><br><br>
</div>

## Dataset
The model has been trained and tested on Flickr8k dataset[2]. There are many other datasets available that can used as well like:	
- Flickr30k
- MS COCO
- SBU
- Pascal
----------------------------------

## Requirements 
- tensorflow
- keras
- numpy
- h5py
- pandas
- Pillow

These requirements can be easily installed by:
	`pip install -r requirements.txt`


