# 後処理たち

+ ①predictionの平滑化：now = now + 0.5next + 0.5previous + 0.25next_next + 0.25previous_previous
+ ②siteで鳥を絞る
+ ③bird毎の閾値最適化（nocallの指数分布による決定）
+ ④クリップごとの閾値調整

③はまだ共有していませんが、いずれissueで上げます。  
④は最終段階で適用したいと思いますので、まだ保留です。

# 結果

### 戸田さん
||post-processing|TS(F1)|LB|memo
|---|---|---|---|---|
|[code](https://www.kaggle.com/takamichitoda/birdclef-infer-each-site/data)|baseline|0.6581|0.62|
|[code]()|+①|0.||
|[code]()|+①③|0.||

### teyoさん
||post-processing|TS(F1)|LB|memo
|---|---|---|---|---|
|[code](https://www.kaggle.com/teyosan1229/birdclef-inference-3ch/data)|baseline|0.6978|0.65|
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-inference-3ch-ppno1#ppNo1)|+①|0.7008||threshold=0.6(default)。0.5と0.7は悪化した
|[code]()|+①②|0.||
|[code]()|+①②③|0.||
