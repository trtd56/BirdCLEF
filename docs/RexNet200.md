# RexNet200たちのアンサンブル
モデルは三種類
+ ①ガウシアンノイズ（fold0~4 exp13）
+ ②+ピンクノイズ（fold0~4 exp17）
+ ③+ESC50（fold0 exp23）

|model|min_vote|TS|LB
|---|---|---|---|
|①|1|0.7704|0.70
|②|1|0.7684|0.71
|③|1|
|①②|1|0.7675|
|①②|2|0.7713|
|①②③|1|0.7311|
|①②③|2|**0.7724**|
|①②③|3|0.7629|
