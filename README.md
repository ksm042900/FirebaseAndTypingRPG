# FirebaseAndTypingRPG
Implement the login and ranking system by applying firebase to the typing RPG.

저번 프로젝트에서 개발하였던 TypingSite인 "타이핑RPG"에 파이어베이스를 적용(연동)하여 로그인 및 랭킹 시스템을 구현한다.

## Firebase
-파이어베이스가 제공하는 데이터베이스 종류-
1. Cloud Database(FireStore)
2. Realtime Database

### Realtime Database 사용
firestore은 읽기 쓰기 연산 횟수에 따라 비용을 측정합니다. 테스트해본 결과, 작은데이터에 대한 트랜잭션이 많이 발생하는 제 프로젝트에는 적합하지 않다고 생각했습니다.
(적은 횟수로 대용량 데이터를 한번에 읽고 쓸때는 firebase가 좋음)

<pre><code>{
<script type="module">
  // Import the functions you need from the SDKs you need
  import { initializeApp } from "https://www.gstatic.com/firebasejs/9.15.0/firebase-app.js";
  import { getAnalytics } from "https://www.gstatic.com/firebasejs/9.15.0/firebase-analytics.js";
  // TODO: Add SDKs for Firebase products that you want to use
  // https://firebase.google.com/docs/web/setup#available-libraries

  // Your web app's Firebase configuration
  // For Firebase JS SDK v7.20.0 and later, measurementId is optional
  const firebaseConfig = {
    apiKey: "",
    authDomain: "",
    databaseURL: "",
    projectId: "",
    storageBucket: "",
    messagingSenderId: "",
    appId: "",
    measurementId: ""
  };

  // Initialize Firebase
  const app = initializeApp(firebaseConfig);
  const analytics = getAnalytics(app);
</script>
}</code></pre>







