学习笔记

#### 大写转成小写字母

- - A = 65

    a = 97

  - 相差32；依次做差即可

- - A |= 32  = a

#### 将字符串流 改成字符串 istringstream

- - #include <sstream>

```
string str=" i an a boy ";  
    istringstream istring(str);  
    string s;  
    while(istring >> s)
        cout << s << endl;  
输出是:
i
am
a
boy
```

#### 大小写转化 位运算

| 大写变小写、小写变大写（全变） | A(a) ^= 32     a(A)   |      |
| ------------------------------ | --------------------- | ---- |
| 大写变小写、小写不变           | A(a)  \|= 32     a(a) |      |
| 小写变大写、大写不变           | A(a) &= -33     A(A)  |      |