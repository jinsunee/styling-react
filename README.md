# Learning CSS skills

`css를 다루는 기술`에 대한 공부 및 정리를 목적으로 만들어진 repository 입니다.
- 참고 url
  - [https://velopert.com/1712](https://velopert.com/1712)
  - [https://velog.io/@velopert/react-component-styling](https://velog.io/@velopert/react-component-styling)

## 목차
- Sass
- CSS Module
- styled-components
- 반응형 디자인 (styled-components)

## 1. Sass 
> - Syntactically Awesome Style Sheets
> - CSS pre-processor로서, 복잡한 작업을 쉽게 해주고 코드의 재활용성을 높여줄 뿐만 아니라, 코드의 가독성을 높여주므로써 유지보수를 쉽게 해줍니다.

Sass에서는 두가지의 확장자를 지원합니다.
 - `.sass`
	```
	$font-stack : Noto-sans, sans-serif
	$primary-color : #333

	body
		font: 100% $font-stack
		color : $primary-color
	```
 - `.scss`
	```
	$font-stack : Noto-sans, sans-serif
	$primary-color : #333

	body {
		font: 100% $font-stack;
		color: $primary-color;
	}
	```

scss 문법은 sass를 거쳐야 사용되고, css 문법과 아주 유사하게 사용할 수 있습니다.

## 1. node-sass 설치
Sass를 CSS로 변환해주는 모듈인 `node-sass` 를 설치합니다.
```
$ npm install node-sass
```

## 2. 간단한 예제로 알아보기 

### SassComponent.scss 작성
src/SassComponent.scss
```
.SassComponent {
	display: flex;
	.box {
		background: red; // 일반 CSS 에선 .SassComponent .box 와 마찬가지  
		cursor: pointer;  
		transition: all 0.3s ease-in;
		&.red {  
		  // .red 클래스가 .box 와 함께 사용 됐을 때  
		  background: $red;  
		 @include square(1);  
		}
		&.orange {  
		  background: $orange;  
		 @include square(2);  
		}  
		&.yellow {  
		  background: $yellow;  
		 @include square(3);  
		}  
		&.green {  
		  background: $green;  
		 @include square(4);  
		}  
		&.blue {  
		  background: $blue;  
		 @include square(5);  
		}  
		&.indigo {  
		  background: $indigo;  
		 @include square(6);  
		}  
		&.violet {  
		  background: $violet;  
		 @include square(7);  
		}  
		&:hover {  
		  // .box 에 마우스 올렸을 때  
		  background: black;  
		}
	}
}
```

### SassComponent.js 작성
src/SassComponent.js
```
import React from 'react';  
import './SassComponent.scss';  
  
const SassComponent = () => {  
    return (  
        <div className="SassComponent">  
			 <div className="box red" />  
			 <div className="box orange" />  
			 <div className="box yellow" />  
			 <div className="box green" />  
			 <div className="box blue" />  
			 <div className="box indigo" />  
			 <div className="box violet" />  
		 </div>  
	);  
}  
  
export default SassComponent;
```


## 3. Sass 알아보기
### 주석 (Comment)
`.sass`
```
/* Hello world! */

//  Hello world! 

/* Happy
 Hello world! 
*/
```
한줄 주석인 `//` 는 CSS로 컴파일 되었을 때 나타나지 않습니다. 여러줄 주석은 CSS 와 동일하며 CSS로 컴팡리 되었을 때 나타납니다.

### 변수 (Variable)
변수로 사용 가능한 형태는 숫자, 문자열, 폰트, 색상, null, lists, maps가 있습니다. 
변수를 사용할 때는 `$` 문자를 사용합니다.

`Sass`
```
$primary-color: #333;

body {
	background-color: $primary-color;
}
```

### 변수 범위 (Variable Scope)
Sass의 변수엔 변수 범위가 있습니다. 변수를 특정 selector (선택자) 에서 선언하면 해당 selector 에서만 접근이 가능합니다.
 
 -  `!global` 플래그 : global (전역) 하게 설정
	 ``$primary-color: #eee !global;``
 -  `!default` : 해당 변수가 설정되지 않았거나 값이 null 일 때 값을 설정합니다.

### 수학 연산자 (Math Operators)
| Operator | Description |
|--|--|
| + | addition |
| - | subtraction |
| / | division |
| * | multiplication |
| % | modulo |
| == | equality |
| != | inequality |

`+` , `-` 사용시, 단위를 언제나 통일시켜야합니다.
- 오류날 경우
	- ``$box-width: 100% - 20px``
- 정상 작동하는 경우 
	- ``$box-width: 300px / 960px * 100% ``

### 내장함수 (Built-in Functions)
[https://sass-lang.com/documentation/modules/list](https://sass-lang.com/documentation/modules/list)

### 중첩 (Nesting)
 Sass의 매우 유용한 기능 중 하나는 선언을 중첩시킬 수 있다는 것입니다.

CSS
```
.container {
	width: 100%;
}

.container h1 {
	color: red;
}
```

간단한 CSS면 문제 없지만, CSS 파일이 커지면 유지보수가 어려워집니다.

따라서 Sass에서는 다음과 같이 할 수 있습니다.
```
.container {
	width: 100%;
	h1 {
		color: red;
	}
}
```

또한, 부모 선택자를 리퍼런스 할 때는 `&` 문자를 사용합니다.
```
a {
  color: black;
  &:hover {
    text-decoration: underline;
    color: gray;
  }
  &:visited {
    color: purple;
  }
}
```

##### ** Sass 코드 중첩일 때, 4 레벨 보다 깊게 들어가지 말 것!! **

### 불러오기 (import)
스타일들을 여러 파일들로 나누고, 다른 파일에서 불러와서 사용하는 기능입니다.
다음과 같이 `@import` directive 를 사용하여 특정.scss 파일을 불러올 수 있습니다.
`import "layout.scss"`

심지어 확장자를 붙이지 않아도 됩니다.

`import "layout"`

### 상속 (Extends)
특정 선택자를 상속할 때, `@extend` directive 를 사용합니다.
`scss`
```
.box {
	border: 1px solid gray;
	padding: 10px;
	display: inline-block;
}

.success-box {
	@extend .box;
	border: 1px solid green;
}
```
다음과 같이 css 파일로 컴파일 됩니다.
```
.box, .success-box {
  border: 1px solid gray;
  padding: 10px;
  display: inline-block;
}

.success-box {
  border: 1px solid green;
}
```

### Placeholder
`%` 를 사용하면 상속은 할 수 있지만 해당 선택자는 컴파일되지 않습니다.
`Sass`
```
%box {
	padding: 0.5em;
}

.success-box {
	@extend %box;
	color: green;
}

.error-box {
	@extend %box;
	color: red;
}
```
다음과 같이 css 파일로 컴파일 됩니다.
```
.success-box, .error-box {
  padding: 0.5em;
}

.success-box {
  color: green;
}

.error-box {
  color: red;
}
```

### 믹스인 (Mixin)
extend 와 비슷하지만 argument(인수) 를 받을 수 있습니다.
`@mixin` directive 를 사용하여 선언하고 사용할 때는 `@include` directive 를 사용합니다.

```
@mixin headline ($color, $size) {
	color: $color;
	font-size: $size;
}

h1 {
	@include headline(green, 12px);
}
```
다음과 같이 css 파일로 컴파일 됩니다.
```
h1 {
	color: green;
	font-size: 12px;
}
```
`@content` directive 를 사용한 예제를 해보겠습니다.
```
@mixin media($queryString) {
	@media #{$queryString} {
		@content;
	}
}

.container {
	width: 900px;
	@include media("(max-width: 767px)") {
		width: 100%;
	}
}
```

다음과 같이 css로 컴파일 됩니다.
```
.container {
	width: 900px;
}
@media (max-width: 767px) {
	.contianer {
		width: 100%;
	}
}
```

- `@content` directive 를 사용하면 나중에 `include` 했을 때 그 선택자 내부의 내용들이 `@content` 부분에 나타나게 됩니다.
- `#{ }` ?
	- 특정 문자열을 따로 처리하지 않고 그대로 출력할 때 사용됩니다.

### 함수 (Function)
Build-in Function 과 달리 이 부분은 임의 함수입니다.
Function은 mixin과 비슷하지만 차이점은 다음과 같습니다.

- mixin 
	- style markup 값을 반환
	- `@mixin` directive 를 사용하여 선언
- function 
	- `@return` directive 를 통하여 값을 반환
	- `@function` directive 를 사용하여 선언

Sass
```
@function calc-percent($target, $container) {
	@return ($target / $container) * 100%;
}

@function cp($target, $container) {
	@return calc-percent($target, $container);
}

.my-module {
	width: calc-percent(650px, 1000px);
}
```

다음과 같이 CSS 파일로 컴파일됩니다.
```
.my-module {
  width: 65%;
}
```

반응형 코드 등 자주 사용할 것 같은 함수를 위와 같이 단축함수로 만들어서 사용하는 것도 좋을 것 같습니다.



## 2. CSS Module
CSS 클래스를 불러와서 사용할 때 [파일이름]_[클래스 이름]__[해쉬값] 형태로 클래스네임을 자동으로 고유한 값으로 만들어줘서 컴포넌트 스타일 중첩현상을 방지해주는 기술입니다.
이를 사용하기 위해선, [파일이름].module.css 이런식으로 파일을 저장해야합니다.

src/CSSModule.module.css
```
/* 자동으로 고유해질 것이므로 흔히 사용되는 단어를 클래스 이름으로 마음대로 사용가능*/
.wrapper {
	background: black;
	padding: 1rem;
	color: white;
	font-size: 2rem;
}

/* 글로벌 CSS 를 작성하고 싶다면 */
:global .something {
	font-weight: 800;
	color: aqua;
}
```

src/CSSModule.js
```
import React from 'react';  
import styles from './CSSModule.module.css';  
  
const CSSModule = () => {  
    return (
	    <div className={styles.wrapper}>
		    Hi, I'm <span className="something">CSS Module!</span>
	    </div>
    );  
}  
  
export default CSSModule;
```

위 코드처럼 styles 를 불러오면 하나의 객체를 전달받게 되는데 그 안에는 CSS Module 에서 사용한 클래스 이름과, 해당 이름을 고유화 시킨 값이 key-value 형태로 들어있습니다.

console.log(styles) 를 하면 다음과 같은 결과가 나타납니다.
```
{
	wrapper: "CSSModule_wrapper__CUMkx"
}
```
이걸 사용하기 위해선 `className={styles.[클래스이름]}` 형태로 설정을 해주면 됩니다.

만약에 CSS Module을 사용한 클래스 이름을 두개 이상 적용할 때는 이렇게 하면 된다.

src/CSSModule.module.css
```
/* 자동으로 고유해질 것이므로 흔히 사용되는 단어를 클래스 이름으로 마음대로 사용가능*/

.wrapper {
  background: black;
  padding: 1rem;
  color: white;
  font-size: 2rem;
}

.inverted {
  color: black;
  background: white;
}

/* 글로벌 CSS 를 작성하고 싶다면 */

:global .something {
  font-weight: 800;
  color: aqua;
}
```

src/CSSModule.js
```
import React from 'react';  
import styles from './CSSModule.module.css';  
  
const CSSModule = () => {  
    return (  
        <div className={`${styles.wrapper} ${styles.inverted}`}>
	        안녕하세요, 저는 <span className="something">CSS Module!</span>
        </div>  
 );  
}  
  
export default CSSModule;
```


### classNames
classNames 는 CSS 클래스를 조건부로 설정할 때 매우 유용한 라이브러리입니다. 그리고, CSS Module을 사용할 때 이 라이브러리를 함께 사용한다면 여러 클래스를 적용할 때 편해집니다.

기본적인 사용법
```
import classNames from 'classnames';

classNames('one', 'two'); // 'one two'
classNames('one', { two : true}); // 'one two'
classNames('one', { two: false}); // 'one'
classNames('one', ['two', 'three']); // 'one two three'

const myClass = 'hello';
classNames('one', myClass, {myCondition: true}); // 'one hello myCondition'
```
이런식으로 여러가지 종류의 파라미터를 조합해 CSS 클래스를 설정할 수 있게 되기 때문에, 컴포넌트에서 조건부로 클래스를 설정할 때 굉장히 편하다. 예를 들어서 props의 값에 따라 다른 스타일을 주게 하는게 쉬워진다.

```
const MyComponent = ({highlighted, theme}) => {
	<div className={classNames('MyComponent', {highlighted}, theme)}>
		Hello
	</div>
}
```
이렇게 하면 위 엘리먼트의 클래스로는 highlighted 값이 true 이나 false에 따라 hightlighted 라는 클래스가 적용될 것이고, 추가적으로 theme 으로 전달받는 문자열이 그대로 클래스에 적용될 것입니다.

만약 이런 라이브러리의 도움을 받지 않으면 이런 형식으로 처리해야합니다.
```
const MyComponent = ({highlighted, theme}) => {
	<div className={`MyComponent ${theme} ${highlighted ? 'highlighted' : ''}`}>Hello</div>
}
```

추가적으로, CSS Module 과 함께 쓸 땐 어떻게 편해질 수 있는지 알아보겠습니다.

classNames 를 불러올 때 `classnames/bind` 를 사용하면 클래스를 넣어줄 때마다 `styles.[클래스]` 형식으로 할 필요 없이, 사전에 미리 styles 에서 받아와서 사용하게끔 설정해두고 `cx('class1', 'class2')` 형태로 사용할 수 있게 됩니다.

한번 CSSModule.js 컴포넌트를 다음과 같이 작성해보세요.

src/CSSModule.js
```
import React from 'react';
import classNames from 'classnames/bind';
import styles from './CSSModule.module.css';

const cs = classNames.bind(styles); // 미리 styles 에서 클래스를 받아오도록 설정하고

const CSSModule = () => {
	return (
		<div className={cx('wrapper', 'inverted')}>
			안녕하세요, 저는 <span className="something">CSS Module!</span>
		</div>
	);
}

export default CSSModule;
```

classnames/bind 를 사용하면, CSS Module 을 사용할 때 클래스를 여러개 설정하거나 또는 조건부로 설정을 하게 될 때, 훨씬 편하게 작성 할 수 있을 것입니다.

## Sass와 함께 사용하기
Sass 를 사용할 때도 파일 이름 뒤에 `.module.scss` 을 입력해주면 CSS Module 로 사용할 수 있습니다. 한번 파일 이름을 변경해보세요. 스타일 코드도 조금 바꾸겠습니다.

CSSModule.module.scss
```
/* 자동으로 고유해 질 것이므로 흔히 사용되는 단어를 클래스 이름으로 마음대로 사용 가능*/

.wrapper{
	background: black;
	padding: 1rem;
	color: white;
	font-size: 2rem;
	&.inverted{
		//inverted가 .wrapper 와 함께 사용 됐을 때만 적용
		color: black;
		background: white;
		border: 1px solid black;
	}
	/* 글로벌 CSS 를 작성하고 싶다면 */
	:global { // :global {}로 감싸기
		.something {
			font-weight: 800;
			color: aqua;
		}
	}
}
```

## 3. styled-components
자바스크립트 파일 안에 CSS 를 작성하는 형태입니다.
```
npm install styled-components
```

src/StyledComponent.js
```
import React from 'react';  
import styled, { css } from 'styled-components';  
  
const Box = styled.div`
	/* props 로 넣어준 값을 직접 전달해줄 수 있습니다. */
	background: ${props => props.color || 'blue'};
	padding: 1rem;
	display: flex;
`;

const Button = styled.button`
	background: white;
	color: black;
	border-radius: 4px;
	padding: 0.5rem;
	display: flex;
	align-items: center;
	justify-content: center;
	box-sizing: border-box;
	font-size: 1rem;
	font-weight: 600;
	/* & 문자를 사용하여 Sass 처럼 자기 자신 선택 가능 */
	&:hover {
		background: rgba(255, 255, 255, 0.9);
	}
	/* 다음 코드는 inverted 값이 true 일 때 특정 스타일을 부여해줍니다. */
	${props => 
		props.inverted && 
		css`
			background: none;
			border: 2px solid white;
			color: white;
			&.hover {
				background: white;
				color: black;
			}
		`};
		& + button {
			margin-left: 1rem;
		}
	}
`;
```

### Tagged Template Literal
styled-components 에서는 스타일을 입력할 때 Tagged 템플릿 리터럴(Template Literal) 이라는 ES6 문법을 사용합니다. 이 문법을 사용하는 이유는, ``를 사용할 때 내부에 JavaScript 객체나 함수가 전달 될 때 이를 따로 추출하기 위함입니다.

예를 들어서,
```
`hello ${{foo : 'bar'}} ${() => 'world'}!`
// 결과 : "hello [object Object] () => 'world'!"
```

### props 에 따른 조건부 스타일링
일반 CSS 클래스를 사용했더라면 주로 클래스 이름으로 조건부 스타일링을 해왔었을 테지만, styled-components 에서는 그냥 props 로도 처리 가능합니다.

```
import styled, { css } from 'styled-components';
/* 단순 변수의 형태가 아니라 여러줄의 스타일 구문을 조건부로 설정해야 하는 경우엔 css를 불러와야 합니다. */

const Button = styled.button`
	${props =>
		props.inverted &&
		css`
			background: none;
			border: 2px solid white;
			color: white;
			&:hover{
				background: white;
				color: black;
			}
		`};
	& + button {
		margin-left: 1rem;
	}
`;
```

## 4. 반응형 디자인
styled-components 에서 반응형 디자인을 어떻게 하는지 알아봅시다.

src/StyledComponent.js 의 Box 컴포넌트
```
const Box = styled.div`
	background: ${props => props.color || 'blue'};
	padding: 1rem;
	display: flex;
	/* 기본적으로는 1024px 에 가운데 정렬을 하고 가로 크기가 작아짐에 따라 사이즈를 줄이고 768px 미만으로 꽉 채웁니다. */
	width: 1024px;
	margin: 0 auto;
	@media(max-width: 1024px) {
		width: 768px;
	}
	@media(max-width: 768px) {
		width: 100%;
	}
`;
```

이런 작업을 함수화하여 더 짧게 할 수 있습니다.

```
import React from 'react';
import styled, { css } from 'styled-components';

const sizes = {
	desktop: 1024,
	tablet: 768
};

// 위에 있는 size 객체에 따라 자동으로 media 쿼리 함수를 만들어줍니다.
const media = Object.keys(sizes).reduce((acc, label) => {
	acc[label] = (...args) => css`
		@media (max-width : ${sizes[label] / 16}em) {
			${css(...args)};
		}
	`;
	return acc;
}, {});

const Box = styled.div`
	/* props 로 넣어준 값을 직접 전달해줄 수 있습니다. */
	background: ${props => props.color || 'blue'};
	padding: 1rem;
	display: flex;
	width: 1024px;
	margin: 0 auto;
	${media.desktop`width: 768px;`}
	${media.tablet`width: 768px;`};
`;
```

