## Web Storage API

| Web Storage API | 설명 |
|-----------------|-----|
| LocalStorage | 이 인터페이스는 브라우저에 데이터를 영구적으로 저장합니다. 데이터는 도메인당 별도로 유지되며, 도메인이나 페이지가 닫혔다 다시 열려도 데이터가 유지됩니다. 이는 사용자의 로컬 스토리지에 키-값 쌍으로 데이터를 저장합니다. |
| SessionStorage | 이 인터페이스는 브라우저 세션 동안 데이터를 저장합니다. 브라우저 세션이 끝나면(브라우저가 닫히거나 탭이 닫힘), 데이터는 삭제됩니다. 이 역시 사용자의 로컬 스토리지에 키-값 쌍으로 데이터를 저장합니다. |
| coockie | 쿠키는 클라이언트 측에서 사용되는 작은 데이터 조각으로, 웹 브라우저에 저장됩니다. 쿠키는 서버에서 클라이언트로 전송되어 웹 사이트 간의 상태 정보를 유지하거나 사용자를 식별하는 데 사용됩니다. 이들은 일반적으로 키-값 쌍으로 저장됩니다. 쿠키는 서버 측에서 HTTP 응답 헤더에 Set-Cookie 헤더를 포함시켜 생성되며, 클라이언트는 해당 쿠키를 자동으로 저장하고, 이후에는 요청할 때마다 해당 쿠키를 서버로 다시 보냅니다. |

- local storage

```js
// LocalStorage에 데이터 저장
localStorage.setItem('cafe', 'coffee');

// LocalStorage에서 데이터 가져오기
const cafe = localStorage.getItem('cafe');
console.log('LocalStorage에서 가져온 cafe :', cafe);
```

- session storage

```js
// SessionStorage에 데이터 저장
sessionStorage.setItem('bakery', '모카빵');

// SessionStorage에서 데이터 가져오기
const bakery = sessionStorage.getItem('bakery');
console.log('SessionStorage에서 가져온 bakery:', bakery);

// 브라우저 세션이 끝나면(브라우저가 닫히거나 탭이 닫힘) SessionStorage의 데이터는 삭제됨
```

- cookie  

> 로컬 파일 시스템에서 HTML 파일을 직접 열 때 쿠키 설정이 작동하지 않을 수 있습니다. 이는 보안 정책 때문입니다. 대부분의 브라우저는 보안상의 이유로 로컬 파일에서 실행되는 JavaScript에서 쿠키 설정을 허용하지 않습니다.  
> 로컬에서 쿠키를 테스트하려면 웹 서버를 설정하고 해당 HTML 파일을 서버에서 제공해야 합니다. 가장 간단한 방법은 Node.js의 내장 모듈인 http-server를 사용하는 것입니다.  

`npm install -g http-server` Nodejs 내장 모듈 서버 설치  
`http-server` 실행  

```js
// 쿠키 생성 (유효 기간: 1시간)
document.cookie
  = "bread=소금빵; expires="
  + new Date(new Date().getTime() + 60 * 60 * 1000).toUTCString()
  + "; path=/";

// 쿠키에서 데이터 가져오기
const cookies = document.cookie.split(';');
let bread;
for (let cookie of cookies) {
  const [name, value] = cookie.trim().split('=');
  if (name === 'bread') {
    bread = decodeURIComponent(value);
    break;
  }
}

console.log('쿠키에서 가져온 bread:', bread);
```