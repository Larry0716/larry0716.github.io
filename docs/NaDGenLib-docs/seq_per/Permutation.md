# Permutation 类

排列生成器，用于生成 $[1,n]$ 的排列。

## 公开的方法

|返回类型|函数定义|
|------:|:------|
||`Permutation(unsigned length)`|
|`void`|`Generate(string split = " ", string ends = "\n")`|
||`~Permutation(void)`|

## 详细注解

### `Permutation` 构造

**描述：**

排列的构造函数。

**语法：**

```cpp
Permutation::Permutation(
    [in]    unsigned length
);
```

**参数：**

- `length`：排列长度。

-----------

### `Generate` 方法

**描述：**

生成并依照固定格式输出排列。

**语法：**

```cpp
void Permutation::Generate(
    [in, optional]  string split,
    [in, optional]  string ends
);
```

**参数：**

- `split`：元素分割方式，默认为空格。
- `ends`：排列输出结束方式，默认为回车。

**警告：**

注意，`split` 和 `ends` 都应当为字符串。

## 使用示例

生成长度范围在 $[1,15]$ 的排列：

```cpp
#include "genlib.h"
using namespace Generator;
using namespace std;
int main()
{
    RedirectToFile("in.in");
    int n = irand(1,15);
    cout << n << endl;
    Permutation p(n);
    p.Generate();
    return 0;
}
```