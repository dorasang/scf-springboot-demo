
## 使用 SCF 部署 Spring Boot

### 操作场景
[Spring Boot](https://spring.io/projects/spring-boot) 是由 Pivotal 团队提供的框架，用来简化新 Spring 应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。

本示例将介绍如何使用 SCF 部署 Spring Boot 并通过 API 网关测试事件模拟请求和获取 spring 返回的处理结构。

### 前提条件

请参考[云函数 JAVA 开发指南](https://cloud.tencent.com/document/product/583/12214)准备开发环境和工具。

### 操作步骤

#### 步骤 1：新建本地项目

点击[此处](https://github.com/dorasang/scf-springboot-demo)下载使用 SCF 部署 Spring Boot 的示例代码，`example`目录下是源代码文件，`target`目录下是使用 `maven` 工具编译后生成的 jar 包等文件。

#### 步骤 2：编译

在 scf-springboot-web 目录下执行 `mvn package`开始编译，编译成功后的 jar 包位于项目文件夹内的 target 目录内，即`scf-springboot-web-1.0-SNAPSHOT.jar`。

#### 步骤 3：函数部署

1）打开[云函数控制台](https://console.cloud.tencent.com/scf/index?rid=1)，在左侧列表栏选择【函数服务】，点击【新建】创建函数；

2）函数名称：scf-springboot-demo，运行环境：Java 8，创建方式：空白函数，如下图所示，点击【下一步】；
![](https://main.qcloudimg.com/raw/b4b10d4387599a94acc2d07d4ffcd52a.png)

3）在函数配置页面，执行方法填为：example.MyHandler::handleRequest，提交方法选择：本地上传zip包，将步骤 2 中获得的`scf-springboot-web-1.0-SNAPSHOT.jar`上传至控制台。spring 初次启动较慢，建议将【高级配置】中的【执行超时时间】设为 25s，避免因函数超时导致测试失败。点击【完成】即完成函数创建和部署；
![](https://main.qcloudimg.com/raw/e0aa9441247d0490e1b8f5b0abd92c0b.png)

#### 步骤 4：函数测试

函数创建完成后会跳转至【函数配置】页，点击【函数代码】，【测试事件】选择“Api Gateway事件模版”，path改为`/hello`，点击【测试】，即可在返回结果和执行日志中查看函数调用结果。
![](https://main.qcloudimg.com/raw/c52902104ab4fdad5b7baadd9ee5a05d.png)

#### 步骤 5：完成

测试成功会返回：
`{statusCode: 200,headers: {Content-Type=text/html;charset=UTF-8, Content-Length=35, Date=Thu, 15 Oct 2020 13:29:34 GMT},body: hello,this is a springboot demo！~}`
 
