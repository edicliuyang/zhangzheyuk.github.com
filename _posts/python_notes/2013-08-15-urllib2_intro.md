---
layout: post
title: "urllib2 intro"
description: ""
category: python 
tags: [python]
---
{% include JB/setup %}


<div id="content">
<h1 class="title">python urllib2 intro</h1>
<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1. ulrlib2</a></li>
<li><a href="#sec-2">2. Basic use</a></li>
<li><a href="#sec-3">3. use the urllib to mirror a Request</a></li>
<li><a href="#sec-4">4. use the urllib to construct a POST request</a></li>
<li><a href="#sec-5">5. GET request</a></li>
<li><a href="#sec-6">6. Headers</a></li>
<li><a href="#sec-7">7. Error handling</a></li>
</ul>
</div>
</div>
<div id="outline-container-sec-1" class="outline-2">
<h2 id="sec-1"><span class="section-number-2">1</span> ulrlib2</h2>
<div class="outline-text-2" id="text-1">
<p>
based on the python manual "how to" part
</p>
</div>
</div>
<div id="outline-container-sec-2" class="outline-2">
<h2 id="sec-2"><span class="section-number-2">2</span> Basic use</h2>
<div class="outline-text-2" id="text-2">
<p>
try to get fetch the webpage
</p>

<div class="org-src-container">

<pre class="src src-python"><span class="linenr">1: </span><span style="color: #fa8072;">import</span> urllib2 
<span class="linenr">2: </span><span style="color: #7fffd4; font-weight: bold;">response</span> = urllib2.urlopen(<span style="color: #ffa07a;">"http://python.org/"</span>)
<span class="linenr">3: </span><span style="color: #7fffd4; font-weight: bold;">html</span> = reponse.read()
</pre>
</div>
</div>
</div>
<div id="outline-container-sec-3" class="outline-2">
<h2 id="sec-3"><span class="section-number-2">3</span> use the urllib to mirror a Request</h2>
<div class="outline-text-2" id="text-3">
<div class="org-src-container">

<pre class="src src-python"><span style="color: #fa8072;">import</span> urllib2

<span style="color: #7fffd4; font-weight: bold;">req</span> =  urllib2.Request(<span style="color: #ffa07a;">'http://www.voidspace.org.uk'</span>)
<span style="color: #7fffd4; font-weight: bold;">response</span> = urllib2.urlopen(req)
<span style="color: #7fffd4; font-weight: bold;">the_page</span> = response.read()
</pre>
</div>
</div>
</div>
<div id="outline-container-sec-4" class="outline-2">
<h2 id="sec-4"><span class="section-number-2">4</span> use the urllib to construct a POST request</h2>
<div class="outline-text-2" id="text-4">
<p>
(can use this feature to do the auto authetication)
</p>

<div class="org-src-container">

<pre class="src src-python"><span style="color: #fa8072;">import</span> urllib
<span style="color: #fa8072;">import</span> urllib2

<span style="color: #7fffd4; font-weight: bold;">url</span> = <span style="color: #ffa07a;">'http://www/someserver.com/cgi-bin/register.cgi'</span>
<span style="color: #7fffd4; font-weight: bold;">value</span> = {<span style="color: #ffa07a;">'name'</span> : <span style="color: #ffa07a;">'Led Chang'</span>
<span style="color: #ffa07a;">'location'</span>: <span style="color: #ffa07a;">'QD'</span>
<span style="color: #ffa07a;">'language'</span>: <span style="color: #ffa07a;">'Python'</span>}

<span style="color: #7fffd4; font-weight: bold;">data</span> = urllib.urlencode(values)
<span style="color: #7fffd4; font-weight: bold;">req</span> = urllib2.Request(url, data)
<span style="color: #7fffd4; font-weight: bold;">response</span> = urllib2.urlopen(req)
<span style="color: #7fffd4; font-weight: bold;">the_page</span> = response.read()
</pre>
</div>
</div>
</div>

<div id="outline-container-sec-5" class="outline-2">
<h2 id="sec-5"><span class="section-number-2">5</span> GET request</h2>
<div class="outline-text-2" id="text-5">
<p>
GET request 明文传输数据
</p>
<blockquote>
<p>
get and post (转)
原理介绍：理论上说，GET是从服务器上请求数据，POST是发送数据到服务器。事实上，GET方法是把数据参数队列（query string）加到一个URL上，值和表单是一一对应的。比如说，name=John。在队列里，值和表单用一个&amp;符号分开，空格用+号替换，特 殊的符号转换成十六进制的代码。因为这一队列在URL里边，这样队列的参数就能看得到，可以被记录下来，或更改。通常GET方法还限制字符的大小（大概是 256字节 ）。事实上POST方法可以没有时间限制的传递数据到服务器，用户在浏览器端是看不到这一过程的，所以POST方法比较适合用于发送一个保密的（比如信用 卡号）或者比较大量的数据到服务器。
GET是把参数数据队列加到提交表单的ACTION属性所指的URL中，值和表单内各个字段一一对应，在URL中可以看到
POST是通过HTTP POST机制，将表单内各个字段与其内容放置在HTML HEADER内一起传送到ACTION属性所指的URL地址。用户看不到这个过程。
对于GET方式，服务器端用Request.QueryString获取变量的值，
对于POST方式，服务器端用Request.Form获取提交的数据。
</p>

<p>
区别：
Post是允许传输大量数据的方法，而Get方法会将所要传输的数据附在网址后面，然后一起送达服务器，因此传送的数据量就会受到限制，但是执行效率却比Post方法好。 
</p>


<p>
建议：
1、get方式的安全性较Post方式要差些，包含机密信息的话，建议用Post数据提交方式；
2、在做数据查询时，建议用Get方式；而在做数据添加、修改或删除时，建议用Post方式；
</p>
</blockquote>

<div class="org-src-container">

<pre class="src src-python">&gt;&gt;&gt; <span style="color: #fa8072;">import</span> urllib
&gt;&gt;&gt; data={}
&gt;&gt;&gt; data[<span style="color: #ffa07a;">'name'</span>] = <span style="color: #ffa07a;">'Somebody Here'</span>
&gt;&gt;&gt; data[<span style="color: #ffa07a;">'location'</span>] = <span style="color: #ffa07a;">'Northampton'</span>
&gt;&gt;&gt; data[<span style="color: #ffa07a;">'language'</span>] = <span style="color: #ffa07a;">'Python'</span>
&gt;&gt;&gt; url_values = urllib.urlencode(data)
&gt;&gt;&gt; <span style="color: #fa8072;">print</span> url_values
<span style="color: #7fffd4; font-weight: bold;">name</span>=Somebody+Here&amp;language=Python&amp;location=Northampton
&gt;&gt;&gt; url = <span style="color: #ffa07a;">'http://www.example.com/example.cgi'</span>
&gt;&gt;&gt; full_url = url + <span style="color: #ffa07a;">'?'</span> + url_values
&gt;&gt;&gt; data = urllib2.urlopen(full_url)
</pre>
</div>
</div>
</div>
<div id="outline-container-sec-6" class="outline-2">
<h2 id="sec-6"><span class="section-number-2">6</span> Headers</h2>
<div class="outline-text-2" id="text-6">
<p>
add headers to the HTTP request
contains about the version of the OS and web browser
</p>

<div class="org-src-container">

<pre class="src src-python"><span style="color: #fa8072;">import</span> urllib
<span style="color: #fa8072;">import</span> urllib2

<span style="color: #7fffd4; font-weight: bold;">url</span> = <span style="color: #ffa07a;">'http://www.someserver.com/cgi-bin/register.cgi'</span>
<span style="color: #7fffd4; font-weight: bold;">user_agent</span> = <span style="color: #ffa07a;">'Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)'</span>
<span style="color: #7fffd4; font-weight: bold;">values</span> = {<span style="color: #ffa07a;">'name'</span> : <span style="color: #ffa07a;">'Michael Foord'</span>,
<span style="color: #ffa07a;">'location'</span> : <span style="color: #ffa07a;">'Northampton'</span>,
<span style="color: #ffa07a;">'language'</span> : <span style="color: #ffa07a;">'Python'</span> }
<span style="color: #7fffd4; font-weight: bold;">headers</span> = { <span style="color: #ffa07a;">'User-Agent'</span> : user_agent }

<span style="color: #7fffd4; font-weight: bold;">data</span> = urllib.urlencode(values)
<span style="color: #7fffd4; font-weight: bold;">req</span> = urllib2.Request(url, data, headers)
<span style="color: #7fffd4; font-weight: bold;">response</span> = urllib2.urlopen(req)
<span style="color: #7fffd4; font-weight: bold;">the_page</span> = response.read()
</pre>
</div>
</div>
</div>
<div id="outline-container-sec-7" class="outline-2">
<h2 id="sec-7"><span class="section-number-2">7</span> Error handling</h2>
</div>
</div>
<div id="postamble" class="status">
<p class="author">Author: zhang led</p>
<p class="date">Created: 2013-08-15 Thu 13:39</p>
<p class="creator"><a href="http://www.gnu.org/software/emacs/">Emacs</a> 23.4.1 (<a href="http://orgmode.org">Org</a> mode 8.0.7)</p>
<p class="xhtml-validation"><a href="http://validator.w3.org/check?uri=referer">Validate XHTML 1.0</a></p>
</div>


