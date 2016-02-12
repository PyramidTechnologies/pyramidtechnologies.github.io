---
layout: post
title: Multiple SSH Keys for Sourcetree
category: Coding
tags: SSH Git
year: 2015
month: 09
day: 12
published: true
summary: How to correctly configure multiple SSH keys on Sourcetree for Windows
image: ssh.png
---

<!-- Content -->
<div class="row">
	<div class="col-md-9 columns">
	<!-- CONTENT HERE -->

    <h1>Multiple SSH Keys for Git on Windows</h1>

<p>We use Git and Sourcetree, primarily on the Windows operating system and love it 99% of the time. Sometimes we work from our personal computers and being developers, we have our own projects outside of work that are associated with different credentials. To avoid SSH key issues we just use simple HTTPS to clone our repos down instead of hassling with multiple SSH keys.</p>

<p>This week we have&nbsp;officially adopted&nbsp;<a href="https://github.com/blog/1614-two-factor-authentication" target="_blank">two-factor authentication</a> for our revision control so guess what?!</p>

<p>As the documentation clearly states, this breaks HTTPS login for Git!</p>

<p> All things considered this is a small issue but getting multi-key SSH configured was surprisingly difficult. What I found most interesting was that every document explaining how to do this omitted one or two critical details. I have recorded the steps I took to guarantee a&nbsp;sure-fire process to achieve functional&nbsp;Windows Sourcetree with Git working on multiple SSH keys.</p>

<p>Obviously this is Windows and Git specific. We&#39;ll be implementing the scenario where you have 1 work and 1 personal Github/Bitbucket/Gitlab account</p>

<hr />

<ol>
	<p><li><a id="step1" name="step1"></a>Configure Sourcetree to use OpenSSH. We don&#39;t use HG so no issues for us!

	<ul>
		<li><b>Existing Keys:</b> If you previously used Putty, load your ppk into PuttyGen and convert it to Open SSH format using the conversion option. Append .rsa to the file name so you can differentiate from your ppk format private key.</li>
		<li><b>Fresh Start:</b> If you want to start from <em>scratch</em>, generate two new keys in PuttyGen. 1 for work and 1 for home. Save the private and public keys for later use.</li>
	</ul>
	</li></p>
	<p><li>Check that <strong>both</strong>&nbsp;of your personal and work account have the correct public keys added for access.</li></p>
	<p><li>Create a .bashrc file at %userprofile%\.bashrc and save the following:
	<div style="background:#eee; border:1px solid #ccc; padding:5px 10px">#! /bin/bash&nbsp;<br />
	eval `ssh-agent -s`&nbsp;<br />
    <br />
    # Note you make change the .rsa to match whatever suffix you choose for your OpenSSH private keys.<br />
	ssh-add ~/.ssh/*.rsa  </div>
	</li></p>
	<p><li><a id="step4"" name="step4"></a>Create a %userprofile%\.ssh\config
	<div style="background:#eee; border:1px solid #ccc; padding:5px 10px">
    Host work<br />
	&nbsp;&nbsp;HostName host.org<br />
    <br />
    &nbsp;&nbsp;# The ~/ means your profile directory. work.rsa should be changed to match<br />
    &nbsp;&nbsp;# the OpenSSH private key name for your work account. <br />
	&nbsp;&nbsp;IdentityFile ~/.ssh/work.rsa<br />
    <br />
    &nbsp;&nbsp;# Tell SSH to only use identities used in this file<br />
	&nbsp;&nbsp;IdentitiesOnly yes<br />
    <br />
	Host home<br />
	&nbsp;&nbsp;HostName host.org<br /><br />
    &nbsp;&nbsp;# home.rsa should be changed to match<br />
    &nbsp;&nbsp;# the OpenSSH private key name for your home account. <br />
	&nbsp;&nbsp;IdentityFile ~/.ssh/home.rsa<br />
	&nbsp;&nbsp;IdentitiesOnly yes</div>
    <p> See the <a href="http://linux.die.net/man/5/ssh_config"> SSH Docs</a> for more information about these options</p>
	</li></p>
	<p><li>Close Sourcetree</li></p>
	<p><li>Close <strong>all&nbsp;</strong>open terminals/shells/cmd prompts</li></p>
	<p><li>Relaunch Sourcetree</li></p>
	<p><li>Launch Terminal via Sourcetree</p>
		<img alt="terminal_sourcetree" src="/img/posts/terminal_st.png" class="img-responsive img-thumbnail"/>	
        <p>and verify that you see similar output:&nbsp;</p>
	<div style="background:#eee; border:1px solid #ccc; padding:5px 10px">Agent pid 11740<br />
	Identity added: /c/Users/yourname/.ssh/home.rsa (/c/Users/yourname/.ssh/home.rsa)<br />
	Identity added: /c/Users/yourname/.ssh/work.rsa (/c/Users/yourname/.ssh/work.rsa)</div>
	</li></p>
	<p><li>If you do not see that output, your .bashrc file is incorrect or in the wrong directory. Redo Step 3. If that still doesn&#39;t work, start over because you probably have the wrong format keys.</li></p>
	<p><li>&nbsp;Running ssh-add -l should list the thumbprints for your two SSH keys.</p>
    	<img alt="ssh-add-l" src="/img/posts/ssh-add-l.png" class="img-responsive img-thumbnail"/>
        </li></p>
	<p><li>You are now ready to clone/pull/push some code!</li></p>
    <p><em>From here, depending on what order you loaded your keys either your home or work will be treated as default. For me, my home registers as default because either key name or thumbprint is alphabetically first. No matter though; we can fix this!&nbsp;</em></p>
    </li></p>
	<p><li>Repos belonging to the non-default account will need to have their git origins modified by replacing the hostname portion of the url with the alias&nbsp;id from your .ssh\config file.</p>
    <div class="funfact"><p>In my case I would replace my origin <i>git@github.com:myname/repo.git</i> with <i>git@work:myname/repo.git</i>.</p></div></li></p>
	<p><li>Once you have updated your git origin for the secondary account to use the config file&#39;s alias from <a href="#step4">step 4</a>, you should be able to push/pul without issue.</li></p>
	<ul>
		<li>If you do have an issue, use Sourcetree menu Tools -&gt; Add SSH Key... dialog to try re-adding the key.</li>
		<li>If that doesn&#39;t work, close Sourcetree, any open console, and try again!</li>
		<li>If that doesn&#39;t work then you probably missed a step or detail. Try again!</li>
	</ul>
    <br />
    <li>
    <p>One final tip before you go. Be sure to clear out any saved username/passwords from the Sourcetree authentication tab that are related to your work/home accounts. If you don't remove these, Sourcetree will keep alerting you to that fact the HTTPS login cannot be performed via OpenSSH. Not a big deal but the modal dialogue gets lost and is super annoying to find.</p>
    </li>
	</li>
</ol>

<p>&nbsp;</p>

<p>Good luck and happy coding!</p>
	  
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
