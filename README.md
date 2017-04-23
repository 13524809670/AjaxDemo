# ajaxdemo
������д�Ŀ���������֪ʶ��ѵ���ϡ���Ҫ���ݷ�Ϊ���¼���

> * ���������
> * ʲô�ǿ�����ʰ�ȫ����
> * ����������������
> * ����ļ���˼·
> * �������δ���������
> * h5
> * �ܽ�

# ���������
1. ʹ��springboot���̨���񣬱�дget����
```Java
@RestController
public class TestController {
	@GetMapping("/get1")
	public ResultBean<String> get1() {
		System.out.println("\n-------TestController.get1()\n");
		return new ResultBean<String>("get1 ok");
	}
}
```
2. ����host����a.com��b.com��ָ�򱾵�
![host����](/pictures/hosts.png)

3. ��д����ҳ�棬ʹ��jq����get��ajax���������ַ��ʹ��b.com�ľ��Ե�ַ
```JavaScript
function get1() {
	$.get("http://b.com:8080/get1", function(data) {
		console.log("get1 Loaded: ", data);
	});
}
```

4. ����a.com,���get��ajax���󣬷����������
![](/pictures/get1.png)
`ע�⣡���ص㣡��̨��get������ִ�гɹ��˵ģ�`
![](/pictures/get1result.png)

5. ��д�޲���post����post1
```Java
@PostMapping("/post1")
public ResultBean<String> post1() {
	System.out.println("\n--------TestController.post1()\n");
	return new ResultBean<String>("post1 ok");
}
```

6. ��дǰ̨���ô���
```JavaScript
function post1() {
	$.ajax({
		type : "POST",
		url : "http://b.com:8080/post1",
		dataType : "json",
		success : function(data) {
			console.log("jsonp Loaded: ", data);
		}
	});
}
```

7. ִ��post1��ǰ̨��������󣬺�̨ͬ��ִ�гɹ���
![](/pictures/post1.png)
![](/pictures/post1-2.png)

8. ��д������post����post2��������ʽΪform-urlencoded��ʽ������a=1&b=2���֣�
```Java
@PostMapping("/post2")
public ResultBean<String> post2(Param param) {
	System.out.println("\n--------TestController.post2, param=" + param);
	return new ResultBean<String>("post2 ok, param=" + param);
}
```

9. ��дǰ̨���ô���
```JavaScript
function post2() {
	var data = {
		key1 : '��form-urlencoded��ʽ���Ͳ���',
		id1 : 12345
	}

	$.ajax({
		type : "POST",
		data : data,
		url : "http://b.com:8080/post2",
		dataType : "json",
		success : function(data) {
			console.log("jsonp Loaded: ", data);
		}
	});
}

```

10. ִ��post2��ǰ̨��������󣬺�̨ͬ��ִ�гɹ���
![](/pictures/post2-1.png)
![](/pictures/post2-2.png)

11. ��д������post����post3��������ʽΪjson��ʽ
```Java
@PostMapping("/post3")
public ResultBean<String> post3(@RequestBody Param param) {
	System.out.println("\n--------TestController.post3, param=" + param);
	return new ResultBean<String>("post3 ok, param=" + param);
}
```

12. ��дǰ̨���ô���
```JavaScript
function post3() {
	var data = {
		key1 : '��json��ʽ����',
		id1 : 12345
	}

	$.ajax({
		type : "POST",
		contentType : "application/json",
		data : JSON.stringify(data),
		url : "http://b.com:8080/post3",
		dataType : "json",
		success : function(data) {
			console.log("jsonp Loaded: ", data);
		}
	});
}
```

10. ִ��post3��ǰ̨���������`��̨û��ִ��post3����`��
![](/pictures/post3.png)
���Կ���post2��post������ҷ�������200�����Ƿ������Ѿ���ȷִ���ˡ�
��post3��options������ص���403����������û��ִ�����
ԭ�����������


5. ���Խ���

# ʲô�ǿ�����ʰ�ȫ����
���ճ����ϵ������ˣ����ҵ������˵��������������ڰ�ȫ���ǣ����첽�����������url��ʱ�򣬻��жϷ������Ƿ�����������������ͻ��׳��������

# ����������������

1. ������������Ϸ���������
��ʵ���������������£����á����ܡ��а�ȫ���⣬���Բ����������������������û��������⣬������java�����е��κ��򶼲����ܱ�������⡣

2.������ajax�첽����
ֱ�ӷ��ʿ϶��ǲ������ġ�
![](/pictures/get2.png)

3. ����
����Э�飬�������˿��κ�һ����ͬ�������

> �ص㣺������첽������������ĸ��������û�п�����첽����ĸ��

# ����ļ���˼·
������������3�������������ж�Ӧ�Ľ��������

## ����������ָ����������������죬����顣
��chromeΪ�������Ӳ���--disable-web-security --user-data-dir=C:\MyChromeDevUserData ����chrome���ɽ��������ʵ�����岻�󣬲�������ʾ���������Ȥ�����Լ����Լ��ɡ�

## ����첽����ʹ��jsonp���첽��ͬ��
`jsonp`�ǱȽ��Ϲŵķ�ʽ�ˣ����ںܶ���ϵͳ���ܿ�����jsonp��ʵ�Ͳ�����һ��script��ǩ����ͬ�������ش��롣��������ԭ���ķ���json���ݣ���ɷ����˵��ú����ġ�js�ű����������ִ�У������������jsonp�����callback����������������Ҫǰ̨������̨�ġ�

����������һ�£���дjson���ô��롣��Ҫ���� `dataType: "jsonp"`
```JavaScript
function getByJsonp(){
	$.ajax({
		  type: "GET",
		  url: "http://b.com:8080/get1",
		  dataType: "jsonp",
		  success: function(data){
			  console.log("jsonp Loaded: " , data);
		  }
		});
}
```

�ֱ�ִ��ԭ����ajax�������д��jsonp ���󣬿��Կ���ԭ����get���������XHR `XMLHttpRequest��д`�첽�����ϣ���jsonp����û�г�����XHR�ϣ�ֻ�����������ϣ����Կ���jsonp��ͬ�������󡣣���������⣬XMLHttpRequestҲ�ܷ���ͬ�����󡣣���ͼ�п��Կ�����jsonp�����ʱ��jq���Զ�����call������
![](/pictures/jsonp1.png)

![](/pictures/jsonp2.png)

���������û��֧��jsonp�����ص���Ȼ��json��ʽ��������ᱨ����json����jsִ���ˣ���
![](/pictures/jsonp3.png)

���������Ҫ֧��jsonp��springboot�¿���������������
```Java
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.servlet.mvc.method.annotation.AbstractJsonpResponseBodyAdvice;

@ControllerAdvice
public class JsonpAdvice extends AbstractJsonpResponseBodyAdvice {
	public JsonpAdvice() {
		super("callback");
	}
}
```
���Ӻ���Զ��ж��Ƿ���jsonp�������json�ͷ��ض�Ӧ��js��

�ٴε��ã��Ѿ�����ȷ��ȡ���ݴ�ӡ����ˡ�
![](/pictures/jsonp4.png)

��Ҫ��������������jsonp�Ĺ���ԭ��Ҳ��Ҫ�Լ�����ʵ��jsonp��������ܶ�֧��jsonp�����ã�ֱ��ʹ�ü��ɡ�

### jsonp�����Եļ���Ӳ��

- �첽���ͬ����
- ����json��ɷ���js�ˣ����Է�������Ҫ�Ķ�֧�ֵģ����ǵ��÷�һ����Ը˵�þ����õġ�
- �����Ƕ�̬��Ƕscript��ǩ����ô�϶��ǲ�֧��post������

���ԣ�jsonpʹ��Խ��Խ�٣����Ƽ���

## ��Կ�����2�ֽ������

## ����������֧�ֿ�����Ϣ
��������������ڰ�ȫ���ǲ����ƿ�����ʣ���ô���ǿ����ڷ������з�������������Ϣ���������֪���������������֧�ֿ�������Ϳ�������ִ�С�
��򵥵ķ�ʽ������@CrossOriginע�⣬��ע����Լ�������Ҳ���Լ��ڷ����ϡ�Ĭ������������������

```Java
@CrossOrigin
@RestController
public class TestController 
```

�ٴε������е�����ȫ���ɹ����������Ѿ�����֧�ֿ����ˡ�
![](/pictures/crossorigin-1.png)
![](/pictures/crossorigin-2.png)

����post3�����Կ����ȷ�����һ��options������ѯ�Ƿ���Կ��򣬷���������Ӧͷ���������������Կ������post3���������ִ�С�����post3����2�������¼��
![](/pictures/crossorigin-2.png)


## ʹ�÷��������
��Ȼ����������������������а�ȫ���⣬��ô����ֻ��Ҫ�����������Ķ�������Լ������Ķ���������Ϳ��Խ��������ʹ�÷����������Ǳ����������������濴������ͬһ��ϵͳ��������Ȼ���õ��Ŀ������⡣
��nginx����Ϊ�������÷ǳ��򵥣��������£�
```
 server {
        listen       80;
        server_name  a.com;

	location / {
	    proxy_pass http://a.com:8080/;
        }

        location /bcom/ {
	    proxy_pass http://b.com:8080/;
        }
}
```
��ʾ /bcom��ͷ������ת���� http://b.com:8080/

Ȼ�����ǰ�����ҳ�����һ��nginx.html������������ַ�ɾ��Ե�ַ `http://b.com:8080/xxx` �ĳ���Ե�ַ `/bcom/xxx`��
���²��ԣ�ȫ���ɹ���
![](/pictures/nginx.png)

���Կ������������� http://a.com/bcom/ ��ͷ�ġ�

# �������δ���������

