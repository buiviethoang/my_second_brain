2025-09-22 22:01
Status: 
Topic: 
Tags: [[algorithm]]
## Main
A **pattern notebook** is the single most powerful tool in competitive programming.  
The idea: whenever you solve a problem (or read an editorial), instead of just saying _“ok I get it”_, you **extract the reusable pattern** in 2–5 sentences.  
Over time, this notebook becomes your **playbook** — in contests, you’ll recognize problems instantly (“aha, this is sliding window + hash map”).

Each note = **When to use + Template + Pitfalls + Example LeetCode IDs**.  
You can keep this as a **master reference** during your 3-month plan.

## **1. Two Pointers**

**When:** Sorted arrays/strings, pairs/triplets, palindrome check.

```java
int l = 0, r = nums.length - 1;
while (l < r) {
    int sum = nums[l] + nums[r];
    if (sum == target) { l++; r--; }
    else if (sum < target) l++;
    else r--;
}
```

⚠️ Pitfall: Infinite loop if pointers don’t move.  
📌 Examples: LC 167, LC 125, LC 15

## **2. Sliding Window**

**When:** Subarray/substring with constraint (“longest”, “smallest”, “at most K”).

```java
int l = 0;
Map<Character,Integer> window = new HashMap<>();
for (int r = 0; r < s.length(); r++) {
    char c = s.charAt(r);
    window.put(c, window.getOrDefault(c, 0) + 1);

    while (/* invalid */) {
        char d = s.charAt(l);
        window.put(d, window.get(d) - 1);
        l++;
    }
    // update answer
}

```

⚠️ Pitfall: Off-by-one errors.  
📌 Examples: LC 3, LC 76, LC 209

## **3. Binary Search**

**When:** Sorted arrays, monotonic conditions.
```java
int l = 0, r = nums.length - 1;
while (l <= r) {
    int mid = l + (r - l) / 2;
    if (nums[mid] == target) return mid;
    else if (nums[mid] < target) l = mid + 1;
    else r = mid - 1;
}

```

⚠️ Pitfall: Wrong mid update → infinite loop.  
📌 Examples: LC 704, LC 875, LC 410

## **4. Prefix Sum**

**When:** Range queries, subarray sum.
```java
int[] prefix = new int[nums.length + 1];
for (int i = 0; i < nums.length; i++)
    prefix[i+1] = prefix[i] + nums[i];
// sum[i..j] = prefix[j+1] - prefix[i]
```

⚠️ Pitfall: Indexing.  
📌 Examples: LC 560, LC 303, LC 238

## **5. Hash Map / Hash Set**

**When:** Count freq, check existence, avoid O(n²).

```java
Map<Integer,Integer> map = new HashMap<>();
for (int x : nums)
    map.put(x, map.getOrDefault(x, 0) + 1);
```

📌 Examples: LC 1, LC 49, LC 347


## **6. Sorting + Greedy**

**When:** Intervals, scheduling, minimizing resources.
```java
Arrays.sort(intervals, (a, b) -> a[1] - b[1]);
int end = Integer.MIN_VALUE, count = 0;
for (int[] iv : intervals) {
    if (iv[0] >= end) {
        count++;
        end = iv[1];
    }
}
```
📌 Examples: LC 435, LC 452, LC 55

## **7. Stack (Monotonic)**

**When:** Next greater/smaller element, histogram, stock span.
```java
Stack<Integer> st = new Stack<>();
for (int i = 0; i < n; i++) {
    while (!st.isEmpty() && nums[st.peek()] <= nums[i]) {
        st.pop();
    }
    st.push(i);
}
```
📌 Examples: LC 84, LC 739, LC 496

## **8. Heap / Priority Queue**

**When:** Top K, running median, scheduling.

```java
PriorityQueue<Integer> pq = new PriorityQueue<>((a,b) -> b - a); // max-heap
pq.offer(x);
pq.poll();
```

📌 Examples: LC 215, LC 295, LC 502

## **9. BFS (Queue)**

**When:** Shortest path in unweighted graph, level traversal.

```java
Queue<Integer> q = new LinkedList<>();
boolean[] visited = new boolean[n];
q.offer(start); visited[start] = true;

while (!q.isEmpty()) {
    int u = q.poll();
    for (int v : graph[u]) {
        if (!visited[v]) {
            visited[v] = true;
            q.offer(v);
        }
    }
}
```

📌 Examples: LC 200, LC 994, LC 127

## **10. DFS (Recursion / Stack)**

**When:** Connected components, trees, backtracking.
```java
void dfs(int u) {
    visited[u] = true;
    for (int v : graph[u]) {
        if (!visited[v]) dfs(v);
    }
}
```
📌 Examples: LC 547, LC 695, LC 79

## **11. Union-Find (Disjoint Set Union)**

**When:** Connected components, Kruskal MST.

```java
class DSU {
    int[] parent, rank;
    DSU(int n) {
        parent = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++) parent[i] = i;
    }
    int find(int x) {
        if (x != parent[x]) parent[x] = find(parent[x]);
        return parent[x];
    }
    void union(int x, int y) {
        int rx = find(x), ry = find(y);
        if (rx == ry) return;
        if (rank[rx] < rank[ry]) parent[rx] = ry;
        else if (rank[rx] > rank[ry]) parent[ry] = rx;
        else { parent[ry] = rx; rank[rx]++; }
    }
}
```

📌 Examples: LC 684, LC 721, LC 128

## **12. Topological Sort**

**When:** DAG, scheduling tasks, course schedule.

```java
Queue<Integer> q = new LinkedList<>();
int[] indegree = new int[n];
for (int u = 0; u < n; u++)
    for (int v : graph[u]) indegree[v]++;
for (int i = 0; i < n; i++)
    if (indegree[i] == 0) q.offer(i);

while (!q.isEmpty()) {
    int u = q.poll();
    for (int v : graph[u]) {
        if (--indegree[v] == 0) q.offer(v);
    }
}
```

📌 Examples: LC 207, LC 210, LC 269

## **13. Dijkstra’s Algorithm**

**When:** Shortest path (weighted graph, no negative weights).

```java
PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[1]-b[1]);
int[] dist = new int[n]; Arrays.fill(dist, INF);
dist[start] = 0;
pq.offer(new int[]{start, 0});

while (!pq.isEmpty()) {
    int[] cur = pq.poll();
    int u = cur[0], d = cur[1];
    if (d > dist[u]) continue;
    for (int[] e : graph[u]) {
        int v = e[0], w = e[1];
        if (dist[u] + w < dist[v]) {
            dist[v] = dist[u] + w;
            pq.offer(new int[]{v, dist[v]});
        }
    }
}
```

📌 Examples: LC 743, LC 1631, LC 1514

## **14. Floyd-Warshall**

**When:** All-pairs shortest path, small graph.

```java
for (int k = 0; k < n; k++)
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);

```

📌 Examples: LC 1334, LC 1144

## **15. Dynamic Programming (Classic)**

**When:** Optimal substructure + overlapping subproblems.

**0/1 Knapsack:**

```java
int[][] dp = new int[n+1][W+1];
for (int i = 1; i <= n; i++) {
    for (int w = 0; w <= W; w++) {
        dp[i][w] = dp[i-1][w];
        if (w >= wt[i-1])
            dp[i][w] = Math.max(dp[i][w], dp[i-1][w-wt[i-1]]+val[i-1]);
    }
}
```

**Pitfalls:** Memory usage → optimize with 1D dp.  
📌 Examples: LC 322, LC 518, LC 494


## **16. Backtracking**

**When:** Generate all solutions (subsets, permutations, N-Queens).

```java
void backtrack(List<Integer> cur, boolean[] used) {
    if (cur.size() == n) {
        ans.add(new ArrayList<>(cur));
        return;
    }
    for (int i = 0; i < n; i++) {
        if (used[i]) continue;
        used[i] = true;
        cur.add(nums[i]);
        backtrack(cur, used);
        cur.remove(cur.size()-1);
        used[i] = false;
    }
}
```

📌 Examples: LC 46, LC 78, LC 51

## **17. Bitmask DP**

**When:** Subset problems, TSP, state compression.

```java
int[][] dp = new int[1<<n][n];
for (int mask = 0; mask < (1<<n); mask++) {
    for (int u = 0; u < n; u++) {
        if ((mask & (1<<u)) == 0) continue;
        for (int v = 0; v < n; v++) {
            if ((mask & (1<<v)) != 0) continue;
            dp[mask | (1<<v)][v] =
                Math.min(dp[mask | (1<<v)][v], dp[mask][u] + cost[u][v]);
        }
    }
}

```

📌 Examples: LC 847, LC 1125

## **18. Binary Search on Answer**

**When:** Min/max feasible value.  
(covered in #3 template).  
📌 Examples: LC 875, LC 1011, LC 1552

## **19. Divide & Conquer**

**When:** Merge Sort, Quick Sort, median of two arrays.
```java
void mergeSort(int[] arr, int l, int r) {
    if (l >= r) return;
    int mid = (l + r) / 2;
    mergeSort(arr, l, mid);
    mergeSort(arr, mid+1, r);
    merge(arr, l, mid, r);
}

```

📌 Examples: LC 23, LC 493

## **20. Math + Number Theory**

**When:** GCD/LCM, modular arithmetic, primes.

```java
int gcd(int a, int b) {
    return b == 0 ? a : gcd(b, a % b);
}
```

📌 Examples: LC 204, LC 869, LC 780


## References