* http://www.cplusplus.com/reference/queue/priority_queue/priority_queue/
* https://blog.csdn.net/txl199106/article/details/44588487
* 他的模板声明带有三个参数，priority_queue<Type, Container, Functional>
* Type 为数据类型， Container 为保存数据的容器，Functional 为元素比较方式。
Container 必须是用数组实现的容器，比如 vector, deque 但不能用 list.
STL里面容器默认用的是 vector. 比较方式默认用 operator< , 所以如果你把后面俩个参数 缺省的话，优先队列就是大顶堆，队头元素最大。
* C++默认是最大堆,即值大的排在前面
* 例子: https://leetcode.com/problems/top-k-frequent-elements/description/

```c++
class Solution {
public:
    struct compareNum{
        bool operator ()(pair<int, int>& a, pair<int, int>& b) { // return true if a ordered before b
            return a.second < b.second;
        }
    };
    
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> m;
        priority_queue<pair<int, int>, vector<pair<int, int>>, compareNum> pq;
        
        for(int i=0; i<nums.size(); i++){
            if(m.count(nums[i]) == 0){
                m[nums[i]] = 1;
            }else{
                m[nums[i]]++;
            }
        }
        
        for(auto it : m){
            pq.push(make_pair(it.first, it.second));
        }
     
        vector<int> res;
        for(int i=0; i<k; i++){
            res.push_back(pq.top().first); pq.pop();
        }
        
        return res;
    }
}; 
```
* (比较函数)[https://blog.csdn.net/u014644714/article/details/68924863]: 如果a排在b的前面,返回true; 所以上面例子中实际是最小堆,值小的排在前面,相当于默认的greater
* 如果要用到小顶堆，则一般要把模板的三个参数都带进去。STL里面定义了一个仿函数 greater<>，对于基本类型可以用这个仿函数声明小顶堆
* 例子

```c++

#include <iostream>
#include <queue>
using namespace std;
int main(){
    priority_queue<int,vector<int>,greater<int> >q;
    for(int i=0;i<10;i++) 
		q.push(i);
    while(!q.empty()){
        cout<<q.top()<< endl;
        q.pop();
    }
    return 0;
}
```



