## Docker install mysql
```bash
docker pull mysql:5.7
mkdir -p ./mysql/conf ./mysql/datadir
# 直接运行
docker run -itd --name mysql  -p 3307:3306 -e MYSQL_ROOT_PASSWORD = root mysql:8.0

# 映射目录
docker run -itd \
	--name mysql \
	--platform \
	linux/amd64 \
	--restart=always \
	-p 3307:3306 \
	-v $(pwd)/mysql/conf:/etc/mysql/conf.d \
	-v $(pwd)/mysql/datadir:/var/lib/mysql \
	-e MYSQL_ROOT_PASSWORD=root \
	mysql:8.0
```

- **含义**：快速启动一个 MySQL 5.7 的容器，用于临时测试。
    
- **参数详解**：
    
    - `docker run`：创建并启动容器。
        
    - `-itd`：
        
        - `i` (Interactive)：保持交互模式。
            
        - `t` (TTY)：分配一个伪终端。
            
        - `d` (Detached)：**后台运行**，即容器启动后不会占用你的命令行窗口。
            
    - `--name mysql`：给容器起个名字叫 "mysql"，方便以后管理。
        
    - `-p 3307:3306`：**端口映射**。
        
        - 冒号左边 `3307` 是你电脑（宿主机）的端口。
            
        - 冒号右边 `3306` 是容器内部 MySQL 的默认端口。
            
        - _意思是你以后连接数据库时，要访问 `localhost:3307`。_
            
    - `-e MYSQL_ROOT_PASSWORD=root`：设置环境变量，将数据库 `root` 用户的密码设为 `root`。
        
    - `mysql:8.0`：使用的镜像版本。

- `--restart=always`：**开机自启**。如果你重启了电脑或 Docker 服务，这个数据库容器会自动重新启动，防止服务中断。
    
- `-v` (Volume)：**挂载卷（目录映射）**。这是最关键的部分。
    
    - 格式为 `宿主机路径:容器内路径`。
        
    - `/opt/db/mysql/conf:/etc/mysql/conf.d`：把你电脑上的 `/opt/db...` 目录映射到容器里的配置目录。这样你直接修改电脑上的文件就能改数据库配置。
        
    - (截图中省略的部分通常是 `-v /opt/db/mysql/data:/var/lib/mysql`)：把数据库的数据存到你电脑硬盘上。**即使你删除了这个 Docker 容器，你的数据（用户、表、记录）依然保存在你的电脑里，不会丢失。**