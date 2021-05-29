# 後処理のメンバーたち

+ ①predictionの平滑化：now = now + 0.5(next + previous + next_next)
+ ②predictionの平滑化：now = now + 0.5(next + previous + next_next + previous_previous + next_next_next + previous_previous_previous)
+ ③siteで鳥を絞る
+ ④bird毎の閾値最適化（[nocallの指数分布による決定](https://github.com/trtd56/BirdCLEF/issues/44)）
+ ⑤クリップごとの閾値調整
+ ⑥クリップ内のbird頻度による閾値緩和
+ ⑦prediction平滑化の後処理

⑤は最終段階で適用したいと思いますので、まだ保留です。

### ⑥クリップ内のbird頻度による閾値緩和
クリップ（10分）内に頻出する鳥は、クリップ全体でbirdcallの傾向にある。  
そこで、クリップを3つ（序盤、中盤、終盤）に分け、各パートで6回/20回以上鳴いたbirdの閾値を緩くする。  
具体的には0.1ほど緩める。（TS0.005くらい改善）

### ⑦prediction平滑化の後処理
①と②を使うと、どうしても頭とおしりのpredictionがFPになりやすい。  
（未来と過去を足しているため、突然nocallになっても対応できない）  
そのため、6個以上連続してbirdcallになったものは、頭とおしりを強制的に消す。  
（TS0.005くらい改善）  

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
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-inference-3ch-ppno2-3-4-easy0-4?scriptVersionId=63525518)|+②③④|0.6712|0.63|threshold=expon.ppf(0.999999) + 0.3　かなりゆるめ
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-inference-3ch-ppno2-3-4-easy0-4?scriptVersionId=63527202)|+②③④|0.6976|0.67|threshold=expon.ppf(0.999999) + 0.4　かなりゆるめ
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-inference-3ch-ppno2-3-4-easy-sub)|+②③④|0.7195|0.68|threshold=expon.ppf(0.999999) + 0.5　ゆるめ
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-inference-3ch-ppno2-3-4-hard-sub)|+②③④|0.7214|0.68|threshold=expon.ppf(0.999999) + 0.6　きつめ

### 最終アンサンブル
||post-processing|モデル数|TS(F1)|LB|memo
|---|---|---|---|---|---|
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-ensemble-toda-teyo-shinumra)|+②③④⑥⑦|6|0.7411|0.69|0.5　たぶんゆるめ
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-ensemble-toda-teyo-shinumra-adjustth)|+②③④⑥⑦|RexNet200のみ|0.7708|0.70|reevir1など閾値緩和、0.5　たぶんゆるめ
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-ensemble-toda-teyo-shinumra-adjustth-sne)|+②③④⑥⑦|RexNet200のみ|0.7704|0.70|reevir1など閾値緩和、0.5　たぶんゆるめ
|[code](https://www.kaggle.com/shinmurashinmura/birdclef-toda-teyo-shinumra-optimthver2-sne)|+②③④⑥⑦|RexNet200のみ|0.7609|0.61|reevir1など閾値緩和、optim threshの見直し


