
<section  data-background='pres/images/container_yard.jpg' data-state='blackout'>
</section>
<section  data-state='blackout' data-background-image="pres/images/container_yard.jpg" ><div class="sl-block" data-block-type="text" style="width: 900px; left: 88px; top: 23px; height: auto;"><div class="sl-block-content" data-placeholder-tag="h1" data-placeholder-text="Title Text" style="color: rgb(255, 255, 255); z-index: 11; border: 5px solid rgb(68, 68, 68); padding: 10px; background-color: rgb(170, 170, 170);">
<h2 style="color:white;">Docker Swarm Demo</h2>
<h4 style="color:white;">Docker Switzerland Meetup #10</h4>
<h4 style="color:white;">13 September 2016</h4>
</div></div>
<div class="sl-block" data-block-type="image" style="min-width: 30px; min-height: 30px; width: 220px; height: 320px; left: 10px; top: 420px;"><div class="sl-block-content" style="z-index: 12;"><img data-natural-width="500" data-natural-height="684" style="" data-src="pres/images/docker-swarm-logo.png"></div></div></section>
---
<section data-state='blackout' data-background-image="pres/images/bees.gif" data-background-size="1300px 850px">
</section>
<section data-state='blackout' data-background-image="pres/images/bees.gif" data-background-size="1300px 850px">
<div class="sl-block" data-block-type="text" style="width: 900px; left: 200px; top: 23px; height: auto;"><div class="sl-block-content" data-placeholder-tag="h2" data-placeholder-text="Title Text" style="color: rgb(255, 255, 255); z-index: 11; border: 5px solid rgb(68, 68, 68); padding: 10px; background-color: rgb(170, 170, 170);">
<h2 style="color:white;">Agenda</h2>
 <ol>
    <li class='fragment fade-up'>Introduction</li>
    <li class='fragment fade-up'>Swarm Overview</li>
    <li class='fragment fade-up'>Build a Swarm</li>
 </ol>
 </div></div>
</section>
<section data-transition='convex' data-background-transition="zoom" data-background-repeat="no-repeat" data-background-position="bottom" data-background="#fffffff">
<div class="sl-block" data-block-type="text" style="width: 800px; left: 23px; top: 161px; height: auto;" data-block-id="c93eb661fd29fc2c5fa38f88c43f79ba"></div>
    <div class="sl-block-content" data-placeholder-tag="p" data-placeholder-text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi nec metus justo. Aliquam erat volutpat." style="z-index: 13; text-align: left;"></div>
<h2> Brian Christner</h2>
 <br />
    <ul>
	<li >Swisscom Cloud Architect</li>
	<li >Docker Captain</li>
	<li >Background in Containers, Cloud, &amp; Engineering
    </li></ul> 
     <br />
      <br />
    <img data-natural-width="228" data-natural-height="683" style="width: 242px; height: 300px; left: 400px; top: 347.605px;" data-src="pres/images/brian_christner.jpg">
    <img style="width: 242px; height: 300px; left: 400px; top: 347.605px;"  data-natural-width="228" data-natural-height="306" data-src="pres/images/docker_captian_image.png">
</section>
---
<section data-transition='zoom'>
<link rel="stylesheet" href="css/theme/serif.css" id="theme">
<h1>Swarm Overview</h1>
</section>
---
<section data-background-transition='convex' data-background="pres/images/engine.jpg" data-background-size="100% 100%">
</section>
---
<section data-background-transition='convex' data-background="pres/images/swarm.png" data-background-transition="zoom" data-background-size="100% 100%" data-background="#fffffff">
</section>
---
<section data-background="pres/images/deploy.png" data-background-transition='fade' data-background-size="100% 100%" data-background="#fffffff">
</section>
---
<section data-background="pres/images/demo.gif" data-background-transition='convex' data-background-size="100% 100%" data-background="#fffffff">
<h1 style="color:white;">DEMO TIME</h1>
</section>
---
<section data-transition='convex'>
<link rel="stylesheet" href="css/theme/serif.css" id="theme">
<h2>Follow along</h2>
<h3>[https://github.com/vegasbrianc/docker-ch-meetup10](github.com/vegasbrianc/docker-ch-meetup10)</h3>
</section>
<section data-transition='convex' data-transition='zoom'>
<link rel="stylesheet" href="css/theme/serif.css" id="theme">

    
<h3>Step 1. Deploy a Standalone App</h3>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker run -d --name cats-app -p 5000:5000 vegasbrianc/cats
</code></pre>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker ps
</code></pre>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ curl 0.0.0.0:5000
</code></pre>

</section>

<section data-transition='convex' data-transition='zoom'>
<link rel="stylesheet" href="css/theme/serif.css" id="theme">
    
<h3>Step 2.</h3>
<h3>If you Build it, the Swarm will come</h3>
<br>
<pre class='fragment fade-up' ><code data-trim data-noescape>$ docker-machine create -d virtualbox mgr</code>
<br>
<code data-trim data-noescape>$ docker-machine create -d virtualbox node01</code></pre>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker-machine create -d virtualbox node02</code></pre>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker-machine ls</code></pre>
</section>
<section data-transition='convex' data-transition='zoom'>
<link rel="stylesheet" href="css/theme/serif.css" id="theme">
    
<h3>Step 3. Initialize the Swarm</h3>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker-machine ssh mgr</code></pre>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker swarm init --advertise-addr 192.168.99.100</code></pre>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape> ```$ docker run -it -d -p 8080:8080 -e HOST=192.168.99.100 \
-v /var/run/docker.sock:/var/run/docker.sock \
--name viz manomarks/visualizer```
</code></pre>
</section>
<section data-transition='convex' data-transition='zoom'>
<link rel="stylesheet" href="css/theme/serif.css" id="theme">
    
<h3>Step 4. Join Nodes to the Swarm</h3>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker-machine ssh node01</code></pre>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>```$ docker swarm join-token worker
To add a worker to this swarm, run the following command:
 docker swarm join \
--token SWMTKN-1-1vh7h94m797al5a4pcma4p7nxdw22vqa2udwgkrkcd0twsz92d-4xgkpsqo1wyi0v7m4pnqcv2eq \
192.168.99.100:237``` </code></pre>
<br>
<h4 class='fragment fade-up'>Repeat for Node02</h4>
</section>
<section data-transition='convex' data-transition='zoom'>
<h3>Step 5. Verify our Swarm</h3>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker-machine ssh mgr</code></pre>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker node ls</code></pre>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker info</code></pre>
<br>
<h4 class='fragment fade-up'>Open the Visualizer 192.168.99.100:8080</h4>
</section>
<section data-transition='convex' data-transition='zoom'>
<h3>Step 6. Create Overlay Network</h3>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker network create -d overlay catnet</code></pre>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker network ls</code></pre>
</section>
<section data-transition='convex' data-transition='zoom'>
<h3>Step 7. DEPLOY</h3>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker service create --network catnet -p 5000:5000 \
--name cat-app vegasbrianc/cats</code></pre>
<br>
<h4 class='fragment fade-up'>Time to Scale</h4>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker service update --replicas 6 cat-app</code></pre>
<br>
<h4 class='fragment fade-up'>Drain a node</h4>
<br>
<pre class='fragment fade-up'><code data-trim data-noescape>$ docker node update --availability drain mgr</code></pre>
</section>
---
<section data-transition='zoom'>
<link rel="stylesheet" href="css/theme/serif.css" id="theme">
<h1>Conclusion</h1>
<br />
    <ul>
    <li class='fragment fade-up'>Created Swarm Nodes</li>
    <li class='fragment fade-up'>Joined Nodes to a Swarm</li>
    <li class='fragment fade-up' >Deployed our Cat service</li>
    <li class='fragment fade-up' >Scaled our Cat service</li>
    <li class='fragment fade-up' >Drained Manager Node</li></ul> 
     <br />
</section>
---
<section data-transition='zoom' data-background="pres/images/questions.png" data-background-size="1300px 700px">
<link rel="stylesheet" href="css/theme/serif.css" id="theme">
</section>
<section data-transition='zoom' data-background="pres/images/monitoring_mayhem.png" data-background-size="1300px 700px">
</section>
<section data-transition='zoom' data-background="pres/images/container_yard.jpg" data-background-size="1300px 700px"><div class="sl-block" data-block-type="text" style="width: 900px; left: 88px; top: 23px; height: auto;"><div class="sl-block-content" data-placeholder-tag="h1" data-placeholder-text="Title Text" style="color: rgb(255, 255, 255); z-index: 11; border: 5px solid rgb(68, 68, 68); padding: 10px; background-color: rgb(170, 170, 170);">
<link rel="stylesheet" href="css/theme/serif.css" id="theme">
<h1 style="color:white;">Thank you</h1>
<br>
<br>
<h3 style="color:white;" >Brian Christner / @idomyowntricks</h3>
<br>
<br>
<h4 style="color:white;">http://veggiemonk.github.io/awesome-docker</h4>
</section>