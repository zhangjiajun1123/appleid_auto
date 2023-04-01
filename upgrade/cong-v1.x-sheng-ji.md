# 从v1.x升级

​程序可以保留数据库，从v1升级到v2。以下是升级步骤。

1. 停止后端appleauto服务\
   `systemctl stop appleauto`\
   \
   删除所有任务容器\
   `docker stop $(docker ps -a | grep "apple-auto*" | awk '{print $1}')`\
   `docker rm $(docker ps -a | grep "apple-auto*" | awk '{print $1}')`
2. 删除前端网站的所有文件
3. 参考[前端网站安装](../install/qian-duan-wang-zhan-an-zhuang.md)的1\~5步
4. 导入`db/update/v2.0.sql`，无需导入初始数据库
5. 登录网站，检查数据是否存在
6. 前往`后端程序安装`，重新安装后端程序。**无需重新安装Selenium（WebDriver）**

