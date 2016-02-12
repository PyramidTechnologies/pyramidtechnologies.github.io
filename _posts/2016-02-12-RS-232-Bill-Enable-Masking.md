---
layout: post
title: RS-232 Bill Enable Masking
category: Coding
tags: binary rs-232 protocol tutorial
year: 2016
month: 02
day: 11
published: true
summary: How to correctly set an RS-232 bill enable mask
image: bits.png
---

<!-- Content -->
<div class="row">
	<div class="col-md-9 columns">
	<!-- CONTENT HERE -->

<p>The RS-232 bill validator protocol allows you to programmatically control exactly which bills are enabled and disabled. For example, if after 10PM you no longer want to accept denominations over $20, you can instruct the bill acceptor to simply reject notes $20 and higher.</p>

<p>This is a nice alternative to writing a fully escrow-enabled host application which is more complex than the typical passive host. In the post we will be discussing the latter.</p>

<p>Referring to the <a href="https://pyramidacceptors.com/pdf/RS_232.pdf" target="_blank">RS-232 bill validator protocol specification</a>, page 4, we see that data byte 0 from the master controls this parameter. As a review we are talking about the Data Fields region in bold below.</p>
<br>
<pre>
<code>| STX | Length | MSG Type and Ack Number | <strong>Data Fields</strong> | ETX | Checksum |</code></pre>
<br>
<p>That means it is the 4th byte in the byte array transmitted by the master to the slave. The format of this byte is as follows:</p>

<ul>
	<li>Bit 0 : Bill 1 (e.g. USA $1)</li>
	<li>Bit 1: &nbsp;Bill 2 (e.g. USA $2 or CAN $10. note that 2$ USA are not commonly accepted)</li>
	<li>Bit 2: &nbsp;Bill 3 (e.g. USA $5)</li>
	<li>Bit 3: &nbsp;Bill 4 (e.g. USA $10)</li>
	<li>Bit 4: &nbsp;Bill 5 (e.g. USA $20)</li>
	<li>Bit 5: &nbsp;Bill 6 (e.g. USA $50)</li>
	<li>Bit 6: &nbsp;Bill 7 (e.g. USA $100)</li>
</ul>
<p>&nbsp;</p>

<p>Notice that only 7 bits of that byte are used. This is because RS-232 is a 7-bit protocol and so we can only support 7 separate denominations. Of course, if you have more than 7 denominations you should talk to our engineering team as we can always make things work.</p>

<p>Back to the bits bytes!</p>

<p>Let&#39;s review a byte in binary with a focus on the terms most and least significant byte. As the you may remember, MSB is the most significant bit in a byte. This means that if the bit is set to 1, the decimal value will be greater than if the LSB was set to 1. For the sake of simplicity we will be ignoring endianess as our API handles this for us.</p>
<br>

<p><img rel="tooltip" title="msb_lsb" target="_blank" class="right" src="/img/posts/bits.png" href="/img/posts/bits.png" /></a></p>	
Each bit from LSB to MSB corresponds to a bill number. With that in mind, here are some examples.<br><br>
<div style="background:#eee;border:1px solid #ccc;padding:5px 10px;">
0 0 0 0 0 0 0 1 &lt;- enables only the $1<br><br>

0 0 0 0 0 1 0 0 &lt;- enabled only the $5 (note: non-USA firmware might not skip the $2 slot)<br><br>

0 0 0 1 1 1 1&nbsp;1 == 30 (decimal format)<br><br>
</div>

<p>&nbsp;</p>

<p>Once you have your mask, all you need to do is apply it. This settings is available through the API as a configuration constant that is polled during every message loop. By default this is 100 milliseconds but may be adjusted between 50 milliseconds and 5 seconds. The syntax for setting this value in the Java API is:</p>

<p><code>...</code></p>

<p><code>RS232Configuration.INSTANCE.setEnableMask(29) // should do the trick.</code></p>

<p><code>...</code></p>

<p>That&#39;s all for today, have fun!</p>

	  
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
