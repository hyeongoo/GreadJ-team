#Explain

# 다익스트라 알고리즘 

##### 다익스트라 알고리즘이란 무엇인가?

다익스트라 알고리즘은 그래프에서 꼭짓점 간의 최단 경로를 찾는 알고리즘이다.

![다익스트라](https://user-images.githubusercontent.com/80919306/113891057-ad9af380-97ff-11eb-82f3-58c7e0fed893.jpg)

위의 그림은 가중치 방향 그래프이다. 다음과 같이 가중치가 부여된 경우에는 가중칠들 계산하여 가중치에 의해 최단거리가 결정된다. 이때 최단거리는 가중치의 합이 가장 작은 경로가 되는데 이번 과제에 사용된 코드의 결과값은 위의 가중치 그래프를 기준으로 하여 풀이했다.

##### Shortest Path의 수행과제

우선 가중치 그래프의 입력부분인 G=(V, E), V(점의 수), E(간선의 수)를 나타내보자.

G=< V, E >

V={a,b,c,d,e,f}

E={<a.b>,<a,d>,<b,c>,<b,e>,<c,d>,<c,f>,<d,e>,<d.f>,<e.f>}

우선 시작점의 위치를 a라고 했을 때 최단경로 선택전이므로 다음과 같이 초기화를 시킨다.

D[b]=D[c]=D[d]=D[e]=D[f]=Integer.MAX_VALUe

###### STEP1

최단경로의 거리를 알아보기 위해 시작점 a에서부터 그래프 G내의 다르 꼭짓점과의 가중치를 정리하면 다음과 같다,

D[b]=20, D[c]=D[e]=D[f]=Integer.MAX_VALUE, D[d]=30

이 단계에서 최단경로가 되는 가중치를 갖는 꼭짓점은 b임을 알 수 있다. 이 과정 이후 탐색하지 않은 꼭짓점은 c,d,e,f가 남게 된다.

###### STEP2

시작점 a와 추가된 꼭짓점 b에서의 다른 꼭짓점까지의 가중치를 비교한다.

D[c]=40, D[d]=30. D[e]=60, D[f]=Integer.MAX_VALUE,

이를 통해 최단경로를 가지는 꼭짓점은 d가 된다. 이 과정 이후 탐색되지 않은 꼭짓점은 c,e,f가 되는데 탐색되지 않는 꼭짓점이 없을 때까지 위의 과정을 반복한다.



###### STEP3

탐색되지 않은 꼭짓점이 없으면 코드는 반복문은 종료되고 결과값이 출력되게 된다. 아래의 그림은 이 과정을 표를 통해 표현한 것이다.

![KakaoTalk_20210405_210848467](https://user-images.githubusercontent.com/80919306/113893829-58141600-9802-11eb-80bd-95a95682d27f.jpg)

-------------구분선

#배열이용한 다익스트라

전체코드 :  https://github.com/hyeongoo/GreadJ-team/blob/dijkstra/dijkstra.md

```
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


```

-------------구분선

#우선순위큐 이용한 다익스트라

전체코드 :  [GreadJ-team/priorityqueuefix.md at dijkstra · hyeongoo/GreadJ-team (github.com)](https://github.com/hyeongoo/GreadJ-team/blob/dijkstra/priorityqueuefix.md)

```
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

```

-------------구분선

#문자열로 입력받기

전체 코드 :  [GreadJ-team/string3.md at dijkstra · hyeongoo/GreadJ-team (github.com)](https://github.com/hyeongoo/GreadJ-team/blob/dijkstra/string3.md)

```

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
```

-------------구분선

#시간복잡도

시간복잡도

다익스트라 알고리즘은 변 경감(edge relaxation)이라고 불리는 연산을 기본 바탕으로 하고 있다. 정점 a에서 정점 b까지의 최단 거리를 이미 알고 있고, b에서 c까지의 거리를 알고 있다면 a에서 c까지의 최단 거리는 a에서 b까지의 거리에 b에서 c까지의 거리를 더해서 구하는 방식이다.  

다익스트라 알고리즘을 코드로 구현할 때에 이 변 경감이라는 것이 기본이 되지만, 이 알고리즘을 짜는 데에 대한 변형 로직은 당연히 여럿 존재한다.
방법으로 대략 한 정점에 대하여 연결된 모든 간선의 가중치를 모두 비교하는 방법과, 가중치를 오름차순 등으로 정렬하여 가중치가 적은 간선을 먼저 가져오는 방법 두 가지가 있는 것 같다. 전자는 배열 등으로 단순하게 구현되는 반면, 후자는 우선순위 큐와 같은 자료 구조를 통한 처리를 동반한다.

이 두 방법을 서로 비교해보고 싶어서 시간복잡도를 계산하여 어떤 방법이 더 효율적인지 계산해 보았다. 그런데 그 전에 먼저  어떤 방법이 더 효율적일지 예측해보았는데, 결과는 예상과 동일했지만 생각과는 조금 다른 점이 있었다.

모든 가중치를 비교하는 방법
![일반](https://user-images.githubusercontent.com/80510925/113894051-99a4c100-9802-11eb-9af1-59d4559eb7a8.PNG)

우선순위 큐를 이용한 방법
![우선순위 큐](https://user-images.githubusercontent.com/80510925/113894200-b8a35300-9802-11eb-892f-7a2cd05905d1.PNG)

결과로는 당연히 우선순위 큐를 이용하여 가중치가 더 적은 간선을 먼저 가져오는 방법이 더 빠른 속도를 가질 것이라고 생각했다.  가장 적은 가중치를 가진 간선 하나를 가져오는 것에 비해 한 정점을 기준으로 다른 정점까지의 모든 간선의 가중치를 비교하는 것은 효율이 더 좋지 않기 때문이다. 하지만 우선순위 큐 자체를 구현하기 위해 코드 줄 수가 더 사용되었고 그에 따라 시간을 더 잡아먹는 점도 생각해야 하기에 단순히 시간복잡도로 계산하는 것이 의미가 있는지 알아야 했다.

그런데 시간복잡도를 가지고 두 방법의 정점과 시간에 관한 그래프를 그려보자 우선순위 큐를 사용한 방법이 다익스트라 알고리즘을 수행하는 데에는 너무나 압도적인 효율을 가진다는 것을 알 수 있어 가중치를 정렬하는데 드는 시간을 고려할 필요가 없다는 결론이 나왔다.

시간복잡도는 V는 정점 수, E는 간선 수 라고 할 때 모든 가중치를 비교하는 방법은 O(V^2), 우선순위 큐를 이용한 방법은 O(ElogV) 의 시간 복잡도를 가졌다. 이 때 우리가 코드를 실행해 볼 때 사용한 임의의 간선 수를 가져와서 간선 수를 9로 놓고 그래프를 그려보았다.

![1](https://user-images.githubusercontent.com/80510925/113893913-6feb9a00-9802-11eb-8057-86ec3ecb3d3b.PNG)

![2](https://user-images.githubusercontent.com/80510925/113893994-8b56a500-9802-11eb-80db-cd867f355553.PNG)

심지어 정점과 가중치가 적은 경우에도 다익스트라 알고리즘을 수행하는 데에는 우선순위 큐가 더 유효하다는 결과가 나와서 이런 경우 정렬을 하기 위한 시간을 추가해도 정점과 가중치가 적으므로 성능에 큰 차이를 보이지 않을 것으로 보인다.

-------------구분선

#코드 에러 픽스

# 코드 오류 - 예외처리 

 배열을 이용한 다익스트라 알고리즘을 이용한 코드를 찾았으나 그 코드는 저희가 구하고자 하는 코드와 약간 달랐습니다.

```
d.input("a","b",4);
		d.input("a","c",3);
		d.input("b","c",2);
		d.input("b","d",5);
		d.input("c","d",3);
		d.input("c","e",6);
		d.input("d","e",1);
		d.input("d","f",5);
		d.input("e","g",5);
		d.input("f","g",2);
		d.input("f","z",7);
		d.input("g","z",4);
```

윗 부분은 코드의 일부분은 나타냈는데 코드 내에 이미 정점과 간선 사이의 가중치가 이미 정해졌기에 코드를 실행하면 저희가 구하고자하는 문제로 바꿀 수 없었습니다. 그렇기 때문에 저희는 input 함수에 삽입될 때 가중치 값이 정해진 것이 아닌 직접 입력하는 쪽으로 바꾸고 싶었습니다.

```
  for(int i=0;i<m;i++){
            String a = sc.nextLine();
            String b = sc.nextLine();
            int c = sc.nextInt();
            d.input(a, b, c);
        }
```

수정한 코드는 다음과 같습니다. 변수 m은 미리 간선의 개수를 입력받은 것이고, 이를 통해 반복문을 통해 정점 a,b와 가중치 c의 값을 입력받아 input함수에 삽입하는 방법을 생각했습니다.

<img width="911" alt="오류" src="https://user-images.githubusercontent.com/80919306/113875794-154a4200-97f2-11eb-8f13-caddeb3fbadd.PNG">

하지만 실행결과 다음과 같은 오류가 발생했습니다. 정상적으로 코드가 작동한다면 주어진 문제의 간선의 개수가 9개이기 때문에 9개의 가중치에 대해 입력받아야 하지만 실제 코드에서 중간에 입력을 멈추고 inputmismatchexception 라는 입력받아야 할 자료형 변수가 일치하지 않았을 때 생기는 예외처리가 발생했습니다. 변수가 일치하지 않는 원인을 생각핸 본 결과 문자열을 입력받았을 때 sc.nextLine()을 사용했는데 이는 문자 한 라인 전체를 입력받기에 공배도 입력되면서 오류가 생기는 것 같아서 next()를 이용해 코드를 돌려봤습니다.

```
for(int i=0;i<m;i++){
            String x = sc.next();
            String y = sc.next();
            int z = sc.nextInt();
            d.input(x, y, z);
        }
```

코드를 다음과 같이 수정한 결과 다음과 같이 나타났습니다.

<img width="934" alt="오류2" src="https://user-images.githubusercontent.com/80919306/113875975-3e6ad280-97f2-11eb-81e1-22cc2937e5ce.PNG">

이번에는 간선의 개수에 맞게 가중치가 입력되는 듯 싶었으나 

**ArrayIndexOutOfBoundsException:**

이라는 배열 인덱스 오류가 발생했습니다. 결국 마땅한 해결책을 찾지 못해서 주어진 문제를 풀기 위해 다음과 같이 코드를 짰습니다.

```
 d.input("a","b",20);
        d.input("a","d",30);
        d.input("b","c",20);
        d.input("b","e",40);
        d.input("c","d",20);
        d.input("c","f",20);
        d.input("d","e",20);
        d.input("d","f",30);
        d.input("e","f",10);
```

### 실행 결과

<img width="595" alt="결과" src="https://user-images.githubusercontent.com/80919306/113901713-16876900-980a-11eb-8d93-c6a94e7cdf97.PNG">