# DELETE TRUNCATE DROP
># 참조 : <https://goddaehee.tistory.com/55>

### Delete
- 데이터만 삭제된다
- 테이블 용량은 줄어들지 않는다.
- 삭제 후 되돌릴 수 있다
- Commit 이전에는 Rollback이 가능하다
- Rollback 정보를 기록하므로 Truncate에 비해서 느리다
- 전체 또는 일부만 삭제 가능하다
- 삭제 행 수를 반환한다.
- 데이터를 모두 Delete해도 사용했던 Storage는 Release 처리 되지 않는다.

### Truncate
- 테이블을 최초 생성된 초기 상태로 만든다.
- 용량이 줄어들고, 인덱스 등도 모두 삭제된다
- Rollback이 불가능하다
- 무조건 전체 삭제만 가능하다
- 삭제 행 수를 반환하지 않는다.
- 테이블이 사용했던 Storage 중, 최초 테이블 생성시, 할당된 Storage만 남기고 Release 처리된다.

### Drop table
- 기존 테이블의 존제를 제거한다. (테이블의 정의 자체를 완전히 삭제)
- Rollback 불가능
- 테이블이 사용했던 Storage는 모두 Release된다
