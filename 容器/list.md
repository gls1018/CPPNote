

**底层实现:**

- 双向链表

**特点:**

- 任意位置插入和删除效率高
- 在所指元素被删除前，迭代器不会失效
- **内存不连续，无法通过索引 [] 来访问元素 **



**初始化**

```cpp
//空列表
std::list<int> list1;

//初始化列表
std::list<int> list2 = {1, 2, 3, 4, 5};
std::list<int> list3 {1, 2, 3, 4, 5}

//指定大小和初值
std::list<int> list4(5);  //5个元素，默认是0
std::list<int> list5(3, 10); //3个元素， 默认是10

//通过迭代器初始化
std::vector<int> vec {1, 2, 3, 4, 5};
std::list<int> list6(vec.begin(), vec.begin()+3);
```



**遍历访问**

```cpp
//使用 范围-for 访问
for(auto &value: list2)
{
    std::cout << value;
}


//使用正向迭代器
for(auto i= list2.begin(); i!= list2.end(); i++)
{
    std::cout << *i << std::end;
}

//使用反向迭代器
for(auto rit = mylist.rbegin(); rit != mylist.rend(); ++rit)
{
	std::cout << *rit << " ";
}

```





**插入元素**

```cpp
```



**删除元素**

```cpp
std::list<int> mylist{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

//删除头部元素
mylist.pop_front();

//删除尾部元素
mylist.pop_end();


//删除特定值的元素
mylist.remove(5);

//删除满足特定条件的元素
mylist.remove_if([](int elem){
    return (elem % 2 === 0)
});


// 使用 erase 删除


```



