### node-vstream
---
https://github.com/joyent/node-vstream

```js
var instream, passthru, outstream;
instream = vstream.wrapStream(fs.createReadStream('/usr/bin/more'), 'source');
passthru = vstream.wrapStream(new stream.PassThrough(), 'passthru');
outstream = vstream.wrapStream(fs.createWriteStream('/dev/null'), 'devnull')
instream.pipe(pasthru);
passthru.pipe(otstream);

instream.on('data', report);
outstream.on('finish', report);
function report()
{
  var head = outstream.vsHead();
  assert.ok(head == instream);
  head.vsWalk(function (stream){ stream.vsDumpDebug(process.stdout); });
  console.log('-----');
}




var instream, linestream, mystream;
var user = 'nobody';
instream = vstream.wrapStream(fs.createReadStream('/etc/passwd'), 'source');
linestream = vstream.wrapTransform(new lstream());
mystream = new stream.Transform({ 'objectMode': true });
mystream._transform = function myTransform(line, _, callback){
  if(line.substr(0, user.length + 1) == user + ':'){
    this.push(user);
    this.vsWarn(new Error('found "' + user + '"'), 'nfoundusers');
  }
  callback();
};
mystream = vstream.wrapTransform(mystream, 'UserSearcher');
instream.pipe(linestream);
linestream.pipe(mystream);
mystream.on('warn', function(context, kind, error){
  console.log('kind: %s', kind);
  console.log('error: %s', error.message);
  console.log('context: %s', context.label());
  mystream.vsHead().vsWalk(function(s){
    s.vsDumpDebug(process.stdout);
  });
});
```

```
```

```
```


