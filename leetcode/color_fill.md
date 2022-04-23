
# bfs方法实现
from queue import Queue
class Solution:
    def floodFill(self, image: List[List[int]], sr: int, sc: int, newColor: int) -> List[List[int]]:
        # 起始颜色和目标颜色相同，则直接返回原图
        if image[sr][sc] == newColor:
            return image
        # 初始化一个队列并将初始坐标入队列
        que = Queue()
        que.put((sr, sc))
        # 记录初始颜色
        originalcolor = image[sr][sc]
        # 四个方向的偏移值（上下左右）
        directions = [(0, -1), (0, 1), (-1, 0), (1, 0)]
        # 开始BFS
        while not que.empty():
            point = que.get() # 取出队头结点
            # if image[point[0]][point[1]] == originalcolor: # 这个判断其实不需要
            #     image[point[0]][point[1]] == newColor
            image[point[0]][point[1]] = newColor
            for i in directions:
                new_i = point[0] + i[0]
                new_j = point[1] + i[1]
                if 0 <= new_i < len(image) and 0 <= new_j < len(image[0]) and image[new_i][new_j] == originalcolor:
                    que.put((new_i,new_j))
        return image

# dfs方法实现