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
def dijkstra(graph, source): 
	# 初始化距离字典，将所有顶点的距离设为无穷大 
	dist = {vertex: float('inf') for vertex in graph} 
	# 源顶点到自身的距离为0 
	dist[source] = 0 
	# 优先队列，存储待处理的顶点和距离 
	pq = [(0, source)] 
	while pq: 
	# 取出距离最小的顶点及其距离 
	current_dist, current_vertex = heapq.heappop(pq) 
	# 如果当前距离大于已记录的距离，跳过 
	if current_dist > dist[current_vertex]: 
		continue 
	# 遍历当前顶点的邻居 
	for neighbor, weight in graph[current_vertex].items(): 
		# 计算到邻居的新距离 
		distance = current_dist + weight 
		# 如果新距离更短，更新距离并将邻居加入优先队列 
		if distance < dist[neighbor]: 
			dist[neighbor] = distance 
			heapq.heappush(pq, (distance, neighbor)) 
	return dist 
	# 示例图 
	graph = { 'A': {'B': 5, 'C': 2}, 
	'B': {'A': 5, 'C': 1, 'D': 3}, 'C': {'A': 2, 'B': 1, 'D': 6}, 'D': {'B': 3, 'C': 6} } source_vertex = 'A' shortest_distances = dijkstra(graph, source_vertex) print("从源顶点", source_vertex, "到其他顶点的最短距离：", shortest_distances)
``` 

### 复杂度分析 
- **时间复杂度**：如果使用邻接矩阵存储图，每次查找未访问顶点中的最小距离顶点需要遍历所有顶点，时间复杂度为 $O(V^2)$，其中 $V$ 是顶点数。如果使用邻接表存储图，并使用优先队列（如堆）来优化查找最小距离顶点的操作，时间复杂度为 $O((V + E)\log V)$，其中 $E$ 是边数。
- **空间复杂度**：算法需要存储每个顶点的最短距离和访问状态等信息，空间复杂度为 $O(V)$。 

### 应用场景 
- **路径规划**：在地图导航中，计算从一个地点到其他地点的最短驾车或步行路线。 
- **网络路由**：在计算机网络中，确定数据包从源节点到目标节点的最佳传输路径。 
- **任务调度**：在项目管理中，安排任务的执行顺序，以最小化总完成时间。
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1ODczNzM4N119
-->