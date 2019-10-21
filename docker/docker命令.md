# Docker 命令

使用方式：docker [OPTIONS] COMMAND

使用 'docker COMMAND --help' 查看一个命令的详细信息

### Options:

​      --config string      客户端配置文件的位置 (默认
​                           			"C:\\Users\\18752\\.docker")
  -D, --debug              	开启 debug 模式
  -H, --host list          	Daemon socket(s) to connect to
  -l, --log-level string   设置日志级别
​                          			 ("debug"|"info"|"warn"|"error"|"fatal")
​                          			 (默认"info")
​      --tls                Use TLS; implied by --tlsverify
​      --tlscacert string   Trust certs signed only by this CA (default
​                           "C:\\Users\\18752\\.docker\\ca.pem")
​      --tlscert string     Path to TLS certificate file (default
​                           "C:\\Users\\18752\\.docker\\cert.pem")
​      --tlskey string      Path to TLS key file (default
​                           "C:\\Users\\18752\\.docker\\key.pem")
​      --tlsverify          Use TLS and verify the remote
  -v, --version            打印版本信息然后退出



### 管理命令:

  builder     Manage builds
  config      Manage Docker configs
  container   Manage containers
  image       Manage images
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes



### 命令：

  attach      把本地的input, output 和 error 标准流绑定到一个运行中的容器中
  build       使用Dockerfile构建一个image
  commit      Create a new image from a container's changes
  cp          在容器和本地文件系统间复制文件/文件夹
  create      创建一个新容器
  diff        监视一个容器的文件系统中文件或文件夹的变化
  events      从服务器中获取实时的时间
  exec        在一个正在运行的容器中执行命令
  export      将一个容器的文件系统导出为一个tar压缩包
  history     展示一个image的history
  images      列出所有的 image
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        杀死一个或多个运行中的容器
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        列出所有的端口映射或指定容器的映射端口
  ps          列出容器
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       开启一个或多个已停止的容器
  stats       Display a live stream of container(s) resource usage statistics
  stop        停止一个或多个运行中的容器
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      更新一个或多个容器的配置
  version     显示 Docker 的版本信息
  wait        Block until one or more containers stop, then print their exit codes



