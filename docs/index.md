# Home

欢迎来到 NaDGenLib 的使用手册！（当然，也是俺的博客啦）

为了保证您的使用体验，下面将会对一些内容进行测试，请查看其是否正确 qwq。

## 下面是数学公式

- 行内公式：$f(x)=\sum_{n=0}^m a_nx^n$
- 行间公式：  
$$
h(x) = \sum_{d\mid x} f(d)g(\frac xd) = \sum_{ab=x}f(a)g(b)
$$

## 下面是表格

| Language | Ratings |
| :------: | :-----: |
|  Python  |  14.83% |
|    C     |  14.73% |
|   Java   |  13.56% |
|   C++    |  13.29% |
|   C#     |   7.57% |

## 下面是代码段

```cpp
// 没啥活好整了，给大家咬个打火机吧
#include <bits/stdc++.h>
using namespace std;
const double alpha = 0.2928;
typedef struct NODE{
    int value;
    int size;
    NODE *lchild,*rchild;
    NODE(int x){
        this->value = x;
        this->size = 1;
        this->lchild = this->rchild = nullptr;
    }
    NODE(){
        this->value = INT_MAX;
        this->size = 0;
        this->lchild = this->rchild = nullptr;
    }
}NODE,*PNODE;

PNODE root;

inline PNODE newNode(int x){
    return new NODE(x);
}

inline void deleteNode(PNODE &T){
    delete T;
    T = nullptr;
}

inline bool isLeaf(PNODE T){
    return T->lchild == nullptr;
}

inline void pushup(PNODE T){
    if(!isLeaf(T)){
        T->value = T->rchild->value;
        T->size = T->lchild->size + T->rchild->size;
    }
}

inline void rotate(PNODE T,bool d){
    PNODE temp;
    if(!d){
        temp = T->rchild;
        T->rchild = T->lchild;
        T->lchild = T->rchild->lchild;
        T->rchild->lchild = T->rchild->rchild;
        T->rchild->rchild = temp;
    }
    else{
        temp = T->lchild;
        T->lchild = T->rchild;
        T->rchild = T->lchild->rchild;
        T->lchild->rchild = T->lchild->lchild;
        T->lchild->lchild = temp;
    }
    pushup(T->lchild);
    pushup(T->rchild);
    pushup(T);
}

inline void maintain(PNODE T){
    bool d = 0;
    if(!isLeaf(T)){
        if(T->lchild->size < T->size * alpha)
            d = 1;
        else if(T->rchild->size < T->size * alpha)
            d = 0;
        else
            return ;
        if(d){
            if(T->rchild->lchild->size >= T->rchild->size * (1-2*alpha)/(1-alpha))
                rotate(T->rchild,!d);
        }
        else{
            if(T->lchild->rchild->size >= T->lchild->size * (1-2*alpha)/(1-alpha))
                rotate(T->lchild,!d);
        }
        rotate(T,d);
    }
}

inline void Insert(PNODE T, int x){
    if(isLeaf(T)){
        T->lchild = newNode(x);
        T->rchild = newNode(T->value);
        if(T->lchild->value>T->rchild->value)
            swap(T->lchild,T->rchild);
        pushup(T);
        return;
    }
    if(T->lchild->value >= x)
        Insert(T->lchild,x);
    else
        Insert(T->rchild,x);
    pushup(T);
    maintain(T);
}

inline void Delete(PNODE &T,int x){
    if(isLeaf(T))
        return ;
    if(x<=T->lchild->value){
        if(isLeaf(T->lchild)){
            if(x!=T->lchild->value)
                return;
            deleteNode(T->lchild);
            PNODE buf = T->rchild;
            *T = *buf;
            deleteNode(buf);
        }
        else
            Delete(T->lchild,x);
    }
    else{
        if(isLeaf(T->rchild)){
            if(x!=T->rchild->value)
                return ;
            deleteNode(T->rchild);
            PNODE buf = T->lchild;
            *T = *buf;
            deleteNode(buf);
        }
        else
            Delete(T->rchild,x);
    }
    pushup(T);
    maintain(T);
}

inline int GetRnk(PNODE T,int x){
    if(isLeaf(T))
        return 1;
    if(x <= T->lchild->value)
        return GetRnk(T->lchild,x);
    return T->lchild->size + GetRnk(T->rchild,x);
}

inline int GetNum(PNODE T,int rnk){
    if(isLeaf(T))
        return T->value;
    if(rnk <= T->lchild->size)
        return GetNum(T->lchild,rnk);
    return GetNum(T->rchild,rnk - T->lchild->size);
}

inline int GetPre(PNODE T,int num){
    return GetNum(T,GetRnk(T,num)-1);
}

inline int GetSuf(PNODE T,int num){
    return GetNum(T,GetRnk(T,num+1));
}

int main(){
    root = new NODE;
    int n;
    cin>>n;
    while(n--){
        int opt;
        cin>>opt;
        switch(opt){
            case 1:{
                int x;
                cin>>x;
                Insert(root,x);
                break;
            }
            case 2:{
                int x;
                cin>>x;
                Delete(root,x);
                break;
            }
            case 3:{
                int x;
                cin>>x;
                cout<<GetRnk(root,x)<<endl;
                break;
            }
            case 4:{
                int x;
                cin>>x;
                cout<<GetNum(root,x)<<endl;
                break;
            }
            case 5:{
                int x;
                cin>>x;
                cout<<GetPre(root,x)<<endl;
                break;
            }
            case 6:{
                int x;
                cin>>x;
                cout<<GetSuf(root,x)<<endl;
                break;
            }
        }
    }
    return 0;
}
```

~~顺便测试了较大文件传输，还有删除线~~

## 下面是图片

树链剖分捏：

![image](/image/tester.png)

AC 自动机捏：

![GIF](/image/ac-automaton2.gif)

**顺带一提，上述图片均来自于 [OI-Wiki](https://oi-wiki.org)**

