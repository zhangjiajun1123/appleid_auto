# 前端网站安装

网页端运行环境推荐 PHP 7.4 & MySQL 8.0，理论支持MySQL5.x，其他版本PHP可能不支持。



1. 前往[Release](https://github.com/pplulee/appleid\_auto/releases)从最新版本下载网页源码（Source code）并解压
2.  将配置文件`.example.env`复制一份，名字改为`.env`，并填写设置项\
    有关后端API请参阅[后端API介绍](../intro/hou-duan-api-jie-shao.md)\


    ```
    # 启用调试模式
    APP_DEBUG = false

    # 是否开启注册功能
    ENABLE_REGISTER = true
    # API Key，用于调用前端的API
    API_KEY = 123456
    # Webdriver地址，末尾不要加斜杠
    WEBDRIVER = http://localhost:4444
    # 是否启用任务后台运行，即不显示浏览器窗口
    TASK_HEADLESS = true
    # 是否启用代理池
    ENABLE_PROXY_POOL = false
    # 当后端报告代理不可用时，是否自动禁用该代理
    PROXY_AUTO_DISABLE = false
    # 当任务执行失败时，是否5分钟后重试，否则直接等待下一次执行任务
    FAIL_RETRY = true
    [BACKEND]
    # 后端API配置
    # 通过后端API可实现在前端控制解锁任务，做到实时更新，并允许用户触发解锁
    # 由于后端API采用HTTP协议，强烈建议监听127.0.0.1而非0.0.0.0
    # 如果前端与后端不在同一台服务器上，强烈建议使用nginx等进行反代
    ENABLE_API = false
    LISTEN_IP = 127.0.0.1
    LISTEN_PORT = 3939
    API_URL = http://127.0.0.1:3939
    TOKEN = 1234561
    [DATABASE]
    # 数据库连接信息
    TYPE = mysql
    HOSTNAME = 127.0.0.1
    DATABASE = appleid_auto
    USERNAME = root
    PASSWORD = 123456
    HOSTPORT = 3306

    [APP]
    # 时区设置
    DEFAULT_TIMEZONE = Asia/Shanghai
    ```
3. 前往PHP设置，删除对putenv函数的禁用\
   对于宝塔用户，请前往`软件商店`->`对应PHP的设置`->`禁用函数`->`删除'putenv'`
4.  前往网站根目录，执行以下指令\


    ```bash
    wget https://getcomposer.org/installer -O composer.phar
    php composer.phar
    php composer.phar install
    ```
5.  设置网站运行目录为`/public`，并设置伪静态为\


    ```nginx
    location ~* (runtime|application)/{
        return 403;
    }
    location / {
        if (!-e $request_filename){
            rewrite  ^(.*)$  /index.php?s=$1  last;   break;
        }
    }
    ```
6. 手动导入数据库文件 (`db/db.sql`)
7. 在网站根目录下执行指令，创建管理员账户\
   `php think register 用户名 密码`
8. 登录网站，此时请先不要添加账号，完成[后端安装](hou-duan-cheng-xu-an-zhuang.md)后再添加
