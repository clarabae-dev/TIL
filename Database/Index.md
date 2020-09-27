### Full Table Scan  
기본적으로 DB는 select문을 수행할 때 Full Table Scan을 수행한다.  
Full Table Scan은 테이블의 각 행을 순차적으로 읽고, 행을 읽으면서 마주한 열이 조건의 유효성을 충족하는지 검사한다.  
찾고자 하는 데이터의 주소를 정확히 모르기 때문에 테이블 전체를 탐색한 후 결과를 반환한다.    
튜플의 수가 많아지면 검색 시간이 매우 오래 걸리는 방법이다. 이를 보완하기 위해 DB는 Index를 제공한다.  
  
  
  
## Database Index  
Indexing은 쿼리 수행 때마다 디스크 I/O 횟수를 최소화 시켜 DB 성능을 최적화하는 방법이다.  
  
![Alt text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190812183525/Structure-of-an-Index-in-Database.jpg)  
  
Index 테이블는 Key-Value 형태로 저장되는데, Index 테이블의 첫번째 컬럼은 탐색키로 테이블의 PK나 후보키의 복사본으로 구성된다.  
Index 테이블의 두번째 컬럼은 데이터 참조나 포인터로 구성된다. 특정 키값을 찾을 수 있는 데이터 블록/레코드의 주소를 가지고 있는 포인터들이다.  
  
실제 읽기 작업을 수행할 때는 데이터 주소를 기억하고 관리하는 Index File과 실제 데이터를 기억하는 Data File을 활용한다.  
데이터를 검색할 때, 먼저 Index File에서 데이터가 저장된 주소를 찾고 이 주소값을 활용해 Data File에서 데이터를 찾는다.  
일례로, 자주 조회하는 컬럼은 Index 테이블을 따로 만들어 select문을 수행할 때 Index 테이블에 있는 값들로 결과 값을 조회할 수 있다.  
  
< 동작 순서 >  
1. Index 테이블에서 select문 where에 포함된 값을 찾는다.  
2. 해당 값의 table_id[PK]를 가져온다.  
3. 가져온 table_id[PK] 값으로 원본 테이블에서 값을 조회해온다.  

Index는 항상 정렬 상태를 유지해야한다. 컬럼 값이 변경되거나 수정, 삭제가 되면 Index도 재정렬해야한다.  
Index는 기본적으로 Key-Value 구조로 구성하며, 테이블의 세부 정보는 가지지 않는다.  
별도의 정보없이 오로지 Key 값을 기초로 하기 때문에 검색과 정렬 속도를 향상시킬 수 있다.  
검색과 정렬 속도를 높이기 위해 DB는 기본적으로 PK를 자동으로 Indexing 한다.  
Index를 많이 사용하면 Index 재정렬에 많은 시간이 소요되어 DB의 성능 저하를 유발할 수 있기 때문에 다양한 알고리즘으로 Index를 관리한다.  
  
  
  
## Indexing Method  
  
1. Clustered Indexing  
2. Non-Clustered Indexing  
3. Multilevel Indexing  
  
  
### Clustered Indexing  
Clustered Indexing 방법은 테이블 데이터를 인덱스에 따라 **정렬**한다.  
데이터 테이블과 인덱스 테이블의 관계는 1:1 이고, 테이블 데이터는 한가지 조건으로만 정렬된다.  
RDBMS에서는 일반적으로 PK 컬럼을 기준으로 정렬하여 Clustered Index를 만든다.  
  
> Primary Indexing은 순차적인 데이터 구성을 유도하는 인덱싱의 기본 형태이다.  
> 인덱스가 두 개의 필드로 고정되어 있다.  
> 첫번째 필드(Key 필드)는 PK와 같으며, 두번째 필드(Value 필드)는 데이터 블록을 가리킨다.  
> PK가 유니크하고 정렬되어 저장되기 때문에, 인덱스의 순서가 곧 레코드의 순서이다.  
  
  
  
1개 이상의 컬럼들로 인덱스를 만들 수도 있지만, 컬럼 조합이 유니크해야한다.  
테이블 레코드들은 조합된 인덱스에 맞추어 재정렬되고, 때문에 테이블 데이터의 물리적 순서가 인덱스 순서와 유사해진다.  
인덱스 Value 필드는 데이터 레코드가 아닌 블록에 대한 포인터를 가지고 있다.  
  
Clustered Index는 인덱스 리프 노드에 실제 데이터를 저장하며, 추가적인 디스크 공간을 필요로 하지 않는다.  
Clustered Index는 인덱스와 데이터가 동일한 공간에 저장되기 때문에 Non-Clustered Index에 비해 더 빠른 데이터 접근이 가능하다.  
  
![Alt text](https://media.geeksforgeeks.org/wp-content/uploads/20200410115906/Clustered_Index.jpg)  
  
### Non-Clustered Indexing  
테이블과 Non-Clustered Index는 서로 다른 곳에 저장된다.  
때문에 추가적인 저장 공간이 필요하며, 테이블 하나당 여러 개의 Non-Clustered Index를 가질 수 있다.(1:N)  
예를 들어, 책은 목차와 알파벳 순의 용어 설명 두가지 색인을 가질 수 있다.  
  
Non-Clustered Index는 *비정렬* 방식으로, PK가 아닌 유니크 키를 활용하여 쿼리 성능을 향상시킨다.  
유니크한 후보키를 활용하기 때문에 Secondary Indexing이라고도 부른다.  
  
Non-Clustered Index는 논리 정렬 인덱스로 인덱스 순서가 실제 물리적인 테이블 데이터 순서와는 다르다.  
인덱스 Value 필드는 데이터 레코드에 대한 포인터를 담고 있다.  
리프노드는 실제 데이터를 담지 않고 데이터가 실제 저장된 위치에 대한 포인터 또는 참조 리스트만 알려준다.  
예를 들어, 목차의 각 항목에는 챕터명과 페이지 수가 적혀있다. 실제 내용을 확인하기 위해 모든 페이지를 볼 필요가 없다.  
데이터를 찾기 위해 포인터를 따라 움직이기 때문에 Clustered Index에 비해 시간이 더 소모된다.  
  
![Alt text](https://media.geeksforgeeks.org/wp-content/uploads/20200410120011/Non-clustered_Index.jpg)  
  
### Multilevel Indexing  
DB의 크기가 커질수록 Index도 커진다.  
Multilevel Indexing은 메인 블록을 여러 개의 작은 블록으로 분리한다.  
Outer 블록은 Inner 블록으로 나뉘며, 차례로 Data 블록을 가리킨다.  
  
![Alt text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190812143045/Untitled-Diagram-41.png)  
  
  
  
  
## Index Type  
  
  
### Dense Index  
데이터 레코드 각각에 대해 Index 레코드가 만들어진다.  
Index 레코드에는 탐색키와 해당 탐색키 값인 데이터 레코드에 대한 참조가 저장된다.  

![Alt text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190812183521/Dense-Index.jpg)  
  
### Sparse Index  
데이터 블록에 대해 Index 레코드가 만들어진다.  
데이터 레코드를 찾기 위해 탐색키 값이 가장 크거나 탐색키 값보다 작거나 같은 인덱스 레코드를 찾는다.  
해당 인덱스 레코드가 가리키는 데이터 레코드부터 원하는 데이터 레코드를 찾을 때까지 포인터를 따라 탐색해나간다.  
  
![Alt text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190812183518/Sparse-Index.jpg)  
  
### Primary Index  
인덱스는 테이블의 키 필드(PK)와 테이블의 키 필드가 아닌 필드에 대한 포인터로 구성한다.  
테이블이 생성될 때 자동으로 생성된다.  
  
### Secondary Index  
PK가 아닌 필드를 기준으로 인덱싱할 때 사용하는 인덱스로 반드시 정렬되어 있다는 보장이 없다.  
인덱스는 인덱싱 기준 필드와 레코드/블록에 대한 포인터로 구성한다.  
  
  
  
## Index Algorithm  
  
  
### 트리 구조  
  
![Alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqycZ2%2FbtqBQnr4QYG%2F7J8KpnmNaJiTjgS0K9TEIK%2Fimg.png)  
  
위 이미지에서 데이터 하나 하나를 node 라 한다.  
가장 상단의 노드를 root node, 중간 노드들을 branch node, 가장 말단 노드들을 leaf node 라 한다.  
트리구조는 탐색에서 성능을 발휘하는데, 탐색해야할 범위를 줄여서 효율을 증진시킨다.  
  
### B-Tree  
  
![Alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcikell%2FbtqBRvDU1xF%2FCdIhvg8XEhHKaP23vE4Ju1%2Fimg.jpg)  

Multilevel Indexing 방식으로, B-Tree는 데이터가 정렬된 상태로 유지된다. 브랜치 노드에 Key와 Value를 모두 담을 수 있다.  
자주 접근하는 노드를 루트 노드 가까이 배치해두면, 브랜치 노드에 Value가 있기 때문에 탐색이 빨라질 수 있다.  

B-Tree는 어떤 데이터에 대해서도 동일한 시간에 결과를 얻을 수 있는데, 이를 '균일성' 이라 한다.  
B-Tree는 균형 트리와 비균형 트리로 나눌 수 있다. 균형 트리란 모든 루트 - 리프 노드의 거리가 일정한 트리를 말한다.  
그러나 B-Tree는 생성 당시에는 균형 트리이나, 테이블 갱신이 반복되면서 균형이 무너지고 성능이 악화된다.  
자동으로 균형을 회복하는 기능이 있지만, 갱신 빈도가 높은 테이블일 경우, 인덱스 재구성을 통해 트리 균형을 복구하는 추가 작업이 필요하다.  
  
### B+Tree  
  
![Alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/3/37/Bplustree.png/800px-Bplustree.png)  
  
B-Tree의 확장 개념으로, 브랜치 노드에 Value를 제외한 Key만 담는다.  
실제 데이터들은 모두 리프 노드에서 찾을 수 있으며, 리프 노드끼리 Linkedlist로 연결되어 있다.  
  
리프 노드 이외에 Value를 담지 않기 때문에 메모리를 더 확보하여 더 많은 Key들을 수용할 수 있다.  
단일 노드에 더 많은 Key들을 담을 수 있기 때문에 트리의 height는 더 낮아지고, cache hit도 높일 수 있다.  
B+Tree는 리프 노드에 모든 데이터가 있기 때문에 선형 탐색이 한번만 수행된다.  
B-Tree는 모든 노드에서 선형 탐색을 수행해야 한다.  
  
  
  
## 출처  
https://www.geeksforgeeks.org/indexing-in-databases-set-1/  
https://www.geeksforgeeks.org/difference-between-clustered-and-non-clustered-index/  
https://dodo000.tistory.com/22  
https://12bme.tistory.com/149?category=682920  
https://en.wikipedia.org/wiki/B%2B_tree  
https://zorba91.tistory.com/293  
https://www.guru99.com/clustered-vs-non-clustered-index.html  