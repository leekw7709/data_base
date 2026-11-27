# 202430323 이기웅

# 11월 26일 강의 내용
# 1.재귀 호출(Recursion)의 개념과 동작 원리
1. 재귀 호출(Recursion)의 개념
재귀 호출이란 함수가 자기 자신을 다시 호출하는 프로그래밍 기법이다.
복잡한 문제를 작은 문제로 나누어 해결할 수 있으며, 반복문을 사용하지 않고도 특정 작업을 반복적으로 수행할 수 있다.
2. 재귀 호출의 동작 원리
재귀 호출은 다음과 같은 순서로 동작한다.
1. 함수가 자기 자신을 호출한다.
2. 호출된 함수가 다시 자기 자신을 호출한다.
3. 종료 조건에 도달하면 재귀 호출을 멈춘다.
4. 이전 함수로 돌아가 남은 작업을 실행한다.
5. 모든 함수가 종료되면 최종 결과를 반환한다.

def callback(num):
    num -= 1
    if num == 0:
        print("Count reached zero. Stopping execution.")
        return
    print("Callback function executed. count", num) # 재귀 진입 시 실행
    callback(num)
    print("Callback function executed. count", num) # 재귀 복귀 시 실행

callback(3)

# 2. 수학적 연산의 재귀 구현

1. 1부터 N까지의 합 구하기 (add_numbers)
end에서 시작하여 1씩 감소시키며 자기 자신을 호출하고, 기저 조건(end <= start)에 도달하면 1을 반환하며 역순으로 누적 합계를 계산합니다.

def add_numbers(start, end):
    if end <= start:
        return 1
    return end + add_numbers(start, end - 1)

print(add_numbers(1, 10)) # 출력: 55

2. 팩토리얼 계산 

n이 1 이하가 될 때까지 재귀적으로 내려갔다가, 반환된 값(foo)에 현재의 n을 곱해 올라오며 
5!=120을 계산합니다.

def factorial(n):
    if n <= 1:
        print("n:", n)
        return 1
    print("n:", n)
    foo = factorial(n - 1)
    print("n:", n)
    return n * foo

print(factorial(5)) # 출력: 120

3.거듭제곱 계산

거듭제곱 계산이란 같은 숫자를 여러 번 곱하는 연산이다.

def power(base, exponent):
    if exponent == 0:
        return 1
    return base * power(base, exponent - 1)

print(power(2, 4)) # 출력: 16

# 3.반복 구조와 패턴 출력의 재귀 및 반복문 구현

1. 반복 구조의 개념
반복 구조란 특정 조건이 만족될 때까지 같은 작업을 여러 번 실행하는 프로그래밍 방법이다.
반복 구조는 주로 반복문(while, for)과 재귀 호출을 이용하여 구현할 수 있다.

2. 반복문을 이용한 패턴 출력
반복문을 사용하면 정해진 횟수만큼 별(*)을 출력할 수 있다.

# 재귀 호출 방식
def countdown(n):
    if n <= 0:
        print("발사!!!")
        return
    print(n)
    countdown(n - 1)

# 반복문 방식 비교
# def countdown(n):
#     for i in range(n, 0, -1):
#         print(i)
#     print("발사!!!")

countdown(5)

def print_starts(n):
    if n <= 0:
        return
    print_starts(n - 1) # 먼저 가장 작은 단계(1)까지 들어간 후
    print("*" * n)      # 복귀하면서 1개부터 n개까지 순서대로 출력

print_starts(5)

def multiplication_table():
    for i in range(1, 10):
        for j in range(1, 10):
            print(f"{i} x {j} = {i * j:2}")
        print()

multiplication_table()

def arr_sum(arr, n):
    if n <= 0:
        return 0
    return arr[n - 1] + arr_sum(arr, n - 1)

arr = [1, 2, 3, 4, 5]
print(arr_sum(arr, 5)) # 출력: 15
반복문과 재귀 호출은 동일한 작업을 여러 번 수행할 수 있는 방법이다. 
반복문은 정해진 조건에 따라 작업을 반복하고, 재귀 호출은 함수가 자기 자신을 호출하여 작업을 수행한다. 두 방법 모두 별 모양과 같은 다양한 패턴을 출력하는 데 활용할 수 있다.

# 11월 19일 강의 내용

# 1.그래프(Graph) 자료구조와 인접 행렬(Adjacency Matrix) 구현

그래프(Graph)는 정점(Vertex)과 간선(Edge)을 이용하여 객체 간의 관계를 표현하는 비선형 자료구조입니다.

class graph:
    def __init__(self, size):
        self.SIZE = size
        self.graph = [[0 for _ in range(size)] for _ in range(size)]

def print_graph(graph):
    print("===" + " 그래프 출력 " + "===")
    for row in range(graph.SIZE):
        for col in range(graph.SIZE):
            print(graph.graph[row][col], end=' ')
        print()

# 2. 무방향 그래프(G1) 구성

무방향 그래프(Undirected Graph)는 정점 사이의 간선에 방향이 없는 그래프입니다.

G1 = graph(4)
G1.graph[0][1] = 1
G1.graph[0][2] = 1
G1.graph[0][3] = 1
G1.graph[1][0] = 1
G1.graph[1][2] = 1
G1.graph[2][0] = 1
G1.graph[2][1] = 1
G1.graph[2][3] = 1
G1.graph[3][0] = 1
G1.graph[3][2] = 1

print_graph(G1)

# 3.방향 그래프(G3) 구성 및 출력

방향 그래프(Directed Graph)는 정점 사이의 간선에 방향이 존재하는 그래프입니다.
무방향 그래프와 달리 간선의 출발점과 도착점이 구분됩니다.

G3 = graph(4)
G3.graph[0][1] = 1
G3.graph[0][2] = 1
G3.graph[3][0] = 1
G3.graph[3][2] = 1

print('=== G3 무방향 그래프 ===')
for row in range(G3.SIZE):
    for col in range(G3.SIZE):
        print(G3.graph[row][col], end=' ')
    print()

# 11월 12일 내용

# 1. 이진 트리 자료구조의 구현
이진 트리는 각 노드가 최대 2개의 자식 노드를 가질 수 있도록 구현하는 자료구조이다. 일반적으로 노드(Node)와 포인터(Pointer)를 사용하여 부모 노드와 왼쪽·오른쪽 자식 노드를 연결한다.

# 1. 트리 노드 클래스 정의
트리 노드 클래스(Node Class)는 트리 자료구조에서 각각의 데이터를 저장하고 연결하는 역할을 하는 클래스이다.

class tree_node:
    def __init__(self):
        self.data = None
        self.left = None
        self.right = None
# 2. 노드 생성 및 계층 구조 연결
루트 노드(node1)부터 시작하여 각 노드의 left와 right 속성에 자식 노드를 할당함으로써 계층적인 트리 구조를 만듭니다.

        커피 (node1)
        /          \
   우유 (node2)    주스 (node3)
    /       \         /
물 (node4) 콜라 (node5) 사이다 (node6)
node1 = tree_node()
node1.data = "커피"

node2 = tree_node()
node2.data = "우유"
node1.left = node2   # 커피의 왼쪽 자식 -> 우유

node3 = tree_node()
node3.data = "주스"
node1.right = node3  # 커피의 오른쪽 자식 -> 주스

node4 = tree_node()
node4.data = "물"
node2.left = node4   # 우유의 왼쪽 자식 -> 물

node5 = tree_node()
node5.data = "콜라"
node2.right = node5  # 우유의 오른쪽 자식 -> 콜라

node6 = tree_node()
node6.data = "사이다"
node3.left = node6   # 주스의 왼쪽 자식 -> 사이다
# 3. 이진 트리 레벨별 출력
루트 노드에서 시작하여 .left와 .right 참조를 연속으로 따라가며 트리의 각 깊이(레벨)에 위치한 노드들의 데이터를 순서대로 출력합니다.

print("=== 이진 트리 구조 ===")
print(node1.data, end="")
print()
print(node1.left.data, node1.right.data, end="")
print()
print(node1.left.left.data, node1.left.right.data, node1.right.left.data)






# 11월 5일 내용


# 1. 큐 자료구조의 구현 및 활용
큐는 먼저 들어간 데이터가 먼저 나오는 선입선출 방식의 자료구조입니다. 파이썬의 리스트와 데이터의 앞/뒤 인덱스를 추적하는 전역 변수를 활용하여 큐의 주요 연산을 구현

# 1. 큐 초기화 및 상태 출력
지정한 크기만큼 비어있는 리스트를 생성하고, 데이터의 맨 앞쪽을 가리키는 front와 맨 뒤쪽을 가리키는 rear를 모두 -1로 초기화합니다. print_queue 함수는 리스트의 처음부터 끝까지 순회하며 전체 큐의 상태와 현재 front, rear의 위치를 출력

def init_queue(size):
    global print_q, front, rear
    print_q = [None] * size
    front = -1
    rear = -1
    return print("큐 초기화 완료! 큐의 크기: " + str(size))

def print_queue():
    print("=== 큐 상태 ===")
    print("큐의 크기: " + str(len(print_q)))
    for i in range(len(print_q)):
        print(print_q[i])
    print("현재 front: " + str(front))
    print("현재 rear: " + str(rear))
    print("=================")

# 2. 큐 꽉 참/비어있음 확인

데이터를 삽입하거나 추출하기 전에 큐의 상태를 확인하는 함수
def is_queue_empty():
    global front, rear
    if front == rear:
        return True
    else:
        return False

def is_queue_full():
    global rear
    if rear == len(print_q) - 1:
        return True
    else:
        return False

# 3. 큐 데이터 삽입, 추출, 확인

def enqueue(data):
    global rear
    if is_queue_full():
        return print("큐가 가득 찼습니다!")
    else:
        rear += 1
        print_q[rear] = data
        return print("현재 rear: " + str(rear))

def dequeue():
    global front, temp
    if is_queue_empty():
        return print("큐가 비어있습니다! 삭제할 데이터가 없습니다.")
    front += 1
    temp = print_q[front]
    print_q[front] = None
    return temp

def peek():
    global front
    if is_queue_empty():
        return print("큐가 비어있습니다! Peek 불가!")
    else:
        temp = print_q[front + 1]
        return temp

# 4. 큐 동작 테스트

작성한 함수를 바탕으로 크기가 5인 큐를 초기화한 후 데이터를 삽입하고 확인하는 테스트 코드입니다. 5개의 요소를 모두 삽입하여 큐를 가득 채운 후, peek() 함수를 통해 가장 앞에 있는(다음에 추출될) 데이터를 확인
init_queue(5)
enqueue("커피")
enqueue("우유")
enqueue("주스")
enqueue("물")
enqueue("콜라")

print("======peek() 함수 호출 전======")
print(peek()) # 큐의 가장 맨 앞(front+1)에 있는 데이터 확인
print("======peek() 함수 호출 후======")

print_queue()

# 10월 29일

# 1. 파이썬 웹 브라우저 제어 (webbrowser 모듈)
파이썬의 내장 모듈인 webbrowser를 활용하여 기본 웹 브라우저를 열고 특정 URL로 접속하는 간단한 실습

import webbrowser

webbrowser.open("https://naver.com")

# 2. 스택 자료구조의 구현 및 활용
스택은 나중에 들어간 데이터가 먼저 나오는 후입선출 구조의 자료구조입니다. 파이썬의 리스트와 전역 변수를 활용하여 스택의 주요 기능들을 함수로 구현
def init_stack(size):
    global stack, top
    stack = [None] * size
    top = -1
    return print("스택 초기화 완료! 스택의 크기: " + str(size))  

def print_stack():
    print("=== 스택 상태 ===")
    # range(start, end, step) : start부터 end까지 step만큼 감소하며 역순 출력
    for i in range(len(stack) -1, -1, -1):
        print(stack[i])
    print("=================")
   # 3. 스택 데이터 삽입, 추출, 확인
    
    def push(data):
    global top
    if is_stack_full():
        return print("스택이 가득 찼습니다!")
    else:
        top += 1
        stack[top] = data
        return print("현재 top: " + str(top))

def pop():
    global top
    if is_stack_empty():
        return print("스택이 비어있습니다! 삭제할 데이터가 없습니다.")
    else:
        data = stack[top]
        stack[top] = None
        top -= 1
        return print("Pop된 데이터: " + str(data) + ", 현재 top: ", top)

def peek():
    global top
    if is_stack_empty():
        return print("스택이 비어있습니다! Peek 불가!")
    else:
        data = stack[top]
        return print("Peek 데이터: " + str(data) + ", 현재 top", top)

# 4. 스택 동작 테스트

# 크기가 7인 스택 초기화
init_stack(7)
print_stack()

# Push 연산 수행
push("커피")
push("녹차")
push("꿀물")
push("레몬차")
push("오렌지주스")
push("밀크티")
push("아이스티")

push("콜라") # 스택이 가득 찼습니다! (크기 7 초과 방어)

print_stack()

peek() # 최상단 데이터 확인 (아이스티)

# Pop 연산 수행
pop()
pop()
pop()
pop()
pop()
pop()
pop()

pop() # 스택이 비어있습니다! 삭제할 데이터가 없습니다.

peek() # 스택이 비어있습니다! Peek 불가

print_stack()
