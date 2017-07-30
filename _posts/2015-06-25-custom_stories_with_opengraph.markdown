---
layout: post
comments: true
title:  "Custom Stories with Open Graph"
excerpt: ""
date:   2015-06-25 11:32:00
---

> 註：當初寫這篇的時候是2014/09/12，那時Facebook sdk還是3.X，現在(2015/06/25)已更新到4.X版，一些方法需要改寫。

舊：

最近在練習寫`android app with Facebook SDK`，想用FB的`Custom Stories with Open Graph`功能，讓使用者會自動在動態時報(Timeline)上發佈跟這個app有關的Story。

照著官網Posting using API calls的範例寫，
```java
 OpenGraphObject book = OpenGraphObject.Factory.createForPost("books.book");  
 OpenGraphAction readAction = OpenGraphAction.Factory.createForPost("books.reads");  
```
其中的`object("books.book")`和`action("books.reads")`都是FB原本提供的。

想說來用自己定義的story (action是Take ,object是 Bus)，卻不知道createForPost裡的參數分別要填什麼，填了("take")和("bus")都不行， 找了好久，注意到books.book(FB提供)和take(自定義)這兩個action的Graph API URL不一樣，才知道原來要加app的`Namespace`。

例如這個app的namespace是xx-yy，那想用自己定義的action和object，就是要填`("xx-yy:take")`和`("xx-yy:bus")`。

* * *
更新(2015/06/25)：

原本的寫法是OpenGraphObject、OpenGraphAction配合RequestBatch，但到了4.X，這三個類別被替換掉了。而發佈custom stories 也變更簡單，根據官網範例，變成:
```java
   // Create an object
   ShareOpenGraphObject object = new ShareOpenGraphObject.Builder()
     .putString("og:type", "xx-yy:bus")
     .putString("og:title", String.valueOf(Information.currentRoute))
     .putString("og:image", imageUrl)
     .putString("og:description", "the bus")
     .build();
   // Create an action
   ShareOpenGraphAction action = new ShareOpenGraphAction.Builder()
     .setActionType("xx-yy:take")
     .putObject("bus", object)
     .build();
   // Create the content
   ShareOpenGraphContent content = new ShareOpenGraphContent.Builder()
     .setPreviewPropertyName("bus")
     .setAction(action)
     .build();
```
接著再透過
```java
ShareDialog.show(activityOrFragment, content);
```
或是
```java
ShareApi.share(content, new FacebookCallback() {.......});
```
將ShareContent發佈出去
