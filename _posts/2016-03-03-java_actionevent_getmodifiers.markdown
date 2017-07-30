---
layout: post
comments: true
title:  "Java ActionEvent getModifiers()"
excerpt: "getModifiers()的心得"
date:   2016-03-03 20:00:00
---

前些日子學弟來問怎麼判斷按下Button時，是否有同時按下`Ctrl+Alt`。學弟是在`actionPerformed`裡，用ActionEvent的`getModifiers()`與`ActionEvent.ALT_MASK`和`ActionEvent.CTRL_MASK`來判斷，不過他執行出來的結果卻是錯的。由於以前也沒有用過getModifiers()，所以花了點時間研究，再加上這過程還發生怎麼在 **Mac上可以用，但在Win上反而不行** 的情況，因此在這邊整理了一下學習心得。

首先是`getModifiers()`的值，我自己遇到的狀況是根據平台以及使用AWT還是Swing的Button而不同，所以debug的時間一直栽在這邊....

<table><tbody>
<tr><th>Key</th><th>Mac, Win(Swing JButton)</th><th>Win(AWT Button)</th></tr>
<tr><td>only click,</td><td>16</td><td>0</td></tr>
<tr><td>with Ctrl,</td><td>16|2=18</td><td>0|128=128</td></tr>
<tr><td>with Alt,</td><td>16|8=24</td><td>0|512=512</td></tr>
<tr><td>with Shift,</td><td>16|1=17</td><td>0|64=64</td></tr>
<tr><td>with Alt+Ctrl,</td><td>16|8|2=26</td><td>0|512|128=640</td></tr>
</tbody></table>

得到了Modifiers的值後，接著就是用MASK來比對。如果是上表左邊的情況，使用ActionEvent提供的`ALT_MASK`和`CTRL_MASK`等等即可；但如果是右邊的情況，就變成要使用`InputEvent`的`ALT_DOWN_MASK`和`CTRL_DOWN_MASK`等等。使用方法是Modifiers值與mask值的`AND`運算結果是否等於mask值，就知道Modifiers是否有按下該Modifier。寫成函式就是：
```java
private boolean checkModifiers(int modifiers, int mask) {
    return((modifiers & mask) == mask);
}
```

若要判斷是否有兩個Modifier key，如`Alt+Ctrl`，則mask就是這兩個Modifier Mask值的`OR`運算。 例如
```java
int altWithCtrlMask = ActionEvent.ALT_MASK | ActionEvent.CTRL_MASK;
```

`altWithCtrlMask`再來跟getModifiers的值進行`AND`運算後是否等於`altWithCtrlMask`。
再舉個例子，如果是同時按下 `Alt+Ctrl+Shift`，getModifiers()會得到27，而`ActionEvent.ALT_MASK | ActionEvent.CTRL_MASK`的值為10， 
```bash
   27 = 00011011
   10 = 00001010
27|10 = 00001010
```
則27 AND 10 == 10，所以有判斷到 `Alt+Ctrl`。 


