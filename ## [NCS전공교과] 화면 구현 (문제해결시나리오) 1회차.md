## [NCS전공교과] 화면 구현 (문제해결시나리오) 1회차
2001020225_23v6.1 UI 설계 확인하기 <br>
2001020225_23v6.2 UI 구현하기 <br>
react프로젝트를 이용하여 회원정보를 출력하고 등록하는 소스코드를 작성하였으나,<br>
프로젝트 실행결과 정상적으로 동작하지 않았습니다.<br>
다음 조건 및 소스코드를 분석하여 원인을 파악하고 조치사항을 작성하시오.<br>
<br>

## [조건]
```
1. 소스코드는 App.js파일에 모두 작성하여 메인페이지에서 바로 나타난다.

2. css는 default.css파일로 App.js파일과 같은 경로에 파일이 존재한다.

3. 기본적으로 3명의 회원이 화면에 나타난다.

4. 회원정보를 입력한 후 등록하면 새로등록한 회원이 마지막에 추가되며,
   입력한 input은 모두 초기화 된다.
```
## [App.js]

```
import { useState } from "react";

function App() {

const [userList, setUserList] = useState([

{ name: "유저1", age: 24, gender: "남자", phone: "010-2732-2241" },

{ name: "유저2", age: 27, gender: "여자", phone: "010-2674-0093" },

{ name: "유저3", age: 30, gender: "남자", phone: "010-3784-2834" },

]);

const [name, setName] = useState("");

const [age, setAge] = useState("");

const [gender, setGender] = useState("");

const [phone, setPhone] = useState("");

const registUser = () => {

const user = { name, age, gender, phone };

userList.push(user);

setUserList([...userList]);

setName("");

setAge("");

setGender("");

setPhone("");

};

return (

<div className="App">

<h1>회원 정보 출력</h1>

<hr></hr>

<table className="member_tbl">

<thead>

<tr>

<th>이름</th>

<th>나이</th>

<th>성별</th>

<th>전화번호</th>

</tr>

</thead>

<tbody>

{userList.map((item, index) => {

<User key={"user" + index} item={item} />;

})}

</tbody>

</table>

<div className="regist-wrap">

<h3>회원 정보 등록</h3>

<hr></hr>

<InputWrap text="이름" data={name} setData={setName} />

<InputWrap text="나이" data={age} setData={setAge} />

<InputWrap text="성별" data={gender} setData={setGender} />

<InputWrap text="전화번호" data={phone} setData={setPhone} />

<button onClick={joinUser}>회원등록</button>

</div>

</div>

);

}

const User = (props) => {

const user = props.user;

return (

<tr>

<td>{user.name}</td>

<td>{user.age}</td>

<td>{user.gender}</td>

<td>{user.phone}</td>

</tr>

);

};

const InputWrap = (props) => {

const text = props.text;

const data = props.data;

const setData = props.setData;

const changeInputValue = (e) => {

setData(e.target.value);

};

return (

<div className="input_wrap">

<label>{text}</label>

<input type="text" value={data} onChange={changeInputValue} />

</div>

);

};

export default App;
```

## [default.css]
```
.member_tbl {

border-spacing: 0;

}

.member_tbl th {

background-color: #000;

color: #fff;

padding: 20px;

}

.member_tbl td {

border: 1px solid #ccc;

text-align: center;

padding: 20px;

}

.input_wrap {

padding: 10px 0px;

}

.input_wrap > label {

display: inline-block;

width: 80px;

}

.input_wrap > input {

width: 150px;

}
```
## 나의 문제풀이(원인)
```
원인 1. 조건2와 같이 default.css파일로 css파일이 따로 존재하는데 import를 해주지 않았다.

원인 2. setUserList([...userList​])만 있으면 조건4와 같이 새로등록한 회원이 마지막에 추가되지 않는다.

원인 3. {userList.map(item, index)​ => {<User key = {"user"+index}item = {item}/>} map 함수 안에서 <User/>를 랜더링하고 있는데​ return 이 없기 때문에 ​실제로 ​반환되지 않는다.

원인 4. 소스코드 아래부분에<button onClick={joinUser}>회원등록</button> 에서 onClick은 {joinUser}라고 되어있는데 소스코드위부분에서 정의된 함수는 registUser이다.

원인 5. User컴포넌트에서 props.user가 아니라 props.item을 사용해야된다. 

원인 6. age는 숫자형식이어야 하는데 문자열이므로 age를 숫자로 변환해주어야 한다.   
```
## 모범답안(원인)	
```
1. css파일을 import 하지 않아서 디자인이 적용되지 않는다.

2. 유저정보 출력 시 map함수에서 return구문이 누락되어 컴포넌트를반환하지 않아 화면에 회원정보가 출력되지 않는다.

3. User 컴포넌트 호출 시 배열에서 꺼낸 데이터를 전달하는 속성이름과 꺼내서 쓰는 속성이름이 달라서 데이터를 꺼내올 수 없다.

4. 회원 등록 시 동작해야하는 함수이름이 달라서 에러가 발생한다.

## 나의 문제풀이(조치내용)
원인1 - 조치내용 : import './default.css';​

원인2 - 조치내용 : setUserList([...userList, user]);​

원인3 - 조치내용 : {userList.map((item, index) => {

                        return <User key={"user" + index} item={item} />;

                })

            }​

원인4 - 조치내용 : button onClick={registUser}

원인5 - 조치내용 : const User = ({ item }) => {

                        return (

                            <tr>

                            <td>{item.name}</td>

                            <td>{item.age}</td>

                            <td>{item.gender}</td>

                            <td>{item.phone}</td>

                            </tr>

                        );

                        };​

원인6 - 조치내용 : <InputWrap text="나이" data={age} setData={(e) => setAge(Number(e.target.value))} />​
```
## 모범답안(조치내용)	
```
1. css 파일을 import 한다. import "./default.css";

2. map함수에 return구문을 추가하여 컴포넌트를 리턴하여 화면에 표현한다.

    {userList.map((item, index) => {

    return <User key={"user" + index} user={item} />;

    })}

3. User 컴포넌트 호출 시 전달하는 속성이름을 통일한다.

    {userList.map((item, index) => {

    return <User key={"user" + index} user={item} />;

    })}

4. 회원 등록 시 동작해야하는 함수이름을 작성한 함수로 설정한다.

    button onClick={registUser}
```