# Random 类

随机数生成器，能生成独立的随机数

## 公开的方法

|返回类型|函数定义|
|------:|:------|
||`Random(void)`|
| `long long` | `irand(long long l, long long r)` |
| `long double` | `frand(long double l, long double r)` |
| `string` | `srand(unsigned long long length, string charset = default_charset)`|

## 详细注解

### `irand` 方法

**描述：**

生成范围在 $[l,r]$ 的随机整数。

**语法：**

```cpp
long long Random::irand(
    [in]    long long l, 
    [in]    long long r
);
```

**参数：**

- `l`：表示生成随机整数的最小值。
- `r`：表示生成随机整数的最大值。

**返回：**

返回一个整数，表示生成的随机整数。

-----------

### `frand` 方法

**描述：**

生成范围在 $[l,r]$ 的随机浮点数。

**语法：**

```cpp
long double Random::frand(
    [in]    long double l,
    [in]    long double r
);
```

**参数：**

- `l`：表示生成随机浮点数的最小值。
- `r`：表示生成随机浮点数的最大值。

**返回：**

返回一个整数，表示生成的随机浮点数。

-----------

### `srand` 方法

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


## 使用示例

生成 $20$ 个范围在 $[1,15]$ 的随机整数：

```cpp
#include "genlib.h"
using namespace Generator;
using namespace std;
int main(){
    RedirectToFile("in.in");
    Random rnd;
    for(int i=1; i<=20; i++) {
        cout << rnd.irand(1,15) << endl;
    }
    return 0;
}
```

生成 $10$ 个范围在 $[5,10]$ 的随机浮点数：

```cpp
#include "genlib.h"
using namespace Generator;
using namespace std;
int main(){
    RedirectToFile("in.in");
    Random rnd;
    for(int i=1; i<=20; i++) {
        cout << rnd.frand(5,10) << endl;
    }
    return 0;
}
```

生成长度为 $30$ 的字符串：

```cpp
#include "genlib.h"
using namespace Generator;
using namespace std;
int main(){
    RedirectToFile("in.in");
    Random rnd;
    cout << rnd.srand(30) << endl;
    return 0;
}
```

