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

<p>The PTI engineering team is super excited to announce the release of their API. Our goal is to provide you, the developer, with all the tools you need in order to make awesome things. We&#39;ve put together a few samples to demonstrate the power of these APIs and hopefully you will find them inspiring.</p>

<p>&nbsp;</p>

<p><a href="/api" target="_blank"><img alt="javadoc_icon" src="/img/posts/javadoc_icon.png"/></a> The API documentation is available <a href="/api" target="_blank">here</a>.</p>

<p>&nbsp;</p>

<p>For our first round of APIs we have targetted the Java platform. Entrepenours and developers work on all platforms and so should our product. Many people have purchased our Apex and Trilogy model bill validators and requested sample code or APIs. We are making good on our promise to deliver.</p>

<p>&nbsp;</p>

<h2>Basic Example</h2>

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

<p>Of course, this is just a basic example. You are free to specify your own port name, port configuration, and event configure event handlers.&nbsp;</p>

<h2>Applet Sample</h2>
 <p><img alt="pyramid_api_applet_sample.png" class="right" src="/img/posts/pyramid_api_applet_sample.png" /></p>
<p>With the example we demonstrate a simple applet that charges money for access to a service. In this case it is a silly count bot that counts words on a web page. With a little time you could adapt this to create a kiosk that serves YouTube videos, music, or any other timed service that you would like to sell</p>

<p>This example demonstrates the event support and device autodetection available with our API. <br>
The source code for this sample is available <a href="https://github.com/PyramidTechnologies/Java-API-applet-sample" rel="tooltip" title="Java API Sample - Applet" target="_blank">here</a>.</p></p>

<h2>Desktop Sample</h2>
 <p><img alt="pyramid_api_desktop_sample.png" class="right" src="/img/posts/pyramid_api_desktop_sample.png" /></p>
<p>This is a more traditional example based on a JFrame. This simply enables the bill validator and reports and event or state change. This sample is good for debugging your application to ensure that your product idea will be rock-solid.</p>
The source code for this sample is available <a href="https://github.com/PyramidTechnologies/Java-API-desktop-sample" rel="tooltip" title="Java API Sample - Desktop" target="_blank">here</a>.</p></p>

<h2>Input Welcome</h2>

<p>Here at Pyramid Technologies we value customer ideas and innovation. 
<br>If you see a need that our API is not providing, feel free to <a href="https://github.com/PyramidTechnologies/Feedback/issues/new">let us know</a>.</p>

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
