---
layout: post
title: API Available on Maven
category: Coding
tags: Gradle, Intellij, Java
year: 2015
month: 5
day: 14
published: false
summary: Get your project built more quickly by using Gradle
image: developers_banner.png
---

<!-- Content -->
<div class="row">
	<div class="col-md-9 columns">
	<!-- CONTENT HERE -->

	<h1>RS-232 API Now Available on Maven</h1>

<p>We have upgraded our API and made it available through Maven Central. We have also updated our desktop sample application and API source code to use Intellij and Gradle to get you up and running even faster.</p>

<p>&nbsp;</p>

<p>To add our API as a dependency to your project, add these lines to your build.gradle:</p>

<div style="background:#eee;border:1px solid #ccc;padding:5px 10px;">dependencies {<br />
&nbsp; &nbsp; compile &#39;com.pyramidacceptors:jPyramid-RS-232:1.1&#39;<br />
}</div>

<p>&nbsp;</p>

<h2>New in 1.1</h2>

<ul>
	<li>Minor bug fixes</li>
	<li>Documentation Improvements</li>
	<li>Better test coverage</li>
</ul>

<p>&nbsp;Keep an eye out for more updates and maybe some cool example projects.&nbsp;</p>

<p>&nbsp;</p>

<p>Do you have an idea for PC bill acceptor application?&nbsp;</p>
	  
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
