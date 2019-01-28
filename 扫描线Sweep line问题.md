### 扫描线问题
# [218. The Skyline Problem](https://leetcode.com/problems/the-skyline-problem/)
* 看九章的视频NineChapter04看到的扫描线问题
* 题目的意思是给出每栋楼的起点终点,让你画出所有楼的全景图
* 思路就是从左往右扫描. 保持一个heap保存当前的最高点, 每到一个特殊点更新最高点
* 这个图画的最清晰 https://briangordon.github.io/2014/08/the-skyline-problem.html
* 高票答案用的是mutliset, 这个就相当于一个带删除的priority_queue, 因为默认是排好序的,并且好删除

```c++

class Solution {
public:
    vector<pair<int, int>> getSkyline(vector<vector<int>>& buildings) {
        vector<pair<int, int>> heights;
        for(auto b : buildings){
            heights.push_back({b[0], -b[2]}); //负数表示左节点
            heights.push_back({b[1], b[2]}); //正数表示右节点
        }
        
        sort(heights.begin(), heights.end());
        multiset<int> m;
        m.insert(0);
        
        int pre = 0, cur =0;
        vector<pair<int,int>> res;     
        for(auto h : heights){
            if(h.second < 0){
                m.insert(-h.second);
            }else{
                auto iter = m.find(h.second);
                m.erase(iter);
            }
            
            auto iter = m.end();
            iter--;
            cur = *iter; //最右边是当前最大值
            if(cur != pre){
                res.push_back({h.first, cur});
                pre = cur;
            }
        }
        
        return res;
    }
};
```

* 最开始按照这个思路自己写的,用了priority_queue, 要在中间频繁更新队列,所以非常慢,beat 1.2%
* 但是思路是一样的

```c++
class Solution {
public:
    vector<pair<int, int>> getSkyline(vector<vector<int>>& buildings) {
        vector<pair<int, int>> heights;
        for(auto b : buildings){
            heights.push_back({b[0], -b[2]}); //负数表示左节点
            heights.push_back({b[1], b[2]}); //正数表示右节点
        }
        
        sort(heights.begin(), heights.end());
        priority_queue<int> q;
        q.push(0);
        
        int pre = 0;
        vector<pair<int,int>> res;       
        for(auto h : heights){
            if(h.second < 0){
                q.push(-h.second);
            }else{
                // h.second > 0表示右节点.说明一个楼已经走完了,需要把它出队
                vector<int> tmp;
                while(!q.empty() && (q.top() != h.second)){
                    //cout<<q.top()<<endl;
                    tmp.push_back(q.top());
                    q.pop();
                }
                q.pop();
                for(auto t : tmp) q.push(t);
            }
            int cur = q.top();
            if(cur != pre){
                res.push_back({h.first, cur});
                pre = cur;
            }
        }
        
        return res;
    }
};


```
