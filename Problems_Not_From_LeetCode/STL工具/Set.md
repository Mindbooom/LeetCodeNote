# set与multiset

set和multiset会根据特定的排序准则，自动将元素进行排序。不同的是后者允许元素重复而前者不允许。
# 头文件
```c++
#include <set>
```
# 初始化
## 1.以template参数定义：
```c++
set<int,greater<int>> col1;
```
## 2.以构造函数参数定义:
```c++

template <class T>
class RuntimeCmp{
public:
	enum cmp_mode{normal,reverse};
private:
	cmp_mode mode;
public:
	RuntimeCmp(cmp_mode m = normal):mode(m){}
 
	bool operator()(const T &t1,const T &t2)
	{
		return mode == normal ? t1 < t2 : t2 < t1;
	}
 
	bool operator==(const RuntimeCmp &rc)
	{
		return mode == rc.mode;
	}
};
 
typedef set<int,RuntimeCmp<int> > IntSet;
```
# 常用函数：
insert();
erase();
# 资料来源：
[Set与multiset](https://blog.csdn.net/xiajun07061225/article/details/7459206)
