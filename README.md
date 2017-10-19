[官方文档](http://site.alibaba.net/ae-wsmobile/fastvalidator-document/)
![test.jpg](http://ata2-img.cn-hangzhou.img-pub.aliyun-inc.com/221293287a54e26303642fbed38aea87.jpg)

-----------

* 详情请参考[wiki](http://site.alibaba.net/ae-wsmobile/fastvalidator-document/index.html)
* **fastvalidator 钉钉群: fastvalidator答疑(群号:11738108)**

-------------

注: 已经使用的BU: ICBU, AE, 集团, 菜鸟, 1688, 阿里妈妈, 天猫, 蚂蚁, 阿里云

## 基本介绍
fastvalidator是一个高性能, 功能丰富, 简单易用验证框架.


## 问题场景

* 你是否为了编写枯燥的验证代码而感到厌烦, 如下图:

```
if (StringUtil.isBlank(name) || !NAME_PATTERN.matcher(name).matches()) {
  return new Response("name_is_illegal","name is illegal");
}

if (StringUtil.isBlank(password) || password.trim().length() < 6) {
  return new Response("password_illegal","password is illegal");
}

if (!password.equals(repassword)){
  return new Response("password_not_equal_repasword","password not equal repassword");
}
```


***用了fastvalidator, 编码就是这样的:***

```java
@ValidateBean
public class Account {

    @NotBlank
    @Pattern(regexp = "^\\s*\\w+(?:\\.{0,1}[\\w-]+)*@[a-zA-Z0-9]+(?:[-.][a-zA-Z0-9]+)*\\.[a-zA-Z]+\\s*$")
    private String            name;
    
    @NotBlank
    @Size(min=6) 
    private String            password;

    @If(sourceCode = "ObjectUtils.equals(bean.password, bean.repassword)", 
    message = "password not equal repassword|password_not_equal_repasword")
    private String            repassword;
}
```

* 你是否经常和服务提供方沟通确认服务接口参数的规则，业务的校验逻辑, 失败时的返回值(返回码还是异常)的含义等等.

* 如果你已经用了验证框架, 你是否担心大量的反射而导致性能下降。[案例: 大量反射引起的惨案](http://www.atatech.org/articles/70280?flag_data_from=headline)

* 验证失败时设置错误码和message真麻烦

* 已有的声明约束太少，无法满足日常开发

* 复杂的业务逻辑无法使用声明, 应用方每次都来确认

* ......

## 价值
提升效率: 开发效率，运行时效率，沟通效率.

## 功能特性
* 拥有60+的常用约束(兼容hibernate-validator已有约束) [代码示例](http://www.atatech.org/articles/68843#combination))
* 支持集合验证 [代码示例](http://www.atatech.org/articles/68843#collection)
* 高性能: 原生调用. 
* 编译期验证约束正确性 [代码示例](http://www.atatech.org/articles/68843#compile_error)
* 支持预热, 提升第一次验证性能 [代码示例](http://www.atatech.org/articles/70089#warmup)
* 指定约束验证的顺序 [代码示例](http://www.atatech.org/articles/68843#sort)
* 方法参数验证失败时, 可自动设置方法返回值的code,message; 或者抛出异常 [代码示例](http://www.atatech.org/articles/68843#code)
* fastvalidator spring boot starter  [代码示例](http://www.atatech.org/articles/70089#springboot)
* 约束可以任意组合[代码示例](http://www.atatech.org/articles/68843#in)
* 支持声明(约束) 中编写复杂业务逻辑的验证[代码示例](https://www.atatech.org/articles/68843#conditional)
* 支持元数据验证[代码示例](http://www.atatech.org/articles/73346)
* 分组验证(分场景验证)[代码示例](https://www.atatech.org/articles/68843#group)

***注: 经我们初步估算, 使用fastvaldator后, 开发工作量一般都能节约20%左右, 如果是基础业务团队，那么节省的沟通成本很可能会超出原有开发成本***



## [核心原理](http://site.alibaba.net/ae-wsmobile/fastvalidator-document/intr/principle.html)

## [性能对比](http://site.alibaba.net/ae-wsmobile/fastvalidator-document/intr/performance.html)

## [约束介绍](http://site.alibaba.net/ae-wsmobile/fastvalidator-document/intr/constraints.html)

## [技术架构](http://site.alibaba.net/ae-wsmobile/fastvalidator-document/intr/architecture.html)



## 参考
* [fastvalidator](/README.md)
* [hibernate-validator](http://hibernate.org/validator/)
* [apache-bval](http://bval.apache.org/)
* [bean validation](http://beanvalidation.org/)
* [jsr 269](https://www.jcp.org/en/jsr/detail?id=269)
* [jsr 349](https://jcp.org/en/jsr/detail?id=349)
