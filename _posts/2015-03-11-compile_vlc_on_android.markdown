---
layout: post
comments: true
title:  "Compile vlc on android"
excerpt: "compile issue?"
date:   2015-03-11 22:13:00
---
https://wiki.videolan.org/AndroidCompile/

紀錄一下遇到的問題：

第一次進行sh compile.sh 時，出現
```
Archive:  gradle-2.2.1-all.zip

  End-of-central-directory signature not found.  Either this file is not

  a zipfile, or it constitutes one disk of a multi-part archive.  In the

  latter case the central directory and zipfile comment will be found on

  the last disk(s) of this archive.

unzip:  cannot find zipfile directory in one of gradle-2.2.1-all.zip or

        gradle-2.2.1-all.zip.zip, and cannot find gradle-2.2.1-all.zip.ZIP, period.
```

在資料夾底下 都會有一個未完整的gradle-2.2.1-all.zip，爬了一下文http://metalkin.tistory.com/82

雖然說是韓文...但大概可以猜到怎麼解

修改 `compile.sh` at `Line 81`:

原：
```sh
wget ${GRADLE_URL} 2>/dev/null || curl -O ${GRADLE_URL}
```
改：
```sh
wget ${GRADLE_URL} 2>/dev/null || curl -O -L ${GRADLE_URL}
```

