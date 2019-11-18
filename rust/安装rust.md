# 安装 Rust

[点击下载安装包地址]( https://www.rust-lang.org/learn/get-started )

由于某些原因，安装 Rust 变得非常非常的慢。

因此，我们通过使用代理来进行安装。

首先，把你的代理软件打开，然后进入 PowerShell 输入以下命令：

```powershell
$proxy='http://127.0.0.1:1080'

$ENV:HTTP_PROXY=$proxy

$ENV:HTTPS_PROXY=$proxy

./rustup-init.exe
```

当然如果无法使用代理，可以使用国内的镜像：(中科大的源)

安装前设置以下环境变量就可以了

```powershell
CARGO_HOME=D:\Environment\rust\.cargo
RUSTUP_HOME=D:\Environment\rust\.rustup
RUSTUP_UPDATE_ROOT=http://mirrors.ustc.edu.cn/rust-static/rustup
RUSTUP_DIST_SERVER=http://mirrors.ustc.edu.cn/rust-static

```



## 常见问题

### 解决下载 crate 太慢的问题

在 `CARGO_HOME` 下创建或编辑 `config` 文件，添加或修改一下内容: (使用中科大的源)

```toml
[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"
replace-with = 'ustc'
[source.ustc]
registry = "git://mirrors.ustc.edu.cn/crates.io-index"
```

