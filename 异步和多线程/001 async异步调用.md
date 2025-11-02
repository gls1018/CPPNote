**关于std::async**

std::async用于异步执行一个任务，其执行的结果由std::future返回

三种启动方式

```cpp
int fun()
{
    return 10;
}

std::future<int> res1= std::async(func);  //默认，MSVC下在新线程中执行

std::future<int> res2 = std::async(std::launch::async, func); //强制在新线程中运行

std::future<int> res3 = std::async(std::launch::deffered, func); //在当前线程中推迟执行，直到调用 res3.get()才开始执行
```





**关于std::future**

std::future是一个模板类，它是std::async函数的返回类型，其结果保存在std::future类对象中



```cpp
std::future res = std::async(func);

res.get(); //获取异步函数执行的结果，会阻塞当前线程，直到异步函数执行完毕
		   // get函数只能调用一次， 多次调用为 UB



res.valid(); //判断res的状态是否有效， 如果之前调用过get, 则状态无效
```





**1. 计算fabonacci数列**

```cpp
size_t fabonacci(int num)
{
	if (num <= 1)
		return 1;
	return fabonacci(num - 1) + fabonacci(num - 2);
}

int main()
{
	std::future<size_t> result = std::async(fabonacci, 10);
	std::print("result == {0}\n", result.get());
	return 0;
}
```





**2.并行计算**

```cpp
size_t parallel_sum(const std::vector<size_t>& vec, size_t start, size_t end)
{
	return std::accumulate(vec.begin() + start, vec.begin() + end, 0);
}

int main()
{
	std::vector<size_t> vec(1000, 2);
	size_t chunk = vec.size() / 4;

    //拆分成四个任务，分别计算
	std::future<size_t> res1 = std::async(parallel_sum, std::ref(vec), 0, chunk);
	std::future<size_t> res2 = std::async(parallel_sum, std::ref(vec), chunk, chunk*2);
	std::future<size_t> res3 = std::async(parallel_sum, std::ref(vec), chunk*2, chunk*3);
	std::future<size_t> res4 = std::async(parallel_sum, std::ref(vec), chunk*3, chunk*4);
	size_t sum = res1.get() + res2.get() + res3.get() + res4.get();
	std::print("sum == {0}\n", sum);
	return 0;
}
```

