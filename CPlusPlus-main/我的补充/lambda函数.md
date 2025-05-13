## 什么事lambda函数？
Lambda 表达式是 C++11 引入的一种轻量、快捷的函数定义方式，常用于回调、临时函数、简洁逻辑等场景。
你可以把 Lambda 理解成 “匿名函数” 或 “临时函数”，也叫 函数对象。
```cpp
[capture](parameters) -> return_type {
    function_body;
}
```
| 部分            | 作用                 |
|-----------------|----------------------|
| `[capture]`      | 捕获外部变量         |
| `(parameters)`   | 传入参数             |
| `-> return_type` | 返回类型（通常可以省略） |
| `{ function_body }` | 函数体，执行的代码     |

```cpp
//三个简单例子
1. 不捕获、不传参：
auto say_hello = []() {
    std::cout << "Hello!" << std::endl;
};
say_hello();  // 输出 Hello!

2. 捕获变量：
int x = 10;
auto print_x = [x]() {
    std::cout << x << std::endl;
};
print_x();  // 输出 10

3. 捕获引用（变量可变）：
int x = 10;
auto modify_x = [&x]() {
    x += 5;
};
modify_x();
std::cout << x << std::endl;  // 输出 15
```
回到ros2cpp下：完整代码见ros2bookcode/chapt3/topic_ws/src/demo_cpp_topic/src/turtlecircle.cpp

```cpp
    timer_ = this->create_wall_timer(
    1000ms,
    [this]() { timer_callback(); })
```
