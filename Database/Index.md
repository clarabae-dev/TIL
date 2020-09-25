출처:  
https://www.geeksforgeeks.org/indexing-in-databases-set-1/  
https://dodo000.tistory.com/22  
https://12bme.tistory.com/149?category=682920  
  
  
## Full Table Scan  
기본적으로 DB는 select문을 수행할 때 Full Table Scan을 수행한다.  
Full Table Scan은 테이블의 각 행을 순차적으로 읽고, 행을 읽으면서 마주한 열이 조건의 유효성을 충족하는지 검사한다.  
찾고자 하는 데이터의 주소를 정확히 모르기 때문에 테이블 전체를 탐색한 후 결과를 반환한다.    
튜플의 수가 많아지면 검색 시간이 매우 오래 걸리는 방법이다. 이를 보완하기 위해 DB는 Index를 제공한다.  

## Database Index  
Indexing은 쿼리 수행 때마다 디스크 I/O 횟수를 최소화 시켜 DB 성능을 최적화하는 방법이다.  
  
![Alt text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190812183525/Structure-of-an-Index-in-Database.jpg)  
  
Index 테이블는 Key-Value 형태로 저장되는데, Index 테이블의 첫번째 컬럼은 탐색키로 테이블의 PK나 후보키의 복사본으로 구성된다.  
이 컬럼은 정렬된 순서로 저장되어 빠르게 데이터에 접근할 수 있다(정렬되지 않을 수도 있다).  
Index 테이블의 두번째 컬럼은 데이터 참조나 포인터로 구성된다. 특정 키값을 찾을 수 있는 디스크 블록의 주소를 가지고 있는 포인터들이다.  
  
실제 읽기 작업을 수행할 때는 데이터 주소를 기억하고 관리하는 Index File과 실제 데이터를 기억하는 Data File을 활용한다.  
데이터를 검색할 때, 먼저 Index File에서 데이터가 저장된 주소를 찾고 이 주소값을 활용해 Data File에서 데이터를 찾는다.  
일례로, 자주 조회하는 컬럼은 Index 테이블을 따로 만들어 select문을 수행할 때 Index 테이블에 있는 값들로 결과 값을 조회할 수 있다.  
  
< 동작 순서 >  
1. Index 테이블에서 select문 where에 포함된 값을 찾는다.  
2. 해당 값의 table_id[PK]를 가져온다.  
3. 가져온 table_id[PK] 값으로 원본 테이블에서 값을 조회해온다.  

Index는 별도의 저장 공간을 차지하고, 항상 정렬 상태를 유지해야한다. 그래서 컬럼 값이 변경되거나 수정, 삭제가 되면 Index도 재정렬해야한다.  
Index는 기본적으로 Key-Value 구조로 구성하며, 테이블에 대한 세부 정보는 가지지 않는다.  
별도의 정보없이 오로지 Key 값을 기초로 하기 때문에 검색과 정렬 속도를 향상시킬 수 있다.  
검색과 정렬 속도를 높이기 위해 DB는 기본적으로 PK를 자동으로 Indexing 한다.  
Index를 많이 사용하면 Index 재정렬에 많은 시간이 소요되어 DB의 성능 저하를 유발할 수 있기 때문에 다양한 알고리즘으로 Index를 관리한다.  
  
  
## Index Algorithm  
  
### B-Tree  
이진트리를 활용해 검색 효율을 증진시킨다.  
  
![Alt text](https://t1.daumcdn.net/cfile/tistory/996A22475AC8939A1B)  
  
> 유색 배경칸은 주소값을, 무색 배경칸은 데이터를 가리킨다.  

  
### B+-Tree  

  
  
## Index Type  

  
### 키에 따른 분류  
1. Primary Index: PK를 포함하는 Index로 키 순서가 레코드 순서를 결정한다.  
2. Secondary Index: Primary Index 이외의 Index로 키 순서가 레코드 순서를 의미하지 않는다.  
  
  
### Sequential File Organization or Ordered Index File  
일반적이고 전통적인 정렬 매커니즘으로, Index는 값의 정렬된 순서를 기반으로 한다.  
이 매커니즘은 다음 두가지 방식으로 저장한다.  

1. Dense Index:  
Data File의 레코드 각각에 대해 하나의 Index 레코드가 만들어진다.  
Index 레코드에는 탐색키와 해당 탐색키 값인 데이터 레코드에 대한 참조가 저장된다.  
  
![Alt text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190812183521/Dense-Index.jpg)  
  
2. Sparse Index:  
Data File의 레코드 그룹에 대해 Index 레코드가 만들어진다.  
데이터 레코드를 찾기 위해 탐색키 값이 가장 크거나 탐색키 값보다 작거나 같은 인덱스 레코드를 찾는다.  
해당 인덱스 레코드가 가리키는 데이터 레코드부터 원하는 데이터 레코드를 찾을 때까지 포인터를 따라 탐색해나간다.  
  
![Alt text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190812183518/Sparse-Index.jpg)  
  
  
### Hash File Organization  
이 방식에서 Index는 버킷 범위에 걸쳐 균일하게 분포되는 값을 기반으로 한다. 값이 할당되는 버킷은 해시함수에 의해 결정된다.  
  
1. Clustered Indexing  
동일한 파일에 두 개 이상의 레코드가 저장되어 있을 때, 이런 종류의 정렬을 Cluster Indexing이라 부른다.  
클러스터 인덱싱을 사용하면 논리 탐색 비용을 줄일 수 있다.  
동일한 것과 관련된 여러 레코드가 한 곳에 저장되고 테이블(레코드)이 두 개 이상 자주 조인되도록 하기 때문이다.  
  
Clustering Index는 순차 Data File로, file은 키가 아닌 필드에서 정렬된다.  
각 레코드들이 유니크하지 않은 PK가 아닌 컬럼을 인덱스로 만드는 경우도 있다.  
이런 경우, 레코드를 빠르게 식별하기 위해 두 개 이상의 컬럼을 그룹화하여 유니크한 값을 만들고 그 값으로 인덱스를 만든다.  
이 방식을 Clustering Index라 한다. 기본적으로 비슷한 특성을 가진 레코드를 함께 묶어 테이블을 재정렬하고, 이에 대해 인덱스를 만든다.  
그래서 테이블의 물리적 순서와 Index 순서가 유사하다.  
예를 들어, 학기별로 학생들을 그룹화하여 각 학기를 Index로 지정할 수 있다.  
  
![Alt text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2016/07/cluster_index.png)  

  
> Primary Indexing  
> 탐색키에 따라 정렬되는 Clustered Indexing 종류로, PK로 인덱스를 만든다.  
> 순차 파일 구성을 유도하는 인덱싱의 기본 형태이다. PK가 유니크하고 정렬되어 저장되기 때문에, 검색이 효율적이다.  

---- 이거 뭐지
PK값이 비슷한 레코드끼리 묶어 정렬된 경우에만 클러스터링 인덱스 또는 클러스터링 테이블 이라 한다.  
PK값에 의해 레코드 저장 위치가 결정되는데, PK값이 변경되면 레코드의 물리적 저장 위치가 변경된다.  
PK값으로 클러스터링된 테이블은 PK값에 의존도가 높아 신중히 PK를 결정해야 한다.  
InnoDB처럼 항상 클러스터링 인덱스로 저장되는 테이블은 PK 기반 검색이 매우 빠르지만 레코드 저장 또는 PK 변경은 상대적으로 느리다.  
--- 여기까지 찾아볼 것
  
2. Non-Clustered or Secondary Indexing  
Non-Clustered Index는 데이터의 위치만 알려준다; 데이터가 실제 저장된 위치에 대한 가상의 포인터 또는 참조 리스트만 알려준다.  
데이터가 인덱스 순서대로 물리적으로 저장되지 않는 대신, 데이터는 리프 노드에 위치한다.  
책의 목차를 예로 들면, 각 항목은 저장된 정보의 페이지 수 또는 위치를 알려준다.  
여기에 책의 각 페이지에 있는 정보인 실제 데이터는 정리되어 있지 않다.  
다만, 데이터 포인트가 실제로 위치한 곳에 대한 정렬된 참조인 페이지를 가지고 있다.  
데이터가 물리적으로 재정렬되지 않아 Sparse ordering이 불가능하기 때문에 Dense ordering만 가능하다.  
데이터를 찾기 위해 포인터를 따라 움직이기 때문에 Clustered Index에 비해 시간이 더 소모된다.  
Clustered Index에서는 데이터가 인덱스 바로 앞에 표시된다.  
  
![Alt text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2016/07/indexing3.png)  
  
3. Multilevel Indexing  
DB의 크기가 커질수록 Index도 커진다. 인덱스는 메인메모리에 저장되기 때문에, single-level 인덱스는 크기가 너무 커질 수 있다.  
Multilevel Indexing은 메인 블록을 여러 개의 작은 블록으로 분리하여 동일한 블록이 단일 블록에 저장될 수 있도록 한다.  
Outer 블록은 Inner 블록으로 나뉘며, 차례로 Data 블록을 가리킨다.  
이 방식은 더 적은 오버헤드만으로 메인메모리에 저장될 수 있다.  
  
![Alt text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190812143045/Untitled-Diagram-41.png)  
  
