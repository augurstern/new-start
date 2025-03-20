以下是**3月17日**的进阶任务清单，今日聚焦复杂场景测试设计和性能测试初探。任务难度升级，请做好时间管理：

---

### 📌 **今日核心目标**  
**掌握因果图/场景法 + 性能测试基础 + 数据库关联查询实战**

---

### 🧩 **任务一：高级测试设计（3小时）**  
1. **因果图法实战（1.5小时）**  
   - 场景：**电商平台优惠券系统**  
     - 输入条件：用户等级（普通/VIP）、订单金额（≥100元）、优惠券类型（满减/折扣）  
     - 结果：是否允许叠加使用优惠券  
   - 要求：  
     - 绘制因果图（可用draw.io）  
     - 生成判定表并导出10个测试用例（Excel格式）  

2. **场景法应用（1小时）**  
   - 设计**在线考试系统**的**“考生交卷”**流程基本流/备选流：  
     - 基本流：正常答题→点击交卷→系统保存→显示分数  
     - 备选流：超时强制交卷/网络中断交卷/重复交卷  
   - 输出：用PlantUML绘制流程图（https://plantuml.com/）  

3. **实战验证（0.5小时）**  
   - 使用Postman测试真实API（任选其一）：  
     - 高德地图API：`https://restapi.amap.com/v3/weather/weatherInfo?city=110101&key=你的key`  
     - 聚合数据API：`https://www.juhe.cn/docs/api/id/39`  
   - 验证：断言响应时间<500ms且包含关键字段  

---

### 📊 **任务二：性能测试初探（2小时）**  
1. **JMeter入门（1小时）**  
   - 下载JMeter 5.6（https://jmeter.apache.org/）  
   - 创建测试计划：  
     - 线程组：10线程，循环5次  
     - HTTP请求：访问百度首页（https://www.baidu.com）  
     - 添加监听器：查看结果树/聚合报告  
   - 重点观察：**Throughput（吞吐量）**和**Error %**  

2. **性能需求分析（1小时）**  
   - 分析共享单车APP的**“扫码开锁”**功能性能指标：  
     - 确定测试类型（负载/压力/稳定性）  
     - 设计性能测试场景（如：500用户同时开锁）  
   - 输出：《性能测试方案》文档（含目标/策略/监控指标）  

---

### 🗃️ **任务三：数据库进阶（2小时）**  
1. **多表关联查询（1小时）**  
   - 在昨日`testdb`库中新增订单表：  
     ```sql
     CREATE TABLE orders (
         order_id INT PRIMARY KEY AUTO_INCREMENT,
         user_id INT,
         amount DECIMAL(10,2),
         FOREIGN KEY (user_id) REFERENCES users(id)
     );
     -- 插入测试数据（至少包含用户表中存在的user_id和不存在的user_id）
     ```
   - 编写SQL解决：  
     - 查询每个用户的订单总量（LEFT JOIN）  
     - 找出有订单但年龄>60岁的用户（EXISTS子查询）  

2. **数据验证测试（1小时）**  
   - 用Python脚本（或Navicat）验证：  
     - 订单表的`user_id`是否全部存在于用户表（外键约束验证）  
     - 用事务模拟“用户下单后余额扣减”的原子性操作  

---

### 🖥️ **任务四：Linux日志分析（1.5小时）**  
1. **日志监控实战**  
   - 在CentOS中部署Nginx：  
     ```bash
     yum install epel-release -y
     yum install nginx -y
     systemctl start nginx
     ```
   - 生成访问日志：用curl或浏览器多次访问`http://虚拟机IP`  

2. **日志分析命令**  
   - 统计HTTP状态码分布：  
     ```bash
     awk '{print $9}' /var/log/nginx/access.log | sort | uniq -c
     ```
   - 找出访问量Top 5的IP：  
     ```bash
     awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -nr | head -5
     ```

3. **Shell脚本编写**  
   - 创建`log_monitor.sh`：  
     - 功能：每小时检查Nginx错误日志新增的`500`错误  
     - 关键命令：`grep " 500 " /var/log/nginx/error.log | wc -l`  

---

### 🔍 **任务五：缺陷分析（1小时）**  
1. **根因定位训练**  
   - 分析昨日Jira中“高德地图崩溃”缺陷：  
     - 使用Charles抓包，对比正常/异常请求的Header和Body差异  
     - 提出3种可能原因（如：缓冲区溢出/未处理异常字符）  

2. **缺陷闭环验证**  
   - 在MySQL中构造数据：当用户年龄被更新为200岁时，测试系统如何处理  
   - 验证：通过接口/UI观察系统是否抛出合理错误提示  

---

### ✅ **提交要求**  
1. GitHub仓库新增：  
   - 因果图与判定表（图片+Excel）  
   - JMeter测试计划.jmx文件  
   - Nginx日志分析结果截图  
2. 更新README：  
   - 记录性能测试中遇到的线程组配置问题  
   - 总结LEFT JOIN与INNER JOIN的区别（用实际查询结果说明）  

---

**⚠️ 重要提示**  
- 今日重点攻克多表查询和性能测试思维，禁止跳过原理直接操作工具！  
- 若JMeter压测出现乱码，需调整`bin/jmeter.properties`中的`sampleresult.default.encoding=UTF-8`  
- 当日完成度将决定明日是否开放Selenium提前学习权限  

**23:00前提交成果**，若遇环境问题需在21:00前紧急反馈！