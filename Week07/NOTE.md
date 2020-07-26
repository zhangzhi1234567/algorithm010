双向BFS模板

```c++
    unordered_set<string> beginSet, endSet, visited, tmp;//set代替queue，因为set查找的时间复杂度为O(1)
    beginSet.insert(beginWord);
    endSet.insert(endWord);
    //bfs start here
    while(!beginSet.empty() && !endSet.empty()) {
        if (beginSet.size() > endSet.size()) {
            tmp = beginSet;
            beginSet = endSet;
            endSet = tmp;
        }
        tmp.clear();
        //处理当前层
        for (string curWord : beginSet) { 
            //这里处理相关逻辑   
            if (endSet.find(curWord) != endSet.end()) {
                //结束;
            }
            if (visited.find(otherWord) == visited.end()) { //other来源于curWord,如果得到根据相关题目确定
                visited.insert(otherWord);
                tmp.insert(otherWord); //如果当前节点没有使用过，添加到下一层去。
            }
        }
        beginSet = tmp; //当前层遍历完，清空，继续下一层遍历。 因为没有queue的出队，所以直接和一个set交换；
    }

```

