---
layout: post
title: Python RS-232 Sample Updated
category: Coding
tags: Python RS-232
year: 2014
month: 02
day: 02
published: true
summary: Pramid's Python RS-232 master sample has been made awesome
image: logo_header.jpg
---

<!-- Content -->
<div class="row">
	<div class="col-md-9 columns">
	<!-- CONTENT HERE -->

	<p>Have you been trying to build an RS-232 bill acceptor host? Well Pyramid Technologies has released a comprehensive update to their Python sample package which should be able to get you up and running in no time.</p>
<br>
	<p>The code is leaner, meaner, and much more portable should you find you are more in a copy/paste mood. It follows a pattern similar to our Slave Emulator sample that was recently released.</p>
<br>

<div class="list-group">
  <a class="list-group-item active">Code</a>  
  <a class="list-group-item media-list" href="https://github.com/PyramidTechnologies/Python-RS-232" target="_blank"> 
    <p>Master<img style="margin-right: 10px;" class="pull-right" src="/img/posts/javadoc_icon.png" alt="javadoc_icon"></p>
  </a>
  <a class="list-group-item media-list" href="https://github.com/corytodd/soft-bill" target="_blank"> 
    <p>Slave<img style="margin-right: 10px;" class="pull-right" src="/img/posts/javadoc_icon.png" alt="javadoc_icon"></p>
  </a>    
</div>

<br>
<p>As always, happy coding and let us know if you have any questions :)</p>
	  
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
