# Beagleの使い方

##### -「第33回 DDBJing 講習会 in 東京 」 2015.11.11
###### NGSを用いたジェノタイピングを様々な解析に用いるには？
***
#### Beagleとは
genotype calling, genotype phasing, ジェノタイピングされていないマーカーの補完(imputation),IBD segment detectionを行うソフトウエア
- 2015.11.11現在の[最新版](http://faculty.washington.edu/browning/beagle/beagle.html)はBeagle version 4.1
- Beagle version 4.1.では家系情報を考慮しない。  
- phaingに親子関係を利用する場合には[Beagle version 4.0](https://faculty.washington.edu/browning/beagle/b4_0.html)を利用  

#### Beagleのインストール

- Beagle 4.1の場合、Java version 8が必要  
- 以下のコマンドでJavaのバージョンを確認　　

`java -version`　

- beagle.21Oct15.abc.jar のダウンロード  

[HPからのBeagleのダウンロード](https://faculty.washington.edu/browning/beagle/beagle.html#download)
- wget を使う方法  

`wget http://faculty.washington.edu/browning/beagle/beagle.21Oct15.abc.jar`　　

- [Beagleのマニュアル](https://faculty.washington.edu/browning/beagle/beagle_4.1_21Oct15.pdf)

***

#### Beagleの入力ファイル
- vcfおよびvcf.gzを利用可能
- vcf fileのformatを確認する必要がある  
vcf format v4.3に関しては[ここ](https://samtools.github.io/hts-specs/VCFv4.3.pdf)で確認
- Beagleで利用するためにはGTあるいはGLのFORMATが必要

__GT__ : genotype, encoded as allele values separated by either of / or |. The allele values are 0 for the reference
allele (what is in the REF field), 1 for the first allele listed in ALT, 2 for the second allele list in ALT and
so on.  　

__GL__ : genotype likelihoods comprised of comma separated floating point log10-scaled likelihoods for all possible　genotypes given the set of alleles defined in the REF and ALT fields.

- 染色体ごとにvcfを分けてから実行すると良い  

***

#### Beagleの実行


-  Format GT vcf file

`java -jar beagle.21Oct15.abc.jar gt="Sbicolor_255_1000snp.vcf" out="Sbicolor_255_out"`  
 testdata sorghum vcf file [こちら](https://github.com/hkanegae/ddbjing-33/blob/master/testdata/Sbicolor_255_1000snp.vcf)からダウンロード可能
  - [Sbicolor_255_1000snp.vcf](https://github.com/hkanegae/ddbjing-33/blob/master/testdata/Sbicolor_255_1000snp.vcf)
  - [phytozome sorghum v.2.1](http://phytozome.jgi.doe.gov/pz/portal.html#!info?alias=Org_Sbicolor)
  - SNP数 3,699,951のうち、1000snpのみを取り出したファイル
  - 22系統
  - 出力されるファイル　
   - [Sbicolor_255_out.log](https://github.com/hkanegae/ddbjing-33/blob/master/testdata/Sbicolor_255_out.log)
   - [Sbicolor_255_out.warnings](https://github.com/hkanegae/ddbjing-33/blob/master/testdata/Sbicolor_255_out.warnings)
   - [Sbicolor_255_out.vcf.gz](https://github.com/hkanegae/ddbjing-33/blob/master/testdata/Sbicolor_255_out.vcf) <- imputed file

リファレンスパネルを利用した欠測の補完
-  Running test analysis with \"ref=\" argument  
-  ref=でリファレンスパネルのvcf fileを指定、gt=でgt fieldのあるvcf fileを指定

`java -jar beagle.21Oct15.abc.jar ref="ref.21Oct15.abc.vcf.gz" gt="target.21Oct15.abc.vcf.gz" out="out.ref"`  

- Format GL vcf file  

`java -jar beagle.21Oct15.abc.jar gl="test.21Oct15.abc.vcf.gz" out="out.gl"`


***

####  conform-gt programの実行
- conform-gt programはreference VCF fileと矛盾がないように、target vcf fileを修正するプログラム
- target VCF fileは少なくとも20個体以上のデータを含む必要がある  

`java -jar conform-gt.jar ref=chr20.1kg.ref.phase1_release_v3.20101123.vcf.gz gt=chr20.vcf.gz chrom=20 out=mod.chr20 excludesamples=non.eur.excl`
