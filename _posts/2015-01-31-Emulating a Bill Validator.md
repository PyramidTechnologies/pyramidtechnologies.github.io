---
layout: post
title: Emulating a Bill Validator
category: Coding
tags: Python RS-232
year: 2015
month: 01
day: 31
published: true
summary: An introduction to emulating RS-232 bill acceptors in a virtual environment
image: developers_banner.png
---

<!-- Content -->
<div class="row">
	<div class="col-md-9 columns">
	<!-- CONTENT HERE -->

	<h1>Emulating a Bill Validator in Software</h1>

<p>We recently had an excellent question presented to us on another topic so we thought we&#39;d dig in and deliver an answer that should help out a lot of other developers.&nbsp;</p>

<p>The original questions was posted <a href="http://developers.pyramidacceptors.com/coding/2014/07/21/Pyramid-API-Release.html#comment-1822777669" target="_blank">here</a>. Like everything else, there is literally a 100 ways we could solve this problem, each with their own benefits and drawbacks.</p>

<ol>
	<li><strong><em>Unit Testing</em></strong>&nbsp;- These should always be written anyways but it can be difficult to mock out the serial port in some languages.</li>
	<li><strong><em>Building Hardware</em></strong>&nbsp;- Don&#39;t bother...<a href="http://shop.pyramidacceptors.com/refurbished-acceptors/" target="_blank"> just buy a refurbished bill acceptor</a> and outsource the really hard stuff.</li>
	<li><em><strong>Rolling your Own</strong></em>&nbsp;- Relatively quick and easy if you understand the protocol and know a least one programming language with good serial port support.</li>
</ol>

<p>Because I love software, have an overabundance of bill acceptors, and don&#39;t really want to write unit tests today, we are going to roll our own. Maybe I&#39;ll write up some unit tests next week :)</p>

<p>Before we get too far along, please make sure that you are familiar with the <a href="http://developers.pyramidacceptors.com/coding/2014/08/26/RS-232-Diagram.html" target="_blank">RS-232 bill validator protocol</a>.</p>

<p>Since we&#39;re running in software, presumably both slave and master on the same computer, we will need a solution to bridge our serial ports.</p>

<p>&nbsp;</p>

<div style="background:#eee; border:1px solid #ccc; padding:5px 10px"><strong>Windows -</strong>&nbsp;I use com0com and have never bothered looking for another solution because it just works so darn well.</div>

<p>&nbsp;</p>

<div style="background:#eee; border:1px solid #ccc; padding:5px 10px"><strong>Linux -&nbsp;</strong><a href="http://stackoverflow.com/questions/23867143/null-modem-emulator-com0com-for-linux" target="_blank">socat</a>&nbsp;appears to be the answer though I have not yet tried it. Post back if you find a better solution!</div>

<p>&nbsp;</p>

<p>The concept is pretty simple:</p>

<ul>
	<li>Start a background thread to run our virtual bill acceptor as&nbsp;<code>Idle</code></li>
	<li>Listen to the keyboard for commands to pass to our virtual bill acceptor
	<ul>
		<li>Such as events, bill values, etc</li>
		<li>This will trigger state machine changes e.g. <code>Accepting->Escrow->Stacking->Stacked</code></li>
	</ul>
	</li>
	<li>Provide on screen directions for commands</li>
</ul>
<br>
<p>A slave device sends a message similar to this:</p>

<div style="background:#eee; border:1px solid #ccc; padding:5px 10px">
<p><code>[STX]&nbsp;[length]&nbsp;[ack]&nbsp;&nbsp;[state] [event] [data] [reserved] [model] [revision] [ETX] [checksum]</code></p>

<p><code>&nbsp;0x02, &nbsp;0x0B, &nbsp;0x20, &nbsp; &nbsp;0x01, &nbsp;0x10, &nbsp; 0x00, &nbsp; &nbsp; 0x00, &nbsp; &nbsp;0x01, &nbsp; 0x01, &nbsp; &nbsp;0x03, &nbsp; 0x3A</code></p>
</div>

<p>&nbsp;</p>

<p>I am particularly fond of tables so enjoy these beauties :) This data was mostly scraped from our <a href="http://www.pyramidacceptors.com/files/RS_232.pdf" target="_blank">RS-232 manual</a> if you prefere to get to the horse of the source.</p>

<table class="table table-striped  table-bordered">
	<caption>
	<h2>RS-232 Slave Table</h2>
	</caption>
	<tbody>
		<tr>
			<td>
			<table class="table table-striped  table-bordered" style="width:600px">
				<caption>
				<h2>RS-232 Slave Message Structure</h2>
				</caption>
				<thead>
					<tr>
						<th scope="col">Name</th>
						<th scope="col">Value</th>
						<th scope="col">Description</th>
					</tr>
				</thead>
				<tbody>
					<tr>
						<td>STX</td>
						<td>0x02</td>
						<td>Start transmission, always 0x02</td>
					</tr>
					<tr>
						<td>Length</td>
						<td>0x0B</td>
						<td>Length of entire message, always 11 for slave</td>
					</tr>
					<tr>
						<td>ACK</td>
						<td>0x20</td>
						<td>Upper nibble indicates mast|slave, lower nibble is message number</td>
					</tr>
					<tr>
						<td>State</td>
						<td>0x01</td>
						<td>Bits are set according to the state table</td>
					</tr>
					<tr>
						<td>Event</td>
						<td>0x10</td>
						<td>Events are set according to the event table</td>
					</tr>
					<tr>
						<td>Data</td>
						<td>0x00</td>
						<td>Extra events and bill value bits</td>
					</tr>
					<tr>
						<td>Reserved</td>
						<td>0x00</td>
						<td>Always set to 0x00 to avoid undefined behavior</td>
					</tr>
					<tr>
						<td>Model</td>
						<td>0x01</td>
						<td>Your BA&#39;s model (00-7FH) as hex value</td>
					</tr>
					<tr>
						<td>Revision</td>
						<td>0x01</td>
						<td>Your BA&#39;s revision (00-7FH) as hex value</td>
					</tr>
					<tr>
						<td>ETX</td>
						<td>0x03</td>
						<td>End transmission, always 0x03</td>
					</tr>
					<tr>
						<td>Checksum</td>
						<td>0x3A</td>
						<td>XOR of each byte length through revision (omit STX, ETX)</td>
					</tr>
				</tbody>
			</table>
			</td>
			<td>
			<table class="table table-striped  table-bordered" style="width:600px">
				<caption>
				<h2>State Table</h2>
				</caption>
				<thead>
					<tr>
						<th scope="col">Name</th>
						<th scope="col">Bit</th>
						<th scope="col">Definition</th>
					</tr>
				</thead>
				<tbody>
					<tr>
						<td>Idling</td>
						<td>0</td>
						<td>Bill acceptor is awaiting note, operating normally</td>
					</tr>
					<tr>
						<td>Accepting</td>
						<td>1</td>
						<td>Note is currently being transported through bill acceptor, not yet validated</td>
					</tr>
					<tr>
						<td>Escrowed</td>
						<td>2</td>
						<td>Note is valid, awaiting stack or return message from master</td>
					</tr>
					<tr>
						<td>Stacking</td>
						<td>3</td>
						<td>Note is being moved to cash box</td>
					</tr>
					<tr>
						<td>Stacked</td>
						<td>4</td>
						<td>Note has been successfully stacked</td>
					</tr>
					<tr>
						<td>Returning</td>
						<td>5</td>
						<td>Note is being returned to patron</td>
					</tr>
					<tr>
						<td>Returned</td>
						<td>6</td>
						<td>Note has been successfully returned</td>
					</tr>
				</tbody>
			</table>

			<p>&nbsp;</p>

			<p>&nbsp;</p>
			</td>
		</tr>
		<tr>
			<td>
			<table class="table table-striped  table-bordered" style="width:600px">
				<caption>
				<h2>Event Table</h2>
				</caption>
				<thead>
					<tr>
						<th scope="col">Name</th>
						<th scope="col">Bit</th>
						<th scope="col">Definition</th>
					</tr>
				</thead>
				<tbody>
					<tr>
						<td>Cheated</td>
						<td>0</td>
						<td>Acceptor suspects cheating (e.g. fishing, pullback)</td>
					</tr>
					<tr>
						<td>Bill Rejected</td>
						<td>1</td>
						<td>Acceptor rejected note (bad feed, unidentified note, disabled note)</td>
					</tr>
					<tr>
						<td>Bill Jammed</td>
						<td>2</td>
						<td>Bill is jammed and acceptor cannot recover</td>
					</tr>
					<tr>
						<td>Stacker Full</td>
						<td>3</td>
						<td>Acceptor cannot accept anymore currency, cashbox is full</td>
					</tr>
					<tr>
						<td>Bill Cassette Present</td>
						<td>4</td>
						<td>Set when present, clear when missing</td>
					</tr>
					<tr>
						<td>Reserved</td>
						<td>5</td>
						<td>Set to 0, avoid undefined behavior</td>
					</tr>
					<tr>
						<td>Reserved</td>
						<td>6</td>
						<td>Set to 0,&nbsp;avoid undefined behavior</td>
					</tr>
				</tbody>
			</table>
			</td>
			<td>
			<table class="table table-striped  table-bordered" style="width:600px">
				<caption>
				<h2>Extra Events and Bill Values</h2>
				</caption>
				<thead>
					<tr>
						<th scope="col">Name</th>
						<th scope="col">Bit</th>
						<th scope="col">Definition</th>
					</tr>
				</thead>
				<tbody>
					<tr>
						<td>Power Up</td>
						<td>0</td>
						<td>Set when BA is initializing, not ready to accept currency</td>
					</tr>
					<tr>
						<td>Invalid Command</td>
						<td>1</td>
						<td>An invalid command was received</td>
					</tr>
					<tr>
						<td>Failure</td>
						<td>2</td>
						<td>The acceptor has failed and cannot recover itself (e.g. motor failure)</td>
					</tr>
					<tr>
						<td>Bill value LSB</td>
						<td>3</td>
						<td>&nbsp;Bits 3-5 are set as the bill numbers, 0-7, where 0 is None/unknown bill</td>
					</tr>
					<tr>
						<td>&nbsp;</td>
						<td>4</td>
						<td>e.g. 010 (binary 2) is the 2nd note, $2 in USA</td>
					</tr>
					<tr>
						<td>Bill value MSB</td>
						<td>5</td>
						<td>e.g. 110 (binary 6) is the 6th note, $50 in USA</td>
					</tr>
					<tr>
						<td>Reserved</td>
						<td>6</td>
						<td>Set to 0, avoid undefined behavior</td>
					</tr>
				</tbody>
			</table>
			</td>
		</tr>
	</tbody>
</table>

<p>&nbsp;</p>

<p>&nbsp;</p>
<div class="row">
	<div class="col-md-8">
		<p>So now we know what is going on with the slave. We have some bits to set that tell our master what we&#39;re up to and how we&#39;re doing. In turn, the master will set some bits to control how we traverse our possible states.&nbsp;The master is another beast entirely but we&#39;re not going to worry about today so please...</p>
		<br><div class="col-md-offset-4">
		<p><b><i>Just assume our master is perfect and sane!</b></i></p>
		</div><br>
		<p>Now that we know our basics, let&#39;s dig into some code!&nbsp;
		Since we like to get things done quickly, we&#39;ll be working with Python and pyserial. We&#39;ll start with defining an Acceptor class that will hold the state of our virtual BA (bill acceptor). 
		</p><p>
		We&#39;re going to want to track the following values:
		<ul>
			<li>State</li>
			<li>Event(s)</li>
			<li>Bill Value</li>
			<li>RS-232 Fields</li>
		</ul>
	</div>
	<div class="col-md-4">
		<img alt="farnsworth" src="/img/posts/farnsworth.jpg" class="img-responsive img-thumbnail"/>	
	</div>
</div>
<p>&nbsp;</p>

<h3>The Object</h3>
<div class="row">
	<div class="col-md-4">
		<img alt="soft_bill_1" src="/img/posts/soft_bill_1.png" class="img-responsive"/>	
	</div>
	<div class="col-md-8">
		<p>Code doesn&#39;t look great on here so I&#39;ll just be linking to my <a href="https://github.com/corytodd/soft-bill" target="_blank">Github Soft Bill Project</a> and then explaining what is going on. <a href="https://github.com/corytodd/soft-bill/blob/master/main.py#L71" target="_blank">We&#39;ll start with the Acceptor class definition</a>.&nbsp;On a sidenote, there are two things that I really dislike in code: flags as&nbsp;globals&nbsp;and unnecessary multidimensional arrays.&nbsp;Here we track our internal state in a single object to avoid having a whole bunch of globals to track. This object is then passed by the main method into the worker thread so we are sitting pretty.<br />
	</div>
</div>
<h3>Threads!</h3>
That&#39;s right, we are working with a background thread so we can leave our virtual BA&#39;s serial TxRx&nbsp;alone while we arbitrarily modify its state and observe how the master behaves. For now we are not going to worry about race conditions and other multithreading headaches. The thread magic is <a href="https://github.com/corytodd/soft-bill/blob/master/main.py#L249" target="_blank">super simple</a>. Spin up a non-daemon thread, pass the proper arguments, then enter our STDIN loop. Please be sure to set the daemon mode to false so as to avoid leaving the serial port resource open. See the code for a link to the quoted documentation explaining why.</p>

<h3>Keyboard Input</h3>
<p>So now we have a background thread and STDIN (keyboard input) thread. How do we get our input into the virtual BAs? We&#39;ve defined a command <a href="https://github.com/corytodd/soft-bill/blob/master/main.py#L146" target="_blank">parser method</a> to handle the interpretation and state modification for us. The last portion is to actually use the data, build our packet, and send it on its way. All the while listening to our master of course. This is all handled in the method we passed into our background thread called <a href="https://github.com/corytodd/soft-bill/blob/master/main.py#L18" target="_blank">serial_runner</a>.</p>
<br>Eventually we will want to incorporate this state machine with out fancy little emulator.</p>

<div style="background:#eee; border:1px solid #ccc; padding:5px 10px">
<p><code>Idling->Accepting->Escrowed->{Stacking, Returning}->{Stacked, Returned}</code></p>
</div>

<br>
<h3>Wrapping Up</h3>
<p>That&#39;s basically it! This is still a work in progress and you may have noticed that our slave does not do much besides report events. There is still a system that needs to be built for mocking the bill movement timing as well as compensation for bad/damaged/missing packets. Feel free to ask questions, share your code, or poke holes in anything that I have said.&nbsp;</p>

<p>&nbsp;</p>

<p class="lead">
Happy coding!
<br>
The Pyramid Software Team
</p>
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
