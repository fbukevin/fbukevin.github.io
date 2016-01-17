title: Ubuntu 用 Binary 的方式安裝 Tomcat
date: 2014-01-05 02:42:00
tags: []
---

<div class="MsoNormal"><span lang="EN-US" style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">1\.</span> <span style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">到 <span lang="EN-US">Apache Tomcat</span>官網下載<span lang="EN-US">apache-tomcat-8.0.0-RC10-tar.gz</span></span></div>

<div class="MsoNormal"><span lang="EN-US" style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">  
</span></div>

<div class="MsoNormal"><span lang="EN-US" style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">2\.</span> <span style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">解壓縮後放到 <span lang="EN-US">/opt</span>、<span lang="EN-US">/usr/local</span> 或 家目錄下<span lang="EN-US"></span></span></div>

<div class="MsoNormal"><span lang="EN-US" style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">  
</span></div>

<div class="MsoNormal"><span lang="EN-US" style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">3\.</span> <span style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">編輯 <span lang="EN-US">~/.bashrc</span>，加入：<span lang="EN-US"></span></span></div>

<div class="MsoNormal"><span lang="EN-US" style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">        export TOMCAT_HOME=”[2</span> <span style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">的路徑<span lang="EN-US">]”</span></span></div>

<div class="MsoNormal"><span lang="EN-US" style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">        export PATH=”$PATH:$TOMCAT_HOME/bin”</span></div>

<div class="MsoNormal"><span lang="EN-US" style="font-family: &quot;Century Schoolbook L&quot;,&quot;serif&quot;; mso-fareast-font-family: &quot;Century Schoolbook L&quot;;">        export CLASSPATH=”$TOMCAT_HOME/lib/jsp-api.jar:$TOMCAT_HOME/lib/servlet-api.jar:$CLASSPATH”</span></div>

<div class="MsoNormal"><span lang="EN-US" style="font-family: 'Century Schoolbook L', serif;">        ( </span><span style="font-family: 'Century Schoolbook L', serif;">或是在 <span lang="EN-US">bin</span> 中執行 <span lang="EN-US">setclasspath.sh )</span></span></div>

[閱讀更多 »](http://veckcode.blogspot.com/2014/01/ubuntu-binary-tomcat.html#more)