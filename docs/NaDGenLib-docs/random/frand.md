# frand 函数

**描述：**

生成范围在 $[l,r]$ 的随机浮点数。

**语法：**

```cpp
long double frand(
    [in]    long double l,
    [in]    long double r
);
```

**参数：**

- `l`：表示生成随机浮点数的最小值。
- `r`：表示生成随机浮点数的最大值。

**返回：**

返回一个整数，表示生成的随机浮点数。

**警告：**

该函数返回的结果在全局上并不独立。

## 使用示例

生成 $10$ 个范围在 $[5,10]$ 的随机浮点数：

```cpp
#include "genlib.h"
using namespace Generator;
using namespace std;
int main()
{
    RedirectToFile("in.in");
    for(int i=1; i<=20; i++) {
        cout << frand(5,10) << endl;
    }
    return 0;
}
```