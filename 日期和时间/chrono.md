**时间单位转换**

- 1秒等于1000毫秒
- 1毫秒等于1000微秒
- 1微秒等于1000纳秒





### 时钟

- system_clock: 
- steady_clock;





### system_clock



```cpp
struct system_clock
{
    using rep = long long;
    using period = nano;
    using duraion = nanoseconds;
    // using nanoseconds = duration<long long, nano>;
};


```





- rep : represention type 的缩写，表示这个 `steady_clock` 的 `duration` 内部将用 `long long` 来保存计数值
- period: 每个tick的时间单位，这里steady_clock的时间单位是nano,纳秒
- duraion: 





### duration 

```cpp
typename <typename Rep, typename Period = ratio<1>>
class duration    
{
    Rep _myrep; // myrep保存计数， 表示 Rep个Period
};
```

- rep : represention type 的缩写，一般是long long, 表示duration内部用long long来保存计数值
- Period: 表示1个tick的时间长度



