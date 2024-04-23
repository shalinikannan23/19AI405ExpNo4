# EX-04 Implement A* Search Algorithm for a Graph
### Aim:
To Implement A* Search algorithm for a Graph using Python 3.

### Algorithm:
1. Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)
3.  while the open list is not empty
    - find the node with the least f on the open list, call it "q"
    - pop q off the open list
    - generate q's 8 successors and set their parents to q
    - for each successor
      - if successor is the goal, stop search    
      - else, compute both g and h for successor
        - successor.g = q.g + distance between successor and q
        - successor.h = distance from goal to successor (This can be done using many ways, we will discuss three heuristics- Manhattan, Diagonal and Euclidean Heuristics)
        - successor.f = successor.g + successor.h
      - if a node with the same position as successor is in the OPEN list which has a lower f than successor, skip this successor

      - if a node with the same position as successor  is in the CLOSED list which has a lower f than successor, skip this successor otherwise, add  the node to the open list end (for loop)
  
    - push q on the closed list
    end (while loop)
### Program:
```Python
DEVELOPED BY: SHALINI K
REGISTER NUMBER: 212222240095

from collections import defaultdict
H_dist ={}
def aStarAlgo(start_node, stop_node):
    open_set = set(start_node)
    closed_set = set()
    g = {}               # store distance from starting node
    parents = {}         # parents contains an adjacency map of all nodes
    #distance of starting node from itself is zero
    g[start_node] = 0  #start_node is root node i.e it has no parent nodes
    parents[start_node] = start_node #so start_node is set to its own parent node
    while len(open_set) > 0:
        n = None #node with lowest f() is found
        for v in open_set:
            if n == None or g[v] + heuristic(v) < g[n] + heuristic(n):
                n = v
        if n == stop_node or Graph_nodes[n] == None:
            pass
        else:
            for (m, weight) in get_neighbors(n): #nodes 'm' not in first and last set are added to first
                if m not in open_set and m not in closed_set: #n is set its parent
                    open_set.add(m)
                    parents[m] = n
                    g[m] = g[n] + weight   #for each node m,compare its distance from start i.e g(m) to the
                else:                      #from start through n node
                    if g[m] > g[n] + weight:
                        #update g(m)
                        g[m] = g[n] + weight
                        #change parent of m to n
                        parents[m] = n
                        if m in closed_set: #if m in closed set,remove and add to open
                            closed_set.remove(m)
                            open_set.add(m)
        if n == None:
            print('Path does not exist!')
            return None
        if n == stop_node:    # if the current node is the stop_node
            path = []     # then we begin reconstructin the path from it to the start_node
            while parents[n] != n:
                path.append(n)
                n = parents[n]
            path.append(start_node)
            path.reverse()
            print('Path found: {}'.format(path))
            return path
        open_set.remove(n) # remove n from the open_list, and add it to closed_list
        closed_set.add(n) # because all of his neighbors were inspected
    print('Path does not exist!')
    return None
def get_neighbors(v): #define fuction to return neighbor and its distance
    if v in Graph_nodes: #from the passed node
        return Graph_nodes[v]
    else:
        return None
def heuristic(n):
    return H_dist[n]
'''Graph_nodes = {                     #Describe your graph here
    'A': [('B', 6), ('F', 3)],
    'B': [('A', 6), ('C', 3), ('D', 2)],
    'C': [('B', 3), ('D', 1), ('E', 5)],
    'D': [('B', 2), ('C', 1), ('E', 8)],
    'E': [('C', 5), ('D', 8), ('I', 5), ('J', 5)],
    'F': [('A', 3), ('G', 1), ('H', 7)],
    'G': [('F', 1), ('I', 3)],
    'H': [('F', 7), ('I', 2)],
    'I': [('E', 5), ('G', 3), ('H', 2), ('J', 3)],
}
'''
graph = defaultdict(list)
n,e = map(int,input().split())
for i in range(e):
    u,v,cost = map(str,input().split())
    t=(v,float(cost))
    graph[u].append(t)
    t1=(u,float(cost))
    graph[v].append(t1)
for i in range(n):
    node,h=map(str,input().split())
    H_dist[node]=float(h)
print(H_dist) 
Graph_nodes=graph
print(graph)
aStarAlgo('S', 'G')
```
#### Sample Graph I

<img height=20% width=50% src="https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a">
<table>
<tr>
<td width=60%>

#### Sample Input
10 14 A B 6 A F 3 B D 2 B C 3 C D 1 C E 5 D E 8 E I 5 E J 5 F G 1 G I 3 I J 3 F H 7 I H 2 A 10 B 8 C 5 D 7 E 3 F 6 G 5 H 3 I 1 J 0
</td> 
<td valign=top>

#### Sample Output:
Path found: ['A', 'F', 'G', 'I', 'J']
</td>
</tr> 
</table>

#### Sample Graph 2
<img height=20% width=50% src="https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3">
<table>
<tr>
<td width=60%>

#### Sample Input
6 6 A B 2 B C 1 A E 3 B G 9 E D 6 D G 1 A 11 B 6 C 99 E 7 D 1 G 0
</td> 
<td valign=top>

#### Sample Output:
Path found: ['A', 'E', 'D', 'G']
</td>
</tr> 
</table>

### Result:
Implementing A * Search algorithm for a Graph using Python 3. is executed successfully.
