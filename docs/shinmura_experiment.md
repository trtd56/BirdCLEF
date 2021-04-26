# PANNs実験

## backbone & resolution search

+ epoch30
+ adam(lr=0.01) + cosineanealing(T=10)
+ fold0
+ noise：ピンク、ブラウン、ホワイト、ランダムSNR 
+ loss:BCE

||data|backbone|resolution|batchsize|post-processing|local_F1|train_soundscape(F1)|memo|
|---|---|---|---|---|---|---|---|---|
|ex1|10HL_44%|cnn14|64x501|32||0.1470|
|ex4|10HL_44%|ENetB0|850x572|6||0.3218
|ex3|10HL_44%|ENetB0|850x843|6||0.2537
|ex2|10HL_44%|ENetB0|570x572|6||0.3753||hop_size=190
|ex5|10HL_44%|ENetB0|450x458|16||**0.5465**||hop_size=350
|ex6|10HL_44%|ENetB0|350x334|16||0.4094||hop_size=480
|ex7|10HL_44%|ENetB0|400x401|16||0.4495||hop_size=400
|ex8|10HL_44%|ENetB0|500x501|16||0.4131||hop_size=320

||data|backbone|resolution|batchsize|post-processing|local_F1|train_soundscape(F1)|memo|
|---|---|---|---|---|---|---|---|---|
|ex9|10HL_44%|ENetV2s|450x458|16||**0.5978**|
|ex10|10HL_44%|ENetV2s|350x334|16||0.5537|
|ex11|10HL_44%|ENetV2s|570x572|8||0.4825|

||data|backbone|resolution|batchsize|post-processing|local_F1|train_soundscape(F1)|memo|
|---|---|---|---|---|---|---|---|---|
|ex15|10HL_44%|RexNet-150|450x458|16||0.3440|
|ex16|10HL_44%|RexNet-150|350x334|16||0.4977|
|ex17|10HL_44%|RexNet-150|250x254|16||**0.6155**|
|ex18|10HL_44%|RexNet-150|200x208|16||0.5475|
|ex19|10HL_44%|RexNet-150|300x|16||0.5309|

||data|backbone|resolution|batchsize|post-processing|local_F1|train_soundscape(F1)|memo|
|---|---|---|---|---|---|---|---|---|
|ex21|10HL_44%|RexNet-200|450x458|16||0.2485|
|ex22|10HL_44%|RexNet-200|350x334|16||0.2557|

||data|backbone|resolution|batchsize|post-processing|local_F1|train_soundscape(F1)|memo|
|---|---|---|---|---|---|---|---|---|
|ex25|10HL_44%|RexNet-100|250x254|16||0.4996|
|ex26|10HL_44%|RexNet-100|350x334|16||0.3968|

## データ個数の比較
+ validation dataは同じ
+ fold0

||クラス数|train data個数/class|train data総数|backbone|resolution|batchsize|local_F1|
|---|---|---|---|---|---|---|---|
|ex31|25|8|200|RexNet-150|250x254|16|0.6255|
|ex32|25|28|697|RexNet-150|250x254|16|0.8253|

## 10HL_44%でsubしてみる
+ threshold=0.5
+ airplane & rain don't contain
+ fold0
+ RexNet-150
+ resolution 250x254

||data|クラス数|train data総数|batch_size|local_F1|train_soundscape(F1)|LB|memo|
|---|---|---|---|---|---|---|---|---|
|ex17|10HL_44%|105|878|16|0.6155|0.5759|0.47
|ex35|30HL_45%|108|1563|64|0.5952|0.5339|0.52
|ex35_nocall|30HL_45%|108|1563|64|0.5952|0.6091|0.55

## 基礎実験
+ threshold=0.5
+ fold0
+ RexNet-150
+ resolution 250x254
+ batchsize=64
+ data 30HL_45%

||local_F1|train_soundscape(F1)|LB|memo|
|---|---|---|---|---|
|ex35|0.5952|0.5759|0.52|baseline
|ex36|0.5414|0.5847|0.52|+ label smoothing(alpha=0.1)=LS
|ex36_only_TS|-|0.6190|0.53|+ LS + only_train_soundscape_species
|ex37|0.6232|0.5727|0.|+ LS + mixup(alpha=0.1)
|ex37_only_TS|-|0.6432|0.54|+ LS + mixup(alpha=0.1) + only_TS
|ex38|0.6248|0.5175|0.|+ LS + 確率的mixup(alpha=0.1)
|ex38_only_TS|-|0.6377|0.|+ LS + 確率的mixup(alpha=0.1) + only_TS
|ex39|0.|0.|0.|+ LS + SpecAug++
|ex40|0.|0.|0.|+ LS + 確率的SpecAug++

## HL vs all_data
+ threshold=0.5
+ fold0
+ RexNet-150
+ resolution 250x254
+ batchsize=64

||クラス数|data総数|epoch|local_F1|train_soundscape(F1)|LB|memo|
|---|---|---|---|---|---|---|---|
|ex36|111|1563(HL)|30|0.5414|0.5847|0.52|baseline + LS
|f_ex36|111|7564|30|0.6330|0.5192|0.45|baseline + LS
|ex41|111|7564|10|0.5699|0.5778|0.53|baseline + LS
|ex40|111|7564(teacher HL model ex36)|10|0.5364|0.6306|0.54|baseline + LS

## 動的なthreshold
+ bird_call と nocall　は音源毎に[二極化](https://www.kaggle.com/shinmurashinmura/train-soundscape-nocall-rate)している。
+ 音源毎にbird_callが多ければthresholdを小さく、nocallが多ければthesholdを大きくする。
+ fold0
+ RexNet-150
+ resolution 250x254
+ batchsize=64

||クラス数|data総数|epoch|local_F1|TS(F1)|LB|memo|
|---|---|---|---|---|---|---|---|
|ex40|111|7564(teacher HL model ex36)|10|0.5364|0.6306|0.54|baseline + LS
|[ex40_optimTH](https://www.kaggle.com/shinmurashinmura/bird2-ex40-adaptiveth-infer-rex150#prediction)|-|-|-|-|0.6428|0.56|baseline + LS

Augmenation(mixup, SpecAug++)は未検証
