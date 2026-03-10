class Solution:
    def isCyclic(self, V, edges):
        # 1. Build Adjacency List from the Edge List
        adj = [[] for _ in range(V)]
        for u, v in edges:
            adj[u].append(v)
            
        visited = [0] * V # 0: unvisited, 1: visiting, 2: visited
        
        # 2. Iterative DFS to handle large V without recursion limits
        for i in range(V):
            if visited[i] == 0:
                stack = [(i, 0)] # (node, neighbor_index)
                while stack:
                    u, idx = stack[-1]
                    
                    if idx == 0:
                        visited[u] = 1 # Mark as visiting (in recursion stack)
                    
                    found_unvisited = False
                    for next_idx in range(idx, len(adj[u])):
                        v = adj[u][next_idx]
                        
                        if visited[v] == 1: # Cycle detected
                            return True
                        if visited[v] == 0:
                            # Pause current node, move to neighbor
                            stack[-1] = (u, next_idx + 1)
                            stack.append((v, 0))
                            found_unvisited = True
                            break
                    
                    if not found_unvisited:
                        visited[u] = 2 # Mark as fully explored
                        stack.pop()
                        
        return False

