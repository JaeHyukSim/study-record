# Transaction
>## 참고 : <https://www.edwith.org/boostcourse-web/lecture/16767/>

### Transaction ?
- Atomicity
- Consistency
- Isolation
- Durability

### Atomicity
- rollback and commit
- 하나의 트랜잭션의 결과는 성공 or 실패! 중간이 있으면 안된다

### Consistency
- 트랜잭션이 진행되는 동한 데이터는 변경된다. 하지만 변경되기 전 데이터를 참조해야 한다.
- 즉, 데이터가 바뀌어도 그것이 바로 보여지는 것이 아니라, 바뀌기 전을 참조.
- 각 사용자는 일관성 있는 데이터를 볼 수 있다.

### Isolation
- 둘 이상의 트랜잭션은 서로의 연산에 끼어들 수 없다.
- 즉 하나의 트랜잭션이 완료될 때까지, 다른 트랜잭션이 특정 트랜잭션의 결과를 참조할 수 없다.

### Durability
- 트랜잭션이 성공한다면 그 결과는 영구적으로 반영되어야 한다.
