# Tasselの使い方

##### -「第33回 DDBJing 講習会 in 東京 」 2015.11.11
###### NGSを用いたジェノタイピングを様々な解析に用いるには？
***
#### Tasselとは
  Trait Analysis by aSSociation, Evolution and Linkage  
  http://www.maizegenetics.net/#!tassel/c17q9  

  - 作物の解析に最適化  
  - 欠測の補完だけではなく、様々な機能がある  
  - GUIが充実しており、コマンドラインからではなく簡単に解析可能  

##### Tasselのインストール
 - HPからのダウンロード 
  - java 1.8 
  - http://www.maizegenetics.net/#!tassel/c17q9

#### Tasselの入力ファイル  
 - メニューのDataからLoadを選択　　→　Make Best Guess
 - vcf fileを含めた様々な形式のファイルを利用可能

#### Tassel　染色体ごとに分けたファイルを作成
 - Dataから Separateを選択  
    元のファイルの下に染色体ごとに分けたファイルが作成される

#### Tassel　データのフィルタリング
 - Filter →　Filter Genotype Table Sitesを選択  
    MAFでフィルタリング

#### Tassel　LD plotの作成
 - Analysis → Linkage Disequilibriumを選択  
   Result フォルダにLDの結果が表示される  
 - Result → LD plot
   LD plot が表示される

####   Tassel　Phenotype の欠測を補完  
 - Tassel formt で　phenotype ファイルを作成し、Load
 - Impute → Numerial Imputeを選択  
 - 欠測を補完する方法を選択  
     たとえば、平均値の代入など
 - 元のファイルの下にImputed ファイルが作成される

#### Tassel　Genotype の欠測を補完  
Tasselには2種類のImpute方法  
集団に合わせて使い分ける

- Impute By FILLIN  
 - Fast, Inbred Line Library ImputatioN  
 - generalized approach

- Impute BY FSFHap  
 - impute missing data in full sib families (bi-parental families)
 - Inbred の両親と後代のImputation
 - 欠測率が高く、ヘテロ率の高いGBSデータ用に開発  
 - 親の遺伝子型と後代の遺伝子型データが必要  
 - 両親の遺伝子型が正確である場合にはこれを利用した方が良い
