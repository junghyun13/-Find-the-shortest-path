# -Find-the-shortest-path
# In some countries there are cities 1 through N and M one-way roads. All roads have a distance of 1. If you enter the number of cities N, the number of roads M, distance information K, and the number X of the city of departure in the first line, a one-way direction is drawn between A and B randomly from the second line to M lines. Among the possible cities, print the city number with the shortest distance K, or -1 if it does not exist! 어떤 나라에는 1번부터 N번까지의 도시와 M개의 단방향 도로가 존재한다. 모든 도로의 거리는 1이다. 첫째 줄에 도시의 개수 N, 도로의 개수 M, 거리 정보 K, 출발 도시의 번호 X를 입력하면 둘째 줄부터 M개의 줄에 걸쳐서 임의의 A와 B사이에 단방향이 그어지는데 X로부터 출발하여 도달할 수 있는 도시 중에서, 최단 거리가 K인 도시번호를 출력하고 존재하지 않으면 -1을 출력해라!
''''import heapq
a=[5,4,3,2,1]
heapq.heappop(a)
print(a)-->[1, 4, 3, 2]
heapq.heappush(a,9)
print(a)-->[1, 4, 3, 2, 9]
heapq.heappush(a,8)
print(a)-->[1, 4, 3, 2, 9, 8]''''
import sys
from heapq import heappop, heappush
input = sys.stdin.readline
inf = sys.maxsize
n, m, k, x = map(int, input().split())
graph = [[] for _ in range(n + 1)]
dp = [inf] * (n + 1)
heap = []
def dijkstra(start):
    heappush(heap, [0, start])
    dp[start] = 0
    while heap:
        w, n = heappop(heap) 
        for n_n, wei in graph[n]: 
            n_w = wei + w
            if n_w < dp[n_n]:
                dp[n_n] = n_w
                heappush(heap, [n_w, n_n]) #가장 가까이 오는 수 찾기
for _ in range(m):
    a, b = map(int, input().split())
    graph[a].append([b, 1])
dijkstra(x)
ans = []
for i in range(1, n + 1):
    if dp[i] == k:
        ans.append(i)
if ans:
    for i in ans:
        print(i)
else:
    print(-1)
#input-->4 4 2 1  1 2  1 3  2 3  2 4
#result-->4
