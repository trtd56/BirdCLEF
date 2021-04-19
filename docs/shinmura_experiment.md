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

## 30HL_50%が出来次第、subしてみる
+ threshold=0.5
+ airplen & rain don't contain

||data|backbone|resolution|batchsize|post-processing|train_soundscape(F1)|LB|memo|
|---|---|---|---|---|---|---|---|---|
|ex5|10HL_44%|ENetB0|450x458|16||
|ex5|10HL_44%|ENetB0|450x458|16|v|
|ex9|10HL_44%|ENetV2s|450x458|16||
|ex9|10HL_44%|ENetV2s|450x458|16|v|
|ex17|10HL_44%|RexNet-150|250x254|16|
|ex17|10HL_44%|RexNet-150|250x254|16|v

Augmenation(mixup, SpecAug++)は未検証
