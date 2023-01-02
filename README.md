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

#### 파이어베이스 연동을 위한 SDK 설정
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


#### 구글로그인 구현 코드
<pre><code>{
const provider = new GoogleAuthProvider();// Google 공급자 개체의 인스턴스 생성

 //google 로그인 팝업 호출
 document.getElementById('googleLoginButton').addEventListener('click',()=>{
    console.log('google login');
    signInWithPopup(auth, provider)
    .then((result) => {
        // This gives you a Google Access Token. You can use it to access the Google API.
        const credential = GoogleAuthProvider.credentialFromResult(result);
        const token = credential.accessToken;
        // The signed-in user info.
        const user = result.user;
        const google_name = user.displayName;
        const google_email = user.email;
        console.log(user.displayName)
        console.log(user.email);
        console.log(auth.currentUser.displayName);

        newPage(); 
       console.log(result);
       
       
        // ...
    }).catch((error) => {
        // Handle Errors here.
        const errorCode = error.code;
        const errorMessage = error.message;
        // The email of the user's account used.
        const email = error.customData.email;
        // The AuthCredential type that was used.
        const credential = GoogleAuthProvider.credentialFromError(error);
       console.log(result);
        // ...
  });
   
  })
}</code></pre>

버튼클릭시 발생하는 이벤트리스터를 정의하고 그 안에 구글로그인 팝업창을 호출하는 signInWithPopup() 함수를 호출.

.then((result) => { .... 로그인 성공시 수행하는 동작들을 정의 
ex)로그인 성공시 newPage() 함수를 호출하여 메인화면으로 이동


![로그인 화면 ㅇ](https://user-images.githubusercontent.com/90131881/210203802-b681b999-b2ba-4787-8e82-e4cca30944ef.PNG)
![1241244](https://user-images.githubusercontent.com/90131881/210204043-6bd40e1a-040a-4a2a-9772-e7dff540b67d.PNG)

※주의할점
해당 연동된 웹의 도메인을 파이어베이스 설정에서 등록을 해주어야 문제없이 구글로그인 팝업이 실행됨




## 로그인 후 새로고침 및 다른 페이지에 접근해도 로그인이 유지되도록 어떻게 하는가
해결방법: 사용자의 고유아이디인 uid에 대한 토큰 정보를 sesstion에 저장
![세션](https://user-images.githubusercontent.com/90131881/210204213-7b55edcf-7bd4-40a0-a854-d30228213491.PNG)
<pre><code>{
 //세션에 유저 정보 저장
  setPersistence(auth, browserSessionPersistence)
  .then(() => {
      // Existing and future Auth states are now persisted in the current
      // session only. Closing the window would clear any existing state even
      // if a user forgets to sign out.
      // ...
      // New sign-in will be persisted with session persistence.
      return signInWithEmailAndPassword(auth, signInEmail, signInPassword);
  })
  .catch((error) => {
      // Handle Errors here.
      const errorCode = error.code;
      const errorMessage = error.message;
  });
}</code></pre>

참고: https://stackoverflow.com/ 

![토큰](https://user-images.githubusercontent.com/90131881/210204408-493888c5-2fdd-411c-af70-75516753bedb.PNG)

## 로그인 상태에 따른 UI변경
<pre><code>{
//만약 로그인된 상태이면 아래 함수 호출
  auth.onAuthStateChanged(function(user) {
    if (user) {
       // 현재 사용자가 로그인 상태일 경우
    } else {
       // 현재 사용자가 로그인 상태가 아닐 경우
    }
    });
}</code></pre>

위 코드를 사용하여 로그인 상태에 따른 웹의 ui 변경이 가능

#
#
#

## 랭킹시스템 구현
let name = [];
let time = [];

<pre><code>{
firebase.database().ref('users/').orderByChild('time').limitToFirst(100).on('child_added',(data)=>{
  if(data.val().time!=null){
    name.push(data.val().name);
    time.push(data.val().time);
  }
    ranker_1.innerHTML = name[0];  rankTime_1.innerHTML = time[0];
    ranker_2.innerHTML = name[1];  rankTime_2.innerHTML = time[1];
    ranker_3.innerHTML = name[2];  rankTime_3.innerHTML = time[2];
    .
    .
    .
    ranker_20.innerHTML = name[19];  rankTime_20.innerHTML = time[19];
})
}</code></pre>







