# <h3> 🔗 event

: 클릭할 때 browser가 a(); 함수를 실행과 동시에 이벤트 객체를 생성해서 인수로 넣어준다.

```javascript
const a = (event) => {
  console.log(event.target.value);
};
document.querySelector("#plus").addEventListener("click", a);
```

<hr />

# <h3> 🔗 고차함수

: 함수를 호출할 때마다 반환 함수를 생성하는 함수

```javascript
const func = () => {
  return () => {
    console.log("hello");
  };
};
```

🔻반환된 함수는 다른 변수에 저장할 수 있고, 그 변수에 저장된 함수를 다시 호출할 수 있다.

```javascript
const innerFunc = func();
innerFunc(); // hello
```

🔻반환하는 값을 바꾸고 싶은 경우 매개 변수를 사용한다.

```javascript
const func = (msg) => {
  return () => {
    console.log(msg);
  }
}

🔻화살표 함수 문법에 따라 함수의 본문에서 바로 반환되는 값이 있으면 { 와 return을 생략할 수 있다.
const func = (msg) => () => {
    console.log(msg);
  }
}
```

🔗 고차함수를 사용하는 이유?
: 비슷한데 특정한 부분만 다른 함수가 많이 나올 경우 `고차함수`를 통해 중복을 제거한다.
함수는 호출하면 어떤 값을 반환한다. 함수가 함수를 반환할 수도 있고, 반환된 함수는 다른 변수에 저장하거나
변수에 저장된 함수를 다시 호출할 수도 있다.

🔻고차함수 형태가 이해하기 어렵다면, 함수가 호출된 코드(함수 이름 뒤에 ()가 붙은 코드)가 있다면 그 부분을 실제
return 값으로 치환한다.

```javascript
const func = () => {
  return () => {
    ...
  }
}

(치환 전)
const innerFunc = func();

(치환 후)
const innerFunc = () => {
  console.log('hello');
};
```

🔻연산자를 operator 변수에 저장하면서 화면에 표시

```javascript
const onClickOperator = (op) => () => {
  if (numOne) {
    operator = op;
    $operator.value = op;
  } else {
    alert("숫자를 먼저 입력하세요.");
  }
};
document.querySelector("#plus").addEventListener("click", onClickOperator("+"));
document
  .querySelector("#minus")
  .addEventListener("click", onClickOperator("-"));
document
  .querySelector("#divide")
  .addEventListener("click", onClickOperator("/"));
document
  .querySelector("#multiply")
  .addEventListener("click", onClickOperator("*"));
```

❔ 다음 코드의 결과는?

```javascript
const hof = (a) => (b) => (c) => {
  return a + b * c;
};
const first = hof(3);
const second = first(4);
const third = second(5);
console.log(third);
```

✅ 23

```javascript
// first
(b) => (c) => {
  return 3 + b * c;
};
// second
(c) => {
  return 3 + 4 * c;
};
// third
3 + 4 * 5;
```

<hr />

# <h3> 🔗 중첩 if문 줄이기

: if문이 중첩되면 코드를 파악하기 어렵기 때문에 if 문의 중첩을 제거한다.

```javascript
예시)
function test() {
  let result = '';
  if (a) {
    if (!b) {
      result = 'c';
    }
  } else {
    result = 'a';
  }
  result += 'b';
  return result;
}
```

순서

1. 공통된 절차를 각 분기점 내부에 넣는다.

```javascript
공통된 절차: result += 'b'; return result;

function test() {
  let result = '';
  if (a) {
    if (!b) {
      result = 'c';
    }
    result += 'b';
    return result;
  } else {
    result = 'a';
    result += 'b';
    return result;
  }
}

```

2. 분기점에서 짧은 절차부터 실행하게 if문을 작성한다. (길이가 짧은 코드를 위로 올린다.)

```javascript
function test() {
  let result = "";
  if (!a) {
    result = "a";
    result += "b";
    return result;
  } else {
    if (!b) {
      result = "c";
    }
    result += "b";
    return result;
  }
}
```

3. 짧은 절차가 끝나면 return이나 break(for문)로 중단한다.
4. else를 제거한다. (중첩 하나 제거)

```javascript
function test() {
  let result = "";
  if (!a) {
    result = "a";
    result += "b";
    return result;
  }
  if (!b) {
    result = "c";
  }
  result += "b";
  return result;
}
```

<hr />
+ 를 제외한 /, -, \*는 알아서 숫자로 바꿔준다
