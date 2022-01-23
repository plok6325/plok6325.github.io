---
title: Markdown 高级语法总结
date: 2017-05-28 01:00:00
categories: Others
---
- 插入音乐  

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=17110575&auto=1&height=66"></iframe>


- 文字居中  
    <h1 align='center'>Image Super-Resolution Using Deep Convolutional Networks</h1>



      \<div align='center'>Image Super-Resolution Using Deep Convolutional Networks</div>

- 居中 

- 插入视频  

<iframe width="1280" height="720" src="https://www.youtube.com/embed/pm4Fn_jYMGI?list=PLWuzIwiU26sNUZGYHHRGo6oxZm5RRBpHc" frameborder="0" allowfullscreen></iframe>


- 网页editor 


<div id="container" style="width:800px;height:600px;border:1px solid grey"></div>

<script src="monaco-editor/min/vs/loader.js"></script>
<script>
	require.config({ paths: { 'vs': 'monaco-editor/min/vs' }});
	require(['vs/editor/editor.main'], function() {
		var editor = monaco.editor.create(document.getElementById('container'), {
			value: [
				'function x() {',
				'\tconsole.log("Hello world!");',
				'}'
			].join('\n'),
			language: 'javascript'
		});
	});
</script>
