# 《实验二：索引操作与文档操作练习》

**学院：省级示范性软件学院**
**题目：**《实验二：索引操作与文档操作练习》
**姓名：**刘双硕
**学号：**2100150421
**班级：**软工2201
**日期：**2024-09-14
**实验环境：**Elasticsearch8.12.2 Kibana8.12.2

# 一、实验目的

1. 掌握Elasticsearch 安装IK分词器安装方法
2. 掌握Elasticsearch 索引操作方法
3. 掌握Elasticsearch 文档操作训练
4. 掌握Elasticsearch 高级查询与DSL训练

# 二、实验内容

## (一) IK分词器安装

跳转到es的bin目录下进行ik分词器安装:

![image-20240914181426893](./assets/image-20240914181426893.png)

安装好后在conf目录下出现ik分词器的文件夹:

![image-20240914181448262](./assets/image-20240914181448262.png)

## (二) 索引操作练习

要求：能够根据字段描述，创建索引，修改索引，删除索引

任务一：

1. 创建索引
2. 修改索引(自己设计，修改要合理）
3. 删除索引
4. 查看所有

### 1. 创建索引

#### 一、 用户信息 (User Information) 索引

##### (一) 代码

![image-20240914181622848](./assets/image-20240914181622848.png)

![image-20240914181647012](./assets/image-20240914181647012.png)



##### (二) 代码运行结果

![image-20240914181746304](./assets/image-20240914181746304.png)

##### (三) 索引查询结果

![image-20240914181801487](./assets/image-20240914181801487.png)

![image-20240914181809486](./assets/image-20240914181809486.png)

#### 二、产品目录 (Product Catalog) 索引

##### (一) 代码

![image-20240914181844669](./assets/image-20240914181844669.png)

![image-20240914181921987](./assets/image-20240914181921987.png)

##### (二) 代码运行结果

![image-20240914181926801](./assets/image-20240914181926801.png)

##### (三) 索引查询结果

![image-20240914181939011](./assets/image-20240914181939011.png)

![image-20240914181943355](./assets/image-20240914181943355.png)

#### 三、订单记录 (Order Records) 索引

##### (一) 代码

![image-20240914181957378](./assets/image-20240914181957378.png)

![image-20240914182004009](./assets/image-20240914182004009.png)

##### (二) 代码运行结果

![image-20240914182008574](./assets/image-20240914182008574.png)

##### (三) 索引查询结果

![image-20240914182019391](./assets/image-20240914182019391.png)

![image-20240914182033892](./assets/image-20240914182033892.png)

### 2. 修改索引

#### 一、用户信息 (User Information) 索引修改

增加了职业的字段,便于用户的分析.

##### (一) 代码

![image-20240914182044244](./assets/image-20240914182044244.png)

##### (二) 执行结果

![image-20240914182048109](./assets/image-20240914182048109.png)

#### 二、产品目录 (Product Catalog) 索引修改

增加商品销售数量的字段,便于按销售数量进行排序.

##### (一) 代码

![image-20240914182051962](./assets/image-20240914182051962.png)

##### (二) 执行结果

![image-20240914182055583](./assets/image-20240914182055583.png)

#### 三、订单记录 (Order Records) 索引修改

增加了负责订单运送的快递公司的字段,便于进行物流的管理.

##### (一) 代码

![image-20240914182058914](./assets/image-20240914182058914.png)

##### (二) 执行结果

![image-20240914182107916](./assets/image-20240914182107916.png)

### 3. 删除索引

#### 一、代码

![image-20240914182431493](./assets/image-20240914182431493.png)

#### 二、执行结果

![image-20240914182440786](./assets/image-20240914182440786.png)

### 4. 查看所有

#### 一、代码

![image-20240914182446755](./assets/image-20240914182446755.png)

#### 二、执行结果

![image-20240914182451398](./assets/image-20240914182451398.png)

## (三) 文档操作练习

要求：文档的CRUD练习

任务二：

1. 创建文档
2. 修改文档(自己设计，修改要合理）
3. 删除文档
4. 查看文档
5. 将下面的Json数据批量导入ES数据库中

在用户信息 (User Information) 索引下进行文档的CRUD.

前四问以需要导入的JSON数据的第一个数据为例进行操作:

![image-20240914182459180](./assets/image-20240914182459180.png)

#### 一、创建文档

##### (一) 代码

![image-20240914182503018](./assets/image-20240914182503018.png)

##### (二) 执行结果

![image-20240914182507026](./assets/image-20240914182507026.png)

##### (三) 查询结果

![image-20240914182510784](./assets/image-20240914182510784.png)

#### 二、修改文档

##### (一) 增量修改

###### 1. 代码

![image-20240914182514208](./assets/image-20240914182514208.png)

###### 2. 执行结果

![image-20240914182518674](./assets/image-20240914182518674.png)

###### 3. 查询结果

![image-20240914182522213](./assets/image-20240914182522213.png)

##### (二) 全量修改

###### 1. 代码

![image-20240914182526439](./assets/image-20240914182526439.png)

###### 2. 执行结果

![image-20240914182529904](./assets/image-20240914182529904.png)

###### 3. 查询结果

![image-20240914182533773](./assets/image-20240914182533773.png)

#### 三、删除文档

##### (一) 代码

![image-20240914182542087](./assets/image-20240914182542087.png)

##### (二) 执行结果

![image-20240914182545972](./assets/image-20240914182545972.png)

#### 四、查看文档

##### (一) 通过id查询文档

###### 1. 代码

![image-20240914182549834](./assets/image-20240914182549834.png)

###### 2. 查询结果

![image-20240914182553091](./assets/image-20240914182553091.png)

##### (二) 查询所有文档

###### 1. 代码

![image-20240914182556547](./assets/image-20240914182556547.png)

###### 2. 查询结果

![image-20240914182609911](./assets/image-20240914182609911.png)

#### 五、将下面的Json数据批量导入ES数据库中

由于导入数据较多,代码和结果仅展示前2个.

##### (一) 导入用户信息

###### 1. 代码

![image-20240914182631528](./assets/image-20240914182631528.png)

###### 2. 执行结果

![image-20240914182645914](./assets/image-20240914182645914.png)

##### (二) 导入产品目录

###### 1. 代码

![image-20240914182650247](./assets/image-20240914182650247.png)

###### 2. 执行结果

![image-20240914182700104](./assets/image-20240914182700104.png)

##### (三) 导入订单记录

###### 1. 代码

![image-20240914182720726](./assets/image-20240914182720726.png)

###### 2. 执行结果

###### ![image-20240914182735269](./assets/image-20240914182735269.png)

## (四) 高级查询&DSL练习

### 1. 用户信息数据

#### 一、查询所有女性用户的姓名和电子邮件。

![image-20240914182740410](./assets/image-20240914182740410.png)

#### 二、查找最后登录日期在2024年9月1日之后的所有活跃用户。

#### ![image-20240914182746337](./assets/image-20240914182746337.png)

#### 三、查询住在"Anytown"的用户。

![image-20240914182750280](./assets/image-20240914182750280.png)

#### 四、查找出生日期在1990年之后的所有用户。

![image-20240914182753700](./assets/image-20240914182753700.png)

#### 五、查询所有状态为"inactive"的用户。

#### ![image-20240914182800716](./assets/image-20240914182800716.png)

#### 六、查找注册日期在2023年1月1日到2023年12月31日之间的用户。

#### ![image-20240914182807669](./assets/image-20240914182807669.png)

#### 七、查询名字为"Bob Smith"的用户的详细信息。

![image-20240914182813273](./assets/image-20240914182813273.png)

#### 八、查找电话号码以"123"开头的用户。

![image-20240914182821820](./assets/image-20240914182821820.png)

#### 九、查询电子邮件域为"example.com"的所有用户。

#### ![image-20240914182831956](./assets/image-20240914182831956.png)

#### 十、查找所有名字中包含"Lee"的用户。

![image-20240914182836155](./assets/image-20240914182836155.png)

### 2. 产品目录数据

#### 一、查询所有类别为"Audio"的产品名称和价格。

![image-20240914182841421](./assets/image-20240914182841421.png)

#### 二、查找价格高于50美元的所有产品。

![image-20240914182847073](./assets/image-20240914182847073.png)

#### 三、查询库存数量少于100的产品。

![image-20240914182852763](./assets/image-20240914182852763.png)

#### 四、查找评分高于4.5的所有产品。

![image-20240914182857124](./assets/image-20240914182857124.png)

#### 五、查询标签中包含"smart"的所有产品。

![image-20240914182903122](./assets/image-20240914182903122.png)

#### 六、查找供应商为"TechCorp"的产品。

#### ![image-20240914210320605](./assets/image-20240914210320605.png)

#### 七、查询发布日期在2023年6月1日之后的所有产品。

#### ![image-20240914210038875](./assets/image-20240914210038875.png)

#### 八、查找描述中包含"wireless"的产品。

![image-20240914210126833](./assets/image-20240914210126833.png)

#### 九、查询价格在20美元到100美元之间的所有产品。

![image-20240914210141400](./assets/image-20240914210141400.png)

#### 十、查找产品名称中包含"Light"的所有产品。

#### ![image-20240914210147239](./assets/image-20240914210147239.png)

### 3. 订单记录数据

#### 一、查询所有状态为"completed"的订单的订单ID和总金额。

#### ![image-20240914210207009](./assets/image-20240914210207009.png)

#### 二、查找总金额大于100美元的所有订单。

#### ![image-20240914210229497](./assets/image-20240914210229497.png)

#### 三、查询支付方式为"paypal"的订单。

![image-20240914210339908](./assets/image-20240914210339908.png)

#### 四、查找订单日期在2024年2月之后的所有订单。

![image-20240914210352305](./assets/image-20240914210352305.png)

#### 五、查询包含产品ID为"P001"的订单。

![image-20240914210405883](./assets/image-20240914210405883.png)

#### 六、查找所有状态为"cancelled"的订单的客户ID。

![image-20240914210414856](./assets/image-20240914210414856.png)

#### 七、查询发货日期在2024年1月15日之前的订单。

![image-20240914210426324](./assets/image-20240914210426324.png)

#### 八、查找使用"credit_card"支付的订单。

![image-20240914210432429](./assets/image-20240914210432429.png)

#### 九、查询总金额在50美元到200美元之间的所有订单。

![image-20240914210437586](./assets/image-20240914210437586.png)

#### 十、查找订单ID中包含"OR01"的所有订单。

![image-20240914210444342](./assets/image-20240914210444342.png)

# 三、问题及解决办法

## (一) JSON数据无法批量导入

给出的JSON数据不符合es批量导入的格式,修改后即可导入.

修改前:![image-20240914210451466](./assets/image-20240914210451466.png)



修改后:

![image-20240914210505617](./assets/image-20240914210505617.png)

## (二) 匹配123开头的手机号时,匹配错误

匹配123开头的手机号时,匹配到了中间为123的手机号.

问题所在:

在设置映射时错误的将phone_number设置为了text,进行了分词.

将其设计为keyword解决了问题.