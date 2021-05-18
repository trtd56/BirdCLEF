# 4300HLでdistilation
+ fold0
+ RexNet-150
+ resolution 250x254
+ batchsize=32
+ BS + LS + SpecAug++(rain, fire, dog)

||data|teacher_model|epoch|local_F1|TS(F1)|LB|memo|
|---|---|---|---|---|---|---|---|
|ex100|4300HL|-|30|0.7560|0.5983|0.|
|ex101|4300HL + other_data|ex100|30|0.7914|0.5958|0.|
|ex102|4300HL + other_data|ex101|30|0.7898|0.5975|0.|
|[ex102_4CV](https://www.kaggle.com/shinmurashinmura/bird2-ex102-4cv-2post-pickupsite-dynamicth-infer/data#prediction)|-|-|-|-|0.6858|0.60|post:2post + pick_up_site + optime_thresh


# site毎にdistilation
+ fold0
+ RexNet-150
+ resolution 250x254
+ batchsize=32(T1以降)、64（T0）
+ BS + LS + modifiedMixup(rain, fire, dog)
+ epoch30
+ **post-processing:2post + pick_up_site**

## とりあえず、SSWとCOR 

||data|teacher_model|SSW(F1)|COR(F1)|TS(F1)|LB|memo|
|---|---|---|---|---|---|---|---|
|T0|ex110|-|0.2742|0.6456|0.5875|0.
|T1|ex111|ex110|0.7139|0.7776|0.6406|0.
|T2|ex112|ex111|0.7606|0.7980|0.6253|0.
|T3|ex113|ex112|0.7486|0.8037|0.|0.

# 243speciesで学習
+ fold0
+ RexNet-150
+ resolution 250x254
+ batchsize=32(T1以降)、64（T0）
+ BS + LS + SpecAug++ (rain, fire, dog)
+ epoch30
+ data: 4300HL(146species) + 9000(97species)
+ **post-processing:pick_up_site**

||teacher_model|loacal_F1|TS(F1)|LB|memo|
|---|---|---|---|---|---|
|ex120|-|0.5428|0.6148|0.
|ex121|ex110|0.5320|0.6558|0.
|ex122|ex111|0.5693|0.6717|0.|ここがbest
|ex123|ex112|0.5555|0.6401|0.|これはやり過ぎ

+ EfficientNetB0

||teacher_model|loacal_F1|TS(F1)|LB|memo|
|---|---|---|---|---|---|
|ex140|-|0.5136|0.6406|0.
|ex141|ex110|0.5156|0.6463|0.
|ex142|ex111|0.5|0.|0.|
