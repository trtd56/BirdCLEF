# PANNs実験

+ epoch30
+ adam(lr=0.01) + cosineanealing(T=10)
+ fold0
+ noise：ピンク、ブラウン、ホワイト、ランダムSNR 
+ threshold=0.5
+ loss:BCE

||HL_data|backbone|resolution|batchsize|post-processing|local_F1|train_soundscape(F1)|memo|
|---|---|---|---|---|---|---|---|---|
|ex1|10HL_44%|cnn14|64x|32||0.|
|ex4|10HL_44%|ENetB0|850x5|6||0.3218
|ex3|10HL_44%|ENetB0|850x8|6||0.
|ex6|10HL_44%|ENetV2|850x|6|||

Augmenation(mixup, SpecAug++)は未検証
