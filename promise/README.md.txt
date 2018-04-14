Promise ����ִ��ajax�첽δ�ܼ������ݵ��³�����Ⱦ����ԭ����ֻ��ͬ��ajaxִ�У�����Promise ���Ч��
> The Promise object is used for asynchronous computations. A Promise represents a single asynchronous operation that hasn't completed yet, but is expected in the future.
���ģ�Promise���������첽����������ʾһ����δ�����Ԥ����δ����ɵ��첽������

https://segmentfault.com/a/1190000007032448

a().then(b()).then(c()); // ֻ����a�ɹ�ִ����֮�󣬲�ִ��b����b�ɹ�ִ����֮����ִ��C(˭������ִ��˭~)

### ʹ�÷���
```js
// ��ȡ������Ⱦ
var Obtain ={
	Id:'609' // ID
};
// Promise ����ִ��ajax�첽δ�ܼ������ݵ��³�����Ⱦ����
// ԭ����ֻ��ͬ��ajaxִ�У�����Promise ���Ч��
function sendRequest() {
    return new Promise(function (resolve, reject) {
        $.ajax({
        	url:'xxxxx',
        	data:Obtain,
	        type:"get",
            success:function(res){
            	if(res.status == 200) {
					// ���ִ�е�then������ֵ
					resolve(res);
            	}
            	else{
            		// ʧ��ʱ���catch������ֵ
            		reject(res.desc)
            	}
                
            },
            error:function(){
            	layer.msg("��ȡ����ʧ��");
            }
        })
    })
}

sendRequest()
.then(function(res) {
    // ��ajax�ĳɹ�ʱ��Ĳ���
	console.log('��һ��then�����',res)
	// ͨ��return��������һ��then�Ĵ�ֵ����
	return '�ڶ���then�����';
})
.then(function(res) { 
    // ������һ����return���
    console.log(res)
})
.catch(function(error){
    //�첽����ʧ�ܺ�Ļص�
    layer.msg(error);
});
```

```js
// ͼƬ����
// ��ͼƬ�ļ���дһ��promise��һ��������ɣ�promise��״̬�ͷ����仯
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
		// ���ִ��
	}
)
.catch(
	function(error){
	    //ʧ��ִ��
	}
)
```