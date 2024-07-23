## CSS Module 사용법

### CSS 작성법

- `foo.module.css` 로 파일명을 선언합니다.

- camelCase를 사용하여 클래스 이름을 선언합니다.

```css
/* box.module.css */

.Box {
  background: black;
  color: white;
  padding: 2rem;
}
```

### 싱글 스타일링

```jsx
import React from "react";
import styles from "./Box.module.css";

function Box() {
  return <div className={styles.Box}>{styles.Box}</div>;
}

export default Box;
```

### 멀티 스타일링

`${style.foo1} ${style.foo2}` 스타일링

```jsx
import React from "react";
import styles from "./App.module.css";

const App = () => {
  return (
    <div className={`${styles.container1} ${styles.container2}`}>
      <h1>I have two Classes</h1>
    </div>
  );
};

export default App;
```

`[styles.container1, styles.container2].join(" ")` 스타일링

```jsx
import React from "react";
import styles from "./App.module.css";

const App = () => {
  return (
    <div className={[styles.container1, styles.container2].join(" ")}>
      <h1>I have two Classes</h1>
    </div>
  );
};
```

clsx 스타일링

> https://www.npmjs.com/package/clsx

```jsx
<div className={clsx(styles.colorRed, styles.backgroundYellow)}>
  // ....
</div>
```

classnames 스타일링

### 조건부 스타일링

인라인 조건부 스타일링

```jsx
<input className={`${styles.one} ${condition ? styles.two : ''}`}>
```

변수 조건부 스타일링

```jsx
import React from 'react';
import styles from './MyComponent.module.css';

const MyComponent = ({ isSpecial }) => {
  // 조건에 따라 클래스를 동적으로 할당
  const containerClassName = isSpecial ? styles.specialContainer : styles.normalContainer;

  return (
    <div className={containerClassName}>
      <p className={styles.text}>Hello, World!</p>
    </div>
  );
};

export default MyComponent;
```

- clsx 조건부 스타일링

```jsx
<input className={
    clsx(styles.input, // 조건이랑 상관없이 무조건 들어감
         {
          [styles.inputError]: !isSuccess && isPasswordConfirm,
          [styles.colorBlue]: isChecked
          [styles.something]: true
         }
        )}
  />
```

### 전역 스타일링

특정 클래스 스타일을 전역으로 사용하고 싶으면, `:global` 을 붙이면 됩니다.

`:global` 을 사용했다면, `import foo.module.css` 파일을 하지 않아도 전역 스타일을 사용할 수 있습니다.

```css
/* foo.module.css */

:global .foo {
	...
}
```

또한 CSS 파일의 전체 스타일을 전역으로 사용하고 싶다면, `global.css` 처럼 일반 CSS를 활용하면 됩니다.

```css
html,
body {
	...
}
```

### 로컬 스타일링

`.module.css` 가 아닌 `.css` 파일에서 `.module.css` 처럼 사용하고 싶다면, 클래스 스타일 앞에 `:local` 을 붙이면 된다.

```css
/* foo.css */

:local .foo {
	...
}
```

### 동적 스타일링

`style` 태그를 사용하여 동적 스타일링을 구현할 수 있다.

```css
/* CardPreview.module.css */

.card {
  display: flex;
  padding: 0px 12px 4px 12px;
  align-items: center;
  margin: 0 auto 0 auto;
  width: 208px;
  height: 123px;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  transition: 0.3s;
  box-shadow: 3px 3px 10px #667085;
}

.chip {
  width: 40px;
  height: 26px;
  background-color: #cbba64;
  border-radius: 4px;
}
```

```jsx
import { useState } from "react";
import styles from "./CardPreview.module.css";
import BlackButton from "../Button/BlackButton/BlackButton";

const PostCssCardPreview = () => {
  const [cardColor, setCardColor] = useState("");

  const handleBlackButton = () => {
    cardColor === "" ? setCardColor("black") : setCardColor("");
  };

  return (
    <article>
      <section className={styles.card} style={{ backgroundColor: cardColor }}>
        <div className={styles.chip} />
      </section>
      <BlackButton onClick={handleBlackButton} />
    </article>
  );
};

export default PostCssCardPreview;
```

### 스타일 재사용

> - https://velog.io/@art11010/CSS-Modules
> - https://github.com/css-modules/css-modules/blob/master/docs/composition.md

#### Composition
같은 css 파일에서 특정 className에 해당하는 스타일 코드를 composes하면 하여 특정 className 정의한 스타일 코드를 그대로 가져옴

```css
.className {
 color: green;
 background: red;
}

.otherClassName {
 composes: className;
 color: yellow;
}
```
#### Dependencies
다른 css 파일에서 특정 className에 해당하는 스타일 코드를 composes 할 수 있음

```css
.otherClassName {
 composes: className from "./style.css";
}
```

### SCSS로 전환

파일명을 `foo.module.scss` 로 변경하면 됩니다.
