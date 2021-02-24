## ACM技巧

### 无明确输入

`while(~scanf("%d",&a))` 不要用EOF

### 测试代码

在程序中加入代码

```cpp
#define mytest//提交时去掉此行即可
#ifdef mytest
	freopen("test.in","r",stdin);
	freopen("test.out"."w",stdout);
#endif
```

在命令行中重定向

`t1.exe < test.in > test.out`

对拍比较输出结果

Win:`fc test1.out test2.out /n`
Linux:`diff test1.out test2.out /n`

### 提高速度

1. 读题快
2. 熟练使用编辑器/IDE
3. 纸上先写代码，不要边敲键盘边思考浪费机时
4. 减少调试，不要动态调试
5. 互相检查
6. 用STL
7. `typedef long long ll`

### 代码规范

- 最好不要用宏
- 变量定义在离调用最近处

## 时间复杂度

```cpp
clock_t start,end;
start=clock();
//此处为需运行的代码
end=clock();
cout<<(double)(end-start)/CLOCK_PER_SEC<<endl;
```

## STL

### vector

```cpp
a.push_back();
a.pop_back();
a.size();
a.empty();
a[index];
a.insert(a.begin()+i,k);//在第i个元素前插入k
a.insert(a.end(),10,5);//尾部插入10个值为5的元素
a.erase(a.begin()+i;//删除第i+1个元素
a.erase(a.begin()+i,a.begin()+j);//删除区间[i,j-1]的元素
a.resize(n);//调整大小为n
a.clear();

reverse(a.begin(),a.end());
sort(a.begin(),a.end());
```

