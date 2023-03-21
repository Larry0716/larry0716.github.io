# 快速上手

本节将会教你如何对快速上手 NaDGenLib。

PS：建议使用 Visual Studio Code 来编写。

## 基本结构

如同 C++ 的基本框架一般，NaDGenLib 也是拥有自己的基本框架。

如果你只想对拍，不想做数据生成器，可以使用如下框架：

```cpp
#include "genlib.h"
using namespace Generator;
using namespace std;
void YourFunction(){
    FlushIOStream();
    //TODO
}
int main(){
    RedirectToFile("filename");
    //TODO
    return 0;
}
```

如果你是题目数据构建者，建议您使用如下框架：

```cpp
#include "genlib.h"
using namespace Generator;
using namespace std;
void YourFunction(int label){
    FlushIOStream();
    //TODO
}
int main(){
    RegisterStdProgram("stdpath");
    AutoGenerate("filename%d.in", 1, 4, YourFunction, true);
    return 0;
}
```

## 生成器

NaDGenLib 对于每一个构造方案都叫做一个生成器，例如无根树生成器 `NoRootTree`，有向无环图生成器 `DAG`。

对于每一个生成器，基本上都有 `Generate` 和 `Output` 方法，有的生成器还拥有 `AutoMode` 方法。

??? warning 
    **警告！Generate + Output 并不等于 AutoMode。**
    
    举个例子，生成器 `AntiSPFA` 调用 `Generate` 完后使用 `Output` 只会输出边。而使用 `AutoMode` 则会输出点数，边数，起点和带权边。

下面是每个生成器支持的方法速览：

| 生成器 | 支持 `Generate` | 支持 `Output` | 备注 |
|:-----:|:-------------:|:-----------:|:----:|
| Random | $\times$ | $\times$ | 生成随机数，被拆分成了三个函数，直接返回值 |
| Sequence | $\checkmark$ | $\times$ | 生成序列，Generate 时包含 Output 了|
| Permutation | $\checkmark$ | $\times$ | 生成排列，Generate 时包含 Output 了| 
| Graph | $\times$ | $\checkmark$ | 作为基类，尽量少用 |
| NoRootTree | $\checkmark$ | $\checkmark$ | 生成无根树 |
| DaisyChain | $\checkmark$ | $\checkmark$ | 生成菊花链 |
| AntiSPFA | $\checkmark$ | $\checkmark$ | 支持 `AutoMode` |
| RandomGraph | $\checkmark$ | $\checkmark$ | 生成随机图 |
| DAG | $\checkmark$ | $\checkmark$ | 生成有向无环图 |
| Cactus | $\checkmark$ | $\checkmark$ | 生成仙人掌 |

如果还不大明白怎么用，这里给你一个示例：

```cpp
//生成一棵无根树
#include "genlib.h"
using namespace Generator;
using namespace std;
int main(){
    RedirectToFile("in.in");
    NoRootTree nrt(30);
    nrt.Generate();
    nrt.Output();
    return 0;
}
```

其他的生成器也像上面示例的那样写就行，只不过每个生成器的构造方案可能不一样，碍于篇幅限制后面将会提到每个生成器具体的构造方法和支持的方法。