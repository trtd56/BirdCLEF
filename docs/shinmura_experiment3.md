## 4300HLでdistilation
+ fold0
+ RexNet-150
+ resolution 250x254
+ batchsize=32
+ BS + LS + SpecAug++(rain, fire, dog)

||data|teacher_model|epoch|local_F1|TS(F1)|LB|memo|
|---|---|---|---|---|---|---|---|
|ex100|4300HL|-|30|0.7560|0.5983|0.|
|ex101|4300HL + other_data|ex100|30|0.|0.|0.|
