# music
# 楽曲レコメンドシステム(KMeansクラスタリングを用いた類似曲推薦）
　このシステムは、ユーザーが選択して楽曲と音響的ににた曲を推薦することを目的としたコンテンツベースのレコメンドシステム。
 　楽曲をクラスタリングし、同じクラスタ内から「音響的に近い楽曲」を選出させた。

  今回はkaggleから用いた「Spotify dataset」を使用し、ユーザー履歴が不要な「コンテンツベースフィルタリング」を採用した。<br>
  [Google](https://www.kaggle.com/datasets/vatsalmavani/spotify-dataset/data)
  
  Spotifyが提供する約17万件の楽曲データセットには、以下のような音響特徴料が含まれている。
  
  acousticness, danceability, energy, instrumentalness,liveness, loudness, speechiness, tempo, valence

これらをもとに、クラスタリングと距離計算を行った。

## 実装手順
1.前処理と特徴量の抽出　*acoustiicness.ipynb*<br>
・音響特徴量を抽出（上記の９つを使用）<br>
・StandardScalerによる標準化

2.KMeansクラスタリングによる学習　*acoustiicness.ipynb*<br>
・KMeans(n_clusters=20) を用いてクラスタリングを実行。<br>
・各楽曲にクラスタラベル(*cluster_label*)を追加。<br>
・学習済みモデルの保存

3.楽曲選択と推薦ロジック *music.py*<br>
・ユーザが選択した曲と同じクラスタに属する楽曲を抽出。<br>
・選曲された楽曲と音響ベクトル間のユークリッド距離を計算。<br>
・最も距離が近い上位５曲を類似曲として推薦。

4.Streamlitによる可視化　*music.py*<br>
・ユーザーがWeb上で曲を選択し、リアルタイムでレコメンドが表示されるインターフェース

## 利用性
### カラオケ向けの応用
　例えばカラオケで「Like a Rolling Stone」という楽曲を歌う人がいるとする。このレコメンドシステムでは「Like a Rolling Stone」と同じクラスタに属するが曲の中から、テンポ感や音響の雰囲気、盛り上がり方が似ている5曲をユークリッド距離で抽出する。<br>
 これにより、自分の声質やリズム感にあった曲を見つけやすくなり、カラオケでの選曲に悩んでいる人にも直感的なレコメンドが可能になる。

##実行手順
pip install streamlit<br>
unzip data_with_clusters.csv.zip<br>
streamlit run music.py




  


  
Main Repository


