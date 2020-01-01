# npm package list

```
"dependencies": {
    "@cubejs-backend/postgres-driver": "^0.10.19",
    "@cubejs-backend/server-core": "^0.10.11",
    "@cubejs-client/core": "^0.9.0",
    "cookie-parser": "^1.4.4",
    "cors": "^2.8.5",
    "debug": "~2.6.9",
    "dotenv": "^8.0.0",
    "ejs": "^2.6.1",
    "express": "~4.16.0",
    "express-session": "^1.16.2",
    "hashmap": "^2.3.0",
    "hbs": "~4.0.1",
    "http-errors": "~1.6.2",
    "i18n": "^0.8.4",
    "jsonwebtoken": "^8.5.1",
    "method-override": "^3.0.0",
    "morgan": "~1.9.0",
    "node-cron": "^2.0.3",
    "node-scheduler": "^1.0.0",
    "pg": "^7.11.0",
    "request": "^2.88.0",
    "socket.io": "^2.2.0"
  }
```
## cube.js
- 커스텀화와 임베딩을 위해 특별히 개발된 분석 프레임워크
- 데이터 엔지니어가 내부 데이터 인프라를 구축하는 데 사용할 수 있는 도구
- 제작, 고객지향 앱 및 분석 기능을 앱에 임베드 할 때 유용
- 프론트 엔드에서 전체 UI를 사용자 정의 할수 있도록 하면서 
- 대규모 데이터 세트로 쉽게 확장 할 수 있음
```
const CubejsServerCore = require('@cubejs-backend/server-core');
const options = {
	basePath: 'api',
	schemaPath: path.join('schema/cubejs'),
	devServer: false,
	logger: (msg, params) => {
	},
	
}
```

## cube.js-backend/postgres-driver

## cube.js-backend/server-core

## cube.js-client/core

## cookie-parser
- 요청된 쿠키를 쉽게 추출할 수 있또록 도와주는 미들웨어입니다.
- epxress의 request 객체에 cookies 속성이 부여됩니다

### 옵션
- secret : signed 시키는 암호키로 string/array 형태 가능
- maxAge : 만료된 시간을 밀리초 단위로 설정
- expires : 만료 날짜를 GMT 시간으로 설정
- path : cookie 의 경로 default "/"
- domain : 도메인 네임 default "loaded"
- secure : https 에서만 cookie 사용 할 수 있또록 하낟
- httpOnly : 웹서버를 통해서만 cookie 접근 할수 있도록 한다
- signed :  cookie 가 서명되어야 할 지를 결정한다

## cors
-  cors 허용
    - 다른 도메인의 리소스 요청시 허용
        - ```Access-Control-Allow-Origin: *``` 
            - header에 적용
- 크로스오리진(다른 도메인 간의 AJAX 요청)을 가능하게 하고요
```
app.all('/*', function(req, res, next) {
  res.header("Access-Control-Allow-Origin", "*");
  res.header("Access-Control-Allow-Headers", "X-Requested-With");
  next();
});
```
- cors package 를 express 의 미들웨어에 적용
```
var express = require('express');
var cors = require('cors');
var app = express();

// CORS 설정
app.use(cors());

app.get('/products/:id', function (req, res, next) {
  res.json({msg: 'This is CORS-enabled for all origins!'})
});

app.listen(80, function () {
  console.log('CORS-enabled web server listening on port 80')
});
```

## debug
- 노드에서 가장 많이 사용하는 디버깅 모듈
- 로그를 구조적으로 기록할 수 있다는 점에서 console.log 보다 뛰어납니다
- 태그를 지정한 로그 함수를 만들 수 있다
- 태그별로 색상을 쥐서 로그 식별이 수월하

## dotenv
- .env 파일에 따로 환경변수를 저장 할 수 있다.
- DB나 다른 자신의 정보를 .env 파일에 분리해서 gitignore 파일로 정보만 따로 제외하고 공유 할 수 있다
```
설정
require('dotenv').config();
```
```
사용
console.log(process.env.환경변수이름);
```

## ejs
- ejs는 Embedded JavaScript Template의 약자로 nodejs 진영에서 많이 사용하는 템플릿엔진이다. 문법이 단순하다.  
### 기본 문법
- 주석 : <%# %>
- js 코드 : <% %>
- 변수 출력 : <%= %>
- 태그 내부 공백제거 : <%_..._%>
- html escape 안하고 변수 출력 : <%-...%>
###  분할
<% include 파일명 %>
### express 연동
```
app.set('view engine', 'ejs');
```
```
const data = {
	title: 'ejs init',
	message: 'Hello Wordl'
};
res.render('index.ejs',data);
```

## express
- 웹 및 모바일 앱을 위한 일련의 강력한 기능을 제공하는 간결하고 유연한 Node.js 웹 앱 프레임워크
- 웹 서버 프레임워크
- http 유틸리티 메소드 및 미들웨어를 통해 쉽게 빠르게 강력한 API 를 작성

## express-session
- express 프레임워크에서 세션을 관리하기 위해 필요한 미들웨어입니다
```
const session = require('express-session');
app.use(session({
  key: 'sid',
  secret: 'secret',
  resave: false,
  saveUninitialized: true,
  cookie: {
    maxAge: 24000 * 60 * 60 // 쿠키 유효기간 24시간
  }
}));
```
```
const session = require('express-session');
app.use(session({
	secret: 'secret',
	resave: false,
	savUnitialized: true
}));
```
- secret : 쿠키를 임의로 변조하는 것을 방지하기 위한 값 입니다. 이 값을 통해서 세션을 암호화하여 저장합니다.
- resave :  세션을 언제나 저장할 지(변경되지 않아도) 저장하는 값
- saveUnitialized : 세션이 저장되기 전에 unitialized 상태로 미리 만들어서 저장

## hashmap (사용 x )
- nodejs 와 브라우저 hashmap 에서  모두 작동하는 클래스 제공
- HashMap 인스턴스는 모든 유형의 키를 허용하는 키 / 값 쌍을 저장합니다
- 일반 객체와 달리 key가 문자열화 되지 않습니다

## hbs
- handlebars
- 정적 사이트 생성도구로 적합

### express 연동
```
app.engine('hbs',hbs{
	extname: 'hbs',
	defaultLayout: 'main',
	layoutDir: __dirname: ='/views/layouts/',
	partialsDir: __dirname: ='/views/partials/',
});
app.set('view engine','hbs');```
```

## http-errors
- express 에서 에러로 http statsu code 통제하기
### 1. Error 던지기
```
cosnt express = require('express');
const app = express();

app.get('/',(req,res)=>{
	throw new Error('BadRequest');
});
app.listen(3000);
```
- Error를 던지만 500 Internal Server Error 발생

### 2. 상황에 맞춰 4xx, 5xx 던지기
```
cosnt express = require('express');
const app = express();

app.get('/',(req,res)=>{
	res.status(400).json({text: 'todo'});
});
app.listen(3000);
```

### 1+ 2 합치기
- BadRequest 라는 에러 던지면 400, NotFound 라는 에러를 던지만 404가 Http status code로 찍히기 만들고 싶다.
```
const express = require('express');
const app = express();
const createError = require('http-errors');

app.get('/',(req,res)=>{
	throw new createError.BadRequest();
});
```

- 왜 throw new Error() 를 쓰면 안되는가?
* reference : [https://libsora.so/web/express-error-and-http-status-code/](https://libsora.so/web/express-error-and-http-status-code/)

## i18n
- 다국어 서비스를 지원하기 위한 모듈
- app.js와 같은 경로에 i8n,js 생성
[i18n,js]
```
const i18n = require('i18n');
i18n.configre({
	locales: ['ko','en'],
	directory: __dirname + '/locales',
	defaultLocale: 'ko',
	cookie: 'lang'
});

module.express = function(req,res,next){
	i18n.init(req,res);
	res.locals.__ = res.__;
	var current_local = i18n.getLocale();
	return next();
}
```
[app.js]
```
const i18n = require('./i18n');

app.use(i18n);
```

* reference : [https://m.blog.naver.com/PostView.nhn?blogId=cck223&logNo=220974896622&proxyReferer=https%3A%2F%2Fwww.google.com%2F](https://m.blog.naver.com/PostView.nhn?blogId=cck223&logNo=220974896622&proxyReferer=https%3A%2F%2Fwww.google.com%2F)

## jsonwebtoken
- 기존 앱은 세션 기반 회원인증시스템 사용
- 요즘 앱은 토큰 기반 회원인증시스템 사용
- 서버의 확장성이 높아지고, 보안시스템 강화 가능
- JSON Web Token을 손쉽게 생성하고, 또 검증 해줌
- JWT : 사용자 정보를 JSON 객체에 담아 이를 암호화하고 해싱 작업을 거쳐 문자열 토큰을 생성하는 기술
- 클라이언트는 이 토큰을 HTTP Header에 추가하여 요청을 보냄으로써 사용자 인증을 얻게 됩니다.
- JWT는 서버에 저장되지 않아 서버 부하를 일으키지 않음
- 해싱을 통해 데이터의 무결성을 보장하는 인증 방식입니다
- 토큰에 사용자 정보와 권한을 명시!
* reference : [https://velopert.com/2448](https://velopert.com/2448)
```
var jwt = require('jsonwebtoken');
cubejsToken = jwt.sign({}, process.env.CUBEJS_API_SECRET, {
  expiresIn: '1y'
}); //1 year
console.log('\ncubejsToken:' + cubejsToken + '\n');
```

## method-override
- HTML 에서 GET/POST만 가능
- REST API에서 PUT과 DELETE 메소드를 사용할 수 있게 합니다.
- Get/Post 말고 Put/Delete 등 다른 Method를 사용하기 위한 기능
- ```Post/?resource_method=DELETE```
```
var methodOverride = require('method-override');
app.use(methodOverride('_method'));
```
- app.post, app.put, app.delete 메소드 사용(put, delete를 사용하기 위해서는 method-override 패키지 설치 필요)

## morgan
- express 서버에서 발생하는 이벤트들을 기록해주는 미들웨어입니다.
```
var logger = require('morgan');
app.use(logger('dev'));
```
```morgan(format, options)```

- format : 미리 정의된 이름의 문자열
	- 인자에 다라 콘솔에 나오는 로그가 다름
	- 개발시 short | dev
	- 배포시 common | combined
- options : 옵션
- 콘솔에 ```GET / 200 51.267 ms - 1539``` 같은 로그게 찍힌다 
	- HTTP요청(GET) 주소(/) HTTP상태코드(200) 응답속도(51.267ms) – 응답바이트(1539)
	- 
## node-cron
- cron 은 유닉스 계열 컴퓨터 운영체제의 시간 기반 Job 스케쥴러
	- 소프트웨어 환경을 설정하고 관리하는 사람들은 작업을 고정된 시간, 날짜, 간격에 주기적으로 실행 할 수 있도록 스케줄링 하기 위해 cron 을 사용함
- node-corn 은 GNU crontab을 기반으로 하는 node.js 용 순수 자바스크립트의 가벼운 작업 스케쥴러 입니다
	- 전체 crontab 구문을 사용하여 node.js 에서 작업을 예약할 수 있습니다
```
var cron = require('node-cron');
cron.schedule('*/1 * * * *', function() {
  console.log('check analysis status..');
  //알람 확인
  alarm_call();
});

var isCronSampleQuery = true;
cron.schedule('*/1 * * * *', function() {
  // 알람 울릴 수 있도록 zeroday sample insert
  if (isCronSampleQuery) {

    scheduleInsert2();
    console.log(' zeroday cron 10min');
    //  cnt++;
    //  console.log('test zeroday query ..cnt: ' + cnt + '   day: ' + Today());
  }
});
```
## node-scheduler (사용 x)
- 로드 서버를 이용한 스케쥴러 구성
```
var schedule = require('node-schedule'); var scheduler = schedule.scheduleJob('00 * * * *', function(){ //function () {....} console.log('정시를 알려드립니다!'); });  \
```
## pg
- node.js 에는 데이터베이스를 이용하기 위한 기능도 포함되어 있음
- PostgreSQL 
	- 로컬 환경에 PostgreSQL 설치 필요
	- 환경변수 설정필요
	- 설치되는 경로 ```C:\Program  Files\PostgreSQL\x.x\bin```

```
var pg = require('pg');
var pool = new pg.Pool(config);
var strQuery = '';
pool.connect(function(err, client, done) {
    if (err) throw new Error(err);
    client.query(strQuery, (err, result) => {
      done() //pool release
      if (err) {
        console.log('error:', err);
      }
      client.end();
      pool.end();
    })
  });
}
```
## request (사용)
-  http request 발생
- pip 기능 까지 함

## socket.io
- HTTP
	- 무상태 프로토콜(stateless protocol) 으로 어떤 이전 요청과도 무괗나 각각의 요청을 독립적인 트랜잭션으로 취급하는 통신 프로토콜이다
	- HTTP는 클라이언트에 의해 초기화 되기 때문에
	- 서버가 변경사항을 클라이언트에게 알릴 수 있는 방벙이 없음
- Socket.io는 이런 HTTP 한계를 벗어나 Node.js 에서 손쉽게 Real-tme communication(RTC, 실시간 양방향 통신) 웹 애플리케이션을 작성할 수 있따
- WebSocket
	- 사용자의 브라우저와 서버 사이의 동적인 양방향 연결 채널을 구성하는 HTML5 	프로토콜
	- HTTP 통신과 다르게 클라이언트가 특정 주기를 가지고 Polling 하지 않아도 변경된 사항을 시기 적적랗게 전달 할 수 있는 지속적이고 완전한 양방향 연결 스트림을 만들어 주는 기술
	- 서버의 데이터를 클라이언트에 즉시 전달 할 수 있는 실시간 애틀리케이션 작성에 매우 효과적인 프로토콜
- WebSocket API를 통해 서버로 메세지를 보내고 요청없이 응답을 받아오는 것
- socket.io 
```
// server code
var socketio = require('socket.io');
io = socketio.listen(app);
io.on('connection',function(socket){
	socket.on('send message',function(name, text){
		console.log(msg);
		io.emit('receive message',msg);
	});
});

function alarm_call(){
	setMessage('receive message', JSON.stringify({}));
}
function setMessage(event,_msg){
	io.emit(event,_msg)
}

app.use(function(){
	alarm_call();
});
cron.schedule('*1/****',function(){
	alarm_call();
})
```

```
// client code
<script src="/socket.io/socket.io.js"></script>
<script>
var socket = io();
socket.on('recieve message',function(msg){
	// code 작섣
});
</script>
```

* reference : [https://poiemaweb.com/nodejs-socketio](https://poiemaweb.com/nodejs-socketio)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEwMzcyMTkyN119
-->