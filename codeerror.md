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

![오류](C:\Users\cjh00\OneDrive\바탕 화면\오류.PNG)

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

![오류2](C:\Users\cjh00\OneDrive\바탕 화면\오류2.PNG)

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

