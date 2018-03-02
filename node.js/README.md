# Node.js Control

Once the server module is loaded onto the ABB robot controller, and started (in automatic mode, ABB Menu Button > Production Window, "PP to Main", press physical start button) any computer on the network can very simply interact with the robot via the Node.js Robot object. 

The Node.js package can be found in this repo's `/node.js`. The package uses only core libraries, no need to install any dependencies.

### Safety
Before moving the robot, you may want to turn the speed down to a low percentage of set speed, do this by clicking the menu button on the lower right of the teach pendant, 25% (or lower)

Keep clear of the robot when the program is running. 

### Lets wave this thing around!

Before setting up anything, you may want to check [this video walkthough](https://www.youtube.com/watch?v=KQEwssUqV9o) as well as a [live demo on a physical controller](https://github.com/garciadelcastillo/open-abb-driver). 

Make sure you have correctly set up your robot or virtual controller in RobotStudio (see main `README.md`), and the `SERVER.mod` module is running. 

Also, make sure you have a recent version of Node.js, like `8.9.x`; the abb module is written in `ES6`.

Go to `/node.js` and start a Node.js REPL:

```
$ node
```

Import the `abb` module and instantiate a new `Robot` object:

``` javascript
> const abb = require('./abb');
> let r = new abb.Robot('127.0.0.1');  // if using a virtual controller
```

You should see a message with connection confirmation. You are ready to start moving the robot around:

``` javascript
> r.setJoints([0,0,0,0,90,0]);  // move joints to a home position
> r.setCartesian([[300, 300, 500], [0, 0, 1, 0]]);  // move linearly to X=300, Y=300, Z=500 and pointing down
```

And it moves! That command will move it to X=300mm, Y=300mm, Z=500mm. The next four numbers represent [quaternion orientation](http://en.wikipedia.org/wiki/Quaternions_and_spatial_rotation), the important thing to remember being that q = [0,0,1,0] points the tool down and q = [1,0,0,0] points the tool up. 

Other commands include joint moves (where you specify the angles of joints 1-6 in degrees)

And many others. Check the `abb.js` for a list of possible actions. 

If you are interested in real-time robotics, you should check this project: [https://github.com/garciadelcastillo/Machina](https://github.com/garciadelcastillo/Machina)

### Reference
Node.js module for abb-communication by [@garciadelcastillo](https://github.com/garciadelcastillo).

Forked from [https://github.com/Humhu/open-abb-driver](https://github.com/Humhu/open-abb-driver).

This doc is adapted from [https://github.com/robotics/open_abb/wiki/Python-Control](https://github.com/robotics/open_abb/wiki/Python-Control).