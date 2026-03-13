# Data-structure-practical-program-29class Solution {
public:
    bool dfs(int node, vector<vector<int>> &adj, vector<int> &vis, vector<int> &rec) {
        vis[node] = 1;
        rec[node] = 1;

        for(int neighbor : adj[node]) {
            if(!vis[neighbor]) {
                if(dfs(neighbor, adj, vis, rec))
                    return true;
            }
            else if(rec[neighbor]) {
                return true;
            }
        }

        rec[node] = 0;
        return false;
    }

    bool isCyclic(int V, vector<vector<int>> &edges) {
        vector<vector<int>> adj(V);

        for(auto &e : edges) {
            adj[e[0]].push_back(e[1]);
        }

        vector<int> vis(V,0), rec(V,0);

        for(int i=0;i<V;i++) {
            if(!vis[i]) {
                if(dfs(i, adj, vis, rec))
                    return true;
            }
        }

        return false;
    }
};
