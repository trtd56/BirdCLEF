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
|ex3|10HL_44%|ENetB0|64*?|64|v
|ex4|10HL_44%|ENetB0|850*|6|||
|ex5|10HL_44%|ENetB0|850*|6|v
|ex6|10HL_44%|ENetV2|850*|6|||
|ex7|10HL_44%|ENetV2|850*|6|v

Augmenation(mixup, SpecAug++)は未検証
