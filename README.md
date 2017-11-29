## RangeSlider

![range.png](http://sandbox.runjs.cn/uploads/rs/234/bxxwrmn8/range.png)





## 开始

- [demo地址](https://htmlpreview.github.io/?https://github.com/zc95/RangeSlider/blob/master/index.html)
- [github地址](https://github.com/zc95/RangeSlider)
- [简易版DEMO](http://jsrun.net/IciKp/show)






## 导入jQuery, CSS和JS

### [https://github.com/zc95/RangeSlider/blob/master/myCSS.css](https://github.com/zc95/RangeSlider/blob/master/myCSS.css)

  ```css
  p {
    font-family: "微软雅黑";
    letter-spacing: -1px;
    text-shadow: -2px -1px 1px #fff, 1px 2px 2px rgba(0, 0, 0, 0.2);
    font-weight: 300;
    font-size: 36px;
    margin: 10px;
  }

  input[type=range] {
  	-webkit-appearance: none;
  	width: 300px;
  	border-radius: 10px; /*这个属性设置使填充进度条时的图形为圆角*/
  	background: -webkit-linear-gradient(#2EB969, #2EB969) no-repeat;/*进度条的颜色*/
  	background-size: 0% 100%;
  }

  input[type=range]:focus {
  	outline: none;
  }
  input[type=range]:hover {
  	cursor:pointer;
  }

  input[type=range]::-webkit-slider-runnable-track {
  	height: 6px;
  	border-radius: 10px; /*将轨道设为圆角的*/
    box-shadow: 0.2px 0.2px 1px 0.8px #cec8c8 inset; /*添加底部阴影*/
  }

  input[type=range]::-webkit-slider-thumb {
  	-webkit-appearance: none;
    cursor: pointer;
    height: 20px;
    width: 20px;
    margin-top:-6px;
    border-radius: 50%;
    background-color:white;
    box-shadow: 0px 0px 3px 1px #DEDEDE;
  }

  ```

  ​

### [https://github.com/zc95/RangeSlider/blob/master/myJS.js](https://github.com/zc95/RangeSlider/blob/master/myJS.js)

  ``` javascript
$.fn.RangeSlider = function(cfg){
 var userAgent = navigator.userAgent;
 var isWebkit = (userAgent.indexOf("AppleWebKit") >= 0);
 var isIE = isIE();
 function isIE() {
  var isIE = false;
  if (window.ActiveXObject || "ActiveXObject" in window) {
    isIE = true;
  } else {
    isIE = (userAgent.indexOf("compatible") > -1 && userAgent.indexOf("MSIE") > -1
    && !(userAgent.indexOf("Opera") > -1));
    isIE = false;
  }
  return isIE;
  }
  this.sliderCfg = {
   min: cfg && !isNaN(parseFloat(cfg.min)) ? Number(cfg.min) : null, 
   max: cfg && !isNaN(parseFloat(cfg.max)) ? Number(cfg.max) : null,
   step: cfg && Number(cfg.step) ? cfg.step : 1,
   callback: cfg && cfg.callback ? cfg.callback : null
  };
  var $input = $(this);
  var min = this.sliderCfg.min;
  var max = this.sliderCfg.max;
  var step = this.sliderCfg.step;
  var callback = this.sliderCfg.callback;
  $input.attr('min', min).attr('max', max).attr('step', step);
  var event = null;
  if (isIE) {
   event = "change";
  } else {
   event = "input";
  }	
  $input.bind(event, function(e){
   $input.attr('value', this.value);		
   if (isWebkit) {
    $input.css( 'background-size', this.value + '% 100%' ); 
   }	
   if ($.isFunction(callback)) {
    callback(this);
   }
 });
};

  ```

  ​







## 使用

```html
<p>
  进度条&emsp;<span id="num">0</span>%
</p>
<input type="range" value="0">
```

```javascript
$(function() {
  $('input').RangeSlider({
    step: 0.1,
    callback: change
  });
});
var change = function($input) {
  /*内容可自行定义*/
  $("#num").text($('input').val());
}
```




