# Graph 类

用于提供存放图的容器，并支持与生成数据相关的函数。

??? Warning
    该类多用作基类，不建议大家直接使用

    自定义生成的时候，请尽量使用继承的方式而不是创建实例。

## 公开的方法：

|返回类型|函数定义|
|------:|:------|
||`Graph( int verCount, bool undirectedMap = false, bool weightedMap = false, bool muiltiedgeCheck = false, bool loopCheck = false )`|
|`bool`|`add_edge(int from, int to)`|
|`bool`|`add_edge(int from, int to, int weight)`|
|`void`|`clear(void)`|
|`int`|`GetEdgeCount(void)`|
|`void`|`Output(bool shuffleOutput = true)`|
||`~Graph(void)`|

## 详细注解：

### `Graph` 构造

**描述：**

`Graph` 类的构造函数。

**语法：**

```cpp
Graph::Graph(
    [in]            int verCount,
    [in, optional]  bool undirectedMap,
    [in, optional]  bool weightedMap,
    [in, optional]  muiltiedgeCheck,
    [in, optional]  loopCheck
);
```

**参数：**

- `verCount`：图的点数
- `undirectedMap`：无向图开关，默认为有向图（false）
- `weightedMap`：带权图开关，默认为不带权（false）
- `muiltiedgeCheck`：重边检查开关，默认为关闭（false）
- `loopCheck`：自环检查开关，默认为关闭（false）

-----------

### `add_edge` 方法

**描述：**

用于添加一条边，边的类型请参照构造函数中 `weightedMap` 部分。

**语法：**

不带权边重载：

```cpp
bool Graph::add_edge(
    [in]    int from,
    [in]    int to
);
```

带边权重载：

```cpp
bool Graph::add_edge(
    [in]    int from,
    [in]    int to,
    [in]    int weight
);
```

**参数：**

- `from`：边的起点
- `to`：边的终点
- `weight`：边的边权（`Override!!`）

**返回：**

若边成功添加，则返回 `true`

否则返回 `false`

**警告：**

该函数的两个重载完全不同，请注意不要混淆，
若不带权图使用了带权图的 `add_edge`，则会触发断言失败，反之亦然。

---------------
