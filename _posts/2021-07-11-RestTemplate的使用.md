---
layout: post
title: "RestTemplate的使用"
date: 2021-07-11 22:30:00 +0800
categories: Java
---



> 在以往的工作中，请求都是在系统内部，很少接触与第三方系统之间发请求。最近项目有对接第三方系统的需求，后端向第三方发请求。实操的时候发现系统有封装好的发http请求的方法，所以之前遇到的都是直接调用了。
>
> 最近遇到的是发送文件，之前封装的方法已经不适合了。所以自己就去了解了一下，发现主流推荐都是用apache的httpclient，很少有说用Spring的RestTemplate。如果只是使用的话，感觉RestTemplate是更省事的，也要少写很多的代码。
>
> 在此，做个记录。



## 工作中的使用

### 引用的包

```java
import com.alibaba.fastjson.JSONObject;
import org.springframework.core.io.FileSystemResource;
import org.springframework.http.HttpEntity;
import org.springframework.http.HttpHeaders;
import org.springframework.util.LinkedMultiValueMap;
import org.springframework.util.MultiValueMap;
import org.springframework.web.client.RestTemplate;
```

### 方法

```java
/**
 * 上传文件方法
 *
 * @param url              地址
 * @param appKey           appKey
 * @param sourceType       文件类型
 * @param verificationSign 验签
 * @param file             文件
 * @param fileExt          文件后缀名
 * @return
 */
static String doComFile(String url, String appKey, String sourceType, String verificationSign, File file, String fileExt) {

    FileSystemResource fileSystemResource = new FileSystemResource(file.getPath());

    MultiValueMap<String, Object> form = new LinkedMultiValueMap<>();
    form.add("appKey", appKey);
    form.add("sourceType", sourceType);
    form.add("verificationSign", verificationSign);
    form.add("file", fileSystemResource);
    form.add("fileExt", fileExt);

    HttpHeaders headers = new HttpHeaders();
    HttpEntity<MultiValueMap<String, Object>> files = new HttpEntity<>(form, headers);

    RestTemplate restTemplate = new RestTemplate();
    return restTemplate.postForObject(url, files, JSONObject.class).toString();
}
```



## 参考



[RestTemplate 最详解](https://zhuanlan.zhihu.com/p/258121569)

[RestTemplate使用](https://www.jianshu.com/p/78f2390793a2)

[RestTemplate 深度解析](https://my.oschina.net/lifany/blog/688889)

[Spring RestTemplate详解](https://blog.csdn.net/congzi0424/article/details/51518819)

[RestTemplate使用](https://www.jianshu.com/p/78f2390793a2)

[SpringBoot配置RestTemplate的代理和超时时间](https://www.cnblogs.com/yangzhilong/p/6640207.html)

[postforobject 设置代理_Spring RestTemplate和代理身份验证](https://blog.csdn.net/weixin_39548606/article/details/111799946)