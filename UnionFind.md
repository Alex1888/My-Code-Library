# UnionFind

* 最简单标准模板:题目[684. Redundant Connection](https://leetcode.com/problems/redundant-connection/description/)

```c++
class DisjoinSet {
private:
    vector<int> parent;
    
public:
    DisjoinSet(int n){
        parent = vector<int>(n+1, 0);
        for(int i =1; i<=n; i++) parent[i] = i;
    }
    
    void Union(int n1, int n2){
        int root1 = Find(n1); // 注意这里是find,而不是用parent[n1]
        int root2 = Find(n2);
        parent[root2] = root1; // 这里把root2赋给root1也可以
    } 
    
    int Find(int x){
        // 因为所有的点都在包含在[0,n]范围你,并且初始时都是自己是自己的parent,所以能保证最后肯定能跳出循环
        while(x != parent[x]){
            x = parent[x];
        }
        return x;
    }
};

class Solution {
public:
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        int n = edges.size();
        DisjoinSet djs(n);
        for(auto edge : edges){
            int u = edge[0];
            int v = edge[1];
            if(djs.Find(u) == djs.Find(v)){
                return edge;
            }
            else{
                djs.Union(u, v);
            }
        }
        return vector<int>();
    }
};

```

* 花花讲解: https://www.youtube.com/watch?v=VJnUwsE4fWA&t=749s

