```
import java.util.Scanner;
class graph{
    int n;
    int map[][];

    public graph(int n){
        this.n = n;
        map = new int[n][n];
    }

    public void input(int i, int j, int w){
        map[i][j] = w;  //i와j사이의 거리가 w
        map[j][i] = w;
    }

    public void dijkstra(int v){
        int distance[] = new int[n];  //거리값 저장할 배열
        boolean [] visit = new boolean[n];    //방문여부 확인

        for(int i=0; i<n; i++){
            distance[i] = Integer.MAX_VALUE;    //처음 거리값을 엄청 큰 수로 설정
        }
        distance[v] = 0;    //처음 시작 노드와 자기 자신의 거리는 0
        visit[v] = true;    //처음 시작 노드 방문

        for(int i=0; i<n; i++){
            if(!visit[i] && map[v][i] != 0) distance[i] = map[v][i];    //방문하지 않았고, v와i의 거리가 0이 아니면, 거리값 = v와i사이의 거리
        }

        for(int k=0; k<n-1; k++){   //다익스트라는 노드의수 -1번 반복하면 된다.
           int min = Integer.MAX_VALUE;
           int min_index = -1;

           for(int i=0; i<n; i++){
               if(!visit[i] && distance[i] != Integer.MAX_VALUE){   //방문하지 않았고 거리가 엄청 큰 수가 아니면
                   if(distance[i] < min){   //거리값이 최솟값보다 작으면
                       min = distance[i];   //최솟값 = 거리값
                       min_index = i;
                   }
               }
           }
           visit[min_index] = true;     //거리가 최솟값이 노드 방문 (ex 노드 a)
           for(int i=0; i<n; i++){
               if(!visit[i] && map[min_index][i] != 0){
                   if(distance[i] > distance[min_index] + map[min_index][i]){   //노드 b의 거리값 < 노드 a의 거리값 + a와b의 거리값 인경우
                       distance[i] = distance[min_index] + map[min_index][i];   //노드 b의 거리값 = 노드 a의 거리값 + a와b의 거리값
                   }
               }
           }
        }
        for(int i=0; i<n; i++){
            System.out.println(i + "번째 노드까지의 거리는" + distance[i] + "입니다.");
        }
    }
}


public class Main {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        System.out.println("노드의 수를 입력해주세요.");
        int n = sc.nextInt();
        graph g = new graph(n);
        System.out.println("연결된 노드와 거리값을 입력해주세요.");
        while(true){
            if(sc.nextInt() == -1) break;
            g.input(sc.nextInt(), sc.nextInt(), sc.nextInt());
        }
        System.out.println("시작 노드를 입력해주세요.");
        int start = sc.nextInt();
        g.dijkstra(start);

        sc.close();
    }
}
```