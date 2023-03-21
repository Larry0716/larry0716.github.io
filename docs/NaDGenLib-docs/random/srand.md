# srand 函数

**描述：**

生成指定长度和字符集的字符串。

**语法：**

```cpp
string Random::srand(
    [in]            unsigned long long length,
    [in, optional]  string charset
);
```

**参数：**

- `length`：表示生成字符串的长度。
- `charset`：表示生成字符串的字符集，默认为 `0123456789qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZMXNCBV`。

**返回：**

返回一个字符串，表示生成的随机字符串。

**警告：**

该函数返回的结果在全局上并不独立。

请注意，可能会与 C 标准的 `srand(unsigned seed)` 函数相混淆从而引发编译错误。

## 使用示例：

生成长度为 $30$ 的字符串：

```cpp
#include "genlib.h"
using namespace Generator;
using namespace std;
int main(){
    RedirectToFile("in.in");
    cout << srand(30) << endl;
    return 0;
}
```