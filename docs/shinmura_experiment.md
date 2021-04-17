# PANNs実験

+ epoch30
+ adam(lr=0.01) + cosineanealing(T=10)
+ fold0
+ noise：ピンク、ブラウン、ホワイト、ランダムSNR 
+ threshold=0.5
+ loss:BCE

||HL_data|backbone|resolution|batchsize|post-processing|local_F1|train_soundscape(F1)|memo|
|---|---|---|---|---|---|---|---|---|
|ex1|10HL_44%|cnn14|64x501|32||0.1470|
|ex4|10HL_44%|ENetB0|850x572|6||0.3218
|ex3|10HL_44%|ENetB0|850x843|6||0.2537
|ex2|10HL_44%|ENetB0|570x572|6||0.3753
|ex5|10HL_44%|ENetB0|450x458|16||0.5465
|ex6|10HL_44%|ENetB0|350x334|16||0.4094
|ex7|10HL_44%|ENetB0|400x401|16||0.
|ex8|10HL_44%|ENetB0|500x|16||0.
|ex|10HL_44%|ENetV2|850x|6|||

Augmenation(mixup, SpecAug++)は未検証
