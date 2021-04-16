# PANNs実験

+ epoch30
+ adam(lr=0.01) + cosineanealing(T=10)
+ fold0
+ noise：ピンク、ブラウン、ホワイト、ランダムSNR 
+ threshold=0.5
+ loss:BCE

||HL_data|backbone|resolution|batchsize|post-processing|local_F1|train_soundscape(F1)|memo|
|---|---|---|---|---|---|---|---|---|
|ex1|10HL_44%|cnn14|64*?|64|||
|ex2|10HL_44%|ENetB0|64*?|64|||
|ex4|10HL_44%|ENetB0|850*|6||0.3218
|ex6|10HL_44%|ENetV2|850*|6|||

Augmenation(mixup, SpecAug++)は未検証
