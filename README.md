# kvf-admin
kvf-admin是一套快速开发框架、脚手架、后台管理系统、权限系统，上手简单，拿来即用。为广大开发者去除大部分重复繁锁的代码工作，让开发者拥有更多的时间陪恋人、家人和朋友。
* 后端采用spring boot、mybatis(已集成mybatis-plus增强插件，开发更迅速，可查看官方文档了解更多：[mybatis-plus](https://baomidou.gitee.io/mybatis-plus-doc/#/quick-start))、shiro框架
* 前端采用layui作为UI框架，实现90%的移动端自适应，支持主题更换
* 提供代码生成器([wiki使用文档](https://github.com/kalvinGit/kvf-admin/wiki/kvf%E4%BB%A3%E7%A0%81%E7%94%9F%E6%88%90%E5%99%A8%E4%BD%BF%E7%94%A8%E6%96%87%E6%A1%A3))，只需编写20%左右的代码，剩下全部自动生成；支持一键及批量功能模块生成，并支持一定程度上的自定义配置并生成代码，相对比较灵活

### 项目结构树
````
kvf-admin
│
│ pom.xml maven依赖管理pom文件
│  
├─sql
│      kvf_sys.sql  项目初始化数据表及基础数据sql脚本
│      
└─src
    ├─main
    │  ├─java
    │  │  └─com
    │  │      └─kalvin
    │  │          └─kvf
    │  │              │  KvfAdminApplication.java   项目启动类
    │  │              │  
    │  │              ├─common  通用模块
    │  │              └─modules 功能模块
    │  │                  ├─generator   代码生成器模块
    │  │                  └─sys 系统模块（核心）
    │  └─resources
    │      │  application.yml   spring boot 配置文件
    │      │  ehcache.xml   ehcache缓存配置文件
    │      │  
    │      ├─mapper mybatis mapper文件
    │      ├─static 静态资料
    │      └─templates  模板
    │          │  403.html  403页面
    │          │  home.html 系统首页页面
    │          │  index.html   主页
    │          │  login.html   登录页
    │          │  
    │          ├─common 通用模板
    │          │      base.html
    │          │      sys_tpl.html
    │          │      
    │          ├─generator  生成器模板
    │          │          
    │          └─sys    系统页面模板
    │                  
    └─test  单元测试块

````

### 软件需求
* jdk8+
* mysql5.7+

### 所用技术
#### 前端
* jQuery 
* [layui v2.5.6](https://www.layui.com/doc/) (UI框架)

#### 后端
* spring boot v2.2.4.RELEASE
* Mybatis
* [Mybatis-plus v3.3.0](https://mp.baomidou.com/guide/wrapper.html#abstractwrapper) (mybatis增强插件，无侵入。非常强大的插件，除了联表操作，几乎都可以使用它的sql条件构造器完成)
* Shiro v1.4.0
* Druid v1.1.21
* ehcache
* redis
* [hutool-all v4.5.1](https://hutool.cn/docs/#/) (java通用工具类，此包几乎包括了所有常用的工具方法，你也可以按需引入相应工具模块包)

### 项目特点
* 非常精简且轻量级的权限系统，代码简洁易懂，无论学习还是项目中应用，都是非常简单易上手的项目
* 拥有界面配置化代码生成器，支持一键生成及简单自定义配置生成代码
* 自动过滤输入的非法字符串，防止XSS攻击
* 使用ehcache + redis作为缓存，对需要加入缓存的方法上添加@Cacheable注解即可（你也可以使用redisTemplate添加获取缓存），提升系统运行速度
* 支持日志记录，可在需要加入日志操作记录的controller方法上添加@Log("业务操作备注")即可完成日志记录
* 系统全局统一异常处理，所有异常信息统一处理返回R对象，前端处理提示信息更方便

### 本地部署
* 通过git/gitee下载源码(推荐使用git，因为gitee不是实时更新的)
* 创建数据库：执行sql/kvf_admin.sql脚本创建数据库及表并初始化系统基础数据
* 修改开发环境配置文件application-dev.yml，配置数据库账号和密码
* 开发工具idea或eclipse还需要安装lombok插件，否则会提示找不到实体类的的get/set方法
* 运行KvfAdminApplication.java，启动项目【kvf-admin】
* idea启动访问：http://localhost/【一般idea都会自动去掉项目名】【这里使用80端口】
* eclipse启动访问：http://localhost/kvf-admin【这里使用80端口】
* 账号密码：admin/123456

### 项目演示
* 演示地址：http://kvfadmin.kalvinbg.cn
* 账号密码：test/123456

### 系统效果图展示

![系统效果图](http://cloud.kalvinbg.cn/image/kvf-admin.png)
![系统效果图](http://cloud.kalvinbg.cn/image/kvf-admin1.png)
![系统效果图](http://cloud.kalvinbg.cn/image/kvf-admin2.png)
![系统效果图](http://cloud.kalvinbg.cn/image/kvf-admin3.png)
![系统效果图](http://cloud.kalvinbg.cn/image/kvf-admin4.png)

### 更新日志
#### 2020-04-02
* 集成UEditor
* 自定义日志注释重命名：【旧】@Action() -> 【新】@Log()
* 升级spring boot v2.2.4.RELEASE、mybatis-plus v3.3.0、druid v1.1.21版本
* 升级最新layui版本v2.5.6
* 优化系统功能体验
* 优化代码生成器
* 重置按钮现在支持重置表单及重置table列表数据
* 优化localDateTime序列化问题
* bug修复
#### 2019-08-18
* 新增定时任务管理（可在yml配置是否开启）
* 增加登录验证码开关（可在yml配置，为了方便开发不用输入验证码登录）
* sql脚本更新
* 优化代码生成器
* 修复了若干个bug
#### 2019-08-11
* 新增字典管理
* 优化代码生成器字段类型转换
* 修复代码生成器生成代码包路径不正确bug
* 删除多余依赖包
* 修复了一些其它bug

#### 2019-07-21
* 修复代码生成器生成日期控件没有实例化
* 修复代码生成器生成的查询字段名称没有转成坨峰命名
* 修复代码生成器生成mapperxml时，表达式缺少半边中括号
* 优化部分功能代码
* 新增logback日志配置

### 开发指南
* 前端通用配置js【kconfig.js】
* 前端通用工具js【kcommon.js】
* 前端静态文件引用统一管理配置【base.html】，在需要引用里面的配置的页面上引用即可，如引用通用的css：`<link th:replace="common/base::static"/>`
* 后端自定义日志注解@Log("业务操作说明")[com.kalvin.kvf.common.annotation.Log]，在需要加入日志的controller方法上加这个注解即可
* 代码生成器使用文档[点我](https://github.com/kalvinGit/kvf-admin/wiki/kvf%E4%BB%A3%E7%A0%81%E7%94%9F%E6%88%90%E5%99%A8%E4%BD%BF%E7%94%A8%E6%96%87%E6%A1%A3)
* Spring上下文工具【SpringContextKit.java】，可使用它手动获取指定bean。如`IUserService userService = SpringContextKit.getBean(IUserService.class);`
* 自定义异常处理类【KvfException.java】，可用于业务层【service】抛出业务异常，如：`throw new KvfException("不存在的任务ID");` ，前端可接收到这个提示信息
* 统一接口返回数据封装类【R.java】，可用于控制层【controller】返回成功或失败等数据。如`R.ok(data); 或 R.fail("验证码不正确");`
* 开发环境【dev】默认关闭登录验证码，若需要开启验证码登录可在application-dev.yml配置开启

### 敬请期待
* 日程管理
* 集成activity工作流引擎
* vue-admin版本

### 交流反馈
* github仓库：https://github.com/kalvinGit/kvf-admin
* gitee仓库：https://gitee.com/kalvinmy/kvf-admin
* 作者QQ：1481397688
* 交流群：214768328
* 如需关注项目最新动态，请Watch、Star项目，同时也是对项目最好的支持

