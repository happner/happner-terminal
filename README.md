# happner-terminal

Terminal for happner (comes bundled).

Provides a prompt into your running mesh. 

#### To activate

```javascript
meshConfig = {
  ...
  components: {
    terminal: {},
    ...
    ...
  }   
  ...
}
```

__Note__: By putting the terminal component first, other components running their startMethods can detect and use the terminal. eg. To install commands into it.


#### Typical startMethod installing a command into the terminal

This in some other mesh component:

```javascript
Module.prototype.start = function($happn, callback) {

  var terminal;

  if (terminal = $happn.exchange.terminal) {

    // terminal is present.

    terminal.register('hello', {
    
      // creates a 'hello' command available in the terminal

      description: 'example',

      help: '\n\n\n',

      run: function(args, callback) {

        // if you don't call the callback you dont het the prompt back, ever!
        // (and you'll need to kill the process from the outside)

        callback(null, '\nHello ' + args[0] + '.\n');
      },

      autoComplete(args, callback) {
        var possible = ['world', 
                        'solarsystem',
                        'galaxy',
                        'universe']; // use args to determine next possibilities
        callback(null, possible);
      }

    });

  }

  callback(null);

}
```


#### Some useful $ things available in terminal.

