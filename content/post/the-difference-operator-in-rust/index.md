---
title: "Rust, 操作符:: 和 . 有什么区别"
description: "在Rust中,:: 和 . 是两种操作符，分别用于路径导航和成员访问，它们有不同的用途和语义。"
date: 2024-12-04T19:00:16+08:00
image: img.png
hidden: false
comments: true
tags:
  - Rust
---

### ::（路径导航操作符）

#### 用途：

:: 用于访问模块、结构体、枚举、常量、静态方法等的路径。

主要场景：

1.	模块路径：导入或引用模块、函数、结构体、枚举等。

```Rust
mod math {
    pub fn add(x: i32, y: i32) -> i32 {
        x + y
    }
}

fn main() {
    let sum = math::add(2, 3); // 使用 :: 导航到模块中的函数
    println!("Sum: {}", sum);
}
```

2.	枚举变体：访问枚举的具体变体。

```Rust
enum Direction {
    North,
    South,
    East,
    West,
}

fn main() {
    let direction = Direction::North; // 使用 :: 访问枚举变体
    match direction {
        Direction::North => println!("Heading North"),
        _ => println!("Not North"),
    }
}
```

3.	关联函数和常量：调用结构体或枚举的关联函数（静态方法）。

```Rust
struct Point {
    x: i32,
    y: i32,
}

impl Point {
    const ORIGIN: Point = Point { x: 0, y: 0 };

    pub fn new(x: i32, y: i32) -> Self {
        Point { x, y }
    }
}

fn main() {
    let origin = Point::ORIGIN; // 使用 :: 访问常量
    let point = Point::new(10, 20); // 使用 :: 调用关联函数
    println!("Point: ({}, {})", point.x, point.y);
}
```

4.	类型声明中的路径：使用 :: 指定完整的命名空间路径。

```Rust
fn main() {
    let s = std::string::String::from("Hello"); // 使用 :: 导航到标准库类型
    println!("{}", s);
}
```


### .（成员访问操作符）

#### 用途：

. 用于访问结构体、枚举或其他类型实例的字段和方法。

主要场景：

1.	字段访问：获取结构体或枚举实例中的字段值。

```Rust
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let p = Point { x: 10, y: 20 };
    println!("x: {}, y: {}", p.x, p.y); // 使用 . 访问字段
}
```

2.	方法调用：调用实例的关联方法或实现的 trait 方法。

```Rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    pub fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect = Rectangle { width: 30, height: 50 };
    println!("Area: {}", rect.area()); // 使用 . 调用方法
}
```

3.	链式操作：链式调用多个方法。
```Rust
fn main() {
    let s = " hello ".trim().to_uppercase(); // 使用 . 链式调用方法
    println!("{}", s); // 输出: "HELLO"
}
```

### 对比总结

| 特性   | ::（路径导航操作符） | .（成员访问操作符）     |  
| ------ | ---- | -------- |  
| 用途   |模块路径、枚举变体、常量、关联函数   |访问字段、调用实例方法、链式调用     |  
| 操作的对象   | 类型、模块、枚举   | 实例（对象）     |  
| 场景   |静态操作：函数、常量、枚举变体   |动态操作：实例字段和方法     |  
| 典型语法	 |模块::函数、类型::关联函数、枚举::变体 |实例.字段、实例.方法()
