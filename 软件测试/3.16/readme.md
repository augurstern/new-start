以下是**3月16日**的进阶任务清单，今日重点深化测试设计能力并开始数据库基础。请集中精力完成以下内容：

---

### 📌 **今日核心目标**  
**掌握等价类/边界值设计法 + SQL基础查询 + Linux环境实操**

---

### 📚 **任务一：测试设计强化（3小时）**  
1. **理论进阶（1小时）**  
   - 精读《软件测试的艺术》第3章（等价类划分与边界值分析）  
   - 输出：  
     - 用流程图解释**“用户年龄输入框（范围1-120岁）”**的边界值测试点（标注有效/无效边界）  
     - 列举电商“商品价格输入框”的等价类划分（有效类：0.01-9999.99，无效类：负数/超范围/非数字）  

2. **视频实战（1小时）**  
   - 观看B站《黑盒测试用例设计实战》（搜索播放量最高系列，重点学习场景法）  
   - 用Excel设计**“飞机票订购系统”**测试用例（覆盖：成人票/儿童票/婴儿票组合场景）  

3. **缺陷分析（1小时）**  
   - 在Jira中创建**2条缺陷报告**，要求：  
     - 缺陷1：模拟“支付宝转账页面缺少金额输入框的千位分隔符”  
     - 缺陷2：模拟“高德地图搜索框输入超长字符串导致界面崩溃”  
   - 附加：为每条缺陷添加**重现步骤视频链接**（可用手机录制后上传网盘）  

---

### 🗄️ **任务二：SQL入门（2小时）**  
1. **环境搭建（30分钟）**  
   - 安装MySQL 8.0（官网下载社区版）  
   - 使用Navicat或DBeaver连接本地数据库  

2. **基础操作（1.5小时）**  
   - 完成以下SQL语句编写：  
     ```sql
     -- 创建测试库
     CREATE DATABASE testdb;
     USE testdb;
     
     -- 创建用户表
     CREATE TABLE users (
         id INT PRIMARY KEY AUTO_INCREMENT,
         username VARCHAR(50) NOT NULL,
         age INT CHECK (age BETWEEN 1 AND 120),
         register_date DATE
     );
     
     -- 插入5条测试数据（包含1条年龄为0的非法数据）
     INSERT INTO users (username, age, register_date) VALUES
     ('张三', 25, '2023-01-01'),
     ('李四', 120, '2023-02-15'),
     ('王五', -5, '2023-03-10'),  -- 故意插入无效数据
     ('赵六', 99, '2023-03-12'),
     ('测试用户', 1, '2023-03-14');
     
     -- 查询年龄在18-60岁且注册日期在2023年的用户
     SELECT * FROM users 
     WHERE age BETWEEN 18 AND 60 
       AND register_date >= '2023-01-01' 
       AND register_date <= '2023-12-31';
     ```
   - **重点练习**：  
     - 使用`WHERE`过滤出年龄非法的用户（age <1 或 age >120）  
     - 用`UPDATE`语句修正王五的年龄为30岁  

---

### 🐧 **任务三：Linux实战（1.5小时）**  
1. **系统启动（30分钟）**  
   - 在VirtualBox中完成CentOS 7安装（必须配置SSH并设置静态IP）  
   - 使用FinalShell或Xshell连接虚拟机  

2. **命令训练（1小时）**  
   - 完成以下操作并记录命令：  
     ```bash
     # 1. 创建测试目录结构
     mkdir -p ~/test_project/{logs,scripts,data}
     
     # 2. 用vim创建日志文件并写入内容
     echo "2023-03-16 10:00:00 [INFO] Service started" >> ~/test_project/logs/app.log
     echo "2023-03-16 10:05:23 [ERROR] Database connection failed" >> ~/test_project/logs/app.log
     
     # 3. 检索日志中的ERROR信息
     grep "ERROR" ~/test_project/logs/app.log
     
     # 4. 压缩日志目录并重命名
     tar -czvf logs_backup.tar.gz ~/test_project/logs
     
     # 5. 查看系统进程（筛选含"ssh"的进程）
     ps aux | grep ssh
     ```
   - **挑战任务**：  
     使用`crontab -e`添加每日凌晨3点自动清理7天前日志的定时任务  

---

### 🔍 **任务四：交叉验证（1小时）**  
1. **数据库与测试结合**  
   - 在Postman中测试以下接口：  
     ```http
     GET http://jsonplaceholder.typicode.com/users/1
     ```
   - 编写断言：验证返回的`address.geo.lat`值为`-37.3159`  
   - 在MySQL中创建相似结构的表，并插入该接口返回的数据  

---

### ✅ **提交要求**  
1. GitHub仓库新增以下内容：  
   - 边界值流程图（可手绘拍照或使用draw.io）  
   - SQL脚本文件（含注释说明操作目的）  
   - Linux命令执行截图（至少包含grep和crontab操作）  
2. 更新README.md，总结今日难点（例如：SQL CHECK约束的实际应用场景）  

---

**⚠️ 注意**  
- 今日SQL部分必须实际执行并验证结果，禁止只写代码不运行！  
- 若Linux安装卡顿，允许改用WSL2（但需说明选择理由）  
- 当日任务完成度将直接影响明日是否增加自动化预学内容  

23:00前提交，超时需说明原因。遇到技术问题请附具体报错信息+截图！