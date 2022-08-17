#### mac安装

##### 1 Brew install 方法安装 redis

```bash
$ brew install redis
```

如果需要后台运行 redis 服务，使用命令 `brew services start redis`

如果不需要后台服务，则使用命令 `redis-server /usr/local/etc/redis.conf`。

```python
➜  ~ brew install redis
Updating Homebrew...
==> Downloading https://homebrew.bintray.com/bottles/redis-4.0.1.el_capitan.bottle.tar.gz
######################################################################## 100.0%
==> Pouring redis-4.0.1.el_capitan.bottle.tar.gz
==> Using the sandbox
==> Caveats
To have launchd start redis now and restart at login:
  brew services start redis
Or, if you don't want/need a background service you can just run:
  redis-server /usr/local/etc/redis.conf
==> Summary
🍺  /usr/local/Cellar/redis/4.0.1: 13 files, 2.8MB
```

运行第一条以后，会出现当前的情况：

```python
➜  ~ brew services start redis
==> Tapping homebrew/services
Cloning into '/usr/local/Homebrew/Library/Taps/homebrew/homebrew-services'...
remote: Counting objects: 12, done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 12 (delta 0), reused 7 (delta 0), pack-reused 0
Unpacking objects: 100% (12/12), done.
Tapped 0 formulae (40 files, 53.7KB)
==> Successfully started `redis` (label: homebrew.mxcl.redis)
```

要运行命令，可以直接到 `/usr/local/bin` 目录下，有

- `redis-server` 服务器运行命令
- `redis-cli` 运行客户端

在这里可以直接运行 `redis-server` 打开服务。然后另外开一个终端，运行 `redis-cli` 运行服务端，在服务端中输入 `quit` 可以退出。



redis命令操作

```bash
$ redis-cli
$ config get requirepass
$ config set requirepass [new password]
```

手动修改密码

第一 找到redis.conf 文件一般是在 /usr/local/redis/redis.conf 目录下（每个人目录不一样）
第二 通过文本编辑打开redis.conf文件，按command+f 查询 # requirepass foobared
更改为   requirepass 你的密码

