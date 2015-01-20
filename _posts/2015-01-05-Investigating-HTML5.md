---
layout: post
title: Investigating HTML5
categories: [tech coop]
tags: []
published: True
---

During my coop term at OICR, I had experience investigating the new technologies in HTML5. This article summarizes the aspects that I discovered.

<style>
#files {
   margin-top: 30px;
   display: inline-block;
   border: 1px solid #999;
   border-radius: 3px;
   padding: 5px 8px;
   outline: none;
   font-size: 10pt;
   font-weight: 700;
   white-space: nowrap;
   text-shadow: 1px 1px #fff;
   width: 300px;
}

#drop_zone {
   border: 3px dashed;
   margin-top: 30px;
   text-align: center;
   width: 300px;
   height: 50px;
   line-height: 40px;
}


#sliders {
   width: 150px;
}

#list, #newlist {
   display: inherit;
   font-size: large;
}

#list ul, #newlist ul {
   list-style-type: none;
}

#tagList {
   list-style-type: none;
   font-size: 25px;
}

#tagList pre {
   margin-left: 0;
   width: 100%;
}

#tagList form {
   text-align: left;
}

::-webkit-input-placeholder { 
   font-size: 25px;
   text-align: center; 
   line-height: 400px;
}


#nols {
   width: 50%;
   height: 430px;
   font-size: 25px;
}

#ls {
   width: 45%;
   height: 380px;
   font-size: 25px;
   position: relative;
   top: -50px;
}

#clear_btn {
   -moz-box-shadow:inset 0px 1px 3px 0px #91b8b3;
   -webkit-box-shadow:inset 0px 1px 3px 0px #91b8b3;
   box-shadow:inset 0px 1px 3px 0px #91b8b3;
   background:-webkit-gradient(linear, left top, left bottom, color-stop(0.05, #768d87), color-stop(1, #6c7c7c));
   background:-moz-linear-gradient(top, #768d87 5%, #6c7c7c 100%);
   background:-webkit-linear-gradient(top, #768d87 5%, #6c7c7c 100%);
   background:-o-linear-gradient(top, #768d87 5%, #6c7c7c 100%);
   background:-ms-linear-gradient(top, #768d87 5%, #6c7c7c 100%);
   background:linear-gradient(to bottom, #768d87 5%, #6c7c7c 100%);
   filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#768d87', endColorstr='#6c7c7c',GradientType=0);
   background-color:#768d87;
   -moz-border-radius:5px;
   -webkit-border-radius:5px;
   border-radius:5px;
   border:1px solid #566963;
   display:inline-block;
   cursor:pointer;
   color:#ffffff;
   font-family:arial;
   font-size:15px;
   font-weight:bold;
   padding:11px 23px;
   text-decoration:none;
   text-shadow:0px -1px 0px #2b665e;
   width: 46%;
   margin-left: 340px;
   position: relative;
   left: 3px;
   top: -50px;
}

#clear_btn:hover {
   background:-webkit-gradient(linear, left top, left bottom, color-stop(0.05, #6c7c7c), color-stop(1, #768d87));
   background:-moz-linear-gradient(top, #6c7c7c 5%, #768d87 100%);
   background:-webkit-linear-gradient(top, #6c7c7c 5%, #768d87 100%);
   background:-o-linear-gradient(top, #6c7c7c 5%, #768d87 100%);
   background:-ms-linear-gradient(top, #6c7c7c 5%, #768d87 100%);
   background:linear-gradient(to bottom, #6c7c7c 5%, #768d87 100%);
   filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#6c7c7c', endColorstr='#768d87',GradientType=0);
   background-color:#6c7c7c;
}


</style>
1. New APIs
   - drag and drop
   - Canvas
   - Audio and Video tag
2. Semantic Web
   - New input tags
   - Sectioning
3. Local Storage

### New APIs

#### Drag and Drop

##### The HTML4 way:
Before, we had to use a "choose file" popup to prompt users for files.

<input type="file" id="files" name="files[]" multiple />
<output id="list"></output>


##### The HTML5 Way:
It is a lot eaiser to upload files with the Drag and Drop API - you just drag and drop it from your local disk. It is known that Googld Drive, Dropbox and many other services have adopted this technology.

<div id="drop_zone">Drop files here</div>
<br>
<output id="newlist"></output>


#### Canvas

Canvas is my favourite technology by far - it's highly customizable, easy to learn and has better performance.

A canvas is very simple on its HTML, like this:
{% highlight html %}
<canvas id="myCanvas"></canvas>
{% endhighlight %}

... and that's it! Its behavious is fully controled by JavaScript.

Here is a demo on canvas:

<div>
<canvas id="mycanvas"></canvas>
<br><br>
<button id="paper_btn">drawPaper</button>
<button id="cat_btn">drawCat</button>
<button id="manycat_btn">drawManyCats</button>
<button id="gradient_btn">drawGradient</button>
<button id="radial_btn">drawRadial</button>
<form id="sliders"></form>
</div>
<br>

Canvas supports hardware acceleration, meaning it takes advantage of the computing power of the GPU in your computer, resulting in much better performance when dealing with heavy graphic canvases.

Examples of heavy-graphics canvas:

- [Microsoft Fish IE Tank](http://ie.microsoft.com/testdrive/performance/fishietank)
- [Glacier Works](http://explore.glacierworks.org/en/#everest/explore)


#### Native Video and Audio Support

HTML5 natively supports playing videos and auddios - meaning by the time it's fully adopted, you can finally throw away your third-party plugins like Flash/Quicktime/Silverlight/etc - which are prone to causing heat and wasting resources. 

You can easily embed a video in your webpage like this:
{% highlight html %}
<video width="640" height="480" controls>
   <source src="files/myVideo.mp4" type="video/mp4">
   <source src="files/myVideo.ogg" type="video/ogg">
   Your browser does not support the video tag
</video>
{% endhighlight %}

Your browser will choose the first child node that it understands (based on the type - maybe the last line - it always understands text), download it, and display it right away. 


### Semantic Web

#### New input tags

HTML5 introduces many new input tags which aim to address cross browser compatibility issues as well as adding optimizations and features. Note that not all browsers have fully adopted all these new tags, therefore it's best to view them in Chrome. Here is a list of my favourites:

{% highlight html %}
<input type="email" name="email">
<!--
Try inputing something that's not a valid email!
-->
{% endhighlight %}

<div>
<form>
   Email address:
   <input type="email" name="email">
   <input type="submit">
</form>
</div>

<br>
{% highlight html %}
<input type="number" name="lucky" min="1" max="100">
<!--
Try inputing something that's not a number / not within the range!
Also observe what Chrome has done on the right side of the input area!
-->
{% endhighlight %}

<div>
<form>
   Input your lucky number: 
   <input type="number" name="lucky" min="1" max="100">
   <input type="submit">
</form>
</div>

<br>
{% highlight html %}
<input type="color" name="favcolor">
<!--
Wow! This brings up the system-native color picker!
-->
{% endhighlight %}

<div>
<form>
   Choose your favorite color:
   <input type="color" name="favcolor">
   <input type="submit">
</form>
</div>

<br>
{% highlight html %}
<input type="date" name="bday">
<!--
In chrome, this brings up a calendar!
Also, in iOS/Android, this also brings up the native date picker
-->
{% endhighlight %}

<form>
   Input your birthday: 
   <input type="date" name="bday">
   <input type="submit">
</form>


#### Sectioning

In HTML4, we use ```<div></div>``` for everything. Some divs are for structuring purposes (e.g., section, subsection), while other divs are for theming purposes (e.g, a wrapper div).

The introduction to sectioning tags in HTML5 solves the problem. The ```<section>``` tag, ```<aside>``` tag, ```<article``` tag,, ```<nav>``` tag, etc are always used for structuring purposes. This helps developers think of the roles of contents, and produce more high-quality internet.

The HTML4 tags:
{% highlight html %}
<div class="section" id="forest-elephants">
   <h1>Forest elephants</h1>
   <p>In this section, we discuss the lesser known forest elephants.</p>
   <div class="subsection" id="forest-habitat">
      <h2>Habitat</h2>
      <p>Forest elephants do not live in trees but among them.</p>
   </div>
   <div class="ads" id="ad1">
      some ads
   </div>
</div>
{% endhighlight %}

The HTML5 tags:
{% highlight html %}
<section>
   <h1>Forest elephants</h1>    
   <p>In this section, we discuss the lesser known forest elephants. 
   <section>
      <h2>Habitat</h2>  
      <p>Forest elephants do not live in trees but among them.
   </section>
   <aside>
      some ads
   </aside>
</section>
{% endhighlight %}


It is also beneficial that these semantic tags serve machines more convieniently - think about how a screen reader for accecibility-aquired users would parse the DOM, or how AdBlock analyzes which piece of content is more likely an ad.


### Local Storage

Local Storage is so fun!!

Here's a demo - try typing something in both boxes and *refresh* or *close the browser tab* or *quit the entire browser*, and reopen - then see the magic!

<div>
<textarea class="old" id="nols" ></textarea>
<textarea class="new" id="ls"></textarea>
<button id="clear_btn">clear</button>
</div>

As the name suggests, local storage stores your data locally, in your browser. It's not sent to the server (like cookies), and it has bigger space for storing data.

This basically is how Google Docs work - with some code to sync your data to the server when it needs to, you can make a web app that can work offline. Imagine you are at an airport and you don't have Internet access - work on your docs as usual, and you'll be able to sync it to the server when you're online.


### Conclusion

HTML5 is so powerful.

HTML5 was announced official and complete on October, 2014 on the HTML5DevConf conference. To contrast, HTML4 was standardized in 1997.

42% of 10,000 developers surveyed by 2014 Vision Mobile is already using HTML5 to build apps - before it was even official.

One of the promises of HTML5 is to lowering the cost of developing powerful, cross-platform applications. The theme is "Write once, deploy anywhere".


<script>
function handleFileSelect5(ev) {
   ev.stopPropagation();
   ev.preventDefault();
   var files = ev.dataTransfer.files;
   var output = [];
   var i, f;
   for (i = 0, f = null; f = files[i]; i++) {
      output.push('<li><strong>', escape(f.name), '</strong> is a <u>', f.type || 'n/a  ', '</u> file with size ', f.size, ' bytes', '</li>');
   }
   document.getElementById('newlist').innerHTML = '<ul>' + output.join('') + '</ul>';
}

function handleDragOver(ev) {
   ev.stopPropagation();
   ev.preventDefault();
   ev.dataTransfer.dropEffect = "copy";
}

var dropZone = document.getElementById('drop_zone');
dropZone.addEventListener('dragover', handleDragOver, false);
dropZone.addEventListener('drop', handleFileSelect5, false);
</script>

<script>
function handleFileSelect(ev) {
   var files = ev.target.files;
   var output = [];
   var i, f;
   for(i = 0, f = null; f = files[i]; i++) {
      output.push('<li><strong>', escape(f.name), '</strong> is a <u>', f.type || 'n/a  ', '</u> file with size ', f.size, ' bytes', '</li>');
   }
   document.getElementById('list').innerHTML = '<ul>' + output.join('') + '</ul>';
}
document.getElementById('files').addEventListener('change', handleFileSelect, false);
</script>

<script>
var canv = document.getElementById('mycanvas');
var ctx = canv.getContext('2d');

canv.width = 500;
canv.height = 375;

function removeSliders() {
   var sliders = document.getElementById('sliders');
   if(sliders) {
      sliders.style.display = "none";
   }
   var examples = canv.parentElement.querySelectorAll('p');
   [].forEach.call(examples, function(example) {
      example.style.display = "";
   });
}

function drawPaper() {
   removeSliders();
   canv.height = canv.height;
   for(var i = 0.5; i < canv.height; i += 10) {
      ctx.moveTo(0, i);
      ctx.lineTo(canv.width, i);
   }
   for(var i = 0.5; i < canv.width; i += 10) {
      ctx.moveTo(i, 0);
      ctx.lineTo(i, canv.height);
   }
   ctx.strokeStyle = "#eee";
   ctx.stroke();

   ctx.beginPath();
   ctx.moveTo(0, 40);
   ctx.lineTo(240, 40);
   ctx.moveTo(260, 40);
   ctx.lineTo(500, 40);
   ctx.moveTo(495, 35);
   ctx.lineTo(500, 40);
   ctx.lineTo(495, 45);
   
   ctx.moveTo(60, 0);
   ctx.lineTo(60, 153);
   ctx.moveTo(60, 173);
   ctx.lineTo(60, 375);
   ctx.moveTo(65, 370);
   ctx.lineTo(60, 375);
   ctx.lineTo(55, 370);
   ctx.rect(100, 150, 100, 100);
   ctx.closePath();
   
   ctx.strokeStyle = "black";
   ctx.stroke();
   
   ctx.beginPath();
   ctx.arc(300, 200, 50, 0, 2*Math.PI);
   ctx.strokeStyle = "black";
   ctx.stroke();
   ctx.closePath();

   ctx.font = "bold 12px sans-serif";
   ctx.fillText("x", 248, 43);
   ctx.fillText("y", 58, 165);

   ctx.textBaseline = "top";
   ctx.fillText("(0, 0)", 8, 5);
   
   ctx.textAlign = "right";
   ctx.textBaseline = "bottom";
   ctx.fillText("(500, 375)", 492, 370);
   
   ctx.fillRect(0, 0, 3, 3);
   ctx.fillRect(497, 372, 3, 3);
};

function drawGradient() {
   removeSliders();
   canv.height = canv.height;
   var grad = ctx.createLinearGradient(0, 0, canv.width, canv.height);
   grad.addColorStop(0, "#9e009e");
   grad.addColorStop(1/7, "#0000ff");
   grad.addColorStop(2/7, "#00ffff");
   grad.addColorStop(3/7, "#00ff00");
   grad.addColorStop(4/7, "#ffff00");
   grad.addColorStop(5/7, "#ff7f00");
   grad.addColorStop(6/7, "#ff0000");
   ctx.fillStyle = grad;
   ctx.fillRect(0, 0, canv.width, canv.height);
}

function drawRadial () {
   var radialForm = document.getElementById('sliders');
   var horizSlider = document.createElement('input');
   var vertiSlider = document.createElement('input');
   var startBtn = document.createElement('button');

   if(radialForm.childElementCount === 0) {
      radialForm.appendChild(horizSlider);
      radialForm.appendChild(vertiSlider);
      radialForm.appendChild(startBtn);
   }

   horizSlider.setAttribute('type', 'range');
   horizSlider.setAttribute('value', canv.width/2);
   horizSlider.setAttribute('min', canv.width/8);
   horizSlider.setAttribute('max', canv.width*7/8);

   vertiSlider.setAttribute('type', 'range');
   vertiSlider.setAttribute('value', canv.height/2);
   vertiSlider.setAttribute('min', canv.height/8);
   vertiSlider.setAttribute('max', canv.height*7/8);

   startBtn.innerHTML = "Start!";
   startBtn.onclick = function(ev) {
      ev.preventDefault();
   }

   radialForm.style.display = "";

   var clickStart = function() {
      var i = 1;
      console.log('calling start');
      function myLoop () {
         setTimeout(function() {
            vertiSlider.value = Math.sin(i * Math.PI / 360) * canv.height * 2;
            horizSlider.value = Math.sin((i+180) * Math.PI / 360) * canv.width * 2;
            i++;
            console.log(i);
            // onInput is not triggered when value is changed programmatically
            onInput();
            if(i < 360 * 6) {
               console.log('calling myLoop()');
               myLoop(); 
            }
         }, 3);
      }
      myLoop();
   }

   var onInput = function() {
      canv.height = canv.height;
      var grad = ctx.createRadialGradient(horizSlider.value, vertiSlider.value, 0, canv.width/2, canv.height/2, canv.width/2);
      grad.addColorStop(0.000, '#ffff00');
      grad.addColorStop(0.200, '#ffff00');
      grad.addColorStop(0.210, '#ff0000');
      grad.addColorStop(0.400, '#ff0000');
      grad.addColorStop(0.410, '#82C2EE');
      grad.addColorStop(0.600, '#82C2EE');
      grad.addColorStop(0.610, '#ffffff');
      grad.addColorStop(0.780, '#ffffff');
      grad.addColorStop(0.790, '#000000');
      grad.addColorStop(0.990, '#000000');
      grad.addColorStop(1.000, '#ffffff');
      ctx.fillStyle = grad;
      ctx.fillRect(0, 0, canv.width, canv.height);
   }

   onInput();
   horizSlider.addEventListener('input', onInput);
   vertiSlider.addEventListener('input', onInput);
   startBtn.addEventListener('click', clickStart);
}

function drawCat() {
   removeSliders();
   canv.height = canv.height;
   var cat = new Image();
   cat.src = "/files/cat.png";
   cat.onload = function() {
      ctx.drawImage(cat, canv.width/2, canv.height/2);
   }
}

function drawManyCats() {
   removeSliders();
   canv.height = canv.height;
   var cat = new Image();
   cat.src = "/files/cat.png";
   cat.onload = function() {
      for(var x = 0, y = 0; x < canv.width && y < canv.height; x += 50, y += 37) {
         ctx.drawImage(cat, x, y, 88, 56);
      }
   }
}
drawPaper();
document.getElementById('paper_btn').addEventListener('click', drawPaper);

document.getElementById('gradient_btn').addEventListener('click', drawGradient);

document.getElementById('radial_btn').addEventListener('click', drawRadial);

document.getElementById('cat_btn').addEventListener('click', drawCat);

document.getElementById('manycat_btn').addEventListener('click', drawManyCats);
</script>

<script>
var submits = document.querySelectorAll('input[type="submit"]');
   [].forEach.call(submits, function(sub) {
      sub.onclick = function() {
         var input = sub.previousElementSibling;
         var val = input.value;
         var parent = sub.parentNode;
         if(input.checkValidity()) {
         // sub.style = "visibility: hidden";
         parent.removeChild(sub);
         parent.removeChild(input);
         parent.innerHTML += val;
         return false;
      }
   }
});
</script>


<script>
   
var nols = document.getElementById('nols');
var ls = document.getElementById('ls');

nols.placeholder = "Without localStorage";
ls.placeholder = "With localStorage";

function onLoad() {
   if(window.localStorage.data) {
      ls.value = window.localStorage.data;
   }
}

function onClear() {
   if(window.localStorage.data) {
      window.localStorage.clear();
   }
   ls.value="";
}

ls.addEventListener('keyup', function() {
   window.localStorage.data = ls.value;
});

document.getElementById('clear_btn').addEventListener('click', onClear);

window.onload = onLoad;
</script>