# Problem: CSS module className not reflecting in build js file

NODE version: 15.14.0
use `@snowpack/plugin-webpack` to bundle 

## How to reproduce 
1. download the repo
2. `yarn && yarn start` to see it's just "Hello World" in yellow text color with black background 
where black background color is global css, and yellow text is in `App.module.css` 
3. `yarn build` to build, notice in `/build/css/styles[hash].css` both black and yellow properties is here
4. use a server application to open the `/build/` as root, the yellow h1 is now showing
5. check the `/js/index[hash].js` file, as below, the jsx is converted into this, though the `u` is correctly creating a random classname, but the `createElement` is not 
```
function (e, t, r) {
  "use strict";
  r.r(t);
  var n = r(0),
    o = (n.c.useEffect, n.c.useState, r(1)),
    u = { _yellowText_1crdi_1: "Fo01xQr36oH9LiM0VHSA7" }; <--------------- CHANGED
  var c = function () {
    return n.c.createElement(
      "h1",
      { className: u.yellowText },    <--------------- UNCHANGED
      "Hello World"
    );
  };
  o.a.render(
    n.c.createElement(n.c.StrictMode, null, n.c.createElement(c, null)),
    document.getElementById("root")
  );
},
```
