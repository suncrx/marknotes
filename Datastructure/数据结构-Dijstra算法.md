Dijkstra算法是由荷兰计算机科学家艾兹格·迪科斯彻（Edsger Wybe Dijkstra）在1959年提出的一种经典的图论算法，用于在带权有向图中找到从一个给定源顶点到其他所有顶点的最短路径。 

### 算法思想 
- 该算法使用了贪心算法的策略，以源点为中心，逐步向外扩展，每次找到离源点最近的未访问顶点，并更新从源点到其他顶点的最短距离。 
- 它维护两个集合，一个是已确定最短路径的顶点集合（记为S），另一个是未确定最短路径的顶点集合（记为U）。初始时，S中只包含源顶点，U包含除源顶点外的其他所有顶点。 

### 算法步骤 
1. 初始化： 
- 将源顶点到自身的距离设置为0，即`dist[source] = 0`，其中`dist`数组用于存储源顶点到各个顶点的最短距离。 
- 将源顶点到其他顶点的距离设置为无穷大，即`dist[v] = ∞`（v ≠ source）。 
- 源顶点加入集合S，即`S = {source}`，U为除源顶点外的其他所有顶点集合。 
2. 找最小距离顶点： 
- 在集合U中找到距离源顶点最近的顶点u，即`u = argmin{dist[v] | v ∈ U}`。 
- 将顶点u加入集合S，即`S = S ∪ {u}`，同时将其从U中移除，`U = U - {u}`。 
3. 更新距离： 
- 对于与顶点u相邻的所有未访问顶点v（v ∈ U），如果`dist[u] + weight(u, v) < dist[v]`，则更新`dist[v]`的值为`dist[u] + weight(u, v)`，其中`weight(u, v)`表示边(u, v)的权值。 
4. 重复步骤2和3，直到集合U为空，此时`dist`数组中存储的就是源顶点到其他所有顶点的最短距离。 

### 代码示例（Python实现） 

```python 
import heapq 
def dijkstra(graph, start): 
	distances = {node: float('inf') for node in graph} distances[start] = 0 priority_queue = [(0, start)] 
	while priority_queue: 
		current_distance, current_node = heapq.heappop(priority_queue) if current_distance > distances[current_node]: continue for neighbor, weight in graph[current_node].items(): distance = current_distance + weight if distance < distances[neighbor]: distances[neighbor] = distance heapq.heappush(priority_queue, (distance, neighbor)) return distances graph = { 'A': {'B': 1, 'C': 4}, 'B': {'A': 1, 'C': 2, 'D': 5}, 'C': {'A': 4, 'B': 2, 'D': 1}, 'D': {'B': 5, 'C': 1} } start_node = 'A' result = dijkstra(graph, start_node) print(f"从节点 {start_node} 到各节点的最短距离: {result}")
``` 

### 复杂度分析 
- **时间复杂度**：如果使用邻接矩阵存储图，每次查找未访问顶点中的最小距离顶点需要遍历所有顶点，时间复杂度为 $O(V^2)$，其中 $V$ 是顶点数。如果使用邻接表存储图，并使用优先队列（如堆）来优化查找最小距离顶点的操作，时间复杂度为 $O((V + E)\log V)$，其中 $E$ 是边数。
- **空间复杂度**：算法需要存储每个顶点的最短距离和访问状态等信息，空间复杂度为 $O(V)$。 

### 应用场景 
- **路径规划**：在地图导航中，计算从一个地点到其他地点的最短驾车或步行路线。 
- **网络路由**：在计算机网络中，确定数据包从源节点到目标节点的最佳传输路径。 
- **任务调度**：在项目管理中，安排任务的执行顺序，以最小化总完成时间。
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM5NzQ4NTE5NV19
-->