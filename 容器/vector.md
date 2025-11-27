### 1. 内存布局

通过栈对象来管理堆对象

```cpp
template<typename T>
class vector {
private:
    T* _start;        // 指向数组的第一个元素
    T* _finish;       // 指向最后一个元素的下一个位置
    T* _end_of_storage; // 指向分配内存的末尾
    // ... 其他成员函数
};
```





### 2. 常用接口





### 3. 注意事项

