---
title: "Let's count to 9 using javascript and CSS"
date: 2018-09-02T19:29:09+05:30
draft: false
author : "arvind"
featured_image: "counter.jpg"
---
<br>

I was scrolling through Instagram and found a cool number counter, I thought they made it in javascript but after looking at hashtags <mark>#3dmax #animation</mark> I came to know it was made in 3D software. I was like, why not remake it in javascript (just for fun). After I created the animated counter, I shared it on my <a target="_blank" href="https://instagram.com/heyarviind">Instagram</a> and got very positive reviews and many for the followers were asking for code and tutorials. 

<!-- <blockquote>"The code is much simpler than you might think let's have a look at the structure"</blockquote> -->

## Creating the structure

The HTML structure is composed of <mark>15 circle</mark> divs wrapped in a div, each row contains 3 circle divs so that we can show the numbers accurately

<pre>
	<code>
	&lt;div class=&quot;container&quot;&gt;
      
      &lt;div class=&quot;circle&quot;&gt;&lt;/div&gt;
      &lt;div class=&quot;circle&quot;&gt;&lt;/div&gt;
      ...

    &lt;/div&gt;
	</code>
</pre>

## Adding styles

I've kept this code simple so that readers can understand it easily, in CSS all I did is made 2 states of the circle, one is smaller grey in color which donates the <mark>inactive state</mark> and the second one is the <mark>.active class</mark> which makes the div bigger in size and colored to indicate the <mark>active</mark> state of the circle

<pre>
	<code>
		.circle{
		  width: 60px;
		  height: 60px;
		  background-color: #536dfe;
		  border-radius: 50%;
		  display: inline-block;
		  transform: scale(.2);
		  background-color: #c4c4c4;
		  transition: transform 1s ease-in-out;
		}

		.circle.active{
		  transform: scale(1);
		  background-color: #536dfe;
		}
	</code>
</pre>

## Events handling

First of all, we need to define the pattern of each number so that it can change the DOM accordingly. What I did is, made an array and defined each number's pattern as shown below.

<pre>
	<code>
		var num_pattern = [
				  [ 
				    1, 1, 1,
				    1, 0, 1,
				    1, 0, 1,		//For 1
				    1, 0, 1,
				    1, 1, 1
				  ],
				  [
				  	1, 1, 1,
				    0, 0, 1,
				    1, 1, 1,		//For 2
				    1, 0, 0,
				    1, 1, 1
				  ]
				  ...
			];
	</code>
</pre>

<strong>0</strong> indicates the <mark>inactive</mark> state and <strong>1</strong> indicates the <mark>active</mark> state

the main concept here is, each <mark>0</mark> and <mark>1</mark> in the pattern donates each element in the DOM. So if there is <mark>1</mark> in the 3rd index of an array, the 4th circle will be active ( Don't get confused here, Array starts from 0 😜)

now we have to change the number on every second so <strong>setTimeInteval</strong> will do the job. On every second we increment the number and check the number pattern in the array and update the DOM.

<pre>
	<code>
		var circles = document.querySelectorAll('.circle');
		var i = 0;

		setInterval(function(){
		  incNum();
		  // Increment the number at every 1 second
		  i++;
		}, 1000);

		function incNum(){
		  // Reset the counter when it reaches > 9
		  if(i == 10) i = 0;

		  for(z = 0; z < num_pattern[i].length; z++){
		    if(num_pattern[i][z]){
		      //If it has '1' then make the circle active
		      //Check if the circle is already active
		      if(!circles[z].classList.contains('active')){
		        circles[z].classList.add("active");
		      }
		    } else {
		      if(circles[z].classList.contains('active')){
		        circles[z].classList.remove("active");
		      }
		    }
		  }
		}
	</code>
</pre>

<strong>Note:</strong> Here we're only updating the DOM if required, this also gives the sweet effect to the animation

<div class="text-center">
	<a target="_blank" class="btn btn-success" href="https://demo.uicard.io/lets-count-to-9-in-javascript/">See the Demo</a>
</div>

