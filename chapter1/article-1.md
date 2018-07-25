# gitBook 使用书名

## 1.添加目录与添加文章

* 点击![](/assets/import.png)按钮，会增加一级文章
* 在文章上右键点击![](/assets/import2.png)会使文章变为一个目录同时，在其中添加文章。

2.对于gitbook不支持嵌入HTML片段（一般需示例效果），可以使用git pages链接，如[示例1](https://fankeke007.github.io/)、[示例2](https://fankeke007.github.io/css_secrets/)

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



