# ddbjing-33

### 「第33回 DDBJing 講習会 in 東京 」 2015.11.11

#### NGSを用いたジェノタイピングを様々な解析に用いるには？
#####         ～高密度SNPデータ解析の処方箋～  
###### 東京大学大学院農学生命科学研究科 生産・環境生物学専攻 生物測定学研究室 特任研究員  
###### 鐘ケ江　弘美  

***

これは第33回 DDBJing 講習会 in 東京の講義資料です。  
[第33回 DDBJing 講習会 in 東京 公式ホームページはこちら](http://www.ddbj.nig.ac.jp/ddbjing/ddbjing-33.html)

### はじめに
育種の現場では様々な分子マーカーが利用されてきました。  
SSRマーカーやSNPマーカーが多く利用されていますが、最近ではNGSを利用したジェノタイピングが増えています。  
RAD-seqデータにおける遺伝子型Imputationの実際について紹介します。

### 講習会参加者の皆様へお知らせ
#### 講義資料に関しては[google drive](https://drive.google.com/file/d/0B-NbQqcD0i0nM0pQMzd5RnQwU2c/view?usp=sharing)からダウンロードしてください。  
[slideshare](http://www.slideshare.net/HiromiKanegae/ngs-54890142)でも利用可能です。  

#### testdataを含めたすべてのデータは、このgithubのページの右側のDownload zipのボタンをクリックすることでダウンロード可能です。
申し訳ございませんが、講習の中では、このデータを使って実際に解析をする予定はありません。  
ファイルの内容を実際にご覧頂くために、また講習会後、実際にソフトを試していただくことを考えて、test dataをアップロードしてあります。  
混乱を招く結果となってしまったことを、深くお詫び申し上げます。

__このページは資料を公開した15.11.09以降も、必要に応じて修正する可能性がございます。__  
__ご迷惑をおかけ致しますが、よろしくお願い致します。__

***
### 講習の予定
- 様々な分子マーカーと特徴
- [Imputationについて](https://github.com/hkanegae/ddbjing-33#1imputationとは)  
  - なぜ Imputationが必要か？
  - Reference panelの利用について
- Imputationのソフトについて  
  - [Tasselの使い方](https://github.com/hkanegae/ddbjing-33/blob/master/Tassel.md)
  - [Beagleの使い方](https://github.com/hkanegae/ddbjing-33/blob/master/Beagle.md)

***
### 様々な分子マーカーと特徴
- Simple Sequence Repeats (SSR) markers

  - 遺伝子のマッピングやQTL解析、マーカー選抜など様々な解析に利用される
  - 共優性マーカー(codominant maker)、multiallelicマーカー
  - 再現性が高く、他の種でも利用可能　　


- Single Nucleotide Polymorphism (SNP) markers　　

  - SSRマーカーと比較するとハイスループット　　
  - 連鎖地図やゲノミックセレクション、GWASに利用されている　　


- Next generation sequencing (NGS) を使ったジェノタイピング　　

  - RAD-seq、GBS、low depth WGS
  - 一度に多くのSNPを得ることができる
  - マーカーの偏りが少ない
  - 欠測も多い



### 1.Imputationとは？  

ゲノムワイド関連解析(GWAS)やゲノミックセレクションを行うためには多数のサンプルを高密度・高精度にジェノタイピングすることが必要となります。  

NGSを用いることで、多数のサンプルをジェノタイピングすることが可能となりました。  

たとえば、RAD­-seqでは低コスト・高精度にSNP部位を検出することが可能ですが、ゲノムの一部しか読むことが出来ず、また欠測率も高くなります。  
また、実験ごとに得られるマーカーが異なる場合があります。
すべてのマーカーを利用して解析を行うためには、imputationが必要です。　

![imputation](https://github.com/hkanegae/ddbjing-33/blob/master/Imputation.jpg)

- マーカーセットが異なるデータを用いる場合  

 - Imputationを行わない場合  
 両方のセットで遺伝子型データのある重なったマーカーしか利用できない  

 - Imputationを行う場合  
 2つのデータセットで共通していないマーカーの遺伝子型を補完するImputationを行うことで、
すべてのマーカーを利用できる

- NGS でのLow coverage と　High coverageの比較　　

 - Low coverage  
  欠測が多い  
  コストが低い  
	遺伝子型の正確性が低下する可能性　　

 - High coverage  
  欠測が少ない  
  コストが高い

そこで、遺伝子型予測ソフトを用い、高精度に遺伝子型を予測することで、コストを抑え、GSの予測精度や、GWASの検出力を高めることを目的としています。

| name     | URL                                                          |
|----------|--------------------------------------------------------------|
| Beagle   | https://faculty.washington.edu/browning/beagle/beagle.html   |
| Tassel   | http://www.maizegenetics.net/#!tassel/c17q9                  |
| IMPUTE2  | https://mathgen.stats.ox.ac.uk/impute/impute_v2.html         |
| PLINK    | http://pngu.mgh.harvard.edu/~purcell/plink/pimputation.shtml |
| minimac2 | http://genome.sph.umich.edu/wiki/Minimac2                    |

GWASやGSに関しては[こちら](http://papaya.ab.a.u-tokyo.ac.jp/sandbox/groups/iwata/wiki/984fd/attachments/1a879/ikushu2012f_ws_iwata_01.pdf?sessionID=af156069a86ea9d33c904040aab88011998880ee)を参照してください。

 - リファレンスパネルを用いた遺伝子型の予測  

  - サンプルとリファレンスパネルの中の個体で、遺伝子型を共有している領域を特定  
  - ゲノムに存在する連鎖不平衡とハプロタイプブロ ック構造を利用  
  - リファレンスパネルの遺伝子型とハプロタイプの情報から欠測している遺伝子型を補完

***
### 2.Imputationの手法  

#### 1.連鎖地図および物理地図のない場合のImputationの例  


RのmissForestを利用可能　　
  [Package ‘missForest’](https://cran.r-project.org/web/packages/missForest/missForest.pdf)　　

random forestを用いて、欠測値を予測

#### 2.物理地図のない場合のImputationの例  

Rのqtlを利用することが可能
[Package ‘qtl‘](http://www.rqtl.org/manual/qtl-manual.pdf)
連鎖地図を作成　　

地図距離に基づいて、欠測値を予測　　
calc.genoprob  : Calculate conditional genotype probabilities　　


#### 3.reference genomeがある場合のImputation　　

reference genomeがある場合は、様々なImputationのためのソフトを利用することが可能です。　　

今回はその中でTasselおよびBeagleを紹介します。  

　1.
  [Beagle](https://github.com/hkanegae/ddbjing-33/blob/master/Beagle.md)

　2.
  [Tassel](https://github.com/hkanegae/ddbjing-33/blob/master/Tassel.md)
  ***


　　
