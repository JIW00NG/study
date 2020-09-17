## 관계대수와 SQL

### 관계 데이터 모델에서 지원되는 두 가지 언어
- 관계 해석(relational claculus)
  - 원하는 것이 이것이다라고 what 에 대한 것을 명시
- 관계 대수(relatinal algebra)
  - 어떤 절차에 걸쳐 결과를 원하는지 how와 what에 대한 것을 명시
  - 얼핏 보면 관계 대수가 더 안좋지만 이해하는데는 쉽다.
<br></br>

### SQL
- 위 두 언어를 모두 표현할 수 있도록 되어 있다.
<br></br>

### 관계 대수
- 초등학교 처음 들어가서 배우는 산수, 즉 사칙연산
- 여기서 operand가 크게 릴레이션이 된다.
- operand가 한개, 두개 이상인 operator가 있다.
- 원하는 relation이 나올 때 까지 하는 것이 관계 대수 이다.
<br></br>

#### 관계 연산자들의 종류  

| 뷴류 | 연산자 | 표기법 | 단항 또는 이항 |
|:---|:---|:---:|:---:|
| 필수적인 연산자 | 셀렉션(selection) | σ | 단항 |
|  | 프로젝션(projection) | π | 단항 |
|  | 합집합(union) | ∪ | 이항 |
|  | 차집합(difference) | - | 이항 |
|  | 카티션 곱(Cartesian product) | X | 이항 |
| 편의를 위해 유도된 연산자 | 교집합(intersection) | ∩ | 이항 |
|  | 세타 조인(theta join) | ⋈ | 이항 |
|  | 동등 조인(equijoin) | ⋈ | 이항 |
|  | 자연 조인(natural join) | * | 이항 |
|  | 세미 조인(semijoin) | ⋉ | 이항 |
|  | 디비전(division) | ÷ | 이항 |  

<br></br>

- 필수적인 연산자란 cpu가 바로 처리할 수 있는 명령어로 꼭 있어야 하는 명령어이다.
- 편의를 위해 유도된 연산자란 필수 연산자를 이용하여 정의 할 수 있는 연산자 이다. 이를 만드는 이유는 편의를 위해 만들었다. (function과 비슷하다고 보면 된다.)
- 임의의 질의어가 적어도 필수연산자 5개로 표현할 수 있으면 **관계적으로 완전(relationally complete)** 하다고 한다.
<br></br>

![relational algebra](https://user-images.githubusercontent.com/56468120/93436771-2ee37500-f906-11ea-9210-be0922750050.png)
(파란색이 결과)
<br></br>

#### 셀렉션
- 조건을 만족하는 투플을 고른 것 (여러 조건이 있을 수 있다.)
  - 셀렉션 조건을 프레디키트(predicate)라고 함
  - 조건은 일반적으로 릴레이션의 임의의 애트리뷰트와 상수, = , <>, <=,<,>=,> 등의 비교 연산자, AND,OR,NOT 등의 부울 연산자를 사용 할 수 있음

##### 예시
![image](https://user-images.githubusercontent.com/56468120/93438124-d57c4580-f907-11ea-8c8b-2347c82e315b.png)
<br></br>

#### 프로젝션
- 원하는 속성만 고른 것
- 중복된 값을 표기 할 수도 있고 중복된 값을 제거 할 수도 있음
  - 중복 제거는 시간이 너무 많이 걸려서 사용자가 원할 때만 중복 제거
  - 중복은 sort보다 훨씬 오래 걸림

##### 예시
![image](https://user-images.githubusercontent.com/56468120/93438338-22f8b280-f908-11ea-91ec-b7b4d7b4611c.png)
<br></br>

#### 집합 연산자
- 집합 연산자의 입력으로 사용되는 두 개의 릴레이션은 합집합 호환(union compatible)이어야 함
  - union compatible이란 두 릴레이션의 각 속성 도메인이 같아야 하고 속성 수가 같아야 한다는 것이다.
- 합집합: 합칠 때 중복은 제거

#### 카티션 곱
- 카티션은 데카르트의 이름으로 테카르트가 만들었다.(아마 맞을거에요)
- A의 투플들과 B의 투플들을 모두 매치 시킨 것으로 A의 투플 n개 B의 투플 m개 라면 결과는 n * m 개가 나온다.
- 시간이 오래 걸린다는 문제가 있다. A(1000개) X B(10000개)를 해보자(느리다.) 결과는 10000000개의 투플을 가진 릴레이션이 나온다.
- 실제로 잘 쓰지 않음 -> 필요없음 -> 조인연산을 위해 필요한 이론적인 연산

##### 예시
![image](https://user-images.githubusercontent.com/56468120/93440055-3efd5380-f90a-11ea-8e19-551f0360bfce.png)
<br></br>

#### 조인
- 두 릴레이션의 연관된 투플들을 결합하는 연산자
- 매주 중요
- 세타 조인(theta join), 동등 조인(equijoin), 자연 조인(natural join), 외부 조인(outer join), 세미 조인(semijoin) 이 있다.(앞 3개가 일반적)
- 조인 한다는 것은 두 릴레이션의 공통 요인으로 묶는 것
##### 세타조인
- 세타연산자(=,<>,<=,<,>=,>) 중 하나로 표현하는 조인 연산

##### 동등조인
- 세타조인에서 세타연산자가 = 인 조인

![image](https://user-images.githubusercontent.com/56468120/93446521-46bdf780-f90c-11ea-86bc-9405216a3742.png)

##### 자연조인
- 중복되는 속성에서 하나를 제외하는 조인
- 실제로 가장 많이 사용

![image](https://user-images.githubusercontent.com/56468120/93446771-90a6dd80-f90c-11ea-88fd-991fc6f10dd8.png)
<br></br>

##### 외부조인
- 오른쪽/왼쪽/완전 외부 조인 할 떄 오른쪽/왼쪽/양쪽을 모두 포함시키고 조인을 하는 것

![image](https://user-images.githubusercontent.com/56468120/93450146-956d9080-f910-11ea-82f3-7ab700aea56f.png)
![image](https://user-images.githubusercontent.com/56468120/93450180-a1595280-f910-11ea-8fd6-2536d496d40c.png)
![image](https://user-images.githubusercontent.com/56468120/93450221-aae2ba80-f910-11ea-83ae-68cb3cb2ac44.png)

#### 디비전
- 차수가 n+m인 릴레이션 R(A1, A2, ..., An, B1, B2, ..., Bm)과 차수가 m인 릴레이션 S(B1, B2, ..., Bm)의 디비전 R ÷ S는 차수가 n이고, S에 속하는 모든 투플 u에 대하여 투플 tu(투플 t와 투플 u을 결합한 것)가 R에 존재하는 투플 t들의 집합
- 뒤쪽 릴레이션의 모든 투플을 갖는 A의 투플을 찾는 연산

![image](https://user-images.githubusercontent.com/56468120/93447122-057a1780-f90d-11ea-82f3-ccc7b4d3fbda.png)
#### 관계 대수 질의의 예

![image](https://user-images.githubusercontent.com/56468120/93447643-98b34d00-f90d-11ea-87e7-ac8308f4fd1d.png)
<br></br>

#### 관계 대수의 한계
- 산술 연산 불가
- 집단 함수(aggregate function) 지원 안함
- 정렬 불가
- 관계 대수는 검색연산만 되어 있어 DB 수정 불가
이러한 한계 떄문에 추가된 관계 대수 연산자가 있다.
  - 집단 함수
  
  ![image](https://user-images.githubusercontent.com/56468120/93449279-83d7b900-f90f-11ea-9677-14a59ecee641.png)

  - 그룹화
  
  ![image](https://user-images.githubusercontent.com/56468120/93449331-92be6b80-f90f-11ea-94e1-33275bc33ea0.png)
   
   - 디스크에 저장된 데이터를 모두 읽어 sort하고 그룹화 하고 평균을 내야 하기 때문에 오래걸린다.

매번 database를 수작업으로 업데이트 하는 것이 오래걸리는 등의 문제로 분석을 온라인으로 realtime으로 하는 것이 필요하여 onlab이 등장하였다.
