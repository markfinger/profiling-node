# profiling-node

I always forget the incantation and end up having to dig through google and old repos,
so this is a brain dump:

```bash
npm install --save v8-profiler
```

```js
const fs = require('fs');
const profiler = require('v8-profiler');

// run your init stuff
// ...

// Start the profiler
profiler.startProfiling('1', true);

// run the code that you want to profile
// ...

// Stop the profiler
const profile = profiler.stopProfiling();

// Export the profiler's data as JSON
profile.export(function(err, result) {
  if (err) throw err;
  
  // Dump the data to a timestamped file in the current working directory
  fs.writeFileSync((new Date()).getTime() + '.cpuprofile', result);
  
  // Cleanup
  profile.delete();
});
```

Load the file into chrome's devtools, and behold the magic.
