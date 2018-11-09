<!--
author:   Your Name

email:    your@mail.org

version:  0.0.1

language: en

narrator: US English Female

comment:  Try to write a short comment about
          your course, multiline is also okay.

script:   https://gitcdn.xyz/repo/liaScript/skulpt_template/master/js/skulpt.min.js
          https://gitcdn.xyz/repo/liaScript/skulpt_template/master/js/skulpt-stdlib.js


@eval
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


Sk.configure({output: function(e){ send.lia("output", e) },
              read: builtinRead,
              inputfun: input(send.handle)});

if( document.getElementById("skulpt_canvas") ) {
  Sk.canvas = "skulpt_canvas";
  (Sk.TurtleGraphics || (Sk.TurtleGraphics = {})).target = 'skulpt_canvas';
}

setTimeout( function(e) {
let myPromise = Sk.misceval.asyncToPromise(function() {
  return Sk.importMainWithBody("<stdin>", false, `@input`, true);
   });
   myPromise.then(function(mod) {
       send.lia("eval", "LIA: stop");
   },
   function(err) {
       send.lia("eval", err.toString(), [], false);
       send.lia("eval", "LIA: stop");
   });
}, 150);

"LIA: terminal";
</script>
@end

-->

# Skulpt Template

This is a template for developing interactive Python courses with LiaScript and
Skulpt.

To find out more about Skulpt, visit the project site: http://www.skulpt.org

See the live rendered version of this document at:
https://raw.githubusercontent.com/liaScript/skulpt_template/master/README.md

Clone or fork this Project and start to develop a course:

Github: https://github.com/liaScript/skulpt_template

## Example

``` python
print "how many hellos should I print"

hellos = input()

for i in range(int(hellos)):
  print "Hello World #", i
```
@eval

## Generator

```python
def genr(n):
    i = 0
    while i < n:
        yield i
        i += 1

print list(genr(12))
```
@eval


## DOM

``` python
import document

pre = document.getElementById('edoutput')
pre.innerHTML = '''
<h1> Skulpt can also access DOM! </h1>
'''
```
@eval

<span id="edoutput"></span>


## Turtle

```python
import turtle

t = turtle.Turtle()

for c in ['red', 'green', 'yellow', 'blue']:
    t.color(c)
    t.forward(75)
    t.left(90)
    print "color", c
```
@eval

<div id="skulpt_canvas" style="border-style: solid; height: 400px; width: 400px"></div>
