## 4300HLでdistilation
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

https://www.kaggle.com/shinmurashinmura/bird2-ex102-4cv-2post-pickupsite-dynamicth-infer/data#prediction

## site毎にdistilation
+ fold0
+ RexNet-150
+ resolution 250x254
+ batchsize=32(T1以降)、64（T0）
+ BS + LS + modifiedMixup(rain, fire, dog)
+ epoch30
+ **post-processing適用**

### とりあえず、SSWとCOR 

||data|teacher_model|SSW(F1)|COR(F1)|TS(F1)|LB|memo|
|---|---|---|---|---|---|---|---|
|T0|ex110|-|0.2742|0.6456|0.5875|0.
|T1|ex111|ex110|0.7139|0.7776|0.6406|0.
|T2|ex112|ex111|0.7606|0.7980|0.6253|0.
|T3|ex113|ex112|0.7486|0.|0.|0.
