---
layout: default
title: React에서 Bootstrap CSS 사용하기
nav_order: 402
description: React Bootstrap
parent: React
---

# React에서 Bootstrap CSS 사용하기

### (1) 라이브러리 설치

→ create-react-app으로 프로젝트 폴더 생성

아래 2개 커맨드 중 1개 선택하여 설치

```
1. npm install bootstrap
2. yarn add bootstrap
```

### (2) css 불러오기

`index.js`를 아래와 같이 작성하여 `bootstrap.min.css`를 import

→ min은 minified의 약자로, css 코드를 압축한 형태라는 것을 의미합니다.  
→ 빈칸, 빈 줄을 최대한 줄여서 웹 브라우저가 코드를 조금이라도 빠르게 읽을 수 있도록

```
import React from "react";
import ReactDOM from "react-dom";
import App from "/.App";
import "bootstrap/dist/css/bootstrap.min.css";

ReactDOM.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>
    document.getElementById("root")
);
```

### (3) Bootstrap 공식 문서에서 필요한 디자인의 class명 확인

[##_Image|kage@oXnk0/btsrh3bzHlm/2wgiVHo79HmDthRMzy3rmK/img.png|CDM|1.3|{"originWidth":1033,"originHeight":462,"style":"alignCenter"}_##]

ex 초록색 버튼에 필요한 css명: `btn`과 `btn-success`

### (4) JSX의 className에 class명 추가

일반 html에서는 `class = "btn btn-success"`

React JSX에서는 `className="btn btn-success"`로 작성

```
<button className="btn btn-success">버튼입니다.</button>
```

[##_Image|kage@dwrJMH/btsq1KLWxqm/DwcizYCbvv5KDsqeN4glqK/img.png|CDM|1.3|{"originWidth":131,"originHeight":54,"style":"alignCenter"}_##]

# 4\. Bootstrap 이해하기 - 컴포넌트 편

## 01 React-Bootstrap이란

```
<button className="btn btn-primary mb-3">버튼</button>
```

한편, **React는 컴포넌트 단위로 웹 화면(UI)를 꾸밉니다.**

컴포넌트는 `<MyComponent />`와 같이 **첫 글자가 대문자**로 시작합니다.

(`<div>, <button>` 등의 기본 element과 구분하기 위함)

만약에 Bootstrap 디자인이 적용된 컴포넌트가 미리 만들어져 있다면, 즉 `<Button />`과 같은 컴포넌트가 있어서 그대로 가져와 쓸 수 있다면 편할 것 같습니다.

Bootstrap은 React를 위해 이런 컴포넌트를 만들었으며, `react-bootstrap` 라이브러리에 포함하였습니다.

### (1) 버튼 예시

예를 들어, 아래의 파란색 버튼은 Boostrap 컴포넌트로 다음과 같이 작성됩니다.

[##_Image|kage@bm9LCm/btsq50AH7LQ/q92VS4Z9jXplr1vtqo0l90/img.png|CDM|1.3|{"originWidth":121,"originHeight":74,"style":"alignCenter"}_##]

```
<Button variant="primary">Primary</Button>
```

**!**기존과의 차이

1.  button이 대묹자인 Button으로 바뀜
2.  className 대신 variant로 바뀜 (이때 variant는 `props`)

위와 같은 컴포넌트를 쓰면, 이제 className마저도 작성하지 않게 됩니다.

필요한 css가 컴포넌트에 이미 내장되어 제공되었기 때문입니다.

(물론, 필요에 따라 className을 작성하는 경우도 종종 있습니다)

추가 컴포넌트들을 아래 링크에서 확인해 보세요!

(사이트 형태가 기존의 css Bootstrap과 유사하게 생겼으나, **다른 사이트**입니다)

[https://react-bootstrap.github.io/components/buttons/](https://react-bootstrap.github.io/components/buttons/)

### (2) 폼(Form) 예시

Bootstrap은 아래와 같이 작성하면 바로 **로그인용 폼**을 만들어 줍니다.

**사이트에서 코드를 복사하고 붙여넣으면 끝**이기에, 디자인 면에서 개발자의 수고를 크게 덜어줍니다.

아래 코드는 길어서 어려워 보이지만, 사실 하기 링크에서 복사하고 문구만 한국어로 수정한 코드입니다.

[##_Image|kage@dSW6Ve/btsrgjMMcIl/F2usAVmJ3hGmdPEuHmJfq1/img.png|CDM|1.3|{"originWidth":318,"originHeight":304,"style":"alignCenter"}_##]

```
function SimpleLogin() {
  return (
    <Form>
      <Form.Group className="mb-3" controlId="formBasicEmail">
        <Form.Label>Email address</Form.Label>
        <Form.Control type="email" placeholder="이메일을 입력하세요." />
        <Form.Text className="text-muted">
          이메일은 안전하게 보관됩니다.
        </Form.Text>
      </Form.Group>

      <Form.Group className="mb-3" controlId="formBasicPassword">
        <Form.Label>Password</Form.Label>
        <Form.Control type="password" placeholder="비밀번호" />
      </Form.Group>
      <Form.Group className="mb-3" controlId="formBasicCheckbox">
        <Form.Check type="checkbox" label="체크박스입니다." />
      </Form.Group>
      <Button variant="primary" type="submit">
        제출
      </Button>
    </Form>
  );
}
```

### (3) 카드 예시

아래와 같이 `Card 컴포넌트`를 쓰면 바로 카드를 만들 수 있습니다.

이 역시 Bootstrap 사이트에서 복사 후 한국어로 문구만 변경한 것입니다.

이때 `className`이 있는 것을 볼 수 있습니다.

컴포넌트를 쓴다고 `Bootstrap css`를 안 쓰는 것이 아니며, 필요한 경우 쓸 수 있습니다.

**Bootstrap 컴포넌트와 css는 섞어서 사용합니다.**

특히 **미세한 간격 조정**을 할 때 className css(`mt-2 등`)를 사용합니다.

[https://react-bootstrap.github.io/components/cards/](https://react-bootstrap.github.io/components/cards/)

[##_Image|kage@IN3Cz/btsrgNth1ps/WReVhCCugyNXMEWkM71bmk/img.png|CDM|1.3|{"originWidth":486,"originHeight":636,"style":"alignCenter"}_##]

아래 코드에서 `Card, Card.Body, Card.Title, Card.text`라는 **총 4종류의 컴포넌트를 찾아!**

```
export default function SimpleCard() {
  return (
    <Card className="w-25">
      <Card.Img variant="top" src="https://placekitten.com/200/200" />
      <Card.Body>
        <Card.Title>카드 제목</Card.Title>
        <Card.Text>안녕하세요, 이 곳은 카드 설명이 적히는 곳입니다.</Card.Text>
        <Button variant="primary">버튼입니다.</Button>
      </Card.Body>
    </Card>
  );
}
```

## 02 React에서 React-Bootstrap 쓰는 법

### (1) 라이브러리 설치

→ create-react-app으로 프로젝트 폴더가 이미 생성되어 있어야 합니다.

아래 2개 커맨드 중 1개를 택하여 설치합니다.

```
1. npm install react-bootstrap
2. yarn add react-bootstrap
```

### (2) 라이브러리에서 필요한 컴포넌트를 불러옵니다.

- `Card`, `Form`, `Button` 만들기

```
import { Card, Button } from "react-bootstrap";
import { Form, Button } from "react-bootstrap";
import { Button } from "react-bootstrap";
```

### (3) JSX에서 해당 컴포넌트 사용

React-Bootstrap 사이트의 예시 코드 참고

사이트를 탐방하면서 익혀 보세요~

Card : [https://react-bootstrap.github.io/components/cards/](https://react-bootstrap.github.io/components/cards/)

Button : [https://react-bootstrap.github.io/components/buttons/](https://react-bootstrap.github.io/components/buttons/)

Form : [https://react-bootstrap.github.io/forms/overview/](https://react-bootstrap.github.io/forms/overview/)

Checkbox, Radios ： [https://react-bootstrap.github.io/forms/checks-radios/](https://react-bootstrap.github.io/forms/checks-radios/)

[##_Image|kage@yhMo4/btsrkP5at0D/A9FAcKc5au7tQumbiVj0a1/img.png|CDM|1.3|{"originWidth":184,"originHeight":138,"style":"alignCenter"}_##]

다양한 형태의 input이 있는 Form ： [https://react-bootstrap.github.io/forms/layout/](https://react-bootstrap.github.io/forms/layout/)

[##_Image|kage@nvSZT/btsrdjfqgkn/0vEJpaxXbhI7NdXPz15fT0/img.png|CDM|1.3|{"originWidth":1123,"originHeight":292,"style":"alignCenter"}_##]

드롭다운 버튼： [https://react-bootstrap.github.io/components/dropdowns/](https://react-bootstrap.github.io/components/dropdowns/)

[##_Image|kage@cqOvIy/btsrkPRDtaS/9gcnQTTbOqF9WbkEni8XFK/img.png|CDM|1.3|{"originWidth":199,"originHeight":178,"style":"alignCenter"}_##]

네비게이션 바 (= 헤더）： [https://react-bootstrap.github.io/components/navs/](https://react-bootstrap.github.io/components/navs/)

[##_Image|kage@QfcQE/btsrgmbCWPm/F2tQBUJcDnWxpPzD4CgtEk/img.png|CDM|1.3|{"originWidth":304,"originHeight":68,"style":"alignCenter"}_##]
