# 后端程序安装

## 注意事项

### 环境需求

后端运行基于Docker和Python，虽然脚本可以检测环境并自动安装，但我们强烈建议先手动安装好环境。

Python版本：3.7+ 需要安装pip。

### Selenium

后端执行任务需要调用Webdriver。\
如需在ARM设备上使用，请参阅[seleniarm/standalone-chromium](https://hub.docker.com/r/seleniarm/standalone-chromium)

#### 单机节点（standalone）

请根据需求修改参数

```bash
docker run -d --name=webdriver --log-opt max-size=1m --log-opt max-file=1 --shm-size="2g" --restart=always -e SE_NODE_MAX_SESSIONS=10 -e SE_NODE_OVERRIDE_MAX_SESSIONS=true -e SE_SESSION_RETRY_INTERVAL=1 -e SE_VNC_VIEW_ONLY=1 -p 4444:4444 -p 5900:5900 selenium/standalone-chrome
```

其中：\
SE\_VNC\_VIEW\_ONLY=1  表示VNC仅允许查看，不允许操作。\
SE\_NODE\_MAX\_SESSIONS=10  表示最多允许10个会话数。\
4444端口用于执行任务和面板，5900端口用于VNC。

#### 集群（grid）

Selenium Grid需要一个中心控制器（Hub），并允许在多台服务器上部署节点（Node）。Hub收到请求后会自动分配Node，实现负载均衡，多IP访问等功能。

快速部署脚本请参考[sahuidhsu/selenium-grid-docker](https://github.com/sahuidhsu/selenium-grid-docker)

## 一键部署后端

```bash
bash <(curl -Ls https://raw.githubusercontent.com/pplulee/appleid_auto/main/backend/install_unblocker.sh)
```

安装时按照提示输入参数即可。\
默认服务名为**appleauto。**\
****部署完成后可查看服务日志。\
**请自行寻找关于如何启停Linux服务，查询服务日志的资料。**

