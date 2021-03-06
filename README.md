# karma-nodewebkit-launcher

> Launcher for node-webkit. 

---

This is a small but experimental launcher, based on the [Safari Launcher](https://github.com/karma-runner/karma-safari-launcher) by Vojta Jina and contributors, and not affiliated with any official or semi-official Karma plugins.

---


## Installation

The easiest way is to keep `karma-nodewebkit-launcher` as a devDependency in your `package.json`.


    {
      "devDependencies": {
        "karma": "~0.10",
        "karma-nodewebkit-launcher": "~0.0.6"
      }
    }


You can do it on the command line by:

    npm install karma-nodewebkit-launcher --save-dev

## Configuration

    // karma.conf.js
    module.exports = function(config) {
      config.set({
        browsers: ['NodeWebkit']
      });
    };


You can pass list of browsers as a CLI argument too:

    karma start --browsers NodeWebkit

## Locally-installed Node modules

If you're using locally-installed Node modules via `require` in your code, in order for the testing environment to find them, you'll have to explicitly set `NODE_PATH` to the path to the local `node_modules` directory in your project.

    export NODE_PATH=/full/path/to/node_modules
    
## Custom node-webkit manifest

The default node-webkit [`package.json`](https://github.com/rogerwang/node-webkit/wiki/Manifest-format) that is used in the launcher is

    {
      "name": "karma-runner",
      "main": "index.html",
      "node-remote": "<local>"
    }
    
You can overwrite and add to these defaults by creating a custom configuration in `karma.conf.js`. For example, to run your tests in kiosk mode

    browsers: ['NodeWebkitKiosk'],

    customLaunchers: {
      'NodeWebkitKiosk': {
        base: 'NodeWebkit',
        options: {
          window: {
            'kiosk': true
          }
        }
      }
    }

The `options` in the above example are merged with the defaults, so the resulting `package.json` used in node-webkit is

    {
      "name": "karma-runner",
      "main": "index.html",
      "node-remote": "<local>",
      "window": {
        "kiosk": true
      }
    }



