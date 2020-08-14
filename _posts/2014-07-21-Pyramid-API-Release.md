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
image: developers_banner.png
---

<!-- Content -->
<div class="row">
	<div class="col-md-9 columns">
	<!-- CONTENT HERE -->
	  
<h1>Updated 5/14/2015! Java API Released</h1>

<p>The PTI engineering team is super excited to announce the <strike>release</strike> update of their new bill validator API. Our goal is to provide you, the developer, with all of the tools you require in order to make awesome things. We have also put together a few samples to demonstrate the power of these APIs that we hope you will find inspiring. All you need is a copy of <a href="https://github.com/PyramidTechnologies/jPyramid-RS-232/releases" target="_blank">PTalk.jar</a>, a Pyramid bill validator, and a serial connection to your PC to get started.</p>

<p>&nbsp;</p>

<div class="list-group">
  <a href="#" class="list-group-item active">
Supported Bill Validators
  </a>
  <a href="https://pyramidacceptors.com/spectra_lp/" class="list-group-item">Spectra</a>
  <a href="https://pyramidacceptors.com/apex-7000/" class="list-group-item">Apex 7000</a>
  <a href="https://pyramidacceptors.com/trilogy-series/" class="list-group-item">Trilogy - <i>RS-232 firmware required</i></a>
  <a href="https://pyramidacceptors.com/curve-series/" class="list-group-item">Curve - <i>RS-232 firmware required</i></a>
  <a href="https://pyramidacceptors.com/apex-series/" class="list-group-item">Apex 5000</a>
</div>

<p>&nbsp;</p>

<div class="list-group">
  <a class="list-group-item active">Supported Operating Systems</a>
  <a class="list-group-item">Windows: XP SP3, Vista SP2, 7, 8.1 - <i>32/64 bit support for all</i></a>
  <a class="list-group-item">OSX 10.7 (Intel based) or better</a>
  <a class="list-group-item">Linux - Debian, Ubuntu, Arch, Fedora, Redhat... pretty much all of them(32/64 bit)</a>
</div>

<p>&nbsp;</p>
<div class="list-group">
  <a class="list-group-item active">Downloads</a>  
  <a class="list-group-item media-list" href="/api" target="_blank"> 
    <p>Download documentation<img style="margin-right: 10px;" class="pull-right" src="/img/posts/javadoc_icon.png" alt="javadoc_icon"></p>
  </a>
  <a class="list-group-item media-list" href="https://search.maven.org/" target="_blank"> 
    <p>Available on Maven (com.pyramidacceptors:jPyramid-RS-232)<img style="margin-right: 10px;" class="pull-right" src="/img/posts/javadoc_icon.png" alt="maven_link"></p>
  </a> 
  <a class="list-group-item media-list" href="https://github.com/PyramidTechnologies/jPyramid-RS-232/releases" target="_blank"> 
    <p>Or Download library (jar)<img class="pull-right" src="/img/posts/api_thumb.png" alt="jar_icon" style="width: 32px; height: 32px; margin-right: 7px;"></p>
  </a>    
</div>

<p>&nbsp;</p>

<h2>Neat Stuff</h2>
<p>For our first round of APIs we have targetted the Java platform. Entrepreneurs and developers work on all platforms so we believe that our tools should be held to the same standard. With the library you will be able to develop desktop, console, and web applications without having to hassle with cross-platform drivers.</p>

<p>&nbsp;</p>

<h3>Basic Example</h3>

<p>The simplest example can be constructed with just two lines of code. 
<ol>
<li>Instantiate a PyramidAcceptor</li>
<li>Connect</li>
<li>Done!</li>
</ol>
&nbsp;</p>

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
<p>&nbsp;</p>

<h3>Feature-rich Example</h3>
In this example we set a custom baud, databit, stopbit, parity, and port name. We also show the ability to change the polling rate
and alter the bill enable disable pattern. This allows the master to block certain denominations from accepting.
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
<div class="alert alert-danger">Applets are not recommended for new development</div>

<br>
<div class="panel panel-info">
<div class="panel-heading">Code</div>
<div class="panel-body">
<p>With the example we demonstrate a simple applet that charges money for access to a service. In this case it is a silly count bot that counts words on a web page. With a little time you could adapt this to create a kiosk that serves YouTube videos, music, or any other timed service that you would like to sell</p>
<div class="alert alert-danger">This requires a bill validator and serial connection between your PC and the bill validator.</div>

</div>
</div>

<h2>Desktop Sample</h2>
<div class="well well-lg">
<p><img alt="pyramid_api_desktop_sample.png" class="right" src="/img/posts/pyramid_api_desktop_sample.png" /></p>
</div>
<p>This is a more traditional example based on a JFrame. This simply enables the bill validator and reports and event or state change. This sample is good for debugging your application to ensure that your product idea will be rock-solid.</p>

<div class="panel panel-info">
<div class="panel-heading">Code</div>
<div class="panel-body">
The source code for this sample is available <a href="https://github.com/PyramidTechnologies/Java-API-desktop-sample" rel="tooltip" title="Java API Sample - Desktop" target="_blank">here</a>.
<div class="alert alert-danger">This requires a bill validator and serial connection between your PC and the bill validator.</div>
  </div>
</div>
<h2>Your Input Welcome</h2>

<p>Here at Pyramid Technologies we value customer ideas and innovation. 
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
			var disqus_url = 'https://pyramidtechnologies.github.com{{ page.url }}';
 
			
			/* * * DON'T EDIT BELOW THIS LINE * * */
			(function() {
				var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
				dsq.src = 'https://' + disqus_shortname + '.disqus.com/embed.js';
				(document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
			})();
		</script>
		<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
		<a href="https://disqus.com" class="dsq-brlink">blog comments powered by <span class="logo-disqus">Disqus</span></a>
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
