## 一、iterators(迭代器)

1. 迭代器是为了能够依序巡防某个聚合物（容器）所含的各个元素，而又不暴露容器的内部表述方式。

2. 迭代器是一种行为类似**指针**的对象，指针最重要的便是内容提领（dereference）和成员访问（member access），因而迭代器最重要的工作是对 **operator*** 和 **operator->** 的重载。

3. traits的特化是针对原生指针而写的。（T*  和 const T*)

## 二、vector和list的异同

因为只看了这两部分，所以先整理这两个，后续再添加。

这部分参考自：

https://www.cnblogs.com/kandid/p/11369057.html

https://blog.csdn.net/lym940928/article/details/83063699

1. #### vector

（1）**连续的存储空间**，和array类似。不同的是array是静态的，一旦配置就不能改变；vector是**动态空间**，随着元素的加入，内部机制会自行扩充空间以容纳新元素。

​		当新增的元素超过当前容量（capacity）时，整个vector就需要另找空间，**容量会扩充至两倍**，若不足，就扩充至足够大（与操作系统有关，不同操作系统的扩充不一定是两倍）。（步骤为：重新配置->移动数据->释放原空间）

（2）**底层实现：数组**

（3）连续的内存空间，故能进行高效的**随机存储，时间复杂度为O(1)**。插入或删除中间节点的性能差O(n)。

（4）适用：对于经常随机访问，且不经常对非尾结点进行插入删除。

------

2. #### list

（1）不能像vector一样采用普通指针作为迭代器，其**节点不在存储空间中连续存在**。

（2）**底层实现：双向环状链表**

（3）非连续存储空间，随机访问性能差O(n)，只能快读访问头尾节点。**插入和删除一般是常数级别的开销**。

（4）适用：对于经常需要插入删除的，且不经常随机访问的。

------

除此以外，vector和list对迭代器的支持不同。

相同点：vector< int >:: iterator和list< int >::iterator都重载了“++”操作。

不同点：vector中，iterator支持“+”，“+=”，“<”等操作，而list中则不支持。



## 三、一些小注意事项：

vector和list没有find成员函数，只能用泛型find函数

```c
vector<int> my={1,5,3,2,6};
auto it=find(my.begin(),my.end(),5);
if(it!=my.end()){
	cout<<*it<<ends;
}

list<int> mylist;
for(int i=0;i<10;i++){
	mylist.push_back(i+5);
}
	
auto my = find(mylist.begin(),mylist.end(),5);
if(my!=mylist.end()){
	cout<<*my<<endl;
}
```

