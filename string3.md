# 배열로 이용한 dij

```
import java.util.Scanner;


class Dijkstra {
    private int n;	//노드 수를 저장할 변수
    private int[][] weight;	//두 노드 사이의 거리를 표현할 배열
    private String[] saveRoute;	//경로를 저장할 배열
    private String[] vertex = {"a","b","c","d","e","f","g","z"};

    public Dijkstra(int n) {
        super();
        this.n = n; //노드 수를 받음
        weight = new int[n][n]; //배열의 크기 지정
        saveRoute = new String[n];
    }

    public int stringToInt(String s) {	//문자열을 int형으로 바꿔준다.
        int x = 0;
        for(int i=0; i<vertex.length; i++) {
            if(vertex[i]==s) x=i;
        }
        return x;
    }

    public void input(String v1, String v2, int w) {
        //먼저 문자열로 입력된 꼭지점 v1와 v2를 해당되는 숫자 인덱스 x1과 x2로 바꿔준다.
        int x1 = stringToInt(v1);
        int x2 = stringToInt(v2);
        weight[x1][x2] = w;	//x1와 x2사이의 거리 = w
        weight[x2][x1] = w;
    }

    public void algorithm(String a) {
        boolean[] visited = new boolean[n]; //방문여부를 확인할 배열
        int distance[] = new int[n]; //거리값을 저장할 배열(거리값 = 시작노드부터 각 노드까지의 거리)

        for(int i=0; i<n; i++) {	//초기 거리값을 엄청 큰 수로 초기화(여기선 int형의 가장 큰 값 2147483647로 초기화한다.)
            distance[i] = Integer.MAX_VALUE;
        }

        int x = stringToInt(a); //문자열로 입력된 시작 노드를 해당되는 숫자 인덱스 x로 바꾸고
        distance[x] = 0; //자기자신과의 거리는 0
        visited[x] = true; //시작 노드점 방문
        saveRoute[x] = vertex[x]; //시작 노드의 경로는 자기 자신을 저장

        for(int i=0; i<n; i++) {
            if(!visited[i] && weight[x][i]!=0) {	//i를 방문하지 않았고, x와i의 거리가 0이아니면(같은 노드가 아니면)
                distance[i] = weight[x][i];	//i의 거리값 = x와i사이의 거리
                saveRoute[i] = vertex[x]; //시작 노드와 인접한 노드의 경로에 시작 노드을 저장
            }
        }

        for(int i=0; i<n-1; i++) {	//다익스트라는 노드의수 -1번만 반복하면 된다
            int minDistance = Integer.MAX_VALUE; //최단거리 minDistance에 일단 가장 큰 정수로 저장하고,
            int minVertex = -1; //그 거리값이 있는 인덱스 minIndex에 -1을 저장해둔다.
            for(int j=0; j<n; j++) {
                //방문하지 않았고 거리를 갱신한 노드 중에서 가장 가까운 노드을 구한다.
                if(!visited[j] && distance[j]!=Integer.MAX_VALUE) {
                    if(distance[j]<minDistance) {
                        minDistance = distance[j];
                        minVertex = j;
                    }
                }
            }
            visited[minVertex] = true; //가장 가까운 노드 방문
            for(int j=0; j<n; j++) {
                if(!visited[j] && weight[minVertex][j]!=0) {
                    if(distance[j]>distance[minVertex]+weight[minVertex][j]) {	//a->c 보다 a->b->c가 더 짧으면
                        distance[j] = distance[minVertex]+weight[minVertex][j];	//distance[c](a->c)에 a->b->c값을 저장
                        saveRoute[j] = vertex[minVertex]; //최단거리가 갱신된 노드의 경로에 minVertex에 해당하는 노드 저장
                    }
                }
            }
        }
        for(int i=0; i<n; i++) {	//결과 출력(거리)
            System.out.println("시작 노드 "+a+"부터 노드 "+vertex[i]+"까지의 거리 :"+distance[i]);
        }

        System.out.println("==================================");

        for(int i=0; i<n; i++) {	//결과 출력(경로)
            String route = "";
            System.out.println("시작 노드 "+a+"부터 노드 "+vertex[i]+"까지의 경로");
            int index = i;
            while(true) {	//무한 반복
                if(saveRoute[index] == vertex[index]) break; //시작 노드일 경우 break
                route += " " + saveRoute[index];
                index = stringToInt(saveRoute[index]); //결정적인 역할을 한 노드을 int형으로 바꿔서 index에 저장
            }
            StringBuilder sb = new StringBuilder(route);
            System.out.println(sb.reverse() + vertex[i]);
        }
    }
}
public class Main{
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        System.out.println("몇 개의 점이 있습니까?");
        int n = sc.nextInt();

        System.out.println("몇 개의 선분이 있습니까?");
        int m = sc.nextInt();


        Dijkstra d = new Dijkstra(n);

        d.input("a","b",20);
        d.input("a","d",30);
        d.input("b","c",20);
        d.input("b","e",40);
        d.input("c","d",20);
        d.input("c","f",20);
        d.input("d","e",20);
        d.input("d","f",30);
        d.input("e","f",10);

        d.algorithm("a");
    }

}
```