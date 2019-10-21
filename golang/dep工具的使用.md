# 安装

配置好 Golang 环境变量后，执行以下命令

```shell
go get -u github.com/golang/dep/cmd/dep
```

# 使用

## 初始化工程

```shell
dep init <目录名> #初始化工程，如果没有目录名，则默认使用当前目录
```

## dep 命令

dep 仅有两个经常用到的命令

- **dep ensure** // 主要的工作命令，并且是改变磁盘状态的唯一命令
- **dep status** // 报告工程状态和Go可视化软件工程域

```shell
# dep ensure

# 添加依赖
dep ensure -add github.com/pkg/errors github.com/foo/bar

# 更新依赖
dep ensure -update github.com/foo/bar
dep ensure -update # 更新所有依赖

# dep check
dep check # 检查同步

```



