## Kruscal Algorithm for minimum spanning tree.

In Kruskal’s algorithm, we sort all edges of the given graph in increasing order. Then it keeps on adding new edges and nodes in the MST if the newly added edge does not form a cycle. It picks the minimum weighted edge at first and the maximum weighted edge at last. Thus we can say that it makes a locally optimal choice in each step in order to find the optimal solution. Hence this is a Greedy Algorithm.

In the below code - the parent array store the number of that node from which spanning is starting.

### Java code
```

class Solution { 
    
    static int rank[];
    static int parent[];
    
    static int kruskalsMST(int V, int[][] edges) {
        
        int n=edges.length;
        // sort edge according to the edge weight in ascending order
        Arrays.sort(edges, (a,b)->Integer.compare(a[2],b[2]));
        // rank array will store the rank to update the parent array
        rank=new int[V];
        
        parent=new int[V];
        for(int i=0; i<V; i++){
            parent[i]=i;
            rank[i]=1;
        }
        
        int cost=0;
        int edgeCount=0;
        for(int i=0; i<n; i++){
            int u=edges[i][0], v=edges[i][1], w=edges[i][2];
            // if both node is from same set then it would form a cycle otherwise add it to so far formed MST
            if(findParent(u)!=findParent(v)){
                cost+=w;
                union(u,v);
                edgeCount++;
                if(edgeCount==V-1){
                    break;
                }
            }
        }
        return cost;
    }
    private static int findParent(int u){
        // find the starting node of this MST
        if(parent[u]!=u){
            // since we know that  starting node of MST will have no parent means same as node. 
            parent[u] = findParent(parent[u]);
        }
        return parent[u];
    }
    private static void union(int u, int v){
        int set1 = findParent(u);
        int set2 = findParent(v);
        if(set1==set2){
            return;
        }
        if(rank[set1] >= rank[set2]){
            parent[set2] = set1;
            rank[set1]++;
        }else{
            parent[set1] = set2;
            rank[set2]++;
        }
    }
}
