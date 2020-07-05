# leetcode_515. 在每个树行中找最大值

您需要在二叉树的每一行中找到最大的值。
示例：
输入:
```
1
     / \
    3   2
   / \   \  
  5   3   9
```
输出: [1, 3, 9]
### golang

---

- BFS
套BFS模板即可，需要注意max初始化为int的最小值
```
func largestValues(root *TreeNode) []int {
    if root == nil {
        return []int{}
    }
    //广度优先
    maxRes := make([]int, 0)
    queue := make([]*TreeNode, 0)
    queue = append(queue, root)
    for len(queue) > 0 {
        //处理当前层
        var maxLevel int
        l := len(queue)
        maxLevel = -1 << 63           //注意需要初始化为最小值
        fmt.Println(maxLevel)
        for i := 0; i < l; i++ {
            //处理当前层节点
            cur := queue[i]
            if maxLevel < cur.Val {
                maxLevel = cur.Val
            }
            if cur.Left != nil { //添加下一层几点
                queue = append(queue, cur.Left)
            }
            if cur.Right != nil {
                queue = append(queue, cur.Right)
            }
        }
        maxRes = append(maxRes, maxLevel)//处理当前层结果
        queue = queue[l:]//当前层出队列
    }
    return maxRes
}
```

---

%E6%82%A8%E9%9C%80%E8%A6%81%E5%9C%A8%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%AF%8F%E4%B8%80%E8%A1%8C%E4%B8%AD%E6%89%BE%E5%88%B0%E6%9C%80%E5%A4%A7%E7%9A%84%E5%80%BC%E3%80%82%0A%E7%A4%BA%E4%BE%8B%EF%BC%9A%0A%0A%E8%BE%93%E5%85%A5%3A%20%0A%0A%20%20%20%20%20%20%20%20%20%201%0A%20%20%20%20%20%20%20%20%20%2F%20%5C%0A%20%20%20%20%20%20%20%203%20%20%202%0A%20%20%20%20%20%20%20%2F%20%5C%20%20%20%5C%20%20%0A%20%20%20%20%20%205%20%20%203%20%20%209%20%0A%0A%E8%BE%93%E5%87%BA%3A%20%5B1%2C%203%2C%209%5D%0A%0A%23%23%23%20golang%0A%0A*%20*%20*%0A%0A*%20BFS%0A%20%20%20%20%E5%A5%97BFS%E6%A8%A1%E6%9D%BF%E5%8D%B3%E5%8F%AF%EF%BC%8C%E9%9C%80%E8%A6%81%E6%B3%A8%E6%84%8Fmax%E5%88%9D%E5%A7%8B%E5%8C%96%E4%B8%BAint%E7%9A%84%E6%9C%80%E5%B0%8F%E5%80%BC%0A%60%60%60go%0Afunc%20largestValues(root%20*TreeNode)%20%5B%5Dint%20%7B%0A%20%20%20%20if%20root%20%3D%3D%20nil%20%7B%0A%20%20%20%20%20%20%20%20return%20%5B%5Dint%7B%7D%0A%20%20%20%20%7D%0A%20%20%20%20%2F%2F%E5%B9%BF%E5%BA%A6%E4%BC%98%E5%85%88%0A%20%20%20%20maxRes%20%3A%3D%20make(%5B%5Dint%2C%200)%0A%20%20%20%20queue%20%3A%3D%20make(%5B%5D*TreeNode%2C%200)%0A%20%20%20%20queue%20%3D%20append(queue%2C%20root)%0A%20%20%20%20for%20len(queue)%20%3E%200%20%7B%0A%20%20%20%20%20%20%20%20%2F%2F%E5%A4%84%E7%90%86%E5%BD%93%E5%89%8D%E5%B1%82%0A%20%20%20%20%20%20%20%20var%20maxLevel%20int%0A%20%20%20%20%20%20%20%20l%20%3A%3D%20len(queue)%0A%20%20%20%20%20%20%20%20maxLevel%20%3D%20-1%20%3C%3C%2063%20%20%20%20%20%20%20%20%20%20%20%2F%2F%E6%B3%A8%E6%84%8F%E9%9C%80%E8%A6%81%E5%88%9D%E5%A7%8B%E5%8C%96%E4%B8%BA%E6%9C%80%E5%B0%8F%E5%80%BC%0A%20%20%20%20%20%20%20%20fmt.Println(maxLevel)%0A%20%20%20%20%20%20%20%20for%20i%20%3A%3D%200%3B%20i%20%3C%20l%3B%20i%2B%2B%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%2F%2F%E5%A4%84%E7%90%86%E5%BD%93%E5%89%8D%E5%B1%82%E8%8A%82%E7%82%B9%0A%20%20%20%20%20%20%20%20%20%20%20%20cur%20%3A%3D%20queue%5Bi%5D%0A%20%20%20%20%20%20%20%20%20%20%20%20if%20maxLevel%20%3C%20cur.Val%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20maxLevel%20%3D%20cur.Val%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20if%20cur.Left%20!%3D%20nil%20%7B%20%2F%2F%E6%B7%BB%E5%8A%A0%E4%B8%8B%E4%B8%80%E5%B1%82%E5%87%A0%E7%82%B9%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20queue%20%3D%20append(queue%2C%20cur.Left)%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20if%20cur.Right%20!%3D%20nil%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20queue%20%3D%20append(queue%2C%20cur.Right)%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20maxRes%20%3D%20append(maxRes%2C%20maxLevel)%2F%2F%E5%A4%84%E7%90%86%E5%BD%93%E5%89%8D%E5%B1%82%E7%BB%93%E6%9E%9C%0A%20%20%20%20%20%20%20%20queue%20%3D%20queue%5Bl%3A%5D%2F%2F%E5%BD%93%E5%89%8D%E5%B1%82%E5%87%BA%E9%98%9F%E5%88%97%0A%20%20%20%20%7D%0A%20%20%20%20return%20maxRes%0A%7D%0A%60%60%60%0A%0A*%20*%20*%0A
