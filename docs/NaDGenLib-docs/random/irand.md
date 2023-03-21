# irand 函数

**描述：**

生成范围在 $[l,r]$ 的随机整数。

**语法：**

```cpp
long long irand(
    [in]    long long l, 
    [in]    long long r
);
```

**参数：**

- `l`：表示生成随机整数的最小值。
- `r`：表示生成随机整数的最大值。

**返回：**

返回一个整数，表示生成的随机整数。

**警告：**

该函数返回的结果在全局上并不独立。

## 使用示例

生成 $20$ 个范围在 $[1,15]$ 的随机整数：

```cpp
#include "genlib.h"
using namespace Generator;
using namespace std;
int main()
{
    RedirectToFile("in.in");
    for(int i=1; i<=20; i++) {
        cout << irand(1,15) << endl;
    }
    return 0;
}
```