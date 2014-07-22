---
layout: post
title: Pyramid API Released
category: Coding
tags: RS-232 Java
year: 2014
month: 7
day: 18
published: true
summary: Pyramid Technologies releases Java RS-232 API
image: logo_1.jpg
---

<!-- Content -->
<div class="row">
	<div class="col-md-9 columns">
	<!-- CONTENT HERE -->
	  
<h1>Java API Released<img alt="logo_1" class="pull-right" src="/img/logo.png" style="height:59px; width:149px" /></h1>

<p>The PTI engineering team is super excited to announce the release of their new bill validator API. Our goal is to provide you, the developer, with all of the tools you need in order to make awesome things. We have also put together a few samples to demonstrate the power of these APIs and hopefully you will find them inspiring. All you need is a copy of <a href="/api/release/PTalk.jar" target="_blank">PTalk.jar</a>, a Pyramid bill validator, and a serial connection to your PC to get started.</p>
<br>
<div class="list-group">
  <a href="#" class="list-group-item active">
Supported Bill Validators
  </a>
  <a href="http://pyramidacceptors.com/apex-7000/" class="list-group-item">Apex 7000</a>
  <a href="http://pyramidacceptors.com/trilogy-series/" class="list-group-item">Trilogy - <i>RS-232 firmware required</i></a>
  <a href="http://pyramidacceptors.com/curve-series/" class="list-group-item">Curve - <i>RS-232 firmware required</i></a>
  <a href="http://pyramidacceptors.com/apex-series/" class="list-group-item">Apex 5000</a>
</div>

<div class="list-group">
  <a class="list-group-item active">
Supported Operating Systems
  </a>
  <a class="list-group-item">Windows: XP SP3, Vista SP2, 7, 8.1 - <i>32/64 bit support for al</i></a>
  <a class="list-group-item">OSX 10.7 (Intel based) or better</a>
  <a class="list-group-item">Linux - Debian, Ubuntu, Arch, Fedora, Redhat... pretty much all of them(32/64 bit)</a>
</div>

<p>&nbsp;</p>
<div class="list-group">
  <a href="" class="list-group-item active">
Supported Bill Validators
  </a>
  <a href="/api" target="_blank" class="list-group-item"><img alt="javadoc_icon" src="/img/posts/javadoc_icon.png">The API documentation is available here.</a>
  <a href="/api/release/PTalk.jar" class="list-group-item"><img alt="jar_icon" src="/img/posts/jar_icon.png">The API jar file is available here.</a>
</div>
<br>

<p>&nbsp;</p>

<h2>Neat Stuff</h2>
<p>For our first round of APIs we have targetted the Java platform. Entrepenours and developers work on all platforms and so should our product. Many people have purchased our Apex and Trilogy model bill validators and requested sample code or APIs. We are making good on our promise to deliver.</p>

<p>&nbsp;</p>

<h3>Basic Example</h3>

<p>The simplest example can be constructed with just two lines of code.&nbsp;</p>

<div style="background:#eee; border:1px solid #ccc; padding:5px 10px">
<pre>
<code><em><a id="sample" name="sample"></a>...
// Create instance of bill acceptor and attempt to autodetect the device
PyramidAcceptor</em> acceptor = PyramidAcceptor.valueOfRS232();
<em> 
// Connect! this handles all the hand shaking and starts up the acceptor</em>
acceptor.connect();
...
</em></code>
</pre>
</div>

<p>&nbsp;</p>

<p>Of course, this is just a basic example. You are free to specify your own port name, port configuration, and even configure event handlers.&nbsp;</p>

<h3>More feature-rich Example</h3>

<div style="background:#eee; border:1px solid #ccc; padding:5px 10px">
<pre>
<code><em><a id="sample" name="sample"></a>...
// Create instance of bill acceptor
acceptor = PyramidAcceptor.valueOfRS232(RS232Configuration.INSTANCE, 
		"COM4", APIConstants.BAUDRATE_9600, APIConstants.DATABITS_7,
		APIConstants.STOPBITS_1, APIConstants.PARITY_EVEN);		
// Connect! this handles all the handsahking
acceptor.connect();

// Set poll rate to 50 ms
acceptor.setPollRate(50);

// Enable only bills 1 and 2
RS232Configuration.INSTANCE.setEnableMask(0x3);
...
</em></code>
</pre>
</div>
<p>The demonstrates the configuration parameters for a PyramidAcceptor object as well as the bill enable masking.&nbsp;</p>

<p>&nbsp;</p>

<h2>Applet Sample</h2>
<p><a href="/api/demo" target="_blank"><img rel="tooltip" title="Click to try live demo" target="_blank" alt="pyramid_api_applet_sample.png" class="right" src="/img/posts/pyramid_api_applet_sample.png" href="api/demo" /></a></p>
<p>With the example we demonstrate a simple applet that charges money for access to a service. In this case it is a silly count bot that counts words on a web page. With a little time you could adapt this to create a kiosk that serves YouTube videos, music, or any other timed service that you would like to sell</p>

<p>This example demonstrates the event support and device autodetection available with our API. <br>
<br>
<div class="panel panel-info">
  <div class="panel-body">
A working sample is available <a href="/api/demo" rel="tooltip" title="Java API Sample - Applet" target="_blank">here</a>.</p></p> This requires a bill validator and serial connection between your PC and the bill validator.<br>
  </div>
</div>
<div class="panel panel-info">
  <div class="panel-body">
The source code for this sample is available <a href="https://github.com/PyramidTechnologies/Java-API-applet-sample" rel="tooltip" title="Java API Sample - Applet" target="_blank">here</a>.</p></p>
  </div>
</div>

<h2>Desktop Sample</h2>
 <p><img alt="pyramid_api_desktop_sample.png" class="right" src="/img/posts/pyramid_api_desktop_sample.png" /></p>
<p>This is a more traditional example based on a JFrame. This simply enables the bill validator and reports and event or state change. This sample is good for debugging your application to ensure that your product idea will be rock-solid.</p>
<div class="panel panel-info">
  <div class="panel-body">
The source code for this sample is available <a href="https://github.com/PyramidTechnologies/Java-API-desktop-sample" rel="tooltip" title="Java API Sample - Desktop" target="_blank">here</a>.</p></p>
  </div>
</div>
<h2>Input Welcome</h2>

<p>Here at Pyramid Technologies, we value customer ideas and innovation. 
<br>If you require a functionality that our API is not providing, feel free to <a href="https://github.com/PyramidTechnologies/Feedback/issues/new">let us know</a>.</p>

<p>&nbsp;</p>

<p>&nbsp;</p>

<p>&nbsp;</p>
	  
	  
	<!-- END CONTENT-->  
	</div>
</div> 

<div class="row">
	<div class="span3 columns">&nbsp;</div>
	<div class="span6 column">
			<p class="pull-right">{% if page.previous.url %} <a href="{{page.previous.url}}" title="Previous Post: {{page.previous.title}}"><i class="icon-chevron-left"></i></a> 	{% endif %}   {% if page.next.url %} 	<a href="{{page.next.url}}" title="Next Post: {{page.next.title}}"><i class="icon-chevron-right"></i></a> 	{% endif %} </p>  
	</div>
</div>
	
<div class="row">	
    <div class="span9 columns">    
		<h2>Comments Section</h2>
	    <p>Feel free to comment on the post but keep it clean and on topic.</p>	
		<div id="disqus_thread"></div>
		<script type="text/javascript">
			/* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
			var disqus_shortname = 'ptidevelopers'; // required: replace example with your forum shortname
			var disqus_identifier = '{{ page.url }}';
			var disqus_url = 'http://pyramidtechnologies.github.com{{ page.url }}';
 
			
			/* * * DON'T EDIT BELOW THIS LINE * * */
			(function() {
				var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
				dsq.src = 'http://' + disqus_shortname + '.disqus.com/embed.js';
				(document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
			})();
		</script>
		<noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
		<a href="http://disqus.com" class="dsq-brlink">blog comments powered by <span class="logo-disqus">Disqus</span></a>
	</div>
</div>

<!-- Twitter -->
<script>!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0];if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src="//platform.twitter.com/widgets.js";fjs.parentNode.insertBefore(js,fjs);}}(document,"script","twitter-wjs");</script>

<!-- Google + -->
<script type="text/javascript">
  (function() {
    var po = document.createElement('script'); po.type = 'text/javascript'; po.async = true;
    po.src = 'https://apis.google.com/js/plusone.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(po, s);
  })();
</script>
