# ddbjing-33

### 「第33回 DDBJing 講習会 in 東京 」

#### NGSを用いたジェノタイピングを様々な解析に用いるには？
#####         ～高密度SNPデータ解析の処方箋～

[第33回 DDBJing 講習会 in 東京 公式ホームページ](http://www.ddbj.nig.ac.jp/ddbjing/ddbjing-33.html)

#### 講義資料
育種の現場では様々な分子マーカーが利用されてきました。
SSRマーカーやSNPマーカーが多く利用されていますが、最近ではNGSを利用したジェノタイピングが増えています。
RAD-seqデータにおける遺伝子型Imputationの実際について紹介します。

***
1.Imputationとは？  

ゲノムワイド関連解析(GWAS)やゲノミックセレクションを行うためには多数のサンプルを高密度・高精度にジェノタイピングすることが必要となります。  

NGSを用いることで、多数のサンプルをジェノタイピングすることが可能となりました。  

たとえば、RAD­-Seqでは低コスト・高精度にSNP部位を検出することが可能ですが、ゲノムの一部しか読むことが出来ず、欠測率も高くなります。  

そこで、遺伝子型予測ソフトを用い、高精度に遺伝子型を予測することでGWASの検出力を高めることを目的としている。


1.連鎖地図および物理地図のない場合のImputation
RのmisForestを利用　　
  [Package ‘missForest’](https://cran.r-project.org/web/packages/missForest/missForest.pdf)　　

random forestを用いて、欠測値を予測

2.物理地図のない場合のImputation
Rのqtlを利用
[Package ‘qtl‘](http://www.rqtl.org/manual/qtl-manual.pdf)

遺伝距離に基づいて、欠測値を予測

3.reference genomeがある場合のImputation　　

reference genomeがある場合は、様々なImputationのためのソフトを利用することが可能です。　　

今回はその中でTasselおよびBeagleを紹介します。
  1. Tassel
  2. Beagle

  ***


　　
