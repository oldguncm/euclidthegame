Euclid The Game
===============

© Kasper Peulen 2014

Feel free to contribute to this project by fixing bugs/typos etc. or by creating new levels.
To create new levels you will need to understand geogebra a little bit.

If the source code of this project looks like I'm bit of a noob with html/javascript etc. Well then that is absolutely right ! That is why I've put this project on github, I'm not so good with html/javascript at all. If you want to make this project more awesome by cleaning up the html code, making some design, or whatever, feel free to do so !

I have written a couple of function that make it easy to test if objects/lines/circles are drawn:

```javascript
function ggbOnInit() {
  ggbApplet.debug("ggbOnInit");
  ggbApplet.registerAddListener("newObjectListener");
}

function newObjectListener(obj) {
  // this functions can check all general objects
  function checkobject(target, step) {
    if (obj != "finished") {
      var cmd = "finished = (" + obj + "== " + target + ")";
      ggbApplet.debug(cmd);
      ggbApplet.evalCommand(cmd);
      finished = ggbApplet.getValueString("finished");
      if (finished.indexOf("true") > -1) {
        ggbApplet.setVisible(step, true);
      }
    }
  }
  // this functions check line segments
  function checksegment(target, step) {
    if (ggbApplet.getObjectType(obj) == "segment") {
      //gives beginpoint and enpoint of object
      var objectcmd = ggbApplet.getCommandString(obj);
	  var openbracket = objectcmd.indexOf('[') + 1;
	  var comma = objectcmd.indexOf(',');
	  var closebracket = objectcmd.indexOf(']');
	  var beginpointobject = objectcmd.substring(openbracket, comma);
	  var endpointobject = objectcmd.substring(comma + 1, closebracket);
      //gives beginpoint and endpoint of target
      var targetcmd = ggbApplet.getCommandString(target); 
	  var openbracket = targetcmd.indexOf('[') + 1;
	  var comma = targetcmd.indexOf(',');
	  var closebracket = targetcmd.indexOf(']');
	  var beginpointtarget = targetcmd.substring(openbracket, comma);
	  var endpointtarget = targetcmd.substring(comma + 1, closebracket);
      //here it checks if endpoints of line segment are equal
      if (obj != "finished") {
        var cmd = "finished =((("+beginpointobject+"=="+beginpointtarget+")||("+beginpointobject+"=="+endpointtarget+"))&&(("+endpointobject+"=="+beginpointtarget+")||("+endpointobject+"=="+endpointtarget+")))";
        ggbApplet.debug(cmd);
        ggbApplet.evalCommand(cmd);
        finished = ggbApplet.getValueString("finished");
        if (finished.indexOf("true") > -1) {
          ggbApplet.setVisible(step, true);
        }
      }
    }
  }
   // this functions can check if line segment has right direction
  function checksegmentdirection(target, step) {
    if (ggbApplet.getObjectType(obj) == "segment" || ggbApplet.getObjectType(obj) == "line") {
    if (obj != "finished") {
      var cmd = "finished = (("+obj+"(1)=="+target+"(1))&&("+obj+"(-1)=="+target+"(-1)))";
      ggbApplet.debug(cmd);
      ggbApplet.evalCommand(cmd);
      finished = ggbApplet.getValueString("finished");
      if (finished.indexOf("true") > -1) {
        ggbApplet.setVisible(step, true);
      }
    }
  }
  }
  // this functions check if the new point is on the targetline
  function checkpointontarget(target, step) {
    if (ggbApplet.getObjectType(obj) == "point") {
    if (obj != "finished") {
      var cmd = "finished = ("+target+"(x("+obj+"))==y("+obj+"))";
      ggbApplet.debug(cmd);
      ggbApplet.evalCommand(cmd);
      finished = ggbApplet.getValueString("finished");
      if (finished.indexOf("true") > -1) {
        ggbApplet.setVisible(step, true);
      }
    }
  }
  }
  //here you can check all objects 


  //which step are neccesary to complete level
  if (ggbApplet.getVisible("step1") ) {
    ggbApplet.setVisible("complete", true);
	document.getElementById("level").style.visibility="visible";
  }
}
```
