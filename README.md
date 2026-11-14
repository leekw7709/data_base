202430323 이기웅

11월 5일


1. 큐 자료구조의 구현 및 활용
큐는 먼저 들어간 데이터가 먼저 나오는 선입선출 방식의 자료구조입니다. 파이썬의 리스트(print_q)와 데이터의 앞/뒤 인덱스를 추적하는 전역 변수(front, rear)를 활용하여 큐의 주요 연산을 구현

1. 큐 초기화 및 상태 출력
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

2. 큐 꽉 참/비어있음 확인
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

3. 큐 데이터 삽입, 추출, 확인
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

4. 큐 동작 테스트
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

10월 29일

1. 파이썬 웹 브라우저 제어 (webbrowser 모듈)
파이썬의 내장 모듈인 webbrowser를 활용하여 기본 웹 브라우저를 열고 특정 URL로 접속하는 간단한 실습

import webbrowser

webbrowser.open("https://naver.com")

2. 스택 자료구조의 구현 및 활용
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
    3. 스택 데이터 삽입(push), 추출(pop), 확인(peek)
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

4. 스택 동작 테스트

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
