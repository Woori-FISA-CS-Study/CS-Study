
## 배열 Array

배열은 메모리 공간에 필요한 크기의 메모리 영역을 미리 잡아 놓고 사용하는 자료구조이기 때문에 **선언 시 그 크기를 반드시 지정**해야 함.

- **정적인 크기의 데이터를 다룰** 때에 적합.
- 데이터의 양이 계속해서 늘어나거나 바뀌는 경우에는 적합하지 않음.
- 데이터를 **중간에 넣거나 삭제**할 때에도 삽입/삭제된 데이터 이후의 데이터들을 모두 옮겨주어야 하기 때문에 매우 **비효율적.**

## 배열 리스트 ArrayList

배열의 단점을 보완한 ArrayList는 **크기를 정해주지 않아도 되는 가변적으로 크기가 변하는 선형 리스트.**

일반적인 배열과 동일하게 순차 리스트이고 index를 이용해 내부의 객체를 관리하지만 ArrayList는 데이터가 추가되어 저장 용량을 초과하면 자동으로 부족한 만큼 용량을 늘림.

- 요소를 추가하면 index 0 부터 차례대로 저장되고 **중간의 특정 index에 데이터를 추가하거나 삭제하면 index 이후에 위치한 데이터를 모두 한칸씩 앞뒤로 옮겨주어야 해 비효율적.**
- 데이터의 크기가 가변적이고 중간에 데이터를 삽입한다거나 삭제하는 경우가 거의 없는 경우에 적절.

## 연결 리스트 LinkedList

- **연속적인 메모리 위치에 저장되지 않는 선형 구조**의 자료구조
- 연속된 메모리를 사용하지 않기 때문에 **포인터를 사용해 메모리들을 연결**
- 배열은 미리 특정한 공간을 할당받아 사용한다면 연결리스트는 필요할 때 마다 데이터를 할당받아 추가하는 구조

### 1. 단순 연결 리스트
<img width="640" alt="1" src="https://github.com/Woori-FISA-CS-Study/CS-Study/assets/35751392/c7de0389-bace-4139-a7aa-1c30898b43c3">


### 2. 이중 연결 리스트

![2](https://github.com/Woori-FISA-CS-Study/CS-Study/assets/35751392/ca2ebfbc-8712-4558-84f7-0e73e7547593)


### 3. 원형 연결 리스트

![5](https://github.com/Woori-FISA-CS-Study/CS-Study/assets/35751392/78bed11e-3405-4efd-b3ae-509d7a3ee1c6)


```java
import java.util.ArrayList; 
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>(); // String 타입의 ArrayList 생성

        // 리스트에 요소 추가
        list.add("CS");
        list.add("완전");
        list.add("정복");

        // 리스트의 요소 출력
        for(String item : list){
            System.out.println(item);
        } //CS 완전 정복

        // 리스트의 특정 위치의 요소를 가져오기
        String firstItem = list.get(0);
        System.out.println("첫 번째 요소: " + firstItem); //CS

        // 리스트의 특정 위치의 요소를 수정하기
        list.set(0, "UPDATE");
        System.out.println("수정 후 첫 번째 요소: " + list.get(0)); //UPDATE

        // 리스트의 특정 요소를 삭제하기
        list.remove(0);
        System.out.println("삭제 후 첫 번째 요소: " + list.get(0)); //완전

        // 리스트의 크기를 가져오기
        int size = list.size();
        System.out.println("리스트의 크기: " + size); //2
    }
}
```

## Stack

스택은 **LIFO(Last In First Out)** 구조의 자료형으로 한 쪽으로만 데이터를 넣고 뺄 수 있는 선형 구조

- push : 데이터를 삽입.
- pop : 데이터 삭제.
- 브라우저에서 뒤로가기, 문서 작업 시 컨트롤+Z 같은 이전 상태로 되돌리기 등에 사용되며 DFS알고리즘에 사용
- **Peek** : 마지막 위치에 해당하는 데이터를 읽기
- **overflow** : 스택에 데이터가 꽉 차서 넣을 공간이 없는데 push를 하게 되는 경우
- **underflow** : 데이터가 없는데 pop을 하는 경우
    
  ![stack](https://github.com/Woori-FISA-CS-Study/CS-Study/assets/35751392/c51f46d0-ebe1-45e6-8463-64a6386ce30e)

    

### 스택을 구현하는 방법

### 1. 배열을 사용하는 방법

- 구현이 쉽고 인덱스를 사용, 데이터의 접근 속도가 빠름.
- 데이터의 최대 개수를 미리 정해야 하며 데이터의 삽입과 삭제가 한 쪽으로만 이루어 지기 때문에 매우 비효율적.

### 2. 연결 리스트를 사용하는 방법

- 최대 개수가 정해져 있지 않음. 데이터들이 순차적으로 나열되어 있음. → 데이터의 삽입과 삭제가 편함.

```java
import java.util.Stack; // Stack 클래스를 사용하기 위한 import 문

public class Main {
    public static void main(String[] args) {
        Stack<String> stack = new Stack<>(); // String 타입의 Stack 생성

        // 스택에 요소 추가
        stack.push("CS");
        stack.push("완전");
        stack.push("정복");

        // 스택의 가장 위에 있는 요소 출력
        System.out.println(stack.peek()); //정복

        // 스택의 가장 위에 있는 요소 제거 및 출력
        System.out.println(stack.pop()); //정복

        // 스택이 비어있는지 확인
        System.out.println(stack.empty()); //false

        // 스택의 요소 수를 출력
        System.out.println(stack.size()); //2
    }
}

```

## Queue

큐는 스택과 반대 개념. **FIFO(First In First Out)** 구조의 자료형으로 선입선출, 대기열이라고도 함.

- 먼저 들어간 데이터가 먼저 나오는 구조로 데이터가 들어오는 곳과 나가는 곳이 다름.
- 데이터가 들어오는 위치는 가장 뒤에 있고 데이터가 나가는 위치는 가장 앞에 있어서 선입선출 구조.
- 때문에 가장 마지막에 들어온 데이터를 삭제하려면 앞에 있는 데이터들을 전부 삭제해야 함.
- push : 데이터를 삽입.
- pop : 데이터 삭제.
- 들어온 **순서를 보장**해야 하는 경우인 **작업 대기, 대기줄, 프로세스 관리** 등에 사용되며 **BFS 알고리즘**에도 사용
- 큐는 우선순위 큐, 원형 큐 등의 변형이 존재
- 입력 동작을 Enqueue, 출력 동작은 Dequeue

![queue](https://github.com/Woori-FISA-CS-Study/CS-Study/assets/35751392/b4cf8354-21e2-48e0-922b-29e35b26411d)


```java
import java.util.Queue;
import java.util.LinkedList; 

public class Main {
    public static void main(String[] args) {
        Queue<String> queue = new LinkedList<>(); // String 타입의 Queue 생성

        // 큐에 요소 추가
        queue.add("용");
        queue.add("가");
        queue.add("리");

        // 큐의 가장 앞에 있는 요소 출력
        System.out.println(queue.peek()); //용

        // 큐의 가장 앞에 있는 요소 제거 및 출력
        System.out.println(queue.poll()); //용

        // 큐이 비어있는지 확인
        System.out.println(queue.isEmpty()); //false

        // 큐의 요소 수를 출력
        System.out.println(queue.size()); //2
    }
}
```

```java
//BFS 예제 코드
import java.util.*;

public class Main {
    static ArrayList<Integer>[] adjList;
    static boolean[] visited;

    public static void bfs(int start) {
        Queue<Integer> queue = new LinkedList<>();
        queue.add(start);
        visited[start] = true;

        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.println(node + " ");

            for (int nextNode : adjList[node]) {
                if (!visited[nextNode]) {
                    queue.add(nextNode);
                    visited[nextNode] = true;
                }
            }
        }
    }

    public static void main(String[] args) {
        int n = 5; // 노드의 수
        adjList = new ArrayList[n + 1];
        for (int i = 0; i <= n; i++) {
            adjList[i] = new ArrayList<>();
        }

        // 간선 정보 입력
        adjList[1].add(2);
        adjList[1].add(3);
        adjList[2].add(4);
        adjList[2].add(5);

        visited = new boolean[n + 1];

        // bfs 시작
        bfs(1);
    }
}
```

## 우선순위큐(Heap)

 **우선순위 큐(Priority Queue)**는 먼저 들어오는 데이터가 아니라, 

우선순위가 높은 데이터가 먼저 나가는 형태의 자료구조

- 우선순위 큐는 일반적으로 **힙(Heap)**을 이용하여 구현

```java
import java.util.PriorityQueue;

public class Main {
    public static void main(String[] args) {
        PriorityQueue<Integer> pq = new PriorityQueue<>(); // Integer 타입의 PriorityQueue 생성

        // PriorityQueue에 요소 추가
        pq.add(3);
        pq.add(1);
        pq.add(2);

        // PriorityQueue의 가장 작은 요소 출력
        System.out.println(pq.peek());

        // PriorityQueue의 가장 작은 요소 제거 및 출력
        System.out.println(pq.poll());

        // PriorityQueue가 비어있는지 확인
        System.out.println(pq.isEmpty());

        // PriorityQueue의 요소 수 출력
        System.out.println(pq.size());
    }
}
```

### 힙이란?

**힙(Heap)**은 우선순위 큐를 위해 고안된 완전이진트리 형태의 자료구조.

여러 개의 값 중 최댓값 또는 최솟값을 찾아내는 연산이 빠름.

**힙의 특징**

- **완전이진트리** 형태로 이루어져 있음.
- 부모노드와 서브트리간 대소 관계가 성립. (반정렬 상태)
- 이진탐색트리(BST)와 달리 중복된 값이 허용.

**힙의 종류**

- **최대 힙 (Max Heap)**
    
    부모 노드의 키 값이 자식 노드보다 크거나 같은 완전이진트리.
    
    *❝ key(부모노드) ≥ key(자식노드) ❞*
    

![최대힙](https://github.com/Woori-FISA-CS-Study/CS-Study/assets/35751392/3b9481e8-6476-4849-bc17-56bb2c349ba2)


- **최소 힙 (Min Heap)**
    
    부모 노드의 키 값이 자식 노드보다 작거나 같은 완전이진트리.
    
![최소힙](https://github.com/Woori-FISA-CS-Study/CS-Study/assets/35751392/5665ad62-29d3-4301-a2e5-fae411e35630)



### 우선순위 큐 구현방법 비교

우선순위 큐를 힙이 아니라 배열 또는 연결리스트를 이용하여 구현할 수도 있음.

하지만 배열과 연결리스트는 선형 구조의 자료구조이므로 삽입 또는 삭제 연산을 위한 시간복잡도는 `O(n)`.

반면 힙트리는 완전이진트리 구조이므로 힙트리의 높이는 `log₂(n+1)`이며, 힙의 시간복잡도는 `O(log₂n)`.

![우선순위큐구현방법표](https://github.com/Woori-FISA-CS-Study/CS-Study/assets/35751392/207b5e0f-3c3f-436e-9a5a-3b1a98411d76)

### 우선순위 큐 구현

### 힙 구현

힙은 일반적으로 **배열을 이용하여 구현.**

완전 이진트리이므로 중간에 비어있는 요소가 없기 때문.

![힙구현](https://github.com/Woori-FISA-CS-Study/CS-Study/assets/35751392/37fd6633-87ce-4055-8aae-246281c2dd1e)


위 그림과 같이 트리의 각 노드에 번호를 붙이고, 이 번호를 배열의 인덱스로 생각하면 효과적으로 힙을 구현할 수 있음.

배열로 구현하였기 때문에 부모 또는 자식 노드를 찾아가는 연산을 구현하기도 간편.

**자식노드를 구하고 싶을 때**

- 왼쪽 자식노드 index = (부모 노드 index) * 2
- 오른쪽 자식노드 index = (부모 노드 index) * 2 + 1

**부모노드를 구하고 싶을 때**

- 부모 노드 index = (자식노드 index) / 2

```java
//최대힙 배열 구현 예제
public class MaxHeap {
    private int[] heap;
    private int size;

    public MaxHeap(int capacity) {
        heap = new int[capacity + 1];
        size = 0;
    }

    public void insert(int val) { //힙에 새로운 요소를 추가
        heap[++size] = val;
        int pos = size;

        while (pos > 1 && heap[pos / 2] < heap[pos]) {
            swap(pos, pos / 2); //추가된 요소가 부모 노드의 값보다 클 경우, 부모 노드와 위치를 바꿈.
            pos /= 2; 
        } 

    *}*

    public int remove() { //힙에서 가장 큰 요소(루트 노드)를 제거하고 반환하는 메소드
//제거된 루트 노드의 자리는 힙의 마지막 요소로 채워지며, 이 요소는 힙의 속성을 유지하기 위해 적절한 위치로 이동
			  int popped = heap[1];
        heap[1] = heap[size--];
        maxHeapify(1);
        return popped;
    }

    private void maxHeapify(int pos) { 
// 주어진 위치의 노드가 자식 노드보다 작을 경우, 가장 큰 자식 노드와 위치를 바꿈.
        if (pos * 2 <= size && heap[pos] < heap[pos * 2]) {
            swap(pos, pos * 2);
            maxHeapify(pos * 2);
        }
        if (pos * 2 + 1 <= size && heap[pos] < heap[pos * 2 + 1]) {
            swap(pos, pos * 2 + 1);
            maxHeapify(pos * 2 + 1);
        }
    }

    private void swap(int pos1, int pos2) { //힙의 속성을 유지하기 위해 적절한 위치로 이동
        int tmp = heap[pos1];
        heap[pos1] = heap[pos2];
        heap[pos2] = tmp;
    }

    public static void main(String[] arg) {
        MaxHeap maxHeap = new MaxHeap(15);
        maxHeap.insert(5);
        maxHeap.insert(3);
        maxHeap.insert(17);
        maxHeap.insert(10);
        maxHeap.insert(84);
        maxHeap.insert(19);
        maxHeap.insert(6);
        maxHeap.insert(22);
        maxHeap.insert(9);

        System.out.println("The Max val is " + maxHeap.remove()); //The Max val is 84
    }
}
```

```java
//배열 형태
heap = [, 84, 22, 19, 10, 5, 17, 6, 3, 9]

//완전이진트리 형태
				 
        84
       /    \
     22      19
    / \     /  \
   10  5   17   6
  / \
 3   9
```

### 삽입 연산

힙에 삽입을 하기 위해서는 힙 트리의 성질을 만족시키면서 새로운 요소를 추가해야 함.

**삽입 방법**

1. 우선 완전이진트리의 마지막 노드에 이어서 새로운 노드를 추가한다.
2. 추가된 새로운 노드를 부모의 노드와 비교하여 교환한다.
3. 정상적인 힙트리가 될 때 까지 (더이상 부모노드와 교환할 필요가 없을 때까지) 2번을 반복한다.

최악의 경우 새로 추가된 노드가 루트노트까지 비교하며 올라가야 하므로 시간복잡도가 `O(log₂n)`이다.

### 삭제 연산

힙 트리에서 루트노드가 가장 우선순위가 높으므로 루트 노드를 삭제해야 함.

삭제가 이뤄진 후 힙 트리의 성질이 유지돼야 하므로 아래와 같은 방법으로 삭제를 진행.

**삭제 방법**

1. 루트 노드를 삭제한다.
2. 루트 노드가 삭제된 빈자리에 완전이진트리의 마지막 노드를 가져온다.
3. 루트 자리에 위치한 새로운 노드를 자식 노드와 비교하여 교환한다.이때 최대 힙인 경우 자식노드 중 더 큰 값과 교환을 하며, 최소 힙인 경우 더 작은 값과 교환을 한다.
4. 정상적인 힙트리가 될 때까지 (더 이상 자식노드와 교환할 필요가 없을 때까지) 3번을 반복한다.

삭제 연산 또한 최악의 경우 루트노트부터 가장 아래까지 내려가야 하므로 시간복잡도가 `O(log₂n)`이다.
