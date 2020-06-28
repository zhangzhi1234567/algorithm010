>数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。
```
输入：n = 3
输出：[
       "((()))",
       "(()())",
       "(())()",
       "()(())",
       "()()()"
     ]
```


### c plus

***

* 递归
```c
/* 括号的判断条件：
** left <= n, n表示括号的个数
** right <= left
*/

class Solution {
public:
    vector<string> res;
    vector<string> generateParenthesis(int n) { 
        generate(0, 0, n, "");
        return res;
    }

    void generate(int left, int right, int n, string s) {
        //终止
        if (left == n && right == n) {
            res.push_back(s);
        }
        //本层处理
        if (left < n) generate(left + 1, right, n, s + "(");
        //先走到底画完左括号，返回的时候left = 2 // left = 1，会执行下面的语句画右括号
        if (right < left) generate(left, right + 1, n, s + ")");
        
    }
};
```
* 递归，先画完整的括号
```c
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> res;
        addingpar(res, n, 0, "", );
        return res;
    }
    void addingpar(vector<string>& v, int left, int right, string str){
        if(left==0 && right==0) {
            v.push_back(str);
            return;
        }
        if(m > 0) addingpar(v, left, right - 1, str + ")"); 
        if(n > 0) addingpar(v, left - 1, right + 1, str + "(");//画了一个左括号后就画右括号
    }
};

```



***

### Golang
***

* 练习

```go
var res []string
func generateParenthesis(n int) []string {
    res = make([]string, 0, n)
    generate(0, 0, n, "")
    return res
}

func generate(left int, right int, n int, s string) {
    if left == n && right == n {
      res = append(res, s)
    }

    if left < n {
        generate(left + 1, right, n, s + "(")
    }
    if right < left {
        generate(left, right + 1, n, s + ")")
    }

}
```

***