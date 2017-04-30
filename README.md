# ajaxdemo
������д�Ŀ���������֪ʶ��ѵ���ϡ���Ҫ���ݷ�Ϊ���¼���

> * ���������
> * ʲô�ǿ�����ʰ�ȫ����
> * ����������������
> * ����ļ���˼·
> * ��cookie�Ŀ�������
> * ���Զ���header�Ŀ�������
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

> ע�⣡���ص㣡��̨��get������ִ�гɹ��˵ģ���Ȼǰ̨���������

![](/pictures/get1-2.png)

��������200��

![](/pictures/get1result.png)

��̨��������ִ�С�

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
			console.log("post1 Loaded: ", data);
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
			console.log("post2 Loaded: ", data);
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
			console.log("post3 Loaded: ", data);
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

�ֱ�ִ��ԭ����ajax�������д��jsonp ���󣬿��Կ���ԭ����get���������XHR `XMLHttpRequest��д`�첽�����ϣ���jsonp����û�г�����XHR�ϣ�ֻ�����������ϣ����Կ���`jsonp��ͬ������`������������⣬��ʵXMLHttpRequestҲ�ܷ���ͬ�����󡣣�

��ͼ�п��Կ�����jsonp�����ʱ��jq���Զ�����call������

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

> ��Ҫ��������������jsonp�Ĺ���ԭ��Ҳ��Ҫ�Լ�����ʵ��jsonp��������ܶ�֧��jsonp�����ã�ֱ��ʹ�ü��ɡ�

### jsonp�����Եļ���Ӳ��

- �첽���ͬ����
- ����json��ɷ���js�ˣ����Է�������Ҫ�Ķ�֧�ֵģ����ǵ��÷�һ����Ը˵�þ����õġ�
- �����Ƕ�̬��Ƕscript��ǩ����ô�϶��ǲ�֧��post������

���ԣ�jsonpʹ��Խ��Խ�٣����Ƽ���

## ��Կ�����2�ֽ������

### ����������֧�ֿ�����Ϣ
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

����post3�����Կ����ȷ�����һ��`OPTIONS��ѯ����` ���Ƿ���Կ��򣬷���������Ӧͷ���������������Կ���Ȼ��post3���������ִ�С�

����post3����2�������¼��

![](/pictures/crossorigin-3.png)

`OPTIONS��ѯ����` ������ÿ�ζ��ᷢ�ͣ���һ�β�ѯ�ķ��ص�ͷ������һ�� `Access-Control-Max-Age:1800`���Ǳ�ʾ��Ч�ڣ����ʱ��β����ٴη��� `OPTIONS��ѯ����` �ˡ� 

### ʹ�÷��������

��Ȼ����������������������а�ȫ���⣬��ô����ֻ��Ҫ�����������Ķ�������Լ������Ķ���������Ϳ��Խ����

����ʹ�÷����������Ǳ����������������濴������ͬһ��ϵͳ��������Ȼ���õ��Ŀ������⡣

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

# ��cookie�Ŀ�������
Ĭ�Ͽ����ǲ���cookie�ġ�

�����Ǻܶ�ʱ����Ҫ����cookie����Ự�ȣ��������������XMLHttpRequest�����ʱ����Ҫ����withCredentialsΪtrue��Ȼ���������Ҫ�޸�֧��cookie���ã���Ҫ����Access-Control-Allow-Credentials:true��Access-Control-Allow-Origin:��Ӧ��������`�˴�������*�������Ǿ��������`��

��дjs����

```JavaScript
function getWithCookie() {
	$.ajax({
		type : "GET",
		url : "http://b.com:8080/getWithCookie",
		xhrFields : {
			withCredentials : true
		},
		success : function(data) {
			console.log("getWithCookie Loaded: ", data);
		}
	})
}
```

��дjava���룬��̨ʹ��spring��@CookieValueע���ȡcookieֵ��

```Java
@GetMapping("/getWithCookie")
public ResultBean<String> getWithCookie(@CookieValue(required=false) String cookie1) {
	System.out.println("\n-------TestController.getWithCookie(), cookie1="+cookie1);
	return new ResultBean<String>("getWithCookie ok, cookie1="+cookie1);
}
```

Ȼ����b.com����Ӷ�Ӧ��cookie��ʹ�ù��߻���document.cookie�����ӣ�����a.com�Ϸ���getWithCookie����b.com���ɹ���

![](/pictures/cookie1.png)

������͵���������û�ж�Ӧ��cookie���ᱨ��

```
{"timestamp":1493552031929,"status":400,"error":"Bad Request","exception":"org.springframework.web.bind.ServletRequestBindingException","message":"Missing cookie 'cookie1' for method parameter of type String","path":"/getWithCookie"}
```

���������� `@CookieValue(required=false)` ����

# ���Զ���header�Ŀ�������

�ܶ�ʱ��������Ҫ�����Զ���ͷ��header�����ʱ��������Ҫ�ڷ����������ܷ�����Щͷ����ʹ�� `@RequestHeader` �õ�ͷ�ֶΡ�

```Java
@GetMapping("/getWithHeader")
@CrossOrigin(allowedHeaders = { "X-Custom-Header1", "X-Custom-Header2", "X-Custom-Header4" })
public ResultBean<String> getWithHeader(
		@RequestHeader(required = false, name = "X-Custom-Header1") String header1) {
	System.out.println("\n-------TestController.getWithHeader(), header1=" + header1);
	return new ResultBean<String>("getWithHeader ok, header1=" + header1);
}
```

> ע�⣬`@CrossOrigin(allowedHeaders = { "X-Custom-Header1", "X-Custom-Header2", "X-Custom-Header4" })`��Ҫ�����ڷ����ϣ���Ҫ����������� `@CrossOrigin` ע���ϣ�����ᵼ��һЩ���⡣

��дjs���룬JQ���������Զ���ͷ��2�ַ�����`headers` �� `beforeSend�¼�` �ӡ� 

```JavaScript
function getWithHeader() {
	$.ajax({
		type : "GET",
		url : "http://b.com:8080/getWithHeader",
		headers : {
			"X-Custom-Header1" : "can not include zhongwen1111"
		},
		beforeSend : function(xhr) {
			xhr.setRequestHeader("X-Custom-Header2", "can not include zhongwen2222");
			xhr.setRequestHeader("X-Custom-Header3", "can not include zhongwen3333");
		},
		success : function(data) {
			console.log("getWithHeader Loaded: ", data);
		},
		error:function(data) {
			console.log("getWithHeader error: ", data);
		},
	})
}

```

> **ע��1��һ��ʼ�� jquery.1.6.1 ���������ô�������Ͳ��ɹ������滻�� 1.11.3 �汾�ɹ��ˡ�**
> ע��2��header�����ֵ����ֱ�ӷ����ģ����ı����Լ����롣
> ע��3���Զ���ͷ��ʹ�� `X-` ��ͷ�����ɺ�ϰ�ߡ�

��������ǰ���ȷ��� `OPTIONS��ѯ����` �����������Ƿ���������Щ�Զ���ͷ��

![](/pictures/head1.png)

> ���������ͷ������˴����е��Զ���ͷ�б�ʹ��Spring`@CrossOrigin` ע��֧�ֿ����ʱ�򣬷��������ط�����֧�ֵ�ͷ���������ͷ�Ľ�������������û�и���������֧�ֵ�ͷ��

Options����᷵��200���ɹ�������������������б������**�Լ��ж�**��һ�����ͻᱨ��

```
XMLHttpRequest cannot load http://b.com:8080/getWithHeader. Request header field X-Custom-Header3 is not allowed by Access-Control-Allow-Headers in preflight response.
```
![](/pictures/head2.png)

�����޸�����js���룬ȥ��������û�����õ� `X-Custom-Header3` �� ���²��ԣ�ȡֵ�ɹ���

![](/pictures/head3.png)

![](/pictures/head4.png)

# �ܽ�

���Ź��������дϸһ�㣬���ֶ������ǱȽ϶�ģ���������д4��СʱӦ�þ���д���ˣ������ĩ���˿�2���д�꣬����ܽ�һ�£��Թ������õ��ϵ�֪ʶ�㡣

* ����������ʵ�����������������ˣ������첽��
* ����첽�Ľ������jsonp�кܶ�Ӳ�ˣ������Ƽ���
* ��������Ϳ�������֮ǰ�����ּ������Ǹ������󣬼�������ֱ���������������жϣ������֧�ֿ��򣬾��ܷ������ɹ�ִ�з���200������������Ǳ���������������ȷ��� `OPTIONS��ѯ����`�������֧�ֿ��򣬷���403��ֹ���ʴ���֧�ַ���200��������һ���ʹ���������ܷ���ȥ��ĳЩ�������������Ҫ�����жϣ���
* �����������Ƚϳ����ĸ���ǿ����Ƿ���json���ݵģ����Զ���ͷ�ġ�����cookie�Ĳ��Ǹ�������
* ʹ��Spring�� `@CrossOrigin` �ܷܺ���Ľ������������⣬����ֻ��Ҫһ�д��롣
* ʹ�÷������ıȽϺõĽ����������˾�ڲ�����Ҳ�Ƚϼ򵥡�
* ѧ��ע�� `@RequestHeader` �� `@CookieValue` ��ʹ�ã���Ҫ�Լ�ȥrequest�����ϻ�ȡ��Щ��Ϣ��


