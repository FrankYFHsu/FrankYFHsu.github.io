---
layout: post
comments: true
title:  "Install Keras on Windows with Anaconda"
excerpt: "Steps for installing Keras using Tensorflow backend on Windows with Anaconda 4.4"
date:   2017-08-10 21:30:00
---

在 Windows 上安裝 Keras + Tensorflow 失敗了幾次，這邊紀錄一下安裝成功的步驟：

首先安裝 [Anaconda](https://www.continuum.io/downloads)。目前要在 Windows 上使用 Pythone + ML/DL 常用到的套件如 Numpy, Pandas, Matplotlib, Scipy 等等，我想用 Anaconda 應該是最簡單方便的吧。
不過因為目前 Tensorflow 只支援到 Python 3.5，而 Anaconda 4.4 預設是 Python 3.6，因此一種方法是直接換成 Python 3.5，一種則是透過 Conda 建立新的環境。

## 第一種 

1. 首先開啟 Anaconda Prompt，會進入到 Anaconda 的 root environment，之後的操作都是在這個 environment。接著用 Conda 安裝 Python 3.5。
```bash
> conda install python=3.5
```
由於降成 3.5，root environment 裡，有些套件的版本也會更著變動。
2. 參考 [Anaconda Cloud 上的解說](https://anaconda.org/conda-forge/tensorflow)，使用 Conda 安裝 Tensorflow
```bash
> conda install -c conda-forge tensorflow 
```
3. 接著安裝 Keras，我在這邊則是使用 pip 來裝
```bash
> pip install keras
```
不過也可以用 Conda 來安裝。[conda-forge / packages / keras ](https://anaconda.org/conda-forge/keras)
```bash
> conda install -c conda-forge keras
```
4. 安裝完後，執行 Python 測試一下。
```bash
>>> import keras
Using TensorFlow backend
```
看起來ok後，就來跑 Keras 提供的 example。找了一個看起來跑比較快的 [mnist_mlp.py](https://github.com/fchollet/keras/blob/master/examples/mnist_mlp.py)，執行結果如下：
<div style="text-align:center;"><img src="/assets/2017-08-10_210936.png"></div>

## 第二種：安裝在新的 environment 

若不想要root environment的 Python 降到 3.5，那麼可以使用 Conda 建立一個使用 Python 3.5 的環境 (environment)，之後要跑 Keras 就切到這個 environment。
開啟 Anaconda Prompt 後：
```bash
> conda create -n keras python=3.5
```
在這邊新建了一個名為 keras 的 environment，然後切換到這個 environment
```bash
> activate keras
```
因為我還不太清楚怎麼讓我新建的 environment 一開始就有我想要的套件，所以上面新建的這個 keras environment 不像 Anaconda 的 root environment 什麼都有。不過如果只是要跑 Keras 的話，這個 environment 安裝 Tensorflow 和 Keras 暫時就足夠了吧。
```bash
> conda install -c conda-forge tensorflow 
> conda install -c conda-forge keras
```
需注意，安裝完 Keras 之後，要在下列的檔案
`Anaconda3\envs\keras\etc\conda\activate.d\keras_activate.bat`
將
```
set "KERAS_BACKEND=theano"
```
改為
```
set "KERAS_BACKEND=tensorflow"
```
否則下次 `activate keras` 時，Keras 會使用 Theano 當 backend。