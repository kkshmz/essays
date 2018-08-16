# 2018/8/18 **Design with .AI - AIとつくり、AIと学ぶ - vol.1 ”AIと音響/音楽のいま”  セミナー資料**
セミナー  [ＧＩＣセミナー情報 | 九州大学 グローバルイノベーションセンター](http://www.gic.kyushu-u.ac.jp/j/seminar/gic014.html)

講師 - 徳井直生  
http://www.naotokui.net /
http://twitter.com/naotokui/
http://qosmo.jp/

AI DJ Project - http://aidj.qosmo.jp/

https://player.vimeo.com/video/259129367


[https://vimeo.com/259129367](https://vimeo.com/259129367)

Imaginary Landscape - NTT ICC OpenSpace 2018 展示中! 

https://www.youtube.com/watch?v=yJhL_xvEEls&


[https://youtu.be/yJhL_xvEEls](https://youtu.be/yJhL_xvEEls)

↑ で利用している技術についても触れます


**流れ**

1. 前提知識
2. 音響処理
  2.1 音の認識/識別 

     2.2 音の合成
3.  音楽生成

  3.1 音符・MIDIレベルの音楽生成
  3.2 音響レベルの音楽生成
4. クロスモーダルモデル
5. 応用例
6. まとめ　     
# 0. 前提知識

最初期のComputer Music 

1951 - Manchester University “God Save the Queen”など by Alan Turing
https://www.theguardian.com/science/2016/sep/26/first-recording-computer-generated-music-created-alan-turing-restored-enigma-code

https://www.youtube.com/watch?v=xLwjz0UR5_A&


[https://youtu.be/xLwjz0UR5_A](https://youtu.be/xLwjz0UR5_A)

1960s’
Daisy Bell - Max Mathews 

https://www.youtube.com/watch?v=41U78QP8nBk&


[https://youtu.be/41U78QP8nBk](https://youtu.be/41U78QP8nBk)

チューリングは40年代からコンピュータによる楽音の生成の実験をしていた.
**Computer Musicの歴史は、コンピュータの歴史そのものと同じくらい古い.**


## 人工知能 / Artificial Intelligence (AI) とは
- 一応の定義 **「生き物(人間、動物)の知能をコンピュータの上に実現すること」**
  - AIとは何かを定義することがAI研究の目的でもある
- なんでもできる「汎用型AI」は存在しない. 
- 特定の用途に特化したAIのみ
  ❌ ドラえもん  ⭕️ 自動運転AI / 画像認識AI / 翻訳AI etc…



## AIと機械学習? - よく混同される言葉
![](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533956665507_image.png)


機械学習ではないAIもある


## 機械学習(Machine Learning)とは 

一般的なプログラミングと比較するとわかりやすい

![一般的なプログラミングはルールとデータから答えを出すことが目的](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533956774315_image.png)

![機械学習はデータと答えから、その答えを導くルールを導くのが目的](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533956784695_image.png)


機械学習はデータと答えから、その答えを導くルールを導くのが目的. いったんルールがわかれば、あとは従来のプログラミングと組み合わせて未知のデータに対しても答えを導き出せる. 


![](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533956872285_image.png)



## Deep Learning 

Neural Network  - TensorFlow playground
https://playground.tensorflow.org/
実際に簡単な例で試してみる. 

![](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533957144935_image.png)



## CNN  (Convolutional Neural Network) 

畳み込みニューラルネットワーク。画像認識などのタスクで広く用いられるアーキテクチャ。


![CNNのアーキテクチャ](http://vision03.csail.mit.edu/cnn_art/data/single_layer.png)



![「畳み込み」の概念 図— http://ufldl.stanford.edu/tutorial/supervised/FeatureExtractionUsingConvolution/](https://cdn-images-1.medium.com/max/1600/1*ZCjPUFrB6eHPRi4eyP6aaA.gif)


画像認識のデモ

- [Video Classification · ml5js](https://ml5js.org/docs/video-classification-example)
  ml5jsは[Processing](http://www.processing.org)の理念を継承し、アーティストやデザイナーが簡単に機械学習を試せるようにという意図のもとに公開されたJavaScirptのパッケージ.  


- Google [Teachable Machine](https://teachablemachine.withgoogle.com/)

     学習済みのモデルを再度学習することで特定の用途に特化したモデルを作る (fine-tuningと呼ばれる)を使っている. ブラウザ上でゼロから学習しているわけではないこと注意. 


- [What Neural Networks See by Gene Kogan | Experiments with Google](https://experiments.withgoogle.com/what-neural-nets-see)

一般的に画像認識で使われているが、スペクトログラム画像に応用することで音の識別などにも使われ
る. 


## RNN (Recurrent Neural Network)


![](https://cdn-images-1.medium.com/max/1600/1*lRur-CtkH5D9m6CkZ5eCYQ.png)


再帰型ニューラルネットワーク.  
出力を入力に戻す再帰的なコネクションを設けることで、結果的に時系列データを扱えるようにしたニューラルネットワーク.

デモ

[Selected Stories](https://cvalenzuela.github.io/Selected_Stories/) - ml5.js
ヘミングウェイ、バージニア・ウルフらの文章を学習したモデル

[マシンと共に書く- Writing with the machine](http://createwith.ai/demo/20170906/954)
SF小説を学習したモデルを使って自分の文章を補間してくれる仕組みを作る.  

![Writing with the machine](https://i0.wp.com/createwith.ai/wp-content/uploads/2017/09/rnn-example-extra-2.gif?zoom=2&fit=640%2C280)



****
## GAN  (Generative Adversarial Network)

Goodfellow, I., Pouget-Abadie, J., & Mirza, M. (2014). Generative Adversarial Networks. *ArXiv Preprint ArXiv: …*, 1–9. https://doi.org/10.1017/CBO9781139058452

Creswell, A., White, T., Dumoulin, V., Arulkumaran, K., Sengupta, B., & Bharath, A. A. (n.d.). Generative Adversarial Networks: An Overview. Retrieved from https://arxiv.org/pdf/1710.07035.pdf



![https://medium.freecodecamp.org/an-intuitive-introduction-to-generative-adversarial-networks-gans-7a2264a81394?gi=ea98121f497d](https://cdn-images-1.medium.com/max/1600/0*2Smzp-1MDx2TTwU6.png)



GAN Playground- GANの学習を実体験. 
https://reiinakano.github.io/gan-playground/

**pix2pix**
J.-Y. Zhu, T. Park, P. Isola, and A. A. Efros, “Unpaired image-to- image translation using cycle-consistent adversarial networks,” in Proceedings of the International Conference on Computer Vision, 2017. [Online]. Available: https://arxiv.org/abs/1703.10593


![](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533959680148_image.png)


[Image-to-Image Demo - Affine Layer](https://affinelayer.com/pixsrv/)
https://ml5js.org/docs/pix2pix-example

**GANで生成された顔 (セレブの顔のデータセットを利用)** 
Karras NVIDIA, T., & Aila NVIDIA Samuli Laine NVIDIA Jaakko Lehtinen, T. (n.d.). PROGRESSIVE GROWING OF GANS FOR IMPROVED QUALITY, STABILITY, AND VARIATION. Retrieved from http://research.nvidia.com/sites/default/files/pubs/2017-10_Progressive-Growing-of//karras2017gan-paper.pdf

https://www.youtube.com/watch?v=XOxxPcy5Gr4&


[https://youtu.be/XOxxPcy5Gr4](https://youtu.be/XOxxPcy5Gr4)


GANの応用としては画像生成がこれまで中心的だったが、最近音響生成/音楽生成に利用され始めている!  

🙆🏻‍♂️  教師なし学習  

![CAN](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533960759879_can_images.png)


    例) [Creative Adversarial Network (CAN)](http://createwith.ai/paper/20170629/839) 
     絵画のデータセットをつかって、GANで画像を生成. 
      Discriminatorを一つ追加. 過去のジャンルにあてはまらまないものを高く評価する → アートらしさ/絵画らしさは担保しつつも過去のジャンルとは違う絵画を生成する可能性
     
🙅🏻‍♂️ 学習が不安定 

- そもそも学習の難しさが discriminator << generator
- mode collapse(generatorが局所解に陥る=特定の顔しか生成しないようになる)が起きる

     GAN Hacks https://github.com/soumith/ganhacks









# 1. 音響処理


## 1.1 認識
****
参考) 
Choi, K., Fazekas, G., Cho, K., & Sandler, M. (2017). **A Tutorial on Deep Learning for Music Information Retrieval.** Retrieved from http://arxiv.org/abs/1709.04396

**畳み込みニューラルネット CNNを音に対して当てはめることで、音の識別ができる！**


![音の表現](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533976059540_image.png)


**音に対するCNN**

- 波形を直接扱う - 1次元の畳み込み
- スペクトログラム (SFT, 人間の聴覚特性に合わせたMel-spectrogram, CQTなどで変換したもの) → 2次元画像として扱える.  (一般に画像の CNNがRGBの3チャンネルのデータを扱うのに対して、スペクトログラムは1チャンネル = グレイスケール画像だと考えられる) 



デモ)
[**Drumkit Audio Classifier**](https://codepen.io/naotokui/pen/rrGGNJ)
スペクトログラムを画像として扱うことで、音の種類(ここでは、キック、スネアといったドラム音色) を識別する. 

![スネア](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533976304258_image.png)
![オープンハイハット](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533976336868_image.png)
![ドラムの識別に使ったモデル](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533976607786_image.png)


研究例

**ジャンル、ボーカルの有無、声と音楽、音楽があたえる感情/印象、環境音などの識別**
**Choi, K., Fazekas, G., Sandler, M., & Cho, K. (2017). Transfer learning for music classification and regression tasks.** Retrieved from http://arxiv.org/abs/1703.09179


![](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533977217874_image.png)


[ESJ65 poster P1-031](http://www.esj.ne.jp/meeting/abst/65/P1-031.html) **畳み込みニューラルネットワークを用いた鳴き声による鳥類の種判別**　　 


    鳥類は、生態系の指標種として扱われることが多く、環境アセスメント等における調査対象項目となっている。しかし、従来の鳥類調査では、専門知識を持った調査員が現地に行って種判別を行っているため、調査員の高齢化による人材不足やコスト面等での問題がある。そこで、機械学習技術を用いて鳴き声による鳥類の種判別を自動的に行うことで、現状の問題解決と様々な場面での活用（長期間モニタリング、危険地帯での調査等）が期待できる。海外では、2014年以降、鳥類の識別器の開発精度を競う国際コンテスト（BirdCLEF）が開催されており、近年、ディープラーニングを用いることで精度の高い識別器が開発されている。一方、日本では、鳥類の種判別を行う研究は少なく、精度の向上や対象種数の拡大等の課題がある。よって、本研究では、鳥類を対象に、畳み込みニューラルネットワークによる機械学習を用いることで、高精度な種判別を自動的に行うことを目的とする。まず2007〜2017年の間に日本の各地で14種類の鳥類の音声を収集した201のWAVEファイル（サンプリング周波数44100Hz, 16bit）を用いた。そのラベル付き音声を100ms間隔でサンプリングし、音圧が3dBバーストした時点を自動検出した。検出された時点を中心に前後500ms間、周波数帯100Hz～12kHzの領域で、224×224pixelのFFTスペクトログラム画像を抽出した。またこの際に、鳥の鳴き声以外の環境中の雑音も別途抽出して、ノイズクラスを含む15クラス、計5585枚の画像データベースを構築した。その画像データベースに対して、畳み込みニューラルネットワーク(Convolutional Neural Networks)のネットワーク構造の一種である事前学習済みのResnet-50をファインチューニングすることで、種レベルの識別で交差検証の正答率が97%であった。今後は実環境下に適用するために、より頑健かつ汎化性の高い識別器の構築を目指し、未知の音声に対する汎化性能を評価する。

精度 97%!

****[**CNNを用いたコウモリの種判別システムの開発と応用 - 増田圭祐**](http://www.see.eng.osaka-u.ac.jp/seege/seege/material/2017/masuda.pdf)
超音波領域でも可能！ 可聴域の環境ノイズが入りにくいので鳥の鳴き声の識別よりも精度が高い. 

![コウモリの種類の判別](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533272001541_image.png)
![正答率](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533272031663_image.png)


[**Recommending music on Spotify with deep learning**](http://benanne.github.io/2014/08/05/spotify-cnns.html)
****http://benanne.github.io/2014/08/05/spotify-cnns.html

協調フィルタリングの問題(cold start問題 = 新しい曲は利用履歴がない→オススメされない)をディープラーニングで解決できないか??  すでスペクトログラムをCNNに入力し、協調フィルタの出力にできるだけ近い値を出力するように学習する.  最終的にある曲が40次元のベクトルで表現される. 

![One of the convolutional neural network architectures I've tried out.](http://benanne.github.io/images/spotify_convnet.png)


ベクトルが近いものを集めると…. 似通った曲のプレイリストができる
https://open.spotify.com/user/sander_dieleman/playlist/6wnPsncVsmApMRj5g7PWkz
https://open.spotify.com/user/sander_dieleman/playlist/66rHmJlejT0PQh74JXV8Ie

この研究でのアウトプット 40次元のベクトルは複雑な音楽の特徴・本質を ぎゅっと圧縮して表現していると考えられる. こうしたベクトルのことを**Latent Vector**(潜在ベクトル?)、このベクトル空間のことを**Latent (Vector) Space と**いう呼び方をする.  

Latent Spaceの特徴

- 似通ったものが近くに、異なるものが遠くに位置付けられる
- 距離と類似度が必ずしも比例するとは限らない (Latent Spaceでの距離が二倍だからといって、二倍違う?とは限らない) 
- 高次元空間なので、t-SNEなどの次元圧縮アルゴリズムで2次元、3次元に圧縮して可視化することが多い. 

例) 

[AI DJ Project](http://aidj.qosmo.jp/) 
スペクトログラムから音楽ジャンル、楽器、ドラムマシンの種類を識別するモデル.  
識別されたクラスではなく、その手前の層が出力する特徴量を使う.  
人間のDJがかけている曲の特徴量に近い曲を選ぶ→ 雰囲気が似た曲が選ばれる(..はず)

![](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1534051973779_image.png)



![楽曲のlatent spaceの表示](http://aidj.qosmo.jp/images/music_selection_02.gif)
![YCAMでのAI DJ](http://aidj.qosmo.jp/images/ycam/01.JPG)


実際にあった選曲 

https://www.youtube.com/watch?v=hvh3u6zPmtw&


[https://youtu.be/hvh3u6zPmtw](https://youtu.be/hvh3u6zPmtw)

https://www.youtube.com/watch?v=opvopULDhVI&t=2m55s


[https://youtu.be/opvopULDhVI?t=2m55s](https://youtu.be/opvopULDhVI?t=2m55s)

**Bird Sounds.**  - 鳥の鳴き声のLatent Spaceをt-SNEで二次元に圧縮して表現したマップ 
https://experiments.withgoogle.com/bird-sounds

https://www.youtube.com/watch?v=31PWjb7Do1s&


[https://youtu.be/31PWjb7Do1s](https://youtu.be/31PWjb7Do1s)


**Atlas 商用のプラグイン**
ドラムセットのlatent spaceを表示. 

https://www.youtube.com/watch?v=jLe6wpHK--Y&


[https://youtu.be/jLe6wpHK--Y](https://youtu.be/jLe6wpHK--Y)


## 1.2 音響合成

ディープラーニングの音響合成は WaveNet がゲームチェンジャー! 

**WaveNet: A Generative Model for Raw Audio  - Deep Mind**
https://deepmind.com/blog/wavenet-generative-model-raw-audio/

Dilated Convolutionで時間的な依存性の問題を解決したのがポイント


![Architecture animation](https://storage.googleapis.com/deepmind-live-cms/documents/BlogPost-Fig2-Anim-160908-r01.gif)


音声合成に使うことを念頭に開発された技術だが、音楽を学習すると… 
ただし、このときはでたらめに音楽っぽい音を生成するのみ. 

https://www.youtube.com/watch?v=Y8UawLT4it0&


[https://youtu.be/Y8UawLT4it0](https://youtu.be/Y8UawLT4it0)


WaveNet Autoencoderをつかった音色の生成
**NSynth - Google Magenta** 
Engel, J., Resnick, C., Roberts, A., Dieleman, S., Eck, D., Simonyan, K., & Norouzi, M. (2017). Neural Audio Synthesis of Musical Notes with WaveNet Autoencoders. Retrieved from http://arxiv.org/abs/1704.01279

[解説] [機械学習を用いたシンセサイザーが持つ可能性 – Making a Neural Synthesizer Instrument –](http://createwith.ai/demo/20170520/751) by piqcyさん
WaveNetをつかったAutoencoder. AutoencoderはEncoderとDecoderからなる. 
Encoderは、入力となる一定時間の音(例えば、1秒間のトロンボーンの音など)を元にサンプリングと圧縮を階層状に実行することで、最終的に特定の長さの数値列を生成します. 

そして、DecoderはEncoderとは逆の動きをします。つまり、入力音から得られた数値列(=音の表現)とピッチ(音の高さ)から、音の生成を行います。
このEncoderとDecoderを学習させる、つまり入力した音を正確に再現できるように学習させると、中間表現である「Z」は音の再生に十二分な表現を獲得するようになります。これにより、洗練された「音の表現」が得られているということです。
このようにして得られた「音の表現」は、それを合成することであたかも元々一つの楽器であったかのような音を生成することができます。これは、単純に二つの音を合成するのとは異なる印象を与えます([こちら](https://magenta.tensorflow.org/nsynth)から、聞き比べることができます)。


![Autoencoderの概念図](https://i1.wp.com/createwith.ai/wp-content/uploads/2017/05/nsynth_architecture.png?resize=640%2C205)
![WaveNet Autoencoder](https://i1.wp.com/createwith.ai/wp-content/uploads/2018/08/wavenet_autoencoder.png?resize=840%2C481)




https://www.youtube.com/watch?v=iTXU9Z0NYoU&


[https://youtu.be/iTXU9Z0NYoU](https://youtu.be/iTXU9Z0NYoU)

デモ https://experiments.withgoogle.com/ai/sound-maker/view/


WaveNet Autoencoderをつかった音楽の変換
📃 **A Universal Music Translation Network**
Mor, N., Wolf, L., Polyak, A., & Taigman, Y. (2018). A Universal Music Translation Network. Retrieved from http://arxiv.org/abs/1805.07848
[解説] [WaveNetを使ったAutoencoderで音楽のドメイン間の変換を可能に! – A Universal Music Translation Network](http://createwith.ai/paper/20180813/1317)

ピアノ曲を交響曲に、口笛をコーラスに変換するといったことが可能に!! 　上のNSynthのWaveNet Autoencoderを拡張したもの.   Encoderは共通. 変換したいドメインごとにDecoderを用意. 

![A Universal Music Translation Network](https://i2.wp.com/createwith.ai/wp-content/uploads/2018/08/universal-music-translation.png?zoom=2&fit=840%2C520)



https://www.youtube.com/watch?v=vdxCqNWTpUs&


[https://youtu.be/vdxCqNWTpUs](https://youtu.be/vdxCqNWTpUs)



**GANの利用**
[GANによる音の生成 – Synthesizing Audio with Generative Adversarial Networks](http://createwith.ai/paper/20180216/1192)
Donahue, C., McAuley, J., & Puckette, M. (2018). Synthesizing Audio with Generative Adversarial Networks. Retrieved from http://arxiv.org/abs/1802.04208

波形を直接生成するWaveGANとスペクトログラムを生成するSpecGANの二つの手法を提案. 

![Synthesizing Audio with Generative Adversarial Networks](https://i1.wp.com/createwith.ai/wp-content/uploads/2018/02/gan_synth.png?zoom=2&fit=840%2C628)


WaveGANのほうが音の多様性、音質共によかったらしいです. 










生成したスペクトログラムをGANのDiscriminatorで識別.

![GAN  DrumMachine](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533980964763_image.png)

https://www.youtube.com/watch?v=z15mU3UORmo&


[https://youtu.be/z15mU3UORmo](https://youtu.be/z15mU3UORmo)

論文の原著者らのオンラインデモ
https://t.co/KEP3Gw7T9X

おまけ - SpecCAN Creative Adversarial Networkの考え方をSpecGANに応用してみた… by 徳井

https://www.dropbox.com/s/4r43rzayr54te25/speccan_gan_audio-4144.mp4?dl=0




# 2.音楽生成 

音楽生成については過去についてはこちらに詳しくまとめてます. 
[**Deep Learningを用いた音楽生成手法のまとめ [サーベイ] – Nao Tokui (Qosmo) – Medium**](https://medium.com/@naotokui/deep-learning%E3%82%92%E7%94%A8%E3%81%84%E3%81%9F%E9%9F%B3%E6%A5%BD%E7%94%9F%E6%88%90%E6%89%8B%E6%B3%95%E3%81%AE%E3%81%BE%E3%81%A8%E3%82%81-%E3%82%B5%E3%83%BC%E3%83%99%E3%82%A4-1298d29f8101)
****
大きく分けて二つの方向


1. **MIDI/楽譜を生成 → シンセサイザーで再生 or 人が演奏**

    MIDIなど以外にもテキストで音楽を表すABC記法やギターのタブ譜を生成する例も
    
    ○ 音楽を構造的に扱いやすい (小節、拍子、スケール etc) 
    × 最終的にシンセで鳴らす音・人の演奏に音楽の質が依存. 
    

![楽譜](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8e/Chopin_Prelude_7.svg/300px-Chopin_Prelude_7.svg.png)
![MIDI](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bb/Computer_music_piano_roll.png/220px-Computer_music_piano_roll.png)



2. **音の波形を直接生成**

○ 音・音楽そのものを生成できる. 
× 計算量が膨大
× 構造を持たせるのが難しい. 


![PCM](https://upload.wikimedia.org/wikipedia/commons/thumb/2/21/4-bit-linear-PCM.svg/1200px-4-bit-linear-PCM.svg.png)
![Waveform](https://qph.fs.quoracdn.net/main-qimg-50fd5810005b18982fc715b760e32c8f)


楽譜/MIDIといったシンボルレベルでの音楽生成が一般的. ここ数年(特にWaveNet以降) 音を直接扱う研究が増えてきている. 



## 2.1 シンボル(楽譜/MIDI)レベルの音楽生成

楽譜/MIDI    アルゴリズム作曲の世界で古くから…  


Deep Learningを用いたシステとしては、**時系列データを扱いやすいRNN(特にLSTM)を使った研究が主流.**  テキストの生成の場合と同様に、たとえば一小節分のメロディーに対して、次の一小節を生成し、それを入力としてそのまた次の一小節を生成する(あるいはある音符一つを入力に次の音符を生成…  )といった形で、長いメロディーが生成される. 

**LSTMをつかった音楽生成**
📃 *Eck, D., & Schmidhuber, J. (n.d.).* ***A First Look at Music Composition using LSTM Recurrent Neural Networks.*** *Retrieved from* [*http://people.idsia.ch/~juergen/blues/IDSIA-07-02.pdf*](http://people.idsia.ch/~juergen/blues/IDSIA-07-02.pdf)


https://w.soundcloud.com/player/?url=https%3A%2F%2Fsoundcloud.com%2Fdeeplearning-music%2Flstm-0224-1510%23t%3D0%3A01&autoplay=false


[https://soundcloud.com/deeplearning-music/lstm-0224-1510#t=0:01](https://soundcloud.com/deeplearning-music/lstm-0224-1510#t=0:01)

![Blues Generation](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1534053057375_image.png)


ある音と伴奏のコードに対して、次の音とコードを出力する. 









**オンライン- デモ - 似た仕組み** 
Google MagentaプロジェクトがWebで遊べるデモを公開している. 

Neural Melody Autocompletion
https://codepen.io/teropa/full/gvwwZL/


Neural Drum Machine
https://codepen.io/teropa/pen/JLjXGK



**演奏の学習 Performance RNN**
[機械学習による、「演奏」の学習 – Performance RNN: Generating Music with Expressive Timing and Dynamics –](http://createwith.ai/demo/20170701/849)
終わり(note-off)の情報も各音符に持たせることでより自然な表現が可能に! 

![](https://i2.wp.com/createwith.ai/wp-content/uploads/2017/07/performance_rnn_time_shift-1.png?resize=640%2C325)



https://www.youtube.com/watch?v=JVf6esaXeLE&


[https://youtu.be/JVf6esaXeLE](https://youtu.be/JVf6esaXeLE)

オンラインデモ
https://magenta.tensorflow.org/demos/performance_rnn/index.html

**音楽生成にGANを使った例**
📃 **Yang, L.-C., Chou, S.-Y., & Yang, Y.-H. (2017). MidiNet: A Convolutional Generative Adversarial Network for Symbolic-domain Music Generation using 1D and 2D Conditions.**

![MidiNet](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1534060136086_image.png)


RNNではなくCNNを利用. 1022のポップスのメロディーを学習。2オクターブの範囲で時間の最小単位が16分音符としてピアノロールのフォーマットで表現しています。またone-hotベクトルで表現したコードの情報を条件付け(conditioning)の入力として使っているのも特徴。


https://w.soundcloud.com/player/?url=https%3A%2F%2Fsoundcloud.com%2Fdeeplearning-music%2Fmidinet-demo-gen6&autoplay=false


[https://soundcloud.com/deeplearning-music/midinet-demo-gen6](https://soundcloud.com/deeplearning-music/midinet-demo-gen6)



    ## 2.2 音楽生成 - 音響レベル

WaveNet x シンボルレベルの表現
[Combining Deep Symbolic and Raw Audio Music Models](http://people.bu.edu/bkulis/projects/music/index.html)
Manzelli, R., Thakkar, V., Siahkamari, A., & Kulis, B. (2018). Conditioning Deep Generative Raw Audio Models for Structured Automatic Music. Retrieved from http://arxiv.org/abs/1806.09905


![アーキテクチャ](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1534054705617_image.png)

https://www.dropbox.com/s/lx6fbm5u21iliy5/CombiningDeepGenearativeRawAudioModels..Symbolic.mp4?dl=0


[https://www.dropbox.com/s/lx6fbm5u21iliy5/CombiningDeepGenearativeRawAudioModels..Symbolic.mp4?dl=0](https://www.dropbox.com/s/lx6fbm5u21iliy5/CombiningDeepGenearativeRawAudioModels..Symbolic.mp4?dl=0)




# 4. クロスモーダル

******Text ↔ Audio   Audio ↔ Image  (Image ↔ Text) などモーダル (情報の形態)をまたいだモデル**


**Aytar, Y., Vondrick, C., & Torralba, A. (2016). SoundNet: Learning Sound Representations from Unlabeled Video, (Nips).** Retrieved from http://arxiv.org/abs/1610.09001
[SoundNet: Learning Sound Representations from Unlabeled Video - MIT](http://soundnet.csail.mit.edu/)


- ビデオの各瞬間のフレーム(画像)と音の関係を学習.  
  - 3つのCNNを利用. そのうち二つは学習済みの画像認識のモデル (一つはImageNetで学習・もう一つは場所の認識を行うPlacesNetで学習)
  -  もうひとつは音の波形に適用する一次元の入力を持ったCNNで未学習のもの (SoundNetと命名されている). 


- ある瞬間のフレームとその時の音をそれぞれのネットワークに入力. 学習済みの画像認識のモデルの出力にSoundNetのアウトプットが「近く」なるように、SoundNetを学習する. 
  - 確率分布の類似度を算出する　KL Divergenceを誤差関数として使用. 
        
    
![SoundNetアーキテクチャ](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533774451376_image.png)



https://www.youtube.com/watch?v=yJCjVvIY4dU&


[https://youtu.be/yJCjVvIY4dU](https://youtu.be/yJCjVvIY4dU)



**Kajihara, Y., Dozono, S., & Tokui, N. (n.d.). Imaginary Soundscape : Cross-Modal Approach to Generate Pseudo Sound Environments. Retrieved from** https://nips2017creativity.github.io/doc/Imaginary_Soundscape.pdf

SoundNetを仕組みを利用し、あらかじめ大量に音のサンプルを用意しておくことで、風景画像にぴったりくる音を選ぶ. Google StreetViewのインタフェースを用いて、仮想のサウンドスケープの中を歩き回ることができる. 

Webサイト
http://imaginarysoundscape.qosmo.jp/

![Imaginary Soundscape](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1533775299061_image.png)

https://www.youtube.com/watch?v=uU-sZq2JOY4&


[https://youtu.be/uU-sZq2JOY4](https://youtu.be/uU-sZq2JOY4)

画像をアップロードして音をつけることも可能…
http://imaginarysoundscape2.qosmo.jp/

Imaginary Landscape - 現在初台のICCで展示中

https://www.youtube.com/watch?v=yJhL_xvEEls&


[https://youtu.be/yJhL_xvEEls](https://youtu.be/yJhL_xvEEls)



**Zhou, Y., Wang, Z., Fang, C., Bui, T., & Berg, T. L. (2017). Visual to Sound: Generating Natural Sound for Videos in the Wild. Retrieved from http://arxiv.org/abs/1712.01393**

**動画から直接音の波形を生成**

https://www.youtube.com/watch?v=eBrsJpuPol0&


[https://youtu.be/eBrsJpuPol0](https://youtu.be/eBrsJpuPol0)


![モデル](https://i1.wp.com/createwith.ai/wp-content/uploads/2018/01/v2audio_model.png?resize=840%2C411)


動画の各フレームの情報を解析するエンコーダと、エンコードされた情報から波形を生成するデコーダから構成される. デコーダには[SampleRNN](https://arxiv.org/abs/1612.07837)のアーキテクチャが用いられました (上図 a)。

画像のフレームをVGG19に入力。出力される特徴量を、デコーダの一番高次のtierのRNNの入力とします。 (動画のフレームレートと音のサンプリングレートでは音のサンプリングレートの方が格段に高いので、動画の同じフレームの情報が複数回繰り返し入力として使われます)　

学習に使ったデータは、赤ちゃんの鳴き声、犬が吠える音、花火、チェーンソーといったカテゴリーごとにYouTubeの動画を集めた[AudioSetのデータ](https://research.google.com/audioset/dataset/index.html)を利用。注意すべきはこのモデルは**あくまでも各カテゴリーごとに動画と音の関係を学習するもので、任意の映像に対して音を生成できるわけではない**ということ(本研究では10のカテゴリーについて学習を行なっています)。


**Owens, A., & Efros, A. A. (n.d.). Audio-Visual Scene Analysis with Self-Supervised Multisensory Features. Retrieved from http://andrewowens.com/multisensory**
動画の音と映像の関係に着目し、動画内の音源の位置の特定や、画面の中で鳴っている音(=音源が映っている音)と画面の外側で鳴っている音を分離したりといったタスクをこなす研究。


https://www.youtube.com/watch?v=rwCIRu_hAJ8&


[https://youtu.be/rwCIRu_hAJ8](https://youtu.be/rwCIRu_hAJ8)

動画を大量に収集→その一部の動画の音をわざとすこしずらす. → 音がずらされているかどうかを識別するモデルを学習 (下の左)  → 「同期している」というアウトプットが映像のどこに反応しているかを可視化すると 音源位置の推定ができる(右下) 


![同期しているかどうかを判定するモデル](https://i0.wp.com/createwith.ai/wp-content/uploads/2018/05/audio-visual-scene.png?resize=542%2C373)
![音源位置の推定](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1534056062479_image.png)


無関係な動画の音をランダムに加えた動画をつくる → それぞれの音のスペウトログラムの分離を行う. →この際に上記の同期しているかどうかを判定しているモデルのレイヤーの情報を入力に加える. 

![](https://i0.wp.com/createwith.ai/wp-content/uploads/2018/05/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88-2018-05-20-21.25.57.png?resize=517%2C442)


 📃 [The Sound of Pixels](http://sound-of-pixels.csail.mit.edu/)
**Zhao, H., Gan, C., Rouditchenko, A., Vondrick, C., McDermott, J., & Torralba, A. (2018). The Sound of Pixels. Retrieved from http://arxiv.org/abs/1804.03160**

https://www.youtube.com/watch?v=2eVDLEQlKD0&


[https://youtu.be/2eVDLEQlKD0](https://youtu.be/2eVDLEQlKD0)


![アーキテクチャ](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1534061589752_image.png)
![学習の仕組み](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1534061610635_image.png)




# 5. 応用例


Neural Beatbox

https://codepen.io/naotokui/pen/NBzJMW

https://www.youtube.com/watch?v=_QUinTO2n2M&


[https://youtu.be/_QUinTO2n2M](https://youtu.be/_QUinTO2n2M)





# まとめ


- 画像処理の技術が音響処理にも応用可能なことが証明されてきた. 


- 音響処理は画像などの付随する情報をも使ったクロスモーダル・モデルの研究があつい！


- 音楽生成はシンボルレベルから音を直接扱う方向に
- GANがやはり音楽領域でも要注目


“Good artists copy, great artists steal.”  Pabro Picaso
人間のつくった過去の音楽を学習することで独創的な音楽を作れるのか?


![](https://d2mxuefqeaa7sj.cloudfront.net/s_9691C22AEB540506669D4C8203AAA653A6715D130A39FB17207BC4EBB80F3799_1534059995283_image.png)

****

# その他の参考資料/リンク
****
チュートリアル
[keunwoochoi/dl4mir: Deep learning for MIR](https://github.com/keunwoochoi/dl4mir)
[tuwien-musicir/DL_MIR_Tutorial: Deep Learning on Music Information Retrieval Tutorial](https://github.com/tuwien-musicir/DL_MIR_Tutorial)

Google Magenta 
音楽を中心に、機械学習 x Artの研究グループ
[Blog](https://magenta.tensorflow.org/blog)



