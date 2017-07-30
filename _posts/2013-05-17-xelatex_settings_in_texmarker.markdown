---
layout: post
comments: true
title:  "Texmaker XeLaTeX設定"
excerpt: ""
date:   2013-05-17 13:24:00
---
最近把Texmaker 3.3 更新到Texmaker 4.0.2後，原本在快速編譯下是沒有`XeLaTeX`這個選項的，不知道從那個版本後，Texmaker終於支援了
<div style="text-align:center;"><img src="/assets/2013-05-17_124957.png"></div>

這樣就可以用比較喜歡的快捷鍵設定來用XeLaTeX編譯(原本的F5用不到，就可以拿來給XeLaTeX)
<div style="text-align:center;"><img src="/assets/2013-05-17_130444.png"></div>

不然之前都是在自定命令裡設XeLaTeX編譯，那樣就只能用`Alt+Shift+F1~5`的組合鍵。不過，有時候文章會修改到cite和ref時，就要加入BibTeX編譯，就變成要`XeLaTeX編譯+BibTeX編譯+XeLaTeX編譯+XeLaTeX編譯`，有時候圖一多，XeLaTeX編譯一次會花不少的時間，所以這樣的組合編譯還是用自定命令會比較省麻煩一點。既然Texmaker已支援XeLaTeX，自定命令的命令設定也就比較簡單一點了，可以用命令精靈來設定
<div style="text-align:center;"><img src="/assets/2013-05-17_131441.png"></div>
