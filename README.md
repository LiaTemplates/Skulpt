<!--
author:   Your Name

email:    your@mail.org

version:  0.0.1

language: en

narrator: US English Female

comment:  Try to write a short comment about
          your course, multiline is also okay.

script:   js/skulpt.min.js
          js/skulpt-stdlib.js


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


``` python
print "how many hellos should I print"

hellos = input()

for i in range(int(hellos)):
  print "Hello World #", i
```
@eval
