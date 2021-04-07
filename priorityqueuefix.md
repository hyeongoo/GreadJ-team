```
import java.util.PriorityQueue;
import java.util.Scanner;

class Element implements Comparable<Element> {
    int index;
    int distance;

    public Element(int index, int distance) {
        this.index = index;
        this.distance = distance;
    }

    @Override
    public int compareTo(Element o) {
        return this.distance - o.distance;
    }
}

public class test {
    static boolean[] visited;
    static int[] dist;
    static int[][] ad;
    static int E = 9, V = 6;
    static int inf = 100000;

    public static void DijkstaMethod(int start) {
        PriorityQueue<Element> pq = new PriorityQueue<>();
        dist[start] = 0;
        pq.offer(new Element(start, dist[start]));

        while(!pq.isEmpty()) {
            int cost = pq.peek().distance;
            int here = pq.peek().index;
            pq.poll();

            if (cost > dist[here]) { 
                continue;
            }

            System.out.print(here + " ");
            
            for (int i = 1; i <= V; ++i) {   
                if (ad[here][i] != 0 && dist[i] > (dist[here] + ad[here][i])) {
                    dist[i] = dist[here] + ad[here][i];
                    pq.offer(new Element(i, dist[i]));
                }
            }

            System.out.println();

            for (int i = 1; i <= V; ++i) {  
                System.out.print(dist[i] + " ");
            }
        }

    }

    public static void main(String[] args) {
        visited = new boolean[V + 1];
        dist = new int[V + 1];
        ad = new int[V + 1][V + 1];

        for (int i = 1; i <= V; ++i) {
            dist[i] = inf;
        }
 Scanner sc= new Scanner(System.in);

int d=sc.nextInt();
for(int i=0;i<d; i++){
            int a = sc.nextInt();
            int b = sc.nextInt();
            int c = sc.nextInt();

            ad[a][b] = c;
        }
        DijkstaMethod(1);
    }
}
//주석제거
```