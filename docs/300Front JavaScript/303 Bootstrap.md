---
layout: default
title: CSS에서 Bootstrap 이해하기
nav_order: 303
description: CSS에서 Bootstrap 이해하기
parent: JavaScript
---

# CSS에서 Bootstrap 이해하기

## 01 Bootstrap이란

Bootstrap이란, css를 이용한 디자인을 조금 더 쉽게 할 수 있도록 해 주는 프론트엔드 프레임워크입니다.

css 단축키(다양한 class)를 제공해 주는 라이브러리라고 할 수 있습니다.

css가 미리 설정되어 있는 여러 가지 class 이름들을 제공해 줍니다.

### (1) 버튼 예시

예를 들어, 아래의 파란색 버튼을 구현해 보자.

[##_Image|kage@PSciE/btsrdi8D1le/Okk8YkamiELgBDRUvJFink/img.png|CDM|1.3|{"originWidth":164,"originHeight":56,"style":"alignCenter"}_##]

위 버튼을 디자인하기 위해서는, 원래라면 css 파일을 따로 작성해야 한다.

위와 같이 색이 변하고, 클릭 효과(테두리가 빛남)가 있는 만들려면 css가 조금 길어진다.

→ html 파일

```
<button class="blue-button">버튼1</button>
```

→ css파일

```
.blue-button {
    color: #fff;
    background-color: #0d6efd;
    border-color: #0d6efd;
    display: inline-block;
    font-weight: 400;
    line-height: 1.5;
    color: #212529;
    text-align: center;
    text-decoration: none;
    vertical-align: middle;
    cursor: pointer;
    -webkit-user-select: none;
    user-select: none;
    background-color: transparent;
    border: 1px solid transparent;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    border-radius: 0.25rem;
    transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
}
```

하지만 bootstrap을 활용한다면, **css 파일을 별도로 작성하지 않아도** 됩니다.

bootstrap은 위와 같은 코드가 적힌 css 파일을 기본으로 제공합니다.

우리는 **미리 정해진 class 이름만 html(혹은 JSX 컴포넌트)에 추가**하면 됩니다.

아래와 같이 작성하면 자동으로 파란색 버튼이 만들어집니다.

```
<button type="button" className="btn btn-primaryr">
  Primary
</button>
```

css 파일을 작성하는 수고를 덜어 주며, `btn`, `btn-primary`와 같은 **단축키 class명 2개만 사용하면 파란색 버튼 디자인이 완성**됩니다.

[https://getbootstrap.com/docs/5.1/components/buttons/](https://getbootstrap.com/docs/5.1/components/buttons/)

### (2) 간격 만들기 예시

[##_Image|kage@zGPPj/btsq5bicmuG/hBjcY0zCP1hziLyM47PgqK/img.png|CDM|1.3|{"originWidth":151,"originHeight":53,"style":"alignCenter"}_##]

두 버튼을 떨어지게 만들어 보자!!

→ html파일

```
<button className="btn btn-primary">버튼1</button>
<button className="btn btn-danger">버튼2</button>
```

→ css파일

```
.btn-primary {
    margin-right: 20px;
}
```

하지만 bootstrap을 활용한다면, css 파일을 별도로 작성하지 않아도 됩니다.

html의 class로 `me-1`혹은 `me-2`혹은 — `me-5`를 적어주면 됩니다.

숫자가 커질수록 간격이 커집니다.

- e는 end의 약자입니다. end는 오른쪽을 의미합니다. `me`는 `margin-right`입니다.
- s는 start의 약자입니다. start는 왼쪽, `ms-1` 등은 `margin-left`를 의미합니다.

[##_Image|kage@cfkyuU/btsrkOyqrgC/3r59DPUqK5F0qJ1dtgzJ70/img.png|CDM|1.3|{"originWidth":171,"originHeight":69,"style":"alignCenter"}_##]

```
<button className="btn btn-primary me-3">버튼1</button>
<button className="btn btn-danger">버튼2</button>
```

[https://getbootstrap.com/docs/5.1/utilities/spacing/](https://getbootstrap.com/docs/5.1/utilities/spacing/)

### (3) 카드 예시

Bootstrap은 아래와 같이 작성하면 바로 카드를 만들어 줍니다.

class명으로 `card`, `card-body`, `card-title`, `card-text`만 써 주면 됩니다.

**위 4개 class명이 아래 코드의 어디에 나오는지**

[##_Image|kage@b0ouOP/btsrfhn9rmm/aD3alFRggaYH3vzozLNAhk/img.png|CDM|1.3|{"originWidth":308,"originHeight":474,"style":"alignCenter"}_##]

```
<div className="card" style {{ width: "18rem" }}>
    <img src="http://placekitten.com/200/200" className="card-img-top w-100 h-100" />
    <div className="card-body">
        <h5 className="card-title">카드 제목</h5>
        <p className="card-text">
            안녕하세요. 고양이입니다. 이곳은 여러가지 설명이 적히는 곳입니다.
        </p>
        <a href="/portfolio" className="btn btn-primary">
            자세히 보기
        </a>
    </div>
</div>
```

### (4) 이외의 예시들

Bootstrap이 제공하는 다양한 단축키 class

| css의 경우    | Bootstrap class명 | 조절 방법                                |
| ------------- | ----------------- | ---------------------------------------- |
| margin-top    | mt                | mt-0 ~ mt-5                              |
| margin-bottom | mb                | mb-0 ~ mb-5                              |
| width         | w                 | w-25, w-50, w-75, w-100의 숫자(%)로 조절 |
| height        | h                 | h-25, h-50, h-75, mb-5의 숫자로 조절     |
