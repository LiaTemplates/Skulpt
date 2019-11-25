<!--
author:   André Dietrich

email:    andre.dietrich@ovgu.de

version:  0.0.3

language: en

narrator: US English Female

logo:     https://upload.wikimedia.org/wikipedia/commons/4/4a/Python3-powered_hello-world.svg

comment:  Macros for Python programming in LiaScript, by making use of the
          skulpt interpreter.

script:   https://gitcdn.xyz/repo/liaTemplates/skulpt/master/js/skulpt.min.js
          https://gitcdn.xyz/repo/liaTemplates/skulpt/master/js/skulpt-stdlib.js


@Skulpt.eval
<script>
function builtinRead(x) {
  if (Sk.builtinFiles === undefined || Sk.builtinFiles["files"][x] === undefined)
    throw "File not found: '" + x + "'";
  return Sk.builtinFiles["files"][x];
}

function input(handle) {
  return function(prompt) {
    return new Promise((resolve, reject) => {	send.handle("input", (e) => resolve(e)) });
  }
}

Sk.configure({
  output: (e) => send.log(true, "", e.toString()),
  read: builtinRead,
  inputfun: input(send.handle)});

if( document.getElementById("@0") ) {
  Sk.canvas = "@0";
  (Sk.TurtleGraphics || (Sk.TurtleGraphics = {})).target = '@0';
}

setTimeout( function(e) {
  let myPromise = Sk.misceval.asyncToPromise(function() {
    return Sk.importMainWithBody("<stdin>", false, `@input`, true);
  });
  myPromise.then(function(mod){ send.lia("LIA: stop") },
   function(err) {
       console.error(err);
       send.lia("LIA: stop");
   });
}, 150);

"LIA: terminal";
</script>
@end
-->

# Skulpt - Template

This is a template for developing interactive Python courses with
[LiaScript](https://LiaScript.github.io) and [Skulpt](http://www.skulpt.org).

__Try it on LiaScript:__

https://liascript.github.io/course/?https://raw.githubusercontent.com/liaTemplates/skulpt/master/README.md

__See the project on Github:__

https://github.com/liaTemplates/skulpt


                         --{{1}}--
There are three ways to use this template. The easiest way is to use the
`import` statement and the url of the raw text-file of the master branch or any
other branch or version. But you can also copy the required functionionality
directly into the header of your Markdown document, see therefor the
[last slide](#5). And of course, you could also clone this project and change
it, as you wish.

                           {{1}}
1. Load the macros via

   `import: https://raw.githubusercontent.com/liaTemplates/skulpt/master/README.md`

2. Copy the definitions into your Project

3. Clone this repository on GitHub


## `@Skulpt.eval`

                         --{{0}}--
Add the macro `@Skulpt.eval` to the end of every Python code-block that you want
to make executable and editable in LiaScript. The given code gets evaluate by
the Skulpt interpreter and the result is shown in a console below.


``` python
print "how many hellos should I print"

hellos = input()

for i in range(int(hellos)):
  print "Hello World #", i
```
@Skulpt.eval


## `@Skulpt.eval` with HTML

                         --{{0}}--
Adding an additional html-tag with an id-attribute you can also manipulate the
DOM. If you add the class `persistent` to your tag, LiaScript will take care of
your changes and restore them, if you load reload the section.

``` python
import document

pre = document.getElementById('edoutput')
pre.innerHTML = '''
<h1> Skulpt can also access DOM! </h1>
'''
```
@Skulpt.eval

<span id="edoutput" class="persistent">
  This is a span with id (edoutput) and class(persistent).
</span>


## `@Skulpt.eval` with Turtle

                          --{{0}}--
You can use the Turtle implementation by adding another html-tag and by passing
its id as a parameter to `@Skulpt.eval`. This element is then used as a canvas
for the turtle and if you also add class persistent to it, then you can preserve
its state.

```python
import turtle

t = turtle.Turtle()

for c in ['red', 'green', 'yellow', 'blue']:
    t.color(c)
    t.forward(75)
    t.left(90)
    print "color", c
```
@Skulpt.eval(skulpt_canvas)

<div class="persistent" id="skulpt_canvas" style="border-style: solid; height: 400px; width: 400px">
  This is a div with id (skulpt_canvas) and class (persistent).
</div>

## Implementation

                         --{{0}}--
The code shows how the macro `@Skulpt.eval` is implemented. The script command
at the top loads two javascript libraries that have to be called in order load
the interpreter.

``` html
script: https://gitcdn.xyz/repo/liaTemplates/skulpt/master/js/skulpt.min.js
        https://gitcdn.xyz/repo/liaTemplates/skulpt/master/js/skulpt-stdlib.js

@Skulpt.eval
<script>
function builtinRead(x) {
  if (Sk.builtinFiles === undefined || Sk.builtinFiles["files"][x] === undefined)
    throw "File not found: '" + x + "'";
  return Sk.builtinFiles["files"][x];
}

function input(handle) {
  return function(prompt) {
    return new Promise((resolve, reject) => {	send.handle("input", (e) => resolve(e)) });
  }
}

Sk.configure({
  output: (e) => send.log(true, "", e.toString()),
  read: builtinRead,
  inputfun: input(send.handle)});

if( document.getElementById("@0") ) {
  Sk.canvas = "@0";
  (Sk.TurtleGraphics || (Sk.TurtleGraphics = {})).target = '@0';
}

setTimeout( function(e) {
  let myPromise = Sk.misceval.asyncToPromise(function() {
    return Sk.importMainWithBody("<stdin>", false, `@input`, true);
  });
  myPromise.then(function(mod){ send.lia("LIA: stop") },
   function(err) {
       console.error(err);
       send.lia("LIA: stop");
   });
}, 150);

"LIA: terminal";
</script>
@end
```


                         --{{1}}--
If you want to minimize loading effort in your LiaScript project, you can also
copy this code and paste it into your main comment header, see the code in the
raw file of this document.

                           {{1}}
https://raw.githubusercontent.com/liaTemplates/skulpt/master/README.md
