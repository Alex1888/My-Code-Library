### 带返回值的情况
* 例题 [690. Employee Importance](https://leetcode.com/problems/employee-importance/)
* 实际上是遍历一条路径到头,因为没办法给出退出条件;

```c++
class Solution {
public:
    int getImportance(vector<Employee*> employees, int id) {
        unordered_map<int, Employee*> map;
        for(auto e : employees) map[e->id] = e;
        return dfs(map, id);
    }

     int dfs(unordered_map<int, Employee*>& map, int id){
        int res =0;
        res += map[id]->importance;
        for(auto i : map[id]->subordinates){
            res += dfs(map, i);
        }

         return res;
    }
};

```
* 类似的[366. Find Leaves of Binary Tree](https://leetcode.com/problems/find-leaves-of-binary-tree/description/)
* 能给出退出条件,实际上就退化成了普通递归

```c++
class Solution {
public:
    vector<vector<int>> findLeaves(TreeNode* root) {
        vector<vector<int>> res;
        while(root){
            vector<int> leaves;
            root=remove(root, leaves);
            res.push_back(leaves);
        }
        return res;
    }
    
private:
    TreeNode* remove(TreeNode* root, vector<int>& leaves){
        if(root == NULL) return NULL;
        if(root->left == NULL && root->right == NULL){
            leaves.push_back(root->val);
            return NULL;
        }
        
        root->left = remove(root->left, leaves);
        root->right = remove(root->right, leaves);
        return root;
    }
};

```
* 带返回值的[698. Partition to K Equal Sum Subsets](https://leetcode.com/problems/partition-to-k-equal-sum-subsets/)

### 标准DFS,不需要回溯的
* https://github.com/Alex1888/Leetcode/blob/master/CPP/399.%20Evaluate%20Division.md

### 需要定义visited的
* 例题:[787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)
* 因为每一层有可能遍历到上一层的重复的点; 而且visited是在for的外层更新,因为下一层遍历时的先决条件就是当前的s已经被访问过
* 说白了这道题是在层与层之间做backtracing

```c++
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int K) {
        unordered_map<int, vector<pair<int, int>>> g;
        for(auto f : flights){
            g[f[0]].push_back(make_pair(f[1], f[2])); 
        }
        
        int res = INT_MAX;
        vector<bool> visited(n, false);
        dfs(g, src, dst, K+1, 0, res, visited);
        
        return res == INT_MAX ?  -1 : res;
    }
    
    void dfs(unordered_map<int, vector<pair<int, int>>>& g, int s, int d, 
             int level, int cur, int&res, vector<bool>& visited){
        if(s == d){
            res = min(cur, res);
            return;
        }
        
        if(level == 0) return;
        
        visited[s] = true;
        
        for(auto p : g[s]){
            int tmp = cur + p.second;
            if(tmp > res) continue;
            dfs(g, p.first, d, level-1, tmp, res, visited);
        }
        
        visited[s] = false;
    }
};

```

### 不需要visited的.
* 例如[Menu Combination](https://github.com/Alex1888/InterviewProblems/blob/master/Airbnb/Menu%20Combination%20Sum/main.cpp)
* 因为每次从start开始,顺序遍历,不可能访问到已经访问过的上层的节点
* 而这道题是在for里面进行backtracing,是在每层的中间的每个元素之间进行回溯

```c++
/*
 * 给一个菜单,和一个target金额,要求输出所有能点的不同的组合,要求用完所有钱
Given a menu (list of items prices), find all possible combinations of items that sum a particular value K.
(A variation of the typical 2sum/Nsum questions).
Return the coins combination with the minimum number of coins. Time complexity O(MN), where M is
the target value and N is the number of distinct coins. Space complexity O(M).
 * 
 * 这道题的dfs不需要从每个index开始,因为是从一个index开始,把所有以它开始的组合都找完,然后再从下一个index开始.
 *
 */
class MenuCombination{
public:
    double precision = 0.000001;
    vector<vector<double>> solve(vector<double>& menu, double target){
        vector<vector<double>> res;
        vector<double> cur;
        sort(menu.begin(), menu.end());

        double curPrice = 0;
        dfs(menu, 0, res, cur, target, curPrice);
        return res;
    }

    // 注意for循环一定要在dfs里.因为对于每个点,都要遍历和他所有相邻的点; 而设置start和排序,只是剪枝的一种方法
    void dfs(vector<double>& menu, int start, vector<vector<double>>& res, vector<double>& cur, double target, double curPrice){
        if(abs(curPrice - target) < precision){
            res.push_back(cur);
            return;
        }

        for(int i=start; i<menu.size(); i++){
            // 这里注意要从i>start开始,而不是i>0;因为我们的目的就是避开start,让start能顺序进入cur;
            // 说白了就是:在当前层,在与start相同的点中.只让start一个进入遍历序列; 而其他的点即使和start相同,也等到再下一层遍历
            // 比如test2中 {10,1,2,7,6,1,5,1,1}; 第一次只让start=1的第一个1进入,然后它就会遍历出[1,1,1,5]这个结果
            // 把这里注释掉,就可以允许不同位置的同样的值的结果同时存在,比如test2中会出现多个[1,1,1,5],里面的1代表不同的菜
            if(i != start && menu[i] == menu[i-1]) {
                continue;
            }

            // 当前值再加上menu[i]大于target,提早结束
            if(curPrice + menu[i] - target > precision) {
                break;
            }

            cur.push_back(menu[i]); //注意是加menu[i],而不是menu[start]
            dfs(menu, i+1, res, cur, target, curPrice + menu[i]);
            cur.pop_back();
        }
    }
};
```

* 典型例题
* [254. Factor Combinations](https://leetcode.com/problems/factor-combinations/)
* [46. Permutations](https://leetcode.com/problems/permutations/)
* [47. Permutations II](https://leetcode.com/problems/permutations-ii/)
