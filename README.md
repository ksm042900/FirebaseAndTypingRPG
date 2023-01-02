# FirebaseAndTypingRPG
Implement the login and ranking system by applying firebase to the typing RPG.

저번 프로젝트에서 개발하였던 TypingSite인 "타이핑RPG"에 파이어베이스를 적용(연동)하여 로그인 및 랭킹 시스템을 구현한다.

## Firebas
파이어베이스가 제공하는 데이터베이스 종류
1. Cloud Database(FireStore)
2. Realtime Database

### Realtime Database 사용
firestore은 읽기 쓰기 연산 횟수에 따라 비용을 측정합니다. 테스트해본 결과, 작은데이터에 대한 트랜잭션이 많이 발생하는 제 프로젝트에는 적합하지 않다고 생각했습니다.
(작은 횟수로 엄청난 데이터를 읽고 쓸때는 firebase가 좋음)



