Promise 避免执行ajax异步未能加载数据导致出现渲染错误，原方法只能同步ajax执行，可用Promise 提高效率
> The Promise object is used for asynchronous computations. A Promise represents a single asynchronous operation that hasn't completed yet, but is expected in the future.
译文：Promise对象用于异步操作，它表示一个尚未完成且预计在未来完成的异步操作。

https://segmentfault.com/a/1190000007032448

a().then(b()).then(c()); // 只有在a成功执行了之后，才执行b，在b成功执行了之后再执行C(谁先请求执行谁~)

### 使用方法
```js
// 获取数据渲染
var Obtain ={
	Id:'609' // ID
};
// Promise 避免执行ajax异步未能加载数据导致出现渲染错误
// 原方法只能同步ajax执行，可用Promise 提高效率
function sendRequest() {
    return new Promise(function (resolve, reject) {
        $.ajax({
        	url:'xxxxx',
        	data:Obtain,
	        type:"get",
            success:function(res){
            	if(res.status == 200) {
					// 完成执行的then操作传值
					resolve(res);
            	}
            	else{
            		// 失败时候的catch操作传值
            		reject(res.desc)
            	}
                
            },
            error:function(){
            	layer.msg("获取数据失败");
            }
        })
    })
}

sendRequest()
.then(function(res) {
    // 对ajax的成功时候的操作
	console.log('第一个then的输出',res)
	// 通过return来进行下一个then的传值操作
	return '第二个then的输出';
})
.then(function(res) { 
    // 根据上一个的return输出
    console.log(res)
})
.catch(function(error){
    //异步操作失败后的回调
    layer.msg(error);
});
```

```js
// 图片加载
// 将图片的加载写一个promise，一旦加载完成，promise的状态就发生变化
const preloadImage = function(path) {
	return new Promise(function (resolve, reject) {
        var image = new Image();
        image.onload 	= resole;
        image.onerror 	= reject;
        img.src 		= path;	 
    })
}

preloadImage
.then(
	function(res){
		// 完成执行
	}
)
.catch(
	function(error){
	    //失败执行
	}
)
```