title: ~Java GUI~ AWT vs Swing
date: 2011-07-15 16:44:00
tags: [Java]
---

Frame、Panel、Dialog、InterFrame、Window、Applet 都是容器  

通常有J開頭的，如JFrame、JDialog、JPanel、JInterFrame、JWindow、JApplet...等元件都是屬於 swing 類別  
而沒有J開頭的，如Frame、Panel、Dialog、InterFrame、Window、Applet...等元件都是屬於 awt 類別  

其中Applet、JApplet、swing與awt的繼承關係為：  
<span class="Apple-tab-span" style="white-space: pre;"></span>java.awt.Panel <-- java.applet.Applet <-- javax.swing.JApple  

通常一個GUI分為兩個部分：Container + Component  
<span class="Apple-tab-span" style="white-space: pre;"></span>  
以swing為例，swing可以被實體化出來的：  

<span class="Apple-tab-span" style="white-space: pre;"></span>容器(Container)：  
<span class="Apple-tab-span" style="white-space: pre;"></span>JFrame <span class="Apple-tab-span" style="white-space: pre;"></span>:General window  
<span class="Apple-tab-span" style="white-space: pre;"></span>JDialog <span class="Apple-tab-span" style="white-space: pre;"></span> :Dialog window  
<span class="Apple-tab-span" style="white-space: pre;"></span>JWindow <span class="Apple-tab-span" style="white-space: pre;"></span> :General window but dosen't have title and other basic component  
<span class="Apple-tab-span" style="white-space: pre;"></span>JInterFrame :用來建立子視窗  
<span class="Apple-tab-span" style="white-space: pre;"></span>JPanel <span class="Apple-tab-span" style="white-space: pre;"></span> :用來建立視窗中的面板  
<span class="Apple-tab-span" style="white-space: pre;"></span>JApplet <span class="Apple-tab-span" style="white-space: pre;"></span> :瀏覽器使用的視窗化容器  
<span class="Apple-tab-span" style="white-space: pre;"></span>  
[閱讀更多 »](http://veckcode.blogspot.com/2011/07/java-gui-awt-vs-swing.html#more)