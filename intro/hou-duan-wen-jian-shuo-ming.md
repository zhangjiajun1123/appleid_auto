# 后端文件说明

* `backend\unblocker_manager.py` 后端管理程序\
  说明：用于定时从API获取任务列表，并部署task对应的docker容器\
  启动参数：`-api_url <API地址> -api_key <API key>` （API地址格式为`http(s)://xxx.xxx` 末尾不需要加`/`或路径）
* `backend\unlocker\main.py` 后端解锁程序\
  说明：通过Webdriver实现账号改密解锁，并向API提交新密码。**该程序依赖API运行**\
  启动参数：`-api_url <API地址> -api_key <API key> -taskid <Task ID>`

**后端管理程序**会自动从API站点获取任务并部署容器，默认同步时间为10分钟（重启服务即可立即同步）\
若不想使用自动同步，也可以手动部署**后端解锁程序** ，docker版 [sahuidhsu/appleid\_auto](https://hub.docker.com/r/sahuidhsu/appleid\_auto)
