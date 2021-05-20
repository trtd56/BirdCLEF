# 後処理のメンバーたち

+ ①predictionの平滑化：now = now + 0.5(next + previous + next_next)
+ ②predictionの平滑化：now = now + 0.5(next + previous + next_next + previous_previous + next_next_next + previous_previous_previous)
+ ③siteで鳥を絞る
+ ④bird毎の閾値最適化（nocallの指数分布による決定）
+ ⑤クリップごとの閾値調整

④はまだ共有していませんが、いずれissueで上げます。  
⑤は最終段階で適用したいと思いますので、まだ保留です。

# 結果

### 戸田さん
||post-processing|TS(F1)|LB|memo
|---|---|---|---|---|
|[code](https://www.kaggle.com/takamichitoda/birdclef-infer-each-site/data)|baseline|0.6581|0.62|
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-infer-each-site-ppno1)|+①|0.6624||threshold=0.5。0.4~0.6で探索した
|[code]()|+①④|0.||

### teyoさん
||post-processing|TS(F1)|LB|memo
|---|---|---|---|---|
|[code](https://www.kaggle.com/teyosan1229/birdclef-inference-3ch/data)|baseline|0.6978|0.65|
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-inference-3ch-ppno1#ppNo1)|+②|0.7042||threshold=0.6(default)。0.5と0.7は悪化した
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-inference-3ch-ppno1-2)|+②③|0.7141|0.67|threshold=0.6。0.3~0.7で探索した
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-inference-3ch-ppno2-3-4-easy-sub)|+②③④|0.7195||threshold=expon.ppf(0.999999) + 0.5　ゆるめ
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-inference-3ch-ppno2-3-4-hard-sub)|+②③④|0.7214|0.68|threshold=expon.ppf(0.999999) + 0.6　きつめ
