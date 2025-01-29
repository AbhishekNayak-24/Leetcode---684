# Leetcode---684
Redundant Connection
// Code in java
public class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        int n = edges.length;
        int[] parent = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            parent[i] = i;
        }
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int rootU = find(parent, u);
            int rootV = find(parent, v);
            if (rootU == rootV) {
                return edge;
            }
            parent[rootU] = rootV;
        }
        return new int[0];
    }

    private int find(int[] parent, int u) {
        if (parent[u] != u) {
            parent[u] = find(parent, parent[u]);
        }
        return parent[u];
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[][] edges = {{1, 2}, {1, 3}, {2, 3}};
        int[] result = solution.findRedundantConnection(edges);
        System.out.println("Redundant connection: [" + result[0] + ", " + result[1] + "]");
    }
}
