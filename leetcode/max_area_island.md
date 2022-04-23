
出现错误：通过案例529/728
```python 
from queue import Queue
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        # 广度优先算法与深度优先算法都可以解决，首先尝试广度优先
        # 对于遍历到的岛屿将之设置为0，避免重复遍历
        max_land = 0 # 记录当前最大岛屿
        directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
        def bfs(x, y):
            que = Queue()
            que.put((x, y))
            count = 1 # 记录包括(x, y)点的岛屿最大面积
            while not que.empty():
                point = que.get()
                grid[point[0]][point[1]] = 0 # 前面①处已经判断此处必为1 错误就出现在这里，每遍历一个点应该先将该点设置为0，否则会出现错误
                for direction in directions:
                    new_x = point[0] + direction[0]
                    new_y = point[1] + direction[1]
                    if 0 <= new_x < len(grid) and 0 <= new_y < len(grid[0]) and grid[new_x][new_y] == 1:
                        que.put((new_x, new_y))
                        count += 1
            return count

        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == 1: # ①
                    max_land = max(bfs(i, j), max_land)
        return max_land
```