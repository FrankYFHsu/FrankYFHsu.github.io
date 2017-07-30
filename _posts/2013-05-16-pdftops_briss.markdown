---
layout: post
comments: true
title:  " \"PDF to EPS\" and \"crop a PDF file\" "
excerpt: ""
date:   2013-05-16 01:12:00
---
最近這幾天在忙投稿的事，由於是用`LaTex`來排版，為了好看，所以圖都是`eps`格式 ( 其實也是可以用pdf格式的圖，然後用pdfLaTex來編譯，但不知道投期刊可否用這種方式。)


而要產生eps格式的數據圖，以住都是excel產生好後，複製貼到power point上(跳過這步的圖都醜醜的...)，再複製貼到visio上另存pdf檔，再用Acrobat去邊，再另存成EPS檔。所以電腦要灌Adobe Acrobat最後才能轉檔，但是Acrobat要錢，不是每台電腦都有這軟體。此外，用Acrobat轉出來的EPS檔莫名的大，包含了一堆訊息，動不動就幾MB，所以最近就在找windows系統有那些小軟體可以用來PDF轉EPS，雖然在miktex下，有pdf2ps這個小工具，但是轉出來的品質我覺得差太多了。最後發現，Xpdf下的`pdftops`，轉出來的品質滿不錯的，可能顏色會偏一點，但其他的都跟原來沒兩樣

Xpdf的下載連結

<http://www.foolabs.com/xpdf/download.html>

不過轉出來的圖若需要切白邊，這時有兩種作法:

1. 第一種是以eps檔去切，也就是用GsView開eps檔，再從工具列點選 File = &gt; PS to EPS這個功能來切邊，它可以幫你自動計算白邊，也可以自己手動點，手動點就考驗一點眼力了，因為它不能即時預覽。
2. 第二種則是在PDF檔時，即先切邊。google到一個還不錯用的軟體叫`Briss`，可以自動計算白邊，也可以手動拉，重點是可即時預覽，滿方便的。

Briss的下載連結

<http://sourceforge.net/projects/briss/>

不過說真的，現在也只有在畫元件圖時，才會這樣從PDF轉EPS，數據圖轉來轉去實在是有點費工，更不用說在excel裡，要畫個xy軸是黃金比例的圖有多難拉，而且如果數據一堆，突然老師說某個名詞要改，或是點線風格該改怎樣，要複製來複製去的真的要花很多時間。所以後來都用`gnuplot`來畫數據圖，要pdf格式還是要eps格式都行。
