```
import java.util.PriorityQueue;
import java.util.Scanner;

class Element implements Comparable<Element> {
    int index;	//노드의 번호
    int distance;	//노드의 거리값(거리값 = 시작노드에서 각 노드까지의 거리)

    public Element(int index, int distance) {
        this.index = index;
        this.distance = distance;
    }

    @Override	//implements로 상속을 받았으니 메소드를 오버라이딩 한다
    public int compareTo(Element o) {
        return this.distance - o.distance;
    }
}

public class test {
    static boolean[] visited;	//방문여부를 확인할 배열
    static int[] dist;	//거리값를 저장할 배열
    static int[][] ad;	//두 노드 사이의 거리를 표현할 배열
    static int E = 9, V = 6;
    static int inf = 100000;

    public static void DijkstaMethod(int start) {
        PriorityQueue<Element> pq = new PriorityQueue<>();
        dist[start] = 0;	//자기자신과의 거리는 0
        pq.offer(new Element(start, dist[start]));	//우선순위큐에 start(시작 노드의 번호)와 start의 거리를 넣는다.

        while(!pq.isEmpty()) {	//큐가 빌 때까지 반복
            int cost = pq.peek().distance;	//cost에 큐에서 peek한 노드의 거리값을 저장
            int here = pq.peek().index;	//here에 큐에서 peek한 노드의 번호 저장
            pq.poll();	//큐에서 노드 제거

            if (cost > dist[here]) {	//cost값이 현재 거리값보다 크면 continue를 다시 반복문으로 돌아간다
                continue;
            }

            System.out.print(here + " ");	//현재 노드의 번호 출력
            
            for (int i = 1; i <= V; ++i) {   
                if (ad[here][i] != 0 && dist[i] > (dist[here] + ad[here][i])) {	//a->c 보다 a->b->c가 더 짧으면
                    dist[i] = dist[here] + ad[here][i];	//dist[c](a->c)에 a->b->c값을 저장
                    pq.offer(new Element(i, dist[i]));	//큐에 노드 i와 i의 거리를 넣는다
                }
            }

            System.out.println();

            for (int i = 1; i <= V; ++i) {  //결과 출력
                System.out.print(dist[i] + " ");
            }
        }

    }

    public static void main(String[] args) {
        visited = new boolean[V + 1];
        dist = new int[V + 1];
        ad = new int[V + 1][V + 1];	//

        for (int i = 1; i <= V; ++i) {	//초기 거리값을 엄청 큰 수로 초기화
            dist[i] = inf;
        }
 Scanner sc= new Scanner(System.in);

int d=sc.nextInt();	//간선의 개수 입력받기
for(int i=0;i<d; i++){	//간선의 개수만큼 반복
            int a = sc.nextInt();
            int b = sc.nextInt();
            int c = sc.nextInt();

            ad[a][b] = c;	//a와b사이의 거리 = c
        }
        DijkstaMethod(1);
    }
}
```