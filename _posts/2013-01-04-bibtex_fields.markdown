---
layout: post
comments: true
title:  "BibTex欄位"
excerpt: ""
date:   2013-01-04 17:50:00
---

最近在整理bib檔，發現以前作的bib檔，欄位都有錯(難怪作出來的ref會被老闆退...)。要修改也是件累人的事，為了給學弟妹參考，想想還是打個心得，不要最後像我改了一個下午還改不完...

欄位會有錯，主要還是bibtex資料都是直接從網站下載下來就貼上去了，尤其是從IEEE下載的bibtex內容，都不太正確(ACM下載的也會有錯)

例如
```bibtex
@INPROCEEDINGS{4215676,
author={Wei-Jen Hsu and Spyropoulos, T. and Psounis, K. and Helmy, A.},
booktitle={INFOCOM 2007. 26th IEEE International Conference on Computer Communications. IEEE},
title={Modeling Time-Variant User Mobility in Wireless Mobile Networks},
year={2007},
month={may},
volume={},
number={},
pages={758 -766},
doi={10.1109/INFCOM.2007.94},
ISSN={0743-166X},}
```

首先在author這個欄位裡，應該用全名，不該有縮寫，因為有些期刊會要求完整的姓名，所以該改為
```bibtex
author = {Wei-Jen Hsu and Thrasyvoulos Spyropoulos and Konstantinos Psounis and Ahmed Helmy},
```
人名與人名間用`and`連接。

booktitle(會議名稱)我是習慣不倒裝，所以改為
```bibtex
booktitle = {Proceedings of the 26th IEEE International Conference on Computer Communications (INFOCOM'07)},
```
至於要不要放會議縮寫我不太確定。另外有些格式會要求Proceedings of the縮為Proc. 然後International縮為Int.
*補：我的期刊論文accept後，編輯人員是有幫我把論文後面的Reference裡，那些關鍵字能縮寫的都縮寫了*

month這欄位，雖然有些格式會要求縮寫，有些又要用全名，但這個就比較好解決，因為不同的bst檔通常會去定義字串符號例如MACRO {jan} {"Jan."}，所以只要改成用三字母的縮寫字串即可，如
```bibtex
month= may,
```
如果有日期，還可改成
```bibtex
month = may # " 6--12,",
```
注意，這欄都沒有用大括號，這是因為may是字串符號(相當於變數名稱吧？)，如果加了大括號就不會自動幫你換了。

pages這欄，我的習慣是用`pages={758--766}`, 但好像沒差，如果是日期那邊就會有差，用兩個減號才產生出長一點的減號(破折號Dash?)，頁碼這裡用一個就是長一點的減號(破折號Dash?)了


所以上述資料整理後：
```bibtex
@INPROCEEDINGS{Hsu2007,
  author = {Wei-Jen Hsu and Thrasyvoulos Spyropoulos and Konstantinos Psounis and Ahmed Helmy},
  title = {Modeling Time-Variant User Mobility in Wireless Mobile Networks},
  booktitle = {Proceedings of the 26th IEEE International Conference on Computer Communications (INFOCOM'07)},
  year = {2007},
  pages = {758--766},
  address = {Anchorage, Alaska, USA},
  month = May # " 6--12,",
  issn = {0743-166X}
}
```

ieee下載下來的bibtex還有另一個問題是journal的名稱，例如
```bibtex
journal={Mobile Computing, IEEE Transactions on}
```
我是習慣改為
```bibtex
journal = {IEEE Transactions on Mobile Computing},
```
或是使用字串符號搭配IEEEabrv.bib or IEEEfull.bib
```bibtex
journal = IEEE_J_MC ,
```
如此，只要`\bibliography{IEEEabrv,mybib}`，就會幫你把 IEEE_J_MC轉成縮寫的型式
```bibtex
"{IEEE} Trans. Mobile Comput."
```
或是`\bibliography{IEEEfull,mybib}`，幫你轉成全名。

至於從ACM下載的bibtex，除了會多一些不會用到的欄位外，唯一有問題的是 `address`和`location`這個欄位，觀察IEEE格式的範本，address應該是會議的地點，但是ACM下載下來的bibtex通常address = {New York, NY, USA}, (ACM的總部?我也不清礎)而location才是地點，如
```bibtex
location = {Dallas, Texas, United States},
```
如果要用IEEEtran的話，就要把address的資料改成location的資料，產生出來的reference list才會正確。
