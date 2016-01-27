# profiling-node

I always forget the incantation and end up having to dig through google and old repos,
so this is a brain dump:

```bash
npm install --save v8-profiler
```

```js
const profiler = require('v8-profiler');

// run your init stuff
// ...

// Start the profiler
profiler.startProfiling('1', true);

// run the code that you want to profile
// ...

// Stop the profiler
const profile1 = profiler.stopProfiling();

// Export the profiler's data as JSON
profile1.export(function(err, result) {
  if (err) throw err;
  
  // Dump the data to a timestamped file in the current working directory
  fs.writeFileSync(+new Date() + '.cpuprofile', result);
  
  // Cleanup
  profile1.delete();
});
```

Load the file into chrome's devtools, and behold the magic.
