```
import java.util.Scanner;
class graph{
    int n;	//노드 수를 저장할 변수
    int map[][];	//두 노드 사이의 거리를 표현할 배열
    int INF = 10000;

    public graph(int n){
        this.n = n;	//노드 수를 받음
        map = new int[n+1][n+1];	//배열의 크기 지정
    }

    public void input(int i, int j, int w){
        map[i][j] = w;  //i와j사이의 거리가 w
        map[j][i] = w;
    }

    public void dijkstra(int v){
        int distance[] = new int[n+1];  //거리값을 저장할 배열(거리값 = 시작 노드에서 각 노드까지의 거리)
        boolean [] visit = new boolean[n+1];    //방문여부를 확인할 배열

        for(int i=1; i<n+1; i++){	//노드 번호를 1번부터 시작하기 위해 이렇게 반복함
            distance[i] = INF;    //처음 거리값을 엄청 큰 수로 설정
        }
        distance[v] = 0;    //처음 시작 노드와 자기 자신의 거리는 0
        visit[v] = true;    //처음 시작 노드 방문

        for(int i=1; i<n+1; i++){
            if(!visit[i] && map[v][i] != 0) distance[i] = map[v][i];    //i를 방문하지 않았고, v와i의 거리가 0이 아니면(같은 노드가 아니면), i의 거리값 = v와i사이의 거리
        }

        for(int k=0; k<n-1; k++){   //다익스트라는 노드의수 -1번만 반복하면 된다.
           int min = INF;	//초기 최솟값은 엄청 큰 수로 초기화
           int min_index = -1;

           for(int i=1; i<n+1; i++){
               if(!visit[i] && distance[i] != INF){   //방문하지 않았고 거리가 엄청 큰 수가 아니면
                   if(distance[i] < min){   //거리값이 최솟값보다 작으면
                       min = distance[i];   //최솟값 = 거리값
                       min_index = i;	//거리가 최솟값인 노드 번호
                   }
               }
           }
           visit[min_index] = true;     //거리가 최솟값인 노드 방문
           for(int i=1; i<n+1; i++){
               if(!visit[i] && map[min_index][i] != 0){
                   if(distance[i]>distance[min_index]+map[min_index][i]){	//a->c 보다 a->b->c가 더 짧으면
                       System.out.print("i=" + i + ", " + "distance[i]=" + distance[i] + ", ");	//distance[c](a->c)와 distance[min_index] + map[min_index][i] (a->b->c)를 각각 출력
                       System.out.print("min_index=" + min_index + ", " + "distance[min_index]=" + distance[min_index] + ", ");
                       System.out.print("map[min_index][i]=" + map[min_index][i]);
                       System.out.println();
                       distance[i] = distance[min_index]+map[min_index][i];	//distance[c](a->c)에 a->b->c값을 저장
                   }
               }
           }
        }
        System.out.println();
        for(int i=1; i<n+1; i++){	//결과 출력
            System.out.println(i + "번 째 노드까지의 거리는" + distance[i] + "입니다.");
        }
    }
}


public class Main {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        System.out.println("노드의 수를 입력해주세요.");
        int n = sc.nextInt();
        System.out.println("간선의 수를 입력해주세요.");
        int m = sc.nextInt();
        graph g = new graph(n);
        System.out.println("연결된 노드와 거리값을 입력해주세요.");
        for(int i=0; i<m; i++){
            g.input(sc.nextInt(), sc.nextInt(), sc.nextInt());
        }
        System.out.println("시작 노드를 입력해주세요.");
        int start = sc.nextInt();
        g.dijkstra(start);

        sc.close();

    }
}


```