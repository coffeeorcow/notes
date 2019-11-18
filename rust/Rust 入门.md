# Rust 入门

## 起步

### Hello World

新建文件 `hello.rs` 编写以下内容：

```rust
fn main() {
    println!("hello world!")
}
```

使用 rustc 命令编译：

```rust
rustc hello.rs
```

编译后生成 `hello.exe` 文件，运行该文件控制台打印 `hello world!`

### Hello World 工程

使用 `cargo ` 工具进行项目的管理

创建一个 `hello_cargo` 工程

```shell
cargo new hello_cargo
```

项目结构如下：

```
|——> .\
|——> src (源码文件夹)
|——————> main.rs (工程入口)
|——> .gitignore (git 忽略配置)
|——> Cargo.tml (cargo 工程皮配置)
```

运行项目

```shell
# 运行项目
cargo run

# 编译项目但不运行
cargo build

# 快速检查项目是否可编译，但不编译项目
cargo check

# 发版项目(比较耗时)
cargo build --release

```

一个猜数字游戏

```rust
use std::io;
use std::cmp::Ordering;
use rand::Rng;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1, 101);

    println!("This secret number is {}", secret_number);

    loop {

        println!("Please input your guess.");

        let mut guess = String::new();

        io::stdin().read_line(&mut guess)
            .expect("Failed read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue
        };
            // .expect("Please type a number:");

        println!("You guesseed: {}", guess);

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            },
        }
    }

}

```



## 基础

### 一些公共的概念

#### 1 Variables &  Mutability (变量和可变量)

- 变量的值不能修改，但是可以通过重新申明的方式覆盖
- 可变量使用 `mut` 关键字申明，值可以修改，但是不可变类型，且不可覆盖

`const` 关键字用于申明常量，并且申明时必须指定类型

#### 2 数据类型

rust 的基础数据类型主要分为数值型和复合型

数值型包括 int, float, bool, char

复合型包括 元组(使用小括号，定长并允许多个类型)和数组(使用中括号，定长且只能有一种类型)

