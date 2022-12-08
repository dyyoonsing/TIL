REDO & UNDO

- 데이터 변경은 캐시에서 이루어짐. 그떄 REDO LOG (변경이력 데이터)가 생성. -> 커밋되기 전에 블록의 데이터가 변경됨

- Buffer Cache가 Disk에 Write하기 전에 항상 관련 redo/undo가 write됨
- redo : 복구 및 archive를 위함 / undo : 읽기 일관성 용도

- DML? 데이터 조작어 (select insert update delete)

대량의 데이터를 변경(update insert delete)할 경우 redo/undo로 인한 추가적인 부하도 고려해야 함.
- 대량의 delete 작업은 table full scan이나 index scan 등과 같이 table access 보다 redo undo와 같은 data 생성, 인덱스가 존재한다면 overhead 발생이 성능 저하의 주 된 이유

- 해결 : DDL을 사용하는 방법을 고려
1. [DELETE]주기적으로 삭제해야한다면 ? 해당 칼럼을 key로 하는 Range Partition 구성, 해당 partition table을 delete(DML)이 아닌 alter table [] drop partition [] (DDL)로 작업 대체. DDL은 redo가 발생하지 않고 해당 partition만 drop하는 작업만 수행하므로 성능 개선, 시간 최소화에 큰 기여를 할 수 있음.
    
     (업무) 테스트용 / 자료출력을 위한 임시 테이블 생성의 경우 delete하지 않고 새로 테이블 만들어서 구성하는 편이 더 낫다! 
2. [INSERT] 데이터 입력 대상 속성변경 (nologging) / 힌트 (/*+ apped */)로 redo 발생 억제 가능. 인덱스가 문제 - 그 개수와 성격에 따라 성능이 좌우

[DML 작업의 성능 개선 방법]
1. 테이블 구조 변경
2. 발생 가능한 redo 최소화
3. index 구조변경
4. drop (DDL)


참고 : https://dataonair.or.kr/db-tech-reference/d-lounge/expert-column/?mod=document&uid=52339

