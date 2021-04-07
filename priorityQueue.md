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

            if (cost > dist[here]) {   // 현재 배열에 있는 값(최단 거리)보다 cost(거리)가 더 길면 continue
                continue;
            }

            System.out.print(here + " ");

            // 아래 for문이 다익스트라의 핵심 코드라고 생각함
            for (int i = 1; i <= V; ++i) {   // 업데이트 시켜주는 for문
                if (ad[here][i] != 0 && dist[i] > (dist[here] + ad[here][i])) {
                    // if 문 조건을 잘 생각하기 (업테이트를 위함)
                    dist[i] = dist[here] + ad[here][i];
                    pq.offer(new Element(i, dist[i]));
                }
            }

            System.out.println();

            for (int i = 1; i <= V; ++i) {   // dist 배열의 중간 결과 보여주기
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
/*
        ad[1][2] = 20;
        ad[1][4] = 30;
        ad[2][3] = 20;
        ad[2][5] = 40;
        ad[3][4] = 20;
        ad[3][6] = 20;
        ad[4][5] = 20;
        ad[4][6] = 30;
        ad[5][6] = 10;

        DijkstaMethod(1);
*/
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
//직접 입력 방식으로 변경
```