# Neural Sign Language Processing With Language Models

This code is based on the implementation of [Sign Language Transformers: Sign Language Transformers: Joint End-to-end Sign Language Recognition and Translation](https://www.cihancamgoz.com/pub/camgoz2020cvpr.pdf), available [here](https://github.com/neccam/slt) and [Frozen Pretrained Transformers for Neural Sign Language Translation](https://users.ugent.be/~mcdcoste/assets/SLT_DeCoster2021Frozen.pdf), available [here](https://github.com/m-decoster/fpt4slt).

 
## Requirements
* Download the feature files using the `data/download.sh` script into the data directory.

* [Optional] Create a conda or python virtual environment.

* Install required packages using the `requirements.txt` file.

    `pip install -r requirements.txt`

* The correct pytorch version is required with GPU support but since the version used is a lot older and replicating it might create issues with CUDA, I have attached a colab environment [here](https://colab.research.google.com/drive/1ur1rVWgLVdi4DJiDQ0YHlk8UBekKmFZf?usp=sharing) which should be able to run it.

## Usage

As mentioned above I have attached a colab environment [here](https://colab.research.google.com/drive/1ur1rVWgLVdi4DJiDQ0YHlk8UBekKmFZf?usp=sharing) which should be able to run it.

Choose the configuration file that you want to reproduce and update the `data.data_path` and `training.model_dir` configuration entries
to the path where your data resides (default: `data/PHOENIX2014T`) and the path where you want the experiment logs and checkpoints to be saved.

  `python -m signjoey train configs/$CONFIG.yaml` 

For the mBART-50 model, you will first need to tokenize the corpus using the mBART-50 tokenizer. You can use the `tokenization/tokenize_mbart50.py` script for this, but the mbart model performs very poorly so we can ignore that and try some of our example config files:

#### Training time on a RTX3070 not including evaluation time

### DeCoster - 2021 - bert2rnd
`python -m signjoey train configs\lc\s2gt\phoenix14t_bert2rnd_50.yaml`

logs: logs/learning_curves/sign2glosstext/phoenix14t_bert2rnd/50/

Training time: 1 hr 46 mins

https://tensorboard.dev/experiment/3D6N6NznQsac1E2N8Vr8nA

DEV: BLEU-4: 19.20

TES: BLEU-4: 19.44


### Our Model - bert2rnd_50_multilingualBert
`python -m signjoey train configs\lc\s2gt\phoenix14t_bert2rnd_50_multilingualBert.yaml`

Best Bleu 4 from validation: 18.81

logs: logs/learning_curves/sign2glosstext/phoenix14t_bert2rnd_multilingual/50/

Training time: 2 hr 38 mins

https://tensorboard.dev/experiment/uzqSdt07QqGniE9EbvMbxg/

DEV: BLEU-4: 19.02

TES: BLEU-4: 19.25


### Our Model - bert2rnd_germanBert
`python -m signjoey train configs\lc\s2gt\phoenix14t_bert2rnd_50_germanBert.yaml`

logs: logs/learning_curves/sign2glosstext/phoenix14t_bert2rnd_german/50/

Training time: 53 mins

https://tensorboard.dev/experiment/auxQWNxORayQi6l6V4dlEQ

DEV: BLEU-4: 17.87

TES: BLEU-4: 18.93


### DeCoster - 2021 - bert2bert
`python -m signjoey train configs\lc\s2gt\phoenix14t_bert2bert_50.yaml`


logs: logs/learning_curves/sign2glosstext/phoenix14t_bert2bert/50/

Training time: 1 hr 9 mins

https://tensorboard.dev/experiment/beTaoOvnT56vjYHabpG1Zw

DEV: BLEU-4: 18.44

TES: BLEU-4: 18.65

### Camgoz - 2020 - No pretrained model

`python -m signjoey train configs\lc\s2gt\phoenix14t_50.yaml`

logs: logs/learning_curves/sign2glosstext/phoenix14t/50/

Training time: 2 hr 41 mins

https://tensorboard.dev/experiment/RSZ71yigT3a3xqykNF2P0Q

DEV: BLEU-4: 18.61

TES: BLEU-4: 18.32


### Our Model - bert2bert_50_germanBert
`python -m signjoey train configs\lc\s2gt\phoenix14t_bert2bert_50_germanBert.yaml`

logs: logs/learning_curves/sign2glosstext/phoenix14t_bert2bert_german/50/

Training time: 44 mins

https://tensorboard.dev/experiment/pe6IziXZQNiKIACrJ7dzMw/

DEV: BLEU-4: 17.76

TES: BLEU-4: 17.64


## Citations

```
@InProceedings{De_Coster_2021_AT4SSL,
    author    = {De Coster, Mathieu and D'Oosterlinck, Karel and Pizurica, Marija and Rabaey, Paloma and Verlinden, Severine and Van Herreweghe, Mieke and Dambre, Joni},
    title     = {Frozen Pretrained Transformers for Neural Sign Language Translation},
    booktitle = {1st International Workshop on Automated Translation for Signed and Spoken Languages},
    month     = {August},
    year      = {2021},
}

@inproceedings{camgoz2020sign,
  author = {Necati Cihan Camgoz and Oscar Koller and Simon Hadfield and Richard Bowden},
  title = {Sign Language Transformers: Joint End-to-end Sign Language Recognition and Translation},
  booktitle = {IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
  year = {2020}
}

@article{info13050220,
	Article-Number = {220},
	Author = {De Coster, Mathieu and Dambre, Joni},
	Doi = {10.3390/info13050220},
	Issn = {2078-2489},
	Journal = {Information},
	Number = {5},
	Title = {Leveraging Frozen Pretrained Written Language Models for Neural Sign Language Translation},
	Url = {https://www.mdpi.com/2078-2489/13/5/220},
	Volume = {13},
	Year = {2022}
}
```
