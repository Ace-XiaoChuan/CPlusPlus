## 我一直很疑惑，构造函数怎么会有类型转换呢？

### 举个例子：
```cpp
#include <iostream>
#include <string>

class Person {
public:
    Person(const std::string& name) {
        std::cout << "Person constructor called with name: " << name << std::endl;
    }
};

void greet(Person p) {
    std::cout << "Hello!" << std::endl;
}

int main() {
    greet("Alice"); // ✅ 编译通过，隐式调用构造函数 Person("Alice")
}
```
正常的话是不行的，因为greet应该接受一个Person类型的对象，但是没有 explicit 时，编译器会自动帮你调用：
```Person p = Person("Alice")  //这里Person()是强制类型转换```
所以代码能正常运行。

---

### 现在看加入了explicit的情况
```cpp
class Person {
public:
    explicit Person(const std::string& name) {
        std::cout << "Person constructor called with name: " << name << std::endl;
    }
};

void greet(Person p) {
    std::cout << "Hello!" << std::endl;
}

int main() {
    greet("Alice"); // ❌ 编译错误：不能隐式将 string 转换为 Person
}
```