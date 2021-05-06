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
|ex36_only_TS|-|~~0.6190~~|0.53|+ LS + only_train_soundscape_species
|ex37|0.6232|0.5727|0.|+ LS + mixup(alpha=0.1)
|ex37_only_TS|-|~~0.6432~~|0.54|+ LS + mixup(alpha=0.1) + only_TS
|ex38|0.6248|0.5175|0.|+ LS + 確率的mixup(alpha=0.1)
|ex38_only_TS|-|~~0.6377~~|0.|+ LS + 確率的mixup(alpha=0.1) + only_TS
|[ex46](https://www.kaggle.com/shinmurashinmura/bird2-ex46-train-rex150)|0.5678|0.5953|0.53|+ LS + SpecAug++
|ex46_dynamicTH|-|0.6320|0.|+ LS + SpecAug++

+ 0.2noise(crickets, click_fire, rain, airplane, wind, sea_waves)

||local_F1|train_soundscape(F1)|LB|memo|
|---|---|---|---|---|
|ex47|0.5770|0.5092|0.45|BS + LS
|ex48|0.2232|0.5460|0.|BS + LS + SpecAug++
|[ex52](https://www.kaggle.com/shinmurashinmura/bird2-ex52-train-rex150)|0.5942|0.6158|0.54|BS + LS + SpecAug++(rain, fire)
|ex53|0.5429|0.5863|0.|BS + LS + SpecAug++(rain, fire, airplane)

+ 2つの鳥を混ぜる

||local_F1|train_soundscape(F1)|LB|memo|
|---|---|---|---|---|
|ex49|0.5949|0.4907|0.|BS + LS + SpecAug++(mistake)
|ex50|0.5598|0.5869|0.|BS + LS + SpecAug++(rand=0.6-0.8)
|ex50_dynamicTH|-|0.6280|0.|BS + LS + SpecAug++(rand=0.6-0.8)
|ex51|0.3754|0.6363|0.|BS + LS + SpecAug++ + max_loss

## HL vs all_data
+ threshold=0.5
+ fold0
+ RexNet-150
+ resolution 250x254
+ batchsize=64

||クラス数|data総数|teacher_model|epoch|local_F1|TS(F1)|LB|memo|
|---|---|---|---|---|---|---|---|---|
|ex36|111|1563(HL)||30|0.5414|0.5847|0.52|baseline + LS
|f_ex36|-|7564||30|0.6330|0.5192|0.45|-
|ex41|-|-||10|0.5699|0.5778|0.53|-

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
|[ex40_dynamicTH](https://www.kaggle.com/shinmurashinmura/bird2-ex40-adaptiveth-infer-rex150#prediction)|-|-|-|-|0.6428|0.56|baseline + LS

## distilation
+ threshold=0.5
+ fold0
+ RexNet-150
+ resolution 250x254
+ batchsize=64

||クラス数|data総数|teacher_model|epoch|local_F1|TS(F1)|LB|memo|
|---|---|---|---|---|---|---|---|---|
|ex40|-|-|ex36|10|0.5364|0.6306|0.54|baseline + LS
|ex54|-|-|ex52|10|0.5261|0.6374|0.56|BS + LS + SpecAug++(rain, fire)
|ex58|-|-|ex54|10|0.5485|0.6286|0.|-
|ex60|-|-|ex54|10|0.5420|0.6378|0.57|BS + LS + SpecAug++(rain, fire, dog)
|ex60_dynamicTH|-|-|-|-|-|0.6502|0.57|BS + LS + SpecAug++(rain, fire, dog)
|ex61|-|-|ex60|10|0.5128|0.6106|0.|0.8alpha

||クラス数|data総数|teacher_model|epoch|local_F1|TS(F1)|LB|memo|
|---|---|---|---|---|---|---|---|---|
|ex62|-|-|ex52|30|0.7057|0.6421|0.|BS + LS + SpecAug++(rain, fire, dog)
|ex63|-|-|ex62|30|0.7372|0.6489|0.|-
|[ex64](https://www.kaggle.com/shinmurashinmura/bird2-ex64-train-rex150)|-|-|ex63|30|0.7706|0.6542|0.57|-
|[ex64_5CV](https://www.kaggle.com/shinmurashinmura/bird2-ex64-5cv-infer-rex150/data#prediction)|-|-|-|-|-|0.6696|0.58|-
ex65|-|-|ex63|30|0.7320|0.6524|0.|0.8alpha
|ex66|-|-|ex64|30|0.7551|0.6685|0.57|-
|ex67|-|-|ex66|30|0.7280|0.6498|0.|-

||クラス数|data総数|teacher_model|epoch|local_F1|TS(F1)|LB|memo|
|---|---|---|---|---|---|---|---|---|
|ex56|-|-|ex52|30|0.5960|0.6335|0.56|BS + LS + SpecAug++(rain, fire)
|ex55|-|-|-|10|0.4975|0.6347|0.|BS + LS + SpecAug++(rain, fire), framewise(beta0.1)
|ex59|-|-|-|10|0.3616|0.6120|0.|BS + LS + SpecAug++(rain, fire), framewise(beta1)
|ex57|-|-|-|30|0.5655|0.6394|0.56|BS + LS + SpecAug++(rain, fire), framewise(beta0.1)

||クラス数|data総数|teacher_model|epoch|local_F1|TS(F1)|LB|memo|
|---|---|---|---|---|---|---|---|---|
|ex68|-|-|ex63|30|0.|0.|0.|BS + LS + 0.5SpecAug++(rain, fire, dog)
|ex69|-|-|ex63|30|0.|0.|0.|BS + LS + mixup + (rain, fire, dog)
