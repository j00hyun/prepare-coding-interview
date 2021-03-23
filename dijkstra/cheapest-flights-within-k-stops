# K 경유지 내 가장 저렴한 항공권 - leetcode 787

- 내 풀이
``` python
def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, K: int) -> int:
    flights_dict = collections.defaultdict(list)
    acc_flights_dict = collections.defaultdict(list)
    min_price = 10000 * (n*(n-1)/2) # 나올수 있는 최대 가격 

    # 시작점: (도착점, 가격) 인접리스트 구현
    for u, v, w in flights:
        flights_dict[u].append((v, w))

    # 경유횟수 0번인 경우 딕셔너리 셋팅
    for tpl in flights_dict[src]:
        acc_flights_dict[0].append(tpl)

    for via_num in range(K + 1):
        for start, acc_price in acc_flights_dict[via_num]:
            # 목적지가 일치하는 경우 최소가격 저장 
            if start == dst:
                min_price = min(min_price, acc_price)
                 
            # 최소가격보다 작은 경우만 골라 탐색 
            if min_price > acc_price:
                for arrive, price in flights_dict[start]:
                    acc_flights_dict[via_num + 1].append((arrive, acc_price + price))
         
    # 주어진 경유횟수 이내의 경로가 존재하지 않는 경우 
    if min_price == 10000 * (n*(n-1)/2):
        return -1

    return min_price
```

- 다른 풀이 (우선순위 큐를 이용하여 더 간단하게 구현)
``` python
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, K: int) -> int:
        graph = collections.defaultdict(list)
        # 그래프 인접 리스트 구성
        for u, v, w in flights:
            graph[u].append((v, w))

        # 큐 변수: [(가격, 정점, 남은 가능 경유지 수)]
        Q = [(0, src, K)]

        # 우선순위 큐 최솟값 기준으로 도착점까지 최소 비용 판별
        while Q:
            price, node, k = heapq.heappop(Q)

            if node == dst:
                return price

            if k >= 0:
                for v, w in graph[node]:
                    alt = price + w
                    heapq.heappush(Q, (alt, v, k-1))

        return -1
```
