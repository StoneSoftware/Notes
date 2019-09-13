### 一、自定义事件语法
event = new CustomEvent(typeArg, customEventInit);
【Parameters】 
	typeArg:事件类型,字符串。类型click、submit等。   
	eventInit:可选,传递EventInit类型的字典。这个EventInit类型的字典也就是我们使用InitEvent()时需要传递的参数：   
　　　　bubbles:事件是否支持冒泡，传递一个boolean类型的参数，默认值为false;   
　　　　cancelable:是否可取消事件的默认行为，传递一个boolean类型的参数，默认值为false;   
　　　　composed:事件是否会触发shadow DOM（阴影DOM）根节点之外的事件监听器，传递一个boolean类型的参数，默认值为false。这个参数是InitEvent()中没有的新参数; 
【Return value】  
	A new CustomEvent object of the specified type, with any other properties configured according to the CustomEventInit dictionary (if one was provided).

### 二、自定义事件使用 
   ``` javascript
     //创建事件
	 var event = new CustomEvent("eventName", {bubbles: false, cancelable: false, composed: false, detail: null});
	 //监听事件
	 window.addEventListener('eventName',function(event){
				debugger;
				console.log('id',id) // 会在控制台打印0010
			});
	 //发起事件
	 event.aaa="aaa";
	 window.dispatchEvent(event);
   ``` 
   ``` javascript
	 You can polyfill the CustomEvent() constructor functionality in Internet Explorer 9 
	 and higher with the following code:

(function () {

    if (typeof window.CustomEvent === "function") return false;

    function CustomEvent(event, params) {
        params = params || { bubbles: false, cancelable: false, detail: null };
        var evt = document.createEvent('CustomEvent');
        evt.initCustomEvent(event, params.bubbles, params.cancelable, params.detail);
        return evt;
    }

    window.CustomEvent = CustomEvent;
	})();
	Internet Explorer >= 9 adds a CustomEvent object to the window, but with correct 
	implementations, this is a function.
   ```
		
		
