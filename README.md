# FruitsRecognitionCamera
## Overview  
Intentカメラ + TensorFlowLite によるフルーツ認識カメラです。  
認識機能は、[TensorFlowLite](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets-2-tflite/#0)を利用。  


識別モデルであるtensorflowLiteファイルの作成はpythonで行いました。  
colab上でkaggleからデータのダウンロード、kerasによるネットワークの構築、学習、保存を行い、h5ファイルを作成、  
このファイルをtfliteファイルに変換し、GoogleDriveに保存。  
その全ての工程は[Fruits_Recognition_Keras.ipynb](https://github.com/maro-amoeba/FruitsRecognitionCamera/blob/master/Fruits_Recognition_Keras.ipynb)にて確認できます。  
  
tfliteファイルをアプリへ組み込み、  
画像のサイズ、識別するクラスファイルに注意しながらコーディングします。  
特に画像は、撮影した画像と識別器に与える大きさが違う為、サイズ変更をしますが、  
その際圧縮ではなく、トリミングを行うことをします。  
今回は100*100のサイズで学習させた為それと同様のBitmap形式になるように加工しています。  

Intentカメラで撮影した画像はとても小さい為、他の用途では好まれていない撮影方法ですが、  
今回識別器には100*100という更に小さいサイズで与えること、  
コードとして非常にシンプルに実装できる為採用しました。  

ちなみに、Intentカメラでの画像は非圧縮の状態で  
width = 135  
height = 240  
でした。224*224というサイズで学習させることもある為、  
別のタスクでは使えない場合もあります。  

## サンプルイメージ
<img src="https://user-images.githubusercontent.com/37995730/50756840-db033a80-12a0-11e9-9ef5-e8dab346e86c.png" width="320px">
