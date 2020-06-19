输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

### c plus

***

* 排序法
```c
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        vector<int> ret(k, 0);
        sort(arr.begin(), arr.end());
        for (int i = 0; i < k; i++) {
            ret.push_back(arr[i]);
        }
        return ret;
    }
};
```

* 大根堆
```c
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        vector<int> ret(k, 0);
        if (k == 0)    return ret;
        priority_queue<int> p;
        for (int i = 0; i < k; ++i) p.push(arr[i]);
        for (int i = k; i < arr.size(); ++i) {
            if (arr[i] < p.top()) {
                p.pop();
                p.push(arr[i]);
            }
        }
        for (int i = 0; i < k; ++i) {
            ret[i] = p.top();
            p.pop();
        }
        return ret;
    }
};

```

***