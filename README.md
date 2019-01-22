# FruitsRecognitionCamera
tensorflowLiteファイルの作成のノートファイルはこちらです。  
[Fruits_Recognition_Keras.ipynb](https://github.com/maro-amoeba/FruitsRecognitionCamera/blob/master/Fruits_Recognition_Keras.ipynb)
## Sample image  
<img src="https://user-images.githubusercontent.com/37995730/50756840-db033a80-12a0-11e9-9ef5-e8dab346e86c.png" width="320px">  

# Overview  

Intentカメラ + 深層学習 によるフルーツ認識カメラです。  
認識機能は、[TensorFlowLite](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets-2-tflite/#0)を利用。  


識別モデルであるtensorflowLiteファイルの作成はpythonで行いました。  
colaboratory上で[Kaggle(Fruits 360 dataset)](https://www.kaggle.com/moltean/fruits/home)からデータのダウンロード、  
kerasによるネットワークの構築、学習、保存を行い、h5ファイルを作成、  
このファイルをtfliteファイルに変換し、GoogleDriveに保存。  
その全ての工程は[Fruits_Recognition_Keras.ipynb](https://github.com/maro-amoeba/FruitsRecognitionCamera/blob/master/Fruits_Recognition_Keras.ipynb)にて確認できます。  
  
tfliteファイルをアプリへ組み込み、  
画像のサイズ、識別するクラスファイルに注意しながらコーディングします。  
特に画像は、撮影した画像と識別器に与える大きさが違う為、サイズ変更をしますが、  
その際縮小ではなく、トリミングを行うことをします。  
今回は100*100のサイズで学習させた為それと同様のBitmap形式になるように加工しています。  

Intentカメラで撮影した画像はとても小さい為、他の用途では好まれていない撮影方法ですが、  
今回識別器には100*100という更に小さいサイズで与えること、  
コードとして非常にシンプルに実装できる為採用しました。  

ちなみに、Intentカメラでの画像は手元の実機の元のサイズの状態で  
width = 135  
height = 240  
でした。224*224というサイズで学習させることもある為、  
別のタスクでは使えない場合もあります。  

# 課題  
データセットの問題になると思いますが、モデルの汎用性が全くありませんでした。  
つまり撮影しても認識できないです。元も子もないです。  

試しに、画像の拡張(訓練画像の回転やら縮小)を施したモデルで識別してみましたがダメでした。  

学習のさせ方というより、選んだデータセットが間違いであったことに気づきました。  
例えばクラスにApple Red1というものがありますが、画像フォルダを確認すると、  
一個のりんごを多角的に撮影したものが格納されています。  
これではデータセットとして不適切でした。  

なぜならこれは、「人間」を学習させるつもりが、「田中太郎」を学習しているようなものだったからだと思います。  
仮に「佐藤次郎」をデータとして与えると、「人間」と識別してくれないモデルが出来上がっています。
より多くの人間の個体を学習させてこそ、「人間」の識別ができる。それと同じことだと考えました。  
