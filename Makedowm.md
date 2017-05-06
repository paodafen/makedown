##MySQL数据库##
###MySQL数据服务器  存储网站数据###
一、分两部分学习：
基本：MySQL基本命令
特级：MySQL优化

二、数据库 database
DB  DBA  DBM  DBMS...　

三、web工作原理                 
　　a)在客户端浏览器输入url地址回车向服务器发送请求  
　　b)服务器接收请求          
　　　i.如果.html文件  直接返回给客户端浏览器  
　　　ii.如果.php文件  通过php解析器(动态生成html) 返回客户端浏览器

　　　　　1.如果php文件中，有连接数据库服务器的操作，那么会向数据库服务器发送请，进行相应操作(增、删除、改、查) ，操作后服务器返回一个相应的结果  

　　　III.由客户端浏览器解析(网页)

四、MySQL服务器  需要  客户端访问   
　　Php   
　　Cmd   
　　图形化界面...

五、数据库分类  
　　a)关系型数据库 MySQL Oracle access SQL server...   
　　　　i.都支持SQL语言  
　　b)非关系型数据库 NoSQL  redis 

六、SQL语言  结构化查询语言  sql命令  
　　1.数据定义语言DDL   
   　　　　 Create创建  drop删除  alter修改   
　　2.数据操作语言DML  
　　　　i.Insert添加  update修改  delete删除   
　　3.数据查询语言 DQL   
　　　　i.Select查询   
　　4.数据控制语言 DCL   
　　　　i.grant

七、数据定义语言DDL   
　a)数据库---数据表---数据
基本命令    
　　1.连接数据库服务器    
　　　　Mysql -u root -p 回车 加密码   
　　2.创建数据库 一个项目一个库   
　　　　a)Create database [if not exists] db_name;   
　　　　b)Show databases; 查看所有库   
　　　　c)Drop database db_name;   
　　3.选择库  创建表  表中行===记录 列===字段   
　　　　a)Use db_name;   
　　　　b)Create table tb_name(  
　　　　　　　　　列名 列类型,   
　　　　　　　　　列名 列类型   
　　　　　　　　　..........   
　　　　　　　　);   
　　　　　　　　最后一列逗号一定没有     
　　　　C)查看所有表 show tables;   
　　　　D)查看表结构 desc tb_name      

八、数据操作语言 DML  查询DQL  
　　a.添加数据   
　　　　a)Insert into tb_name(列名1,列名2......) values(列对应的值1,列对应的值2....);   
　　b.查询数据   
　　　　a)Select 字段名称,字段名称... Form tb_name;   
　　　　b)Select * from tb_name;  * 所有字段   
　　ｃ.修改    
　　　　ａ)update tb_name set 字段名称=新值,字段名称=新值....where id=2;   
　　ｄ.删除   
　　　　ａ)delete from tb_name where id=1;    
 
九、创建表  utf8   
　Create table tb_name(   
　　　　　　字段名称 字段类型 [字段属性],   
　　　　　　字段名称 字段类型 [字段属性],   
　　　　　　......   
　　　　　　字段名称 字段类型 [字段属性]   
　　)表类型 表字符集;   
　　Engine=myisam 　 charset=utf8   

字段类型  mysql数据类型 4种类型   
一、数值    
　　　i.整数：根据范围去选择 tinyint　  int   
　　　ii.小数：float(n,m)　 double(n,m)　 decimal(n,m)  
　　　　　1.N共几位数  m小数点后几位


二、字符  varchar() 　text 　longtext　  完整性   
　　i.Char(n) 固定长度  密码 32 手机号char(11)  n:0-255   
　　ii.Varchar(n) 可变长度 n:0-65535  utf8 21845   

　　　区别：如果传入的字符个数 > n 会截取到n  mysql5.7.19 超过报错

　　iii.Text   
　　iv.Longtext   
　　　Enum单选  enum(‘a’,’b’,’c’);  
　　　Set 多选 set(‘a’,’b’,’c’);  ‘a,b,c’   
　　　存储值必须加引号      
　　　‘ > 提示少分号   
三、时间和日期类型  存成int 时间戳   
四、null

##Php连接mysql##
1.连接数据库服务器  
　$link = Mysqli_connect(主机，用户名，密码);    
2.判断连接是否成功    
　Mysqli_connect_errno   
　Mysqli_connect_error  
3.选择数据库 并判断是否成功    
　Mysqli_select_db($link, 数据库名);   
4.设置字符集
　Mysqli_set_charset($link, ‘字符集’)   
5.准备sql   
　Ddl  DML  DQL   
　$sql = “”;    
6.执行sql   
　$res = Mysqli_query($link, $sql);   
7.判断执行结果   
　DML 返回布尔值    
　If($res){   
　　　　成功    
　}else{   
　　　　失败   
　}   
DQL  返回对象(资源)　从资源中获取结果(数组)   
　mysqli_num_rows($res); //结果条数    
　Mysqli_fetch_assoc($res); 一次取一条记录 循环取   
　If($res && mysqli_num_rows($res)){   
　　　　查询到结果 需要获取   
　　　　While($uinfo = Mysqli_fetch_assoc($res)){   
　　　　　　Var_dump($uinfo);   
　　　　}      
　}else{  
　　　没有查询到结果   
　}   

8.关闭数据库连接   
　Mysqli_close($link);    
　添加 接收表单数据 insert   
　修改 先显示表单中  再修改   
　删除 传值  接值    
　查询 表格  