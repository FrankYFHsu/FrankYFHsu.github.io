---
layout: post
comments: true
title:  "Requires ACCESS_MOCK_LOCATION secure setting"
excerpt: "Android setting"
date:   2015-03-15 17:58:00
---

紀錄一下：

在執行有使用到Mock Location的app時，出現
```
E/AndroidRuntime(889): Caused by: 
java.lang.SecurityException: Requires ACCESS_MOCK_LOCATION secure setting
```

雖然`AndroidManifest`裡已有設定權限了，這問題還是存在。原來使用實體手機驗証時，需要把開發人員選項裡的"允許模擬位置"打開才行。