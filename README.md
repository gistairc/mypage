# AIST Big Solar Panel Image in Japan (ABSoPI)  (タイトル未定)
## Overview
 **A**IST **B**ig **So**lar **P**anel **I**mage (**ABSoPI**) dataset using satellite imagery in Japan.  


The number of solar power plants is growing so globally and rapidly that we need to rely on satellitel observations and efficient machine learning methods for the monitoring. AAAA  is a  training and validation dataset by  AIST (正式名称) to support global survey of solar power plants all over the world.  


The source data is the multiband imagery taken by Landsat 8 satellite （リンク） and .the detailed description can be found in Ishii et al. (ICPR paper)  

We have picked up the location of all the solar power plants on（WEB の URL） which generates more than 5MW electricity and the construction had been completed by 2015. The multiband images of these target area, taken by Landsat-8, were cropped into a 16 × 16 grid covering a 480 × 480 meter area.  

![fig:ABSoPI image patch example](https://github.com/hmiyamoto/ABSoPIdataset/blob/master/fig1.jpg "megasolar image patch example")  


Landsat 8の説明 リンクはっとけばいいのでは？  

・ICPR論文のfig1 fig2を利用  
・テーブルを載せるband1~7  






This patch images are classified as “positives” if the solar panels coverwith more than 20% of the total areas, while patches with no solar panels are considered “negatives”. It should be noted that patches whose coverage lies between 0% and 20%were neither “positives” and “negatives”.)  and smaller (<5MW) and newer (after 2015) solar power plants are not included in this datase.  


検知された結果に入っている、新しいのや小さいのは training には入ってないけど test  だか　Validation には追加したんだっけ？　であれば、その記述も。。。  

You can download AAAA with two different format (HDF5 and GeoTiff) and the source code for the classification described in AAAA.  


There are papers using ABSoPI dataset.  
[1] *Tomohiro Ishii, Edgar Simo-Serra, Satoshi Iizuka, Yoshihiko Mochizuki, Akihiro Sugimoto, Ryosuke Nakamura, Hiroshi Ishikawa ,"Detection by Classification of Buildings in Multispectral Satellite Imagery," ICPR 2016.* (http://www.f.waseda.jp/hfs/IshiiICPR2016.pdf)  
[2] *Nevrez Imamoglu, Motoki Kimura, Hiroki Miyamoto, Aito Fujita, Ryosuke Nakamura,"Solar Power Plant Detection on Multi-Spectral Satellite Imagery using Weakly-Supervised CNN with Feedback Features and m-PCNN Fusion," BMVC 2017.* (https://arxiv.org/abs/1704.06410)  

and open this paper[1]'s source code.  

## Download  
**IMPORTANT** -- Please read the [Terms of Use](https://github.com/hmiyamoto/ABSoPIdataset/blob/master/LICENSE.md) before downloading the ABSoPI dataset.


#### hdf5
HDF5 version (for using Torch version code) of the dataset can be downloaded from [here](http://data.airc.aist.go.jp/ABSoPIdataset/ABSoPIdata_hdf.zip) (4.6GB) .  
Or type the following in the terminal.  

```
$ wget http://data.airc.aist.go.jp/ABSoPIdataset/ABSoPIdata_hdf.zip
$ unzip ABSoPIdata_hdf.zip
```

Schematic of the directory configuration in the unzipped files is as follows:  
```
./resource/
train/  
	LC81060302015147LGN00.hdf5
	LC81070302015266LGN00.hdf5 ...
val/
	LC81060302015147LGN00.hdf5
	LC81070302015266LGN00.hdf5 ...
test/
	LC81060302015147LGN00.hdf5
	LC81070302015266LGN00.hdf5 ...
```

#### tiff
Tiff version (for using Chainer version code) of the dataset can be downloaded from [here](http://data.airc.aist.go.jp/ABSoPIdataset/ABSoPIdata_tiff.zip) (4.2GB) .  
Or type the following in the terminal.  
```
$ wget http://data.airc.aist.go.jp/ABSoPIdataset/ABSoPIdata_tiff.zip
$ unzip ABSoPIdata_tiff.zip
```
Schematic of the directory configuration in the unzipped files is as follows:  
```
./resource/
train/
	positive/
		LC81060302015147LGN00_274_300_2064.tiff
		LC81060302015147LGN00_274_300_13289.tiff ...
	negative/
		LC81060302015147LGN00_100_105.tiff
		LC81060302015147LGN00_100_114.tiff ...
val/
	positive/
		LC81070352015298LGN00_206_266.tiff
		LC81070352015298LGN00_374_160.tiff ...
	negative/
		LC81060302015147LGN00_2_86.tiff
		LC81060302015147LGN00_4_88.tiff ...
test/
	positive/
		LC81060302015147LGN00_79_323.tiff
		LC81060302015147LGN00_80_323.tiff ...
	negative/
		LC81060302015147LGN00_100_100.tiff
		LC81060302015147LGN00_100_101.tiff ...
```

## Source
### Torch ver  
#### Requierment
* torch7  
For torch installition see http://torch.ch/  
* torch_toolbox  
Download from https://github.com/e-lab/torch-toolbox  
Unzip it and put on it same directory.  
```
FOR EXAMPLE
	<dir>torch/
		<dir>resource
		<dir>torch-toolbox
		train-cnn.lua
		train-cnn.sh
		test-cnn.lua
		test-cnn.sh ...
```
 
Can be changed by passing in train-cnn.lua line 9.

#### Training
For trainging, type the following this code in the terminal.  

```
$ sh train-cnn.sh
```
Models are saved to "./ishiinet_p1n15/cnn_nm_epXXXX.net" (Can be changed by passing in train-cnn.sh) .  

#### Testing

Type the following this code in the terminal.  

```
$ sh test-cnn.sh
```
Result file are saved to "./ishiinet_p1n15/test_th0.999_all_cm.txt".  
Can be changed by passing in this shell file.  


### Chainer ver
#### Requierment
* Python 2.7.*  
* Chainer 1.24.*  
For chainer Installition see from https://chainer.org/  

#### Training
Type the following this code in the terminal.   

```
$ sh train.sh
```
 
Models are save to ./result/ (Can be changed by passing in this shell file) . 

#### Testing
Type the following this code in the terminal.   

```
$ sh test.sh > result.log
```

Result file are created to ./result.log .  

## Acknowledgement
This dataset and source code are based on results obtained from a project commissioned by the New Energy and Industrial Technology Development Organization (NEDO).  
