# Air-Universe-DockerInstall
Docker-compose for Air-Universe

### 安装 Docker
```
curl -fsSL https://get.docker.com | bash
curl -L "https://github.com/docker/compose/releases/download/1.25.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod a+x /usr/local/bin/docker-compose
# 创建个软链接，以后用 dc 命令来代替 docker-compose
rm -rf which dc  # 若系统中存在 dc 则删除，这个 dc 就是个计算器，完全没有用
ln -s /usr/local/bin/docker-compose /usr/bin/dc
```

### Clone仓库
首先安装git
```shell
apt install git 或 yum Install git
```
然后cd到欲安装目录，执行
```shell
git clone https://github.com/crossfw/Air-Universe-DockerInstall
cd Air-Universe-DockerInstall
```

### 配置配置文件
一般来说，只需要修改 `airu.json` 中的 `panel` 部分即可

> `type`: string
   
您使用的面板类型， 目前支持
- `sspanel` - [SSPanel-Uim](https://github.com/Anankke/SSPanel-Uim)
- `v2board` - [v2board](https://github.com/v2board/v2board)

> `url`: string

面板的通信地址，确保使用 "http://" 或 "https://" 开始

> `key`: string

面板通信密钥
> `node_ids`: [uint32]

一个数组，每个元素都是你将要部署的nodeId.(多个之间使用逗号分隔)

> `nodes_type` [string]

节点类型，仅在使用v2board时使用，多个节点请依次输入，支持类型
- `vmess` - V2Ray(VMess)
- `trojan` - Trojan
- `ss` - Shadowsocks
请加上引号，多个间用逗号分隔，例子如下
```shell
    "nodes_type": ["vmess", "ss"]
```

### 启动
```shell
dc up -d
```

### 多面板对接

1. `cp ./airu.json ./airu2.json`
2. 请参考 [配置文件文档](https://github.com/crossfw/Air-Universe/wiki/%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6) 添加 airu 和 airu2 配置文件的 proxy.in_tags 确保tag名称不一样, 自行完成 `panel` 部分的修改。
3. 请复制 docker-compose.yml 的 airu1 项至最后一行，取名任意(建议airu2). 
4. 修改 airu2中的volumes的第一项配置文件地址到 `./airu2.json:/etc/au/config.json`
5. 启动
