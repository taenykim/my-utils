# My Utils

내가 쓰는 유틸함수들을 기록하는 레포지토리

### 1. rgb 컬러 -> 16진법 컬러

> arr : [r, g, b] => #000000 : string

```js
const rgbTohexColor = (arr) => arr.reduce((acc, cur) => acc + Number(cur).toString(16), "#")
```

### 2. 랜덤컬러생성

> base : string(0123456789ABCDEF) => #000000 : string

```js
const generateRandomColor = (base) =>
  Array(6)
    .fill()
    .reduce((acc, _) => acc + base[Math.floor(Math.random() * base.length)], "#")
```

### 3. customFetch

> fetch Wrapper function

```js
const getFetch = async (query) => {
  const response = await fetch(`${query}`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
    },
  })
  const json = await response.json()
  return json
}

const postFetch = async (query, body) => {
  const response = await fetch(`${query}`, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(body),
  })
  const json = await response.json()
  return json
}

const putFetch = async (query, body) => {
  const response = await fetch(`${query}`, {
    method: "PUT",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(body),
  })
  const json = await response.json()
  return json
}

const deleteFetch = async (query, body) => {
  const response = await fetch(`${query}`, {
    method: "DELETE",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(body),
  })
  const json = await response.json()
  return json
}

export { getFetch, postFetch, putFetch, deleteFetch }
```

### 4. DOM API

> dom Wrapper function

```js
const $ = (selector, base = document) => base.querySelector(selector)

const $$ = (selector, base = document) => base.querySelectorAll(selector)

const $new = (selector, type) => {
  const elem = document.createElement(type)
  if (selector[`class`]) elem.className = selector[`class`]
  if (selector[`id`]) elem.id = selctor[`id`]
  return elem
}

const $style = (elem, obj) => {
  for (const prop in obj) {
    elem.style[prop] = obj[prop]
  }
}

export { $, $$, $style, $new }
```

### 5. getDate

> 한국기준 현재시간을 SQL datetime으로 반환

```js
const getDateTime = () => {
  const date = new Date()
  return (
    date.getFullYear() +
    "-" +
    ("00" + (date.getMonth() + 1)).slice(-2) +
    "-" +
    ("00" + date.getDate()).slice(-2) +
    " " +
    ("00" + date.getHours()).slice(-2) +
    ":" +
    ("00" + date.getMinutes()).slice(-2) +
    ":" +
    ("00" + date.getSeconds()).slice(-2)
  )
}

export { getDateTime }
```

### 6. prompt

```js
const prompt = (() => {
  const QUESTION_MESSAGE = " > "
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
  })
  return () => {
    rl.question(QUESTION_MESSAGE, (input) => {
      if (input === "q") {
        rl.close()
        process.exit(0)
      }
      const output = inputHandle(input)
      console.log(output)
      rl.close
      prompt()
      return
    })
  }
})()

prompt()
```

### 7. generate Hash Code

```js
const generateHashCode = (s) =>
  s.split("").reduce((a, b) => {
    a = (a << 5) - a + b.charCodeAt(0)
    return a & a
  }, 0)
```

### 8. 약수 구하는 함수

```js
getFactors = (number) =>
  Array(number)
    .fill()
    .map((_, i) => number % (i + 1) === 0 && i + 1)
    .filter((item) => item !== false)
```

### 9. 진법 변환 (10진법 -> x진법)

> target : 변환될 숫자, base : 진법 -> string

```js
const decTo = (target, base) => Number(target).toString(base)
```

### 10. 진법 변환 (x진법 -> 10진법)

> target : 변환할 숫자, base : 진법 -> string

```js
const toDec = (target, base) => parseInt(target, base)
}
```

### 11. 토끼

```js
;`
|￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣￣|
|         hello!        |
|＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿|
　　      ᕱ ᕱ  ||
　       ( ･ω･ ||
 　      /　つΦ> 
`
```

### 12. 랜덤 날짜 생성기

> start : Date, end : Date -> Date (시작날짜와 끝날짜 사이 랜덤 날짜 생성)

```js
const generateDate = (start, end) => new Date(start.getTime() + Math.random() * (end.getTime() - start.getTime()))
```

### 13. URL 토큰화 (정규표현식)

```js
const pattern = /^((\w+):)?(\/\/((\w+)?(:(\w+))?@)?([^\/\?:]+)(:(\d+))?)?(\/?([^\/\?#][^\?#]*)?)?(\?([^#]+))?(#(\w*))?/
const url = "http://user:pass@naver.com:34/taeeun/kim?query=123".match(pattern)
```
