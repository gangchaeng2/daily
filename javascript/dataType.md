1\. 동적 타입 언어
------------

 자바스크립트는 동적 타입 언어로 변수의 타입 지정없이 값이 할당되는 과정에서 자동으로 변수의 타입이 결정됩니다. 즉, 변수는 고정된 타입 없이 같은 변수에 여러 타입의 값을 자유롭게 할당할 수 있습니다.

```js
let val = 'Hello';
typeof val; // string
val = 777;
typeof val; // number
val = true;
typeof val; // boolean
```

2\. 데이터 타입
----------

 데이터 타입은 프로그래밍 언어에서 사용할 수 있는 데이터의 종류를 말합니다.

 자바스크립트의 모든 값은 데이터 타입을 갖고 ECMAScript 표준(ECMAScript 2015 (6th))는 7개의 데이터 타입을 제공합니다.

* 원시타입 (Primitive data type)
  * boolean
  * null
  * undefined
  * number
  * string
  * symbol (ES6 추가)

* 객체 타입 (Object / reference type)
  * object

###  2.1 원시타입

 원시 타입의 값은 변경 불가능한 값**(immutable value)**으로 **(pass-by-value)** 입니다.

####  2.1.1 number

 자바스크립트의 경우 정수와 실수 모두 하나의 타입으로 관리한다.

####  2.1.2 string

 문자열은 배열처럼 인덱스를 통해 접근할 수 있다. 이와 같은 특성을 **유사배열**이라 한다.

 한번 생성된 문자열은 read only로서 변경할 수 없다. 이것을 변경 불가능(immutable)이라 한다.

 문자열은 수정하고 싶다면 새로운 문자열을 만들어서 재할당해야 한다.

```js
var str = 'string';
// 문자열은 유사배열이다.
for (var i = 0; i < str.length; i++) {
  console.log(str[i]);
}

// 문자열을 변경할 수 없다.
str[0] = 'S';
console.log(str); // string
str = 'String'
console.log(str); // String
```

###  2.1.3 boolean

 불리언 타입의 값은 참, 거짓을 나타내는 true, false만 존재한다.

 비어있는 문자열(‘’), null, undefined, 0은 boolean으로 타입변환 시 false값으로 나타나는 것을 알 수 있다.

```js
var bool = false;
bool = 0; 
Boolean(bool); // false
bool = '';
Boolean(bool); // false
bool = undefined;
Boolean(bool); // false
bool = 1;
Boolean(bool); // true
```

###  2.1.4 undefined

 변수 선언 후 값을 할당하지 않은 변수에 접근하거나 존재하지 않는 객체 프로퍼티에 접근할 경우 undefined가 반환된다.

###  2.1.5 null

 프로그래밍 언어에서 null은 의도적으로 변수에 값이 없다는 것을 명시할 때 사용합니다.

###  2.1.6 symbol

 ES6에 새롭게 추가된 타입으로 변경 불가능한 원시 타입의 값입니다.



###  2.2 객체타입

 원시타입을 제외한 나머지 값들은 모두 객체타입으로(배열 객체, 함수…) **pass-by-reference(참조에 의한 전달)** 방식으로 전달된다.



3\. 메모리 구조
----------

 자바스크립트에서 원시타입 변수들은 스택(First-In-Last-Out)에 추가되고 객체타입은 힙 메모리 영역에 추가 됩니다. 

** (단 메모리 주소는 스택에 보관 됨)**

```js
const num1 = 90
const num2 = 100

// Number의 경우 원시타입으로 스택메모리에 추가 됩니다.

// Heap
// ----
// |  |
// |  |
// |  |
// |  |

// Stack 
// memory addr
//           -----
// num2 000 | 100 |
//      001 |     |
//      002 |     |
// num1 003 |  90 |
//      004 |     |
//      005 |     |

// Object 경우 객체타입으로 힙에 할당되고 주소값이 스택에 추가 됩니다.

const obj1 = { val: 80 }
const obj2 = { val: 90 }

// Heap
// mem addr 
//       ----
//  020 |    |
//  021 | 80 |
//  022 |    |
//  023 | 90 |
//  024 |    |

// Stack 
// memory addr
//           -----
// obj2 000 | 023 |
//      001 |     |
//      002 |     |
// obj1 003 | 021 |
//      004 |     |
//      005 |     |

// obj3의 값을 obj1로 복사하는 경우 obj1의 주소값이 obj3의 스택에 추가 됩니다.

const obj1 = { val: 80 }
const obj2 = { val: 90 }
const obj3 = obj1

// Stack 
// memory addr
//           -----
// obj2 000 | 023 |
//      001 |     |
//      002 |     |
// obj1 003 | 021 |
//      004 |     |
// obj3 005 | 021 |
```