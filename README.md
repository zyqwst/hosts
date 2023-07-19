### 文档更新日志
| 版本 | **更新时间** | **更新内容** |
| --- | --- | --- |
| V1.0.0 | 2020-11-9 | 增加 **调试任务** 功能 |
| V1.0.1 | 2020-11-16 | 1.增加应用的复制功能；
2.增加应用删除功能；
3.优化连接池处理，节省服务器开销； |
| V1.0.2 | 2020-11-22 | 增加SQL语句和SQL构建器查询任务的分页功能 |
| V1.0.3 | 2020-11-25 | 1.增加自定义接口响应格式的功能；
2.优化【后台管理-基础设置】界面排版； |
| V1.0.4 | 2020-12-3 | 1.后台管理增加用户密码重置功能；
2.增加登录用户密码修改功能； |
| V1.2.0 | 2021-06-03 | 1.修复分页查询时SQL结果没有转换驼峰命名的bug;
2.增加接口参数【一键复制】功能；
3.增加接口搜索功能；
4.优化部分操作体验； |
| V2.0 | 2021-10-22 | 【**重大变更**】
升级http服务 |
| V2.1.0 | 2021-12-22 | 1.增加仪表盘页面
2.get请求字符串数字做宽容处理 |
| V2.1.1 | 2022-01-04 | 升级接口响应参数设置，可以从json数据逆向生成json-schema |
| V2.2 | 2022-03-29 | 增加接口签名模块，应用管理里可开启接口访问验签开关 |
| V3.1.0 | 2022-05-25 | 增加定义全局变量的功能 |
| V3.2.0 | 2022-06-23 | 增加达梦数据库支持，支持数据库：mysql、oracle、postgre、达梦8； |
| V3.4.0 | 2022-09-14 | SQL增加占位符功能，类似mybatis的$符 |
| V4.0 |  | 增加接口结果缓存选项，开启后，接口如调用失败，会返回最近一次缓存的结果
ALTER TABLE `tb_api` 
ADD COLUMN `cached` tinyint(1) NOT NULL DEFAULT 0 COMMENT '是否缓存结果 1-是' ; |
| V4.0.1 | 2022-09-28 |  修复应用复制时已删除接口被复制报错的问题 |
| V4.2.0 |  | 1.修复和优化已知问题；
2.升级jdk版本到jdk11，升级ECMAScript引擎为graalvm；
3.添加接口跨域配置
ALTER TABLE `tb_app` 
ADD COLUMN `cross_origin` tinyint(1) UNSIGNED ZEROFILL NOT NULL DEFAULT 0 COMMENT '是否允许跨域1-是'
ALTER TABLE `tb_app` 
ADD COLUMN `allow_origin` varchar(255) NULL COMMENT '允许跨域的域名' AFTER `cross_origin`;
4.增加应用的导出和导入功能
5.第三方接口请求去掉ssl/tls校验（https://ip也能正常访问）
6.后台管理登录密码错误多次后需输入验证码；
7.增加接口token检查功能
ALTER TABLE `controller-plus`.`tb_api` 
ADD COLUMN `check_token` tinyint(1) NOT NULL DEFAULT 0 COMMENT '是否需要校验token' AFTER `cached`; |

	

API+  `发音：[eɪ pi aɪ] [plʌs]`  是一款快速、灵活的低代码接口创建平台
### 特性
支持原生SQL、SQL构建器 [(参照MyBatis文档SQL语句构建器)  ](https://mybatis.org/mybatis-3/zh/statement-builders.html)、静态数据、第三方接口调用 ;

- 支持接口参数校验[(参照笔者造的轮子)](http://json-schema-editor.sviip.com)
- 支持接口多个任务创建、编排，上级任务执行结果可作为下级任务的输入参数，任务可以根据条件动态执行；
- 支持接口文档生成；
- 支持ECMAScript 5语法；

### 架构
平台架构设计简约，无微服务、无复杂中间件，支持集群部署；
![API+架构图.jpeg](https://cdn.nlark.com/yuque/0/2021/jpeg/627161/1637811926414-5c1d368c-f4d7-446b-852b-3fe47b8249fd.jpeg#averageHue=%23c9f8c9&clientId=u89e07f7e-b308-4&errorMessage=unknown%20error&from=paste&height=365&id=u9603e10f&originHeight=730&originWidth=1293&originalType=binary&ratio=1&rotation=0&showTitle=false&size=52725&status=error&style=none&taskId=u995f9c69-20e5-47c8-a920-5294f81ed37&title=&width=646.5)

**下面开始一个最佳实践。**
### 平台访问地址

- API+后台访问地址：**私密**
- 接口创建成功后访问地址：**私密**
#### 接口访问说明
接口访问URL格式：http://111.111.111.111:8088/应用名称/接口名称，例如：
```javascript
http://111.111.111.112:8088/my-app/list-by-id?id=123
```
### 用户体系
管理员创建用户，也可以授予用户管理员角色。用户是接下来创建项目的基础，只有用户能创建项目，并且能把其他用户添加到本项目组
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601361506994-e2ab4bf3-8089-4702-8555-6eb82e7a319b.png#averageHue=%232d3930&height=470&id=ztWRO&originHeight=940&originWidth=1915&originalType=binary&ratio=1&rotation=0&showTitle=false&size=89441&status=done&style=none&title=&width=957.5)
### 创建一个应用
项目负责人创建应用，输入应用基础信息、项目组成员、数据源信息。

点击“创建应用”开始创建，输入项目的基本信息，上传logo。
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601349147065-e0f6ba29-e47e-46f3-ab4f-1bd3241004e1.png#averageHue=%2383888a&height=833&id=nDTmA&originHeight=1666&originWidth=3358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=486050&status=done&style=none&title=&width=1679)

为项目组添加项目成员，项目成员在后续的工作中创建接口
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601350390041-d103e0b1-42ad-4ee8-9cc2-2fe6b9a37f7f.png#averageHue=%237b8082&height=833&id=iQiSB&originHeight=1666&originWidth=3354&originalType=binary&ratio=1&rotation=0&showTitle=false&size=570432&status=done&style=none&title=&width=1677)

为项目添加数据源，为后续创建接口做前期的准备
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601350521130-3d994591-12e6-4de4-8305-c751a2a57e15.png#averageHue=%23303325&height=832&id=GrcyL&originHeight=1664&originWidth=3358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=334475&status=done&style=none&title=&width=1679)

#### 应用设置
![image.png](https://cdn.nlark.com/yuque/0/2022/png/627161/1648542510610-edefc7fa-1e53-47c9-9765-c24f6c17ca9b.png#averageHue=%23fcfcfc&clientId=u72555461-d9ae-4&errorMessage=unknown%20error&from=paste&height=633&id=u5ce0e54f&originHeight=633&originWidth=1150&originalType=binary&ratio=1&rotation=0&showTitle=false&size=135277&status=error&style=none&taskId=uceb78155-4f23-4f4e-9e03-580923f7bfe&title=&width=1150)
#### 接口签名（V2.2+支持）
在【应用设置】打开接口签名后，接口访问需要增加签名信息。规则如下：
```json
1.生成签名
sign = MD5(appKey + appSecret + timestamp)

2.请求接口时把appKey,timestamp,sign加入到请求Header里。

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/627161/1648542755234-39376dbc-18bb-40da-a4de-e3009ae60fb1.png#averageHue=%23f6f6f6&clientId=u72555461-d9ae-4&errorMessage=unknown%20error&from=paste&height=1076&id=ufb05ce90&originHeight=1076&originWidth=1552&originalType=binary&ratio=1&rotation=0&showTitle=false&size=281585&status=error&style=none&taskId=uc8bd3209-eabe-4681-bbbb-0b14cec57b0&title=&width=1552)
#### 接口Token(V4.2.0+)

![image.png](https://cdn.nlark.com/yuque/0/2023/png/627161/1688373490065-72de7083-50a8-4802-81a0-b8007515d277.png#averageHue=%23fdfdfc&clientId=u179bd98f-9ba8-4&from=paste&height=465&id=u7aa87303&originHeight=930&originWidth=2246&originalType=binary&ratio=2&rotation=0&showTitle=false&size=302104&status=done&style=none&taskId=ub1e106d4-f599-4c2a-a08a-4622d17b4b0&title=&width=1123)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/627161/1688373535768-9098fc71-d23c-4830-b18a-b7b3afb03518.png#averageHue=%23ededec&clientId=u179bd98f-9ba8-4&from=paste&height=616&id=u1a9dc14f&originHeight=1232&originWidth=1118&originalType=binary&ratio=2&rotation=0&showTitle=false&size=316242&status=done&style=none&taskId=u3caad550-0ed1-497a-afbe-ec2a4bd1377&title=&width=559)
在【应用设置】-【接口Token】可以设置当前应用的登录和Token校验业务；点击【新增Token配置】后弹窗设置认证token业务；

| 字段 | 说明 | 默认值 |
| --- | --- | --- |
| 认证接口 | 选择创建好的接口设置为认证接口，保存并提交。之后访问该接口将返回AccessToken字符串 | 无 |
| Token有效期 | 用户认证登录后生成的AccessToken有效期 | 1小时 |
| 调用接口自动延长有效期 | 选中后用户调用其他接口则自动刷新有效期 | 是 |
| 同一用户登录后其他登录设备Token强制下线 | A账号登录后，将强制踢掉A账户其他登录设备 | 否 |
| Token名称 | 其他接口请求携带Token的http-header名称 | AccessToken |
| 用户信息接口 | 通过AccessToken换取用户信息的接口 |  |
| 登出接口 | 退出登录的接口，退出后删除Token |  |

具体调用方式如下：

1. 登录接口
```shell
curl 'http://localhost:8888/{应用名}/{login}?{username=用户名}&{password=密码}'

# 花括号里内容根据实际接口情况修改
```

2. 请求接口时在http header增加参数
```shell
AccessToken=99_7d4a302aba3a418abe77152620477daa
```

3. 获取用户信息
```shell
curl --location 'http://localhost:8888/应用/getUserInfo' \
--header 'AccessToken: 99_7d4a302aba3a418abe77152620477daa'
```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/627161/1688378991140-91a6e037-c47a-4d26-8f60-a3c8fbf3dbf6.png#averageHue=%23f7f7f6&clientId=u179bd98f-9ba8-4&from=paste&height=674&id=u1160360f&originHeight=1348&originWidth=1462&originalType=binary&ratio=2&rotation=0&showTitle=false&size=453786&status=done&style=none&taskId=u9da84e85-536a-4701-b4d0-57ed13e8b22&title=&width=731)

4. 登出
```shell
curl --location 'http://localhost:8888/应用/logout' \
--header 'AccessToken: 99_7d4a302aba3a418abe77152620477daa'
```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/627161/1688379060531-816497e2-8626-45d4-93d8-ed22bdb3e7f9.png#averageHue=%23f6f6f5&clientId=u179bd98f-9ba8-4&from=paste&height=633&id=uca537239&originHeight=1266&originWidth=1458&originalType=binary&ratio=2&rotation=0&showTitle=false&size=451053&status=done&style=none&taskId=u2684749b-f388-469e-b9a2-0382f107eba&title=&width=729)

### 创建一个接口
到了这里，开始步入正题了。首先为了更清晰的组织各个接口，先创建接口分组  `接口分组类似于JavaWeb程序里的controller` ，  创建一个分组【分组一】。
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601350778956-ec504466-dfb5-427c-952b-dbad12bd5c0d.png#averageHue=%23cfd5da&height=841&id=oX460&originHeight=1682&originWidth=3358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=650150&status=done&style=none&title=&width=1679)
在分组一下创建一个接口 `/liangshan` ，选择分组和数据源
![image.png](https://cdn.nlark.com/yuque/0/2023/png/627161/1681376838546-f2d589d2-4be7-42cb-9fd3-dcbf049c111d.png#averageHue=%23b0b0b0&clientId=uf3b5cab2-e178-4&from=paste&height=627&id=ue34b37a6&originHeight=627&originWidth=979&originalType=binary&ratio=1&rotation=0&showTitle=false&size=58206&status=done&style=none&taskId=ufc56f07a-f858-45d0-83ec-52ea4575c9b&title=&width=979)
#### 接口开启缓存(V4.2.0+)
正如上图所示,创建接口时打开【开启缓存】功能，在后续接口调用出错时，将返回最近一次正确的接口结果。如之前接口未调用成果过，则返回调用失败。临时要跳过缓存获取实时结果时可在http请求header添加参数:
`disable-api-cache=true` 


接口创建成功后，点击接口右侧的“详情”按钮，进入到接口详情页面，如下图所示：
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601351214237-4e9948cc-abfd-4a0f-98a0-ce605405a9f3.png#averageHue=%23d6854b&height=835&id=xVq1M&originHeight=1670&originWidth=3354&originalType=binary&ratio=1&rotation=0&showTitle=false&size=335778&status=done&style=none&title=&width=1677)
> 强烈建议规范应用英文名、接口路径命名。须统一用小写字母，多个单词用-连接。

### 
### 接口参数设置
首先设置接口的请求参数，参数可以设置是否必填，可以设置是日期、时间、email等格式。后续发起接口请求时会对接口参数进行验证。当然也可以不设置任何参数，直接点击“保存参数”按钮。

### 接口任务列表
接口的任务支持**原生SQL、SQL语句构建器、静态数据、第三方接口**四种方式。

#### 原生SQL任务
首先创建第一个任务，如下图所示创建了一个原生SQL任务；

1. **任务结果变量名称：**指任务执行结束后如何接收任务执行的结果集，这里将结果赋值给变量list；
2. **结果集类型：**任务返回的结果类型（Array或Object）；
3. **SQL类型：**可以选择查询、更新、插入、删除；如果选择更新、插入和删除三种类型时，接口将自动增加事务管理（需要确保底层数据支持）；
4. **SQL语句：**SQL语句支持NamedParameter参数占位符，动态传入SQL参数，可[参照Spring官网](https://docs.spring.io/spring-framework/docs/5.2.8.RELEASE/spring-framework-reference/data-access.html#jdbc-NamedParameterJdbcTemplate); 如果想直接替换可以使用`${p}`占位符的处理方式，与mybatis的$符号类似**【注意SQL注入问题】**。

```sql
select * from T_ACTOR where first_name = :firstName;
select * from T_ACTOR where first_name in (:forstNameList);
select * from T_ACTOR where createTime between :start and :end;
select * from ${tableName} where createTime between :start and :end;
```
然后点击“创建任务”按钮，保存该任务；
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601351721364-418f8e3e-f049-4a05-95be-f267971921ff.png#averageHue=%237a7d65&height=829&id=An3Yv&originHeight=1658&originWidth=3358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=324262&status=done&style=none&title=&width=1679)

### 生成接口文档
对于原生SQL的方式，支持接口文档一键生成，如下图，点击“生成接口文档”按钮，自动生成下面的接口字段描述内容，最后点击“保存参数”按钮，经过以上三个步骤，该接口已经创建完成并且自动发布。
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601352636031-813fb5bb-e913-43d2-8508-b389eec0f9d2.png#averageHue=%23d1d7db&height=935&id=P5vmZ&originHeight=1870&originWidth=3358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1214044&status=done&style=none&title=&width=1679)
> 有时候**生成接口文档**因为数据库限制或者第三方API创建接口，无法自动生成接口文档，此时可以从接口返回的json数据逆向生成接口文档

![image.png](https://cdn.nlark.com/yuque/0/2022/png/627161/1641261664634-7b3b1acb-266c-4845-95db-75f5fcdb934f.png#averageHue=%23fdfcfb&clientId=uf1da42c2-6a81-4&errorMessage=unknown%20error&from=paste&height=422&id=uef59dcbc&originHeight=843&originWidth=1702&originalType=binary&ratio=1&rotation=0&showTitle=false&size=305175&status=error&style=none&taskId=ub66bbfe2-7137-431f-a613-35cc1061ae9&title=&width=851)
接下来可以在应用页面查看打开项目文档，点击“查看文档”，浏览器打开该应用的接口文档
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601361106363-8b2e8641-8d6e-4332-9bdb-ec1afccacbf0.png#averageHue=%23e7ebec&height=470&id=E4ATc&originHeight=939&originWidth=1916&originalType=binary&ratio=1&rotation=0&showTitle=false&size=69329&status=done&style=none&title=&width=958)
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601361163914-be24db8f-d8b1-4f86-9b9f-59e83ed6cca5.png#averageHue=%23fcfbfb&height=471&id=Zf3JI&originHeight=942&originWidth=1917&originalType=binary&ratio=1&rotation=0&showTitle=false&size=95729&status=done&style=none&title=&width=958.5)
### 其他任务类型
前面介绍了如何创建一个原生SQL任务，如果接口内部逻辑比较复杂，可以考虑创建多个任务，并且对任务进行编排。
#### 创建静态数据任务
有一些常量型的数据，后期可能会变化，那么可以考虑静态数据任务
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601358392219-dca9120e-2a36-4087-921a-699b6bff5caa.png#averageHue=%23788965&height=831&id=OSW0M&originHeight=1662&originWidth=3358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=313593&status=done&style=none&title=&width=1679)
#### 创建SQL构建器任务
当需要根据参数值动态创建SQL，那么SQL语句构建器可以帮助你。

1. **SQL片段拼接条件：**只有条件满足的时候才会拼接该段SQL，这里是一段JavaScript表达式，返回值是布尔类型；

![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601358528322-73ad1813-d9ae-4e52-a75d-3b4525e9e783.png#averageHue=%237b7c65&height=835&id=wi3XB&originHeight=1670&originWidth=3356&originalType=binary&ratio=1&rotation=0&showTitle=false&size=351505&status=done&style=none&title=&width=1678)
#### 创建第三方接口任务
有时候接口里不仅对数据库操作，还会调用第三方的接口，那么可以创建一个第三方接口任务。

> 第三方接口调用支持 `${p}` 占位符，在URL、params、headers、body里都支持输入占位符，占位符参数值从上下文动态获取。可以作为占位符参数的有：接口入参、上级任务的结果、上级任务创建的变量。

![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601358875214-bfc56028-527b-4408-a949-6730eda23b65.png#averageHue=%237b7c65&height=832&id=Awtdm&originHeight=1664&originWidth=3358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=327412&status=done&style=none&title=&width=1679)
### 多级任务
这是API+区别于其他接口工具的核心功能，在创建一个接口时，支持顺序的添加多个任务，而且任务执行的结果可以作为下级任务的参数，极大的增强了接口内部逻辑的灵活性。比如说有以下场景：
> 需求：通过指标代码查询该指标的数据返回。
> 思路：指标代码查询到指标元数据，从而拿到该指标的业务数据表；再查询业务数据，一并返回；

![image.png](https://cdn.nlark.com/yuque/0/2022/png/627161/1663138825365-5a226a76-4de1-4359-9c57-25f9eb8f5075.png#averageHue=%23f7f7f3&clientId=u59c440a1-3a5b-4&errorMessage=unknown%20error&from=paste&height=593&id=udd0ac864&originHeight=1186&originWidth=3444&originalType=binary&ratio=1&rotation=0&showTitle=false&size=620614&status=error&style=none&taskId=u067b7628-ff75-4636-9ba1-62b57e5b5cc&title=&width=1722)
上图中`meta`是任务1执行后的结果，在任务2中，可以使用把`meta`作为参数使用。
### 创建高级任务
如果需要对任务执行后的结果集进行进一步的加工，该怎么办？don't worry，API+有能力协助你进行这项复杂的工作。
例如，我需要对SQL任务查询到的数组统计其条数size，并且一起返回给接口。

1. **高级任务切换按钮**：点击后切换为高级任务编辑模式；高级任务增加了 **前置条件、后置处理、任务返回值** 三个编辑框；
2. **前置条件：**支持JavaScript语句，返回值是布尔类型，不填为true，只有为true时该任务才会被执行；
3. **后置处理：**支持JavaScript语句，可定义变量，变量可以一起返回给接口；
4. **任务返回值：**选择该任务需要返回的结果，包括任务变量名和后置处理增加的变量。在基础模式下无需此操作，默认返回任务变量名；

![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1601359744634-b2c827d6-1572-44a7-b8eb-6172d9bc19e9.png#averageHue=%23738664&height=540&id=iBWu6&originHeight=1079&originWidth=1919&originalType=binary&ratio=1&rotation=0&showTitle=false&size=140886&status=done&style=none&title=&width=959.5)

### 调试任务
在任务编辑窗口点击 **去调试** 按钮打开任务调试界面
![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1604896197248-0c686701-6f32-4e82-8ba8-7ba945a02226.png#averageHue=%237e8370&height=832&id=Zgdl6&originHeight=1664&originWidth=3358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=359864&status=done&style=none&title=&width=1679)
打开任务调试抽屉

- 输入任务所需要的参数（json格式），点击 **调试** 按钮开始调试任务，如果运行失败，则提示任务调试失败，具体原因可查看下方的任务执行日志
- 对于下图第4点，因为会随时调整任务定义信息，调整后需要刷新下任务定义信息到调试区域，继续调试任务。

![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1604896361985-9c9f8d9f-06d6-4588-a0e7-d2a04c56b8e2.png#averageHue=%23bbbaba&height=1049&id=woKx6&originHeight=2098&originWidth=3358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=539076&status=done&style=none&title=&width=1679)
### 分页功能
SQL分页是必不可少的功能，分页功能使用方法

1. 构建方式选择 **原生SQL** / **SQL构建器** ，SQL类型选择 **SELECT** 后自动激活分页插件；
2. 选择 **添加分页** ，输入 **每页条数** 和 **当前页码** 
3. **当前页码** ：因为当前查询的页码需要动态传入，所以可以设置一个变量，变量值从参数中获取；例如：pageNum。 **每页条数** ：一般而言每页条数是10、20等常量，当然也支持变量的方式，例如：pageSize。

![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1606036934629-ef97ae65-8065-45d8-b41f-3768cb74f8dd.png#averageHue=%237c806b&height=828&id=ms2Xr&originHeight=1656&originWidth=3356&originalType=binary&ratio=1&rotation=0&showTitle=false&size=344203&status=done&style=none&title=&width=1678)
下面是一次分页查询返回的结果
```javascript
{
  "total": 31,	// 总条数
  "list": [	// 本页数据
    {
      "id": 68,
      "name": "b",
      "xxxx": "b"
    }
  ],
  "pageNum": 4, //当前页码
  "pageSize": 10, //每页条数
  "size": 1, // 当前页查询到的记录数
  "startRow": 30, // 当前查询的起始行号(不包含)
  "endRow": 40, // 当前查询的终止行号
  "pages": 4, // 总页数
  "hasPreviousPage": true, //是否有上一页
  "hasNextPage": false, // 是否有下一页
  "firstPage": false, //是否第一页
  "lastPage": true //是否最后一页
}
```
### 自定义接口响应数据格式
对于一般的接口访问，API+ 提供了默认的接口封装格式，如下所示：
```javascript
{
  code: "${code}", // 请求状态，200表示正常
  msg: "${msg}", // 如果code<>200，则显示错误信息
  result: "${result}" // 具体数据
}
```
对于需要自定义接口响应格式的用户，可以在【应用设置】-【基础设置】-【接口格式】里添加自定义格式。设置接口执行成功和接口执行失败的接口响应格式。可以设置占位符，占位符在运行时系统动态替换成业务数据，内置的占位符有如下三个：

| **占位符** | **说明** |
| --- | --- |
| **${code}** | 表示接口返回的状态，一般返回200(接口调用成功),500(接口执行失败),401(接口没有正确的授权) |
| **${result}** | 表示接口返回的实际数据，当code不等于200时，值为null |
| **${msg}** | 表示接口调用提示信息，当code不等于200时，值为接口调用失败的原因 |

![image.png](https://cdn.nlark.com/yuque/0/2020/png/627161/1606313676746-132763d5-cfcd-4e89-b365-ddb43af958fb.png#averageHue=%23de9b6a&height=918&id=JSmNI&originHeight=1836&originWidth=3336&originalType=binary&ratio=1&rotation=0&showTitle=false&size=516423&status=done&style=none&title=&width=1668)

### 高级技能

1. 在调用第三方接口时，一般都需要鉴权加签；在API+可以创建一个任务，生成签名，然后把签名只传递给下一个任务；比如有一个第三方接口，调用时需要把参数、时间戳、appkey等字段值用$符号隔开，并MD5生成签名。

![image.png](https://cdn.nlark.com/yuque/0/2021/png/627161/1634839306343-ed149859-008c-4ffc-91a6-84a603e3ad92.png#averageHue=%23c0bfbf&clientId=ud5820d67-313e-4&errorMessage=unknown%20error&from=paste&height=933&id=u55e404b5&originHeight=1866&originWidth=3578&originalType=binary&ratio=1&rotation=0&showTitle=false&size=466348&status=error&style=none&taskId=u36b12706-a799-4939-a330-cb3a2eef3c3&title=&width=1789)

### 一些非填不可的坑、一些小惊喜

1. **（坑）**在后置处理器中，如果变量是数组，那么要通过Arrays.asList(object[] arr)进行一次转换，否则数组会变成对象;**（3.3.0+版本已修复）**
```javascript
var array = [1,2,3];
array = Arrays.asList(array);
```

2. 为JavaScript语法提供了[Lodash](https://www.html.cn/doc/lodash/)、[Crypto-js(3.3.0)](https://github.com/brix/crypto-js)、[moment.js(2.29.1)](http://momentjs.cn/)加持。比如你可以在后置处理器中对数组进行分组；
```javascript
// 按照动物和植物分组
var arr = [{'type':1,'value':'犀牛'},{'type':2,'value':'橘子'},{'type':1,'value':'河马'}];
var groupList = _.groupBy(arr,'type');

// 一个很复杂的加密案例
var accessKey = 'eca09229a0ce43fa9e362542bd4dc9ab';
var secretKey = 'f37652ac46c244149bb9676f18690f89';
var projectKey = '6f899a5eff1248acbb200a541c18629c';
var t = Date.now()+'';

var contentMD5 = 'sfzhm=230281199004284219';
contentMD5 = CryptoJS.MD5(contentMD5);
contentMD5= contentMD5.toString(CryptoJS.enc.Base64);
var stringToSign = 'POST' + '\n' + contentMD5 + '\n' + 'application/x-www-form-urlencoded' + 
                   '\n' + t + '\n' + '/gateway/api/001003001029/certificate/Ib08k8lz2bx6R396.htm';
var signature = CryptoJS.HmacSHA1(stringToSign,secretKey);
signature = signature.toString(CryptoJS.enc.Base64);
var authorization = accessKey + ':' + signature;




//日期格式化
var x = moment().format('YYYY-MM-DD HH:mm:ss')
```

3. 在API+编写JS代码，为了规避undefined的问题，建议携带作用域this；例如：判断变量p1是否存在，如果存在必须大于0
```javascript
this.p1 && this.p1>0
```
### 下一步规划 (删除线的功能表示已经上线)

1. ~~**任务调试功能**~~

~~如果对API+有过深入的体验，那么一定会发现对于业务比较复杂的接口，接口创建成功后才能验证是否正确。所以下一步的规划是对任务的测试功能，创建接口的过程中可以直接测试每个任务的正确性。~~

2. **接口安全控制**

接口的访问授权规划有两种方案：

- **IP白名单：**针对应用增加IP白名单，支持固定IP或IP段授权访问；
- **~~AK认证：~~**~~为应用创建app_key和app_secret；~~
3. ~~**接口返回参数格式自定义封装**~~

~~目前接口返回数据结构是固定的，如下所示：~~
```javascript
{
  code: 200/500/401..., // 请求状态，200表示正常
  msg: '错误信息', // 如果code<>200，则显示错误信息
  result: {} // 具体数据
}
```
~~为了更加灵活的兼容其他系统，下一步将增加自定义响应体的功能。~~

4. ~~**SQL查询任务的分页功能**~~

~~尽管分页查询功能目前可以通过创建两个任务的方式实现，但是这一个小问题极大的影响了创建接口的效率，不符合API+的理念。所以增加SQL查询任务的分页插件支持。~~

5. ~~后台管理添加用户密码修改的功能。~~
6.  后台功能优化
- ~~接口和任务的一键复制功能；~~
- ~~进入接口任务后，返回后没有选中之前选择的分组；~~
7. ~~开发同学建议，增加搜索接口的功能；~~
8. ~~接口页面分页后显示的序号不对，每页都是1-10；~~
9. ~~SQL查询开启驼峰，PageableJdbcTemplate没有做到；这是一个重大bug;~~
10. ~~增加应用以及接口的导出和导入功能。~~
11. 【页面优化】任务编辑器增加支持的js库说明。
12. ~~接口结果缓存功能，接口请求出错时，可以返回最近一次正确的结果。~~
13. 接口巡检功能。
14. ~~接口允许跨域配置。~~
15. 接口任务增加多线程执行，以缩短请求耗时；
16. ~~升级java内置JavaScript引擎，目标是支持es6；(V4.2.0)~~
17. ~~【BUG】接口文档如接口中文名一样，菜单栏锚点跳转不正确~~
18. ~~【优化】接口页面顺序不对，需要改成按照创建时间顺序排列；(V4.2.0)~~
