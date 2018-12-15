* BFS用queue来实现, 在while循环里注意每次都要先出去q的size, 然后依次出队
* 求点到点最小值的题,一般都用BFS,典型例题:
* [815. Bus Routes](https://leetcode.com/problems/bus-routes/)
* [773. Sliding Puzzle](https://leetcode.com/problems/sliding-puzzle/)
* ** 上面两道题都是把某种状态或者点看做是图中的node,然后从这个状态所在的level一层一层往下遍历,所以一旦发现结果,那结果肯定是最小的路径;
* 所以每到都是在while循环里的for之外进行res++; 这里的res实际上就是层数
