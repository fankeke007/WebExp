```js
/*simpleTouch.js
**2018-06-13
**参照SwipTouch.js v=1.0 实现:http://plugins.jquery.com/project/touchSwipe
**/
;(function(){
    var LEFT = 'left';
        var RIGHT = 'right';
        var UP = 'up';
        var DOWN = 'down';
        var NONE = 'none';



        var PHASE_START = 'start';
        var PHASE_MOVE = 'move';
        var PHASE_END = 'end';
        var PHASE_CANCEL = 'cancel';

    function TouchSwipe(options){

        var defaults = {
            debug : false,
            fingers : 1,
            threshold : 75,
            swipe : function(event,direction){if(defaults.debug) console.log('swiped' + direction)},
            swipeLeft : function(event) {},
            swipeRight : function(event) {},
            swipeUp : function(event) {},
            swipeDown : function(event) {},

            triggerOnTouchend : true,
            swipeStatus : null
        };



        this.phase = 'start';
        this.options = _extend(defaults,options);
        this.start = {x:0,y:0};
        this.end = {x:0,y:0};
        this.delta = {x:0,y:0};
        this.fingerCount = 0;
        this.distance = null;

        this.init();
    }

    TouchSwipe.prototype = {

        touchStart : function(event){

            event.preventDefault();

            this.phase = PHASE_START;
            this.fingerCount = event.touches.length;

            if(this.fingerCount == this.options.fingers){
                this.start = {x:event.touches[0].pageX,y:event.touches[0].pageY};
                this.options.swipeStatus&&this.triggerHander(event,this.phase);
            }else{
                this.touchCancel(event);
            }

        },

        touchMove : function(event){

            if(this.phase == PHASE_END || this.phase == PHASE_CANCEL){
                return;
            }
            event.preventDefault();

            this.phase = PHASE_MOVE;
            this.fingerCount = event.touches.length;

            if(this.fingerCount == this.options.fingers){

                this.end = {x:event.touches[0].pageX,y:event.touches[0].pageY};

                if(this.options.swipeStatus){
                    this.distance = this.calculateDistance();
                    this.direction = this.calculateDirection();
                    this.triggerHander(event,this.phase,this.direction,this.distance);
                }

                if(!this.options.triggerOnTouchend){
                    if(!this.distance){
                        this.distance = this.calculateDistance();
                    }
                    if(distance >= defaults.threshold){
                        this.phase = PHASE_END;
                        this.direction = this.calculateDirection();
                        this.triggerHander(event,this.phase,this.direction,this.distance);
                        this.touchCancel();
                    }
                }
            }else{
                this.phase = PHASE_CANCEL;
                this.triggerHandler(event, this.phase);
                this.touchCancel(event);
            }

        },

        touchEnd : function(event){

            event.preventDefault();

            if(this.options.triggerOnTouchend){
                this.phase = PHASE_END;
                if(this.fingerCount = this.options.fingers && this.end.x != 0){

                    this.distance = this.calculateDistance();

                    if(this.distance >= this.options.threshold){
                        this.direction = this.calculateDirection();
                        this.triggerHandler(event, this.phase, this.direction, this.distance);
                        this.touchCancel(event);
                    }else{
                        this.phase = PHASE_CANCEL;
                        this.triggerHandler(event, this.phase, this.direction, this.distance);
                        this.touchCancel(event);
                    }
                }else{
                    this.phase = PHASE_CANCEL;
                    this.triggerHandler(event, this.phase);
                    this.touchCancel(event);
                }
            }else if(this.phase==PHASE_MOVE){
                this.phase = PHASE_CANCEL;
                this.triggerHandler(event, this.phase);
                this.touchCancel(event);
            }

        },

        touchCancel : function(event){
            //reset default value
            this.fingerCount = 0;
            this.start = {x:0,y:0};
            this.end = {x:0,y:0};
            this.delta = {x:0,y:0};
        },

        calculateDistance : function(){
            return Math.round(Math.sqrt(Math.pow(this.end.x - this.start.x,2) + Math.pow(this.end.y - this.start.y,2)));
        },

        calculateAngle : function(){
            var X = this.start.x-this.end.x;
            var Y = this.end.y-this.start.y;
            var Z = Math.round(Math.sqrt(Math.pow(X,2)+Math.pow(Y,2))); //the distance - rounded - in pixels
            var r = Math.atan2(Y,X); //angle in radians (Cartesian system)
            var angle=0;

            angle = Math.round(r*180/Math.PI); //angle in degrees

            if ( angle < 0 )
                angle =  360 - Math.abs(angle);

            return angle;
        },

        calculateDirection : function(){
            var angle = this.calculateAngle();

            if ( (angle <= 45) && (angle >= 0) )
                return LEFT;

            else if ( (angle <= 360) && (angle >= 315) )
                return LEFT;

            else if ( (angle >= 135) && (angle <= 225) )
                return RIGHT;

            else if ( (angle > 45) && (angle < 135) )
                return DOWN;

            else
                return UP;
        },

        triggerHandler : function(event,phase,direction,distance){
            if (this.phase == PHASE_END)
            {
                switch(this.direction)
                {
                    case LEFT :
                        this.options.swipeLeft(event);
                        break;

                    case RIGHT :
                        this.options.swipeRight(event);
                        break;

                    case UP :
                        this.options.swipeUp(event);
                        break;

                    case DOWN :
                        this.options.swipeDown(event);
                        break;
                }

                //trigger catch all event handler
                this.options.swipe(event, direction);
            }

            if (this.options.swipeStatus)
                this.options.swipeStatus(event, this.phase, direction || null, distance || 0);
        },

        init : function(){
            this.options.el.addEventListener("touchstart", this.touchStart.bind(this), false);
            this.options.el.addEventListener("touchmove", this.touchMove.bind(this), false);
            this.options.el.addEventListener("touchend", this.touchEnd.bind(this), false);
            this.options.el.addEventListener("touchcancel", this.touchCancel.bind(this), false);
            // var self = this; //self 版实现代码量会更大
            // this.options.el.addEventListener("touchstart", function(event){self.touchStart.call(self,event)}, false);
            // this.options.el.addEventListener("touchmove", function(event){self.touchMove.call(self,event)}, false);
            // this.options.el.addEventListener("touchend", function(event){self.touchEnd.call(self,event)}, false);
            // this.options.el.addEventListener("touchcancel", function(event){self.touchCancel.call(self,event)}, false);
        }
    }
    window.TouchSwipe = TouchSwipe;
})();

function _extend(target,source,deep){
    for(var i in source){
        if(deep){
            if(_type(source[i])==='object'){
                _extend(target[i],source[i])
            }else if(_type(source[i])==='array'){
                target[i] = Array.prototype.slice.call(source[i]);
            }else{
                target[i] = source[i];
            }
        }else{
            target[i] = source[i];
        }
    }
    return target;
}

function _type(param){
    return Object.prototype.toString.call(param).slice(8,-1).toLowerCase();
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=0,minimum-scale=1.0,maximum-scale=1.0">
    <title>Touch Event Learning</title>
    <title>参照1.0 实现版本</title>
    <style>

        *{
            box-sizing:border-box;
            padding:0;
            margin:0;
        }
        html,body{
            width:100%;
            height:100%;
        }
        #test01{
            display: flex;
            width: 100%;
            height: 100%;
            background: lightblue;
            align-items: center;
            justify-content: center;
        }
        #test02{
            display: flex;
            width: 100%;
            height: 100%;
            background: lightgreen;
            align-items: center;
            justify-content: center;
        }
    </style>
</head>
<body>
    <div id="test01">
        <span>tset01</span>
    </div>
    <div id="test02">
        <span>test02</span>
    </div>
    <select name="" id="">
        <option value="">请选择</option>
        <option value="0">000</option>
        <option value="1">001</option>
        <option value="2" selected >002</option>
    </select>
    <script src="simpleTouch.js"></script>
    <script>
        const { log, table } = console;
        const { abs } = Math;
        const getEle = (el) => document.querySelector(el);
        let test01 = getEle('#test01');
        let test02 = getEle('#test02');
        var touch1 = new TouchSwipe({
            el:test01,
            swipe             : function(event, direction ){},
            swipeLeft        : function(event)    {log('LEFT')},
            swipeRight        : function(event)    {log('RIGHT')},
            swipeUp            : function(event)    {log('UP')},
            swipeDown        : function(event)    {log('DOWN')}
        });
        var touch2 = new TouchSwipe({
            el:test02,
            swipe             : function(event, direction ){},
            swipeLeft        : function(event)    {log('LEFT')},
            swipeRight        : function(event)    {log('RIGHT')},
            swipeUp            : function(event)    {log('UP')},
            swipeDown        : function(event)    {log('DOWN')}
        });

        let select=document.querySelector('select');
        select.addEventListener('blur', function(){log(1)}, false);
        select.addEventListener('blur', function(){log(2)}, false);
        select.addEventListener('focus',function(){log(3)}, false);


        //
        //
        //
        //
    </script>
</body>
</html>
```



