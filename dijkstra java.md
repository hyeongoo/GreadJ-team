```
import java.util.ArrayList;
import java.util.Scanner;
class Node{
    int idx;
    int cost;

    Node(int idx, int cost){
        this.idx = idx;
        this.cost=cost;
    }
}
public class test {
    public static void main(String[] args){
        Scanner sc =new Scanner(System.in);

        int vertex = sc.nextInt();
        int edge = sc.nextInt();

        int start = sc.nextInt();

        ArrayList<ArrayList<Node>> graph=new ArrayList<ArrayList<Node>>();
        for (int i = 0; i < vertex + 1; i++) {
            graph.add(new ArrayList<>());
        }
        for (int i = 0; i < edge; i++) {
            int a = sc.nextInt();
            int b = sc.nextInt();
            int cost = sc.nextInt();

            graph.get(a).add(new Node(b, cost));
        }
        boolean[] visited = new boolean[vertex+ 1];
        int[] dist = new int[vertex + 1];
        for (int i = 0; i < vertex + 1; i++) {
            dist[i] = Integer.MAX_VALUE;
        }
        dist[start] = 0;
        for (int i = 0; i < vertex; i++) {
            int nodeValue = Integer.MAX_VALUE;
            int nodeIdx = 0;
            for (int j = 1; j < vertex + 1; j++) {
                if (!visited[j] && dist[j] < nodeValue) {
                    nodeValue = dist[j];
                    nodeIdx = j;
                }
            }
            visited[nodeIdx] = true;
            for (int j = 0; j < graph.get(nodeIdx).size(); j++) {
                Node adjNode = graph.get(nodeIdx).get(j);
                if (dist[adjNode.idx] > dist[nodeIdx] + adjNode.cost){
                    dist[adjNode.idx] = dist[nodeIdx] + adjNode.cost;
                }
            }
        }
        for (int i = 1; i < vertex+ 1; i++) {
            if (dist[i] == Integer.MAX_VALUE) {
                System.out.println("INF");
            } else {
                System.out.println(dist[i]);
            }
        }
        sc.close();
    }
}
```

/*
횟수, 노드 개수
1
숫자, 숫자, 숫자
...(노드개수)
숫자, 숫자, 숫자
*/