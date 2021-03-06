# Experiment

## ラベルの頻度毎に学習

### 500-400

#### only fold-0

|exp id|train|infer|local f0|local mAP|train soundscape|LB|detail|memo|
|--|--|--|--|--|--|--|--|--|
|exp0000|[code](https://github.com/trtd56/BirdCLEF/blob/main/works/notebook/BirdCLEF_Train_exp0000.ipynb)|[code](https://www.kaggle.com/takamichitoda/birdclef-infer-split-model?scriptVersionId=59153670)|0.9085||0.4923|0.43|baseline||
|exp0001|[code](https://github.com/trtd56/BirdCLEF/blob/main/works/notebook/BirdCLEF_Train_exp0001.ipynb)||||||loss masking|5 epochくらい学習したけどスコア上がらず|
|exp0002|[code](https://github.com/trtd56/BirdCLEF/blob/main/works/notebook/BirdCLEF_Train_exp0002.ipynb)|[code](https://www.kaggle.com/takamichitoda/birdclef-infer-split-model?scriptVersionId=59189961)|0.8166|0.9137|0.5558||先頭5sに固定, mAP優先|5 epochまでのBEST|
|exp0002|[code](https://github.com/trtd56/BirdCLEF/blob/main/works/notebook/BirdCLEF_Train_exp0002.ipynb)|[code](https://www.kaggle.com/takamichitoda/birdclef-infer-split-model?scriptVersionId=59189961)|0.8371|0.9138|0.2697|0.33|先頭5sに固定, mAP優先|5 epochでサチってるのでそんくらいでよさげ|
|exp0003||[code](https://www.kaggle.com/takamichitoda/birdclef-infer-split-model?scriptVersionId=59658911)|0.8268|0.9188|0.4335||先頭5sに固定, mAP優先, 5 epoch||
|exp0004|[code](https://github.com/trtd56/BirdCLEF/blob/main/works/notebook/BirdCLEF_Train_exp0004.ipynb)|[code](https://www.kaggle.com/takamichitoda/birdclef-infer-split-model?scriptVersionId=59673420)|0.8293|0.9308|0.5535||先頭5sに固定, mAP優先, 5 epoch, +ガウシアンノイズ||

#### 5 CV
|exp id|train|infer|CV mAP|train soundscape|LB|detail|memo|
|--|--|--|--|--|--|--|--|
|exp0003||[code](https://www.kaggle.com/takamichitoda/birdclef-infer-split-model?scriptVersionId=59538507)|0.9101|0.5701|0.50|baseline|||
|exp0004|[code](https://github.com/trtd56/BirdCLEF/blob/main/works/notebook/BirdCLEF_Train_exp0004.ipynb)|[code](https://www.kaggle.com/takamichitoda/birdclef-infer-split-model?scriptVersionId=59684179)|0.9126|0.5949|0.53|+ガウシアンノイズ|||
|exp0005|[code](https://github.com/trtd56/BirdCLEF/blob/main/works/notebook/BirdCLEF_Train_exp0005.ipynb)|[code](https://www.kaggle.com/takamichitoda/birdclef-infer-split-model?scriptVersionId=59884081)|0.9080|0.6017|0.55|+pink, brown, ガウシアンSNR||
|exp0006|[code](https://github.com/trtd56/BirdCLEF/blob/main/works/notebook/BirdCLEF_Train_exp0006.ipynb)|[code](https://www.kaggle.com/takamichitoda/birdclef-infer-split-model?scriptVersionId=59988707)|0.9086|0.6410|0.57|+airplane,rain||

### 300-250
|exp id|train|infer|CV mAP|train soundscape|LB|detail|memo|
|--|--|--|--|--|--|--|--|
|exp0024|[code](https://github.com/trtd56/BirdCLEF/blob/main/works/notebook/BirdCLEF_Train_exp0024.ipynb)|[code](https://www.kaggle.com/takamichitoda/birdclef-infer-split-model?scriptVersionId=61287530)|0.9636|0.6376|0.54|baseline|しきい値0.9だった|
|exp0024|[code](https://github.com/trtd56/BirdCLEF/blob/main/works/notebook/BirdCLEF_Train_exp0024.ipynb)|[code](https://www.kaggle.com/takamichitoda/birdclef-infer-split-model-2-type?scriptVersionId=61288115)|0.9636|0.6407|0.58|500-400と組み合わせ||


## 後処理

新村さんの後処理(しきい値平滑化): https://github.com/trtd56/BirdCLEF/blob/main/docs/post_processing_experiment.md

|しきい値|なにもしない|①|②|
|--|--|--|--|
|0.5|0.6490|0.6586|0.6562|
|0.3|0.6586|0.6386|0.6260|
