# Neural Baby Talk

This is FDU nndl pj3, and I reproduced Neural Baby Talk for novel object captioning. Thanks to [@Jiasen Lu](https://github.com/jiasenlu) for his paper and his original implementation in python 2.7.

Here is the results:

|        | bottle | bus  | couch | microwave | pizza | racket | suitcase | zebra | Avg      |
| ------ | ------ | ---- | ----- | --------- | ----- | ------ | -------- | ----- | -------- |
| F1     | 11.1   | 74.2 | 46.1  | 66        | 69.5  | 32.2   | 53.1     | 90.3  | 55.3125  |
| SPICE  | 15.2   | 15.9 | 17.3  | 17.9      | 17.1  | 16.7   | 13       | 16.9  | 16.25    |
| METEOR | 22.4   | 21   | 25.1  | 25.2      | 22.9  | 24.3   | 19.6     | 0.242 | 20.09275 |
| CIDEr  | 75.4   | 44.5 | 61.5  | 62        | 49.7  | 31.5   | 54.8     | 0.452 | 47.4815  |

## requirement

Inference:
Python 3.6 is used. Please refer to `requirements.txt` for the required packages.

Data Preparation:

- [stanford-corenlp](https://stanfordnlp.github.io/CoreNLP/)

Evaluation:

- [coco-caption](https://github.com/jiasenlu/coco-caption): Download the modified version of coco-caption and put it under `tools/`

## Training and Evaluation

### Data Preparation
Head to `data/README.md`, and prepare the data for training and evaluation.
Also, you need to download pretrained weights of resnet101 into `data/imagenet_weights/resnet101.pth`.

### Novel Object Captioning

##### Training and Evaluation
Modify the cofig file `cfgs/noc_coco_res101.yml` with the correct file path. And `opts.py` for other training options. Then run the following command to train the model.

```
python main.py
```

## Demo

#### Constraint beam search
This code also involve the implementation of constraint beam search proposed by Peter Anderson. I'm not sure my impmentation is 100% correct, but it works well in conjuction with neural baby talk code. You can refer to [this](http://users.cecs.anu.edu.au/~sgould/papers/emnlp17-constrained-beam-search.pdf) paper for more details. To enable CBS while decoding, please set the following flags:
```
--cbs True|False : Whether use the constraint beam search.
--cbs_tag_size 3 : How many detection bboxes do we want to include in the decoded caption.
--cbs_mode all|unqiue|novel : Do we allow the repetive bounding box? `novel` is an option only for novel object detection task.
```

