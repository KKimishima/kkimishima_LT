<!-- $theme: gaia -->
<!-- page_number: true -->

## ラズパイとPythonではじめてのIoT

----

# 自己紹介
- 名前	 : KKimishima
- Twitter :@k_kimikatsu123
- github	:KKimishima
- 仕事	 : 茨木の工場でIT管理部門
- プログラム歴　:趣味の独学2年
- 好きな言語 Java,Python,Ruby
- 最近のHack
RubyのSinatraでフルスクラッチでブロク作製中

---

# コーディングが楽しすぎて
# 転職を考え中

---

# はじめてのLTなので
# 生温かい目で見てください!!!

---

## 世間ではIotが流行っている!?
#### *自分*も手軽にお金をかけずにIoTやってたい!!!
#### なんとかやってみたい!!!
#### ド素人なので下記は点は目をつぶってください
- ~~セキュリティ~~
- ~~スケール~~
- ~~継続性~~

---

# 今回使用した
# 手軽でお金がかからない物!!!

---

![110% center](../img/rc4.jpeg)
- 温度センサー　Eltech RC-4
- 職場から貰った中国製安価温度センサー
- 無料 (~~2,000円~~)

---

![110% center](../img/raspi.jpg)
- レシバー raspberryPi3B  
- 買ってから全く使っていない可愛そうなラズパイ
- 無料(~~5,220円~~)

---

![70% center](../img/heroku.png)
- ホスティングサービス heroku
- freeプランでやってみる
- 無料
---

# やったこと
- RaspberryPiに温度センサーRC-4を取り付け
- Pythonで2~3分ごとにデータ測定データをhttpリクエスト送る
- Heroku上にデプロイしたWebアプリがリクエストをキャッチ表示する
- いい感じにWeb上に表示する

---
### こんな感じです
![100% center](../img/drawing.svg)

---

# 実演!!!

---

RaspberryPiのpythonのコード
civic Sasakiさんの "elitech-datareader"
https://pypi.org/project/elitech-datareader/

```python
import time,json,requests
import elitech
# ドライバの設定
device = elitech.Device("/dev/ttyUSB0")
# 無限ループ
while True:
    body = device.get_latest()
    data = {"id":str(body[0]),"datetime":str(body[1]),
        　　　"temp":str(body[2])}
    requests.get("http://hogehoge.com",params=data)
    time.sleep(120)
```

---
Spring bootにWebApiを作製
javaですみません!!!
```
- 温度データ登録

POST /api/v1/temp

- 全件温度データ取得

GET /api/v1/temp

- 最後の一件の温度データ取得

Get /api/v1/temp/last

- 一件削除
DELETE /api/v1/temp/:id

- 全件削除
DELETE /api/v1/temp
```

---

いい感じのwebサイトをjqruryとboostrapで作製
jsが苦手なので出来は良くないです...
![100% center](../img/screenshot.png)

---

# まとめ
- ド素人でも手軽に~~ほとんど~~お金をかけずに
IoTっぽいのは作れた!?
- herokuのfreeプランだと24時間起動ができないので、hobbyプランかAWSでやってみたい
- 次回は、セキュアなIotを目指したい
- 実は、pythonは数行しか書いていなので
pythonのflaskでWebアプリを書いてみたい
- 楽しかったです!!!
