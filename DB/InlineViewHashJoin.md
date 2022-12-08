### Inline View ? 
- 서브쿼리가 from절 안에서 사용 되는 경우 해당 서브쿼리를 inline view라고 부름

### Hash Join ?
- 조인될 두 테이블 중 하나를 해시 테이블로 선정하여 조인될 테이블의 조인 키 값을 해시 알고리즘으로 비교하여 매치되는 결과값 얻는 방식

### 쿼리 튜닝 과정
- TABLE A : 수익평가이력
- TABLE B : 계좌원장
- TABLE C : 약정원장

C 테이블이 드라이빙 테이블로 A 테이블 OUTER JOIN, B 테이블 INNER JOIN
- BUT) 
1. C 테이블 where 검색조건을 만족하는 데이터 결과값:36만건
2. 플랜 조회해보니 nested loop join으로 진행
    nested loop join의 경우 드라이빙 테이블 데이터가 많을수록, inner table의 인덱스에 따라 불리해지기 때문에 많은 양의 데이터를 join하는데 유리한 hash join으로 튜닝 

- 해결)
1. C 테이블 및 그 조건절을 Inline View로 설정 + no_merge 힌트 부여
2. hash join 힌트 사용
- /*+ no_merge(c) use_hash(a b c) */
