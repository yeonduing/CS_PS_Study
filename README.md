# CS_PS_Study
부스트캠프 이후 CS / PS 공부 모임

<br/>

## 참여자

류연수 | 유선규 | 조병건 | 조수정 
--- | --- | --- | ---
[@yeonduing](https://github.com/yeonduing) | [@sunkest](https://github.com/sunkest) | [@marulloc](https://github.com/marulloc) | [@Sueaty](https://github.com/Sueaty)

<br/>

## 🔨 규칙
매일 모여 한 시간 반동안 공부한 내용을 발표 및 공유하고 그에 맞는 알고리즘 문제를 4시간 동안 풉니다. 문제 선정은 사전에 하며 난이도는 하, 중하, 중, 중상으로 총 4 문제를 풉니다. 매일 시험을 본다는 생각으로 정해진 시간에 풀어야하며 난이도 하, 중하 문제의 경우 한 번에 통과하지 못할 시 딱밤🔨이 적립됩니다. 5시 이후에 문제 풀이를 합니다. 문제풀이 시간에는 각자의 풀이를 공유하며 해답을 찾습니다. 

<br/>

## 🕙 시간표
시간 | 일정 | 비고
:---: | :--- | ---
10:30<br>-<br>11:50 | CS 관련 지식 공부<br>각자 공부한 개념 공유 및 발표 | 
11:50<br>-<br>13:00 | 점심시간<br> | 
13:00<br>-<br>17:00 | 알고리즘 문제 풀기<br>총 4 문제 | 브론즈: 0-1개<br>실버: 1-2개<br>골드4-5: 1개<br>골드1-3: 1개
17:10<br>-<br>19:00 | 문제 풀이 및 각자의 풀이법 공유

<br/>

## 📆 스케쥴(1 주차)
요일<br>담당자 | 월 | 화 | 수 | 목 | 금 | 토 | 일
:---: | --- | --- | --- | --- | --- | --- | ---
병건 | [코사라주]()<br>[이론 정리](https://github.com/yeonduing/CS_PS_Study/blob/main/Algorithm/Kosraju's%20Algorithm.md) | | | | | | |
선규 | [위상정렬](https://programmers.co.kr/learn/courses/30/lessons/67260)<br>[이론 정리](https://github.com/yeonduing/CS_PS_Study/blob/main/Algorithm/위상%20정렬%20(Topological%20Sort).md) | | | | | | |
수정 | [다익스트라](https://www.acmicpc.net/problem/10282)<br>[이론 정리](https://github.com/yeonduing/CS_PS_Study/blob/main/Algorithm/The%20Dijkstra's%20Algorithm.md) | | | | | | |
연수 | [타잔](https://www.acmicpc.net/problem/2150)<br>[이론 정리]() | | | | | | |

<br/>

## CS 공부 목차

### 코테에 도움이 될만한, 생소한, 알고리즘
- 면접용
  - 정렬
    - 버블 선택
    - 퀵 머지
    - 계수 정렬
- 코테용
   - 투포인터
   - KMP
   - SUFFIX ARRAY
   - 크루스칼
   - 벨만포드
   - 다익스트라(수정)
   - 플로이드
   - SCC
       - 위상정렬(선규)
       - 타잔(련수)
       - 코사라주(병건)
          - 최대힙 최소힙
          - DISJOINT SET
     
### 지식
- bigO 
   - 시간복잡도
   - 공간복잡도

- 디자인
   - oop vs fp

- 자바
  - 오버로딩 vs 오버라이딩
  - 컬렉션 프레임워크 
  - 가비지 컬렉션
  - 얕은 복사 & 깊은 복사
  - String Builder
  - 가변크기배열 


### 자료구조
- 해시테이블
    
- 스택 큐 데크

- 최소힙 최대힙

- 트리
   - 최소신장트리
   - 레드블랙
   - avl
  
- 트라이

### 소프트웨어 공학
- 시스템 설계 및 확장성
     - 단계별 접근법 등등...
     - 시스템 설계 기법
- 애자일

### 데이터베이스 
- 비정규화 vs 정규화 데이터베이스(책에 있는거 위주로)
- 설계(책에 있는 거 그대로)
   - 소규모 데이터 베이스 설계
   - 대규모 데이터 베이스 설계
- NOSQL VS SQL
- RDBMS 내부 동작

### 운영체제 & 컴구조
- 프로세스와 스레드
   - 프로세스 3가지 상태와 상태 변이
   - 컨텍스트 스위치 
       - PCB
       - 인터럽트      
- 동기화 ipc
    - MUTUAL EXLUSION 설꼐할 때 주의
    - 뮤텍스
    - 세마포어
    - 교착상태와 교착상태 방지
- 스케쥴링 방식
    - RR이거나 등등
- 페이징과 세그멘테이션
- 2의 보수와 음수 (1의 보수와 차이점) 
    - lert, right shift
    - 부동소수점  
- 컴파일러 VS 인터프리터
    - 오토마타
    - 어휘분석과 구문분석
    - 어셈블리

### 네트워크
- OSI 7계층
- IP
  - 서브넷 마스크
  - IPv6
- HTTP
- TCP/UDP
   - 3 WAY
- DNS
- 브로드캐스트 /멀티캐스트 / 유니캐스트 등등의 차이

### WEB
- 브라우저 동작 방법
- 쿠키 & 세션
- Web Server와 WAS
- 프록시 & 방화벽
- 로드밸런서
- CDN
- CORS

### JS
- 얕은 복사 & 깊은 복사
- node 런타임
  - NODE의 쓰레딩이든 뭐 
  - JS의 이벤트 풀?? ㅇㅇ 그런거
- 호이스팅
- CALLBACK, PROMISE, ASYNC/AWAIT
- 실행컨텍스트 & closure & this
- 번들러 & 트랜스파일링
- SPA
- SSR VS CSR
- REST API

### iOS
- Combine
- GCD
- Core Data
