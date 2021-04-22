  * [Types](#types)
    + [1. number](#1-number)
    + [2. string](#2-string)
    + [3. boolean](#3-boolean)
    + [4. Object](#4-object)
    + [5. Array](#5-array)
    + [6. Tuple (Fixed length and type)](#6-tuple--fixed-length-and-type-)
    + [7. Enum](#7-enum)
    + [Union](#union)
    + [Type Aliases](#type-aliases)
    + [Function return Types and Void](#function-return-types-and-void)
    + [Function types](#function-types)
    + [Function types with CB](#function-types-with-cb)
    + [Never](#never)
  * [Compile ts](#compile-ts)
  * [tsconfig.json](#tsconfigjson)
  * [DOM html](#dom-html)

## Types

### 1. number

### 2. string

### 3. boolean

### 4. Object

```tsx
const person: {} = { name: "Wilker", age: 18 }
const person: object = { name: "Wilker", age 18 }

const person: {name: string; age: number} = { name: "Wilker", age: 18 }
```

### 5. Array

```tsx
const person = { name: "Wilker", age: 18, hobbies: ['coding', 'travel'] }

let someArray: string[]; // ["coding"]
someArray = ['Coding', 'Travel'];
```

### 6. Tuple (Fixed length and type)

```tsx
const person: { hobbies: string[]; role: [number, string] } 
				= { hobbies: ['coding', 'travel'], role: [2, 'author'] }

person.role.push("admin"); // no error! why? typescript 沒辦法抓到 push的
person.role[1] = 10 // this cause error, becuase it should string

```

### 7. Enum

Automatically enumerated global constant identifiers

```tsx
enum Role {
	ADMIN, // 0
	READ_ONLY, // 1
}

/* 如果你不要 開始 從0  */
enum Role {
	ADMIN = 5, // 5
	READ_ONLY, // 6
}

/* 也可以 放 string */
enum Role {
	ADMIN = ‘ADMIN’, 
	READ_ONLY = 100,
}

const person = { 
	name: "Wilker",
	age: 18,
	hobbies: ['coding', 'travel'],
	role: Role.ADMIN 
}

```

### Union

multiple types

```tsx
function combine (input1: number | string, input2: number | string) { ... }
```

### Type Aliases

```tsx
type Combinable = number | string;

function combine (input1: Combinable, input2: Combinable) { ... }
```

### Function return Types and Void

如果你不知道 要return 什麼 type， 就不要 defined 讓 typescript 自己去做

```tsx
// return 是 number
function add(n1: number, n2: number):number { ... }

// return 的是 string
function add(n1: number, n2: number):string { ... }

// console log 是 return void 來的 
function printResult (num: number): void { console.log(num) }

// undefined 很少會用到這個
function printResult (num: number): undefined { 
	console.log(num);	  
	return;
}
```

### Function types

```tsx
let conbimeFn: Function;

function add(n1: number, n2: number):number { return n1 + n2 }
let combineFunction = (n1: number, n2: number) => number;

combineFunction = add;
combineFunction(8, 1);
```

### Function types with CB

```tsx
function addAndHandle(n1: number, n2: number, cb: (num: number) => void) {
	const result = n1 + n2;
	cb(result);
}

addAndHandle(1, 4, (result) => {
	console.log(result);
});
```

### Never

告訴 別的 developer 這個 function 是 intented 沒有 return 任何東西， 它可能 是 error了

```tsx
function generteError(msg: string, code: number): never {
	throw { message: msg, errorCode: code }
}

generteError("An error happen", 500);
```

## Compile ts

```bash
npx tsc app.ts --watch 
npx tsc app.ts -w
```

## tsconfig.json

在 raw的 file 不能 work， 我的 mac os tsc command 是 undefined

```tsx
tsc init
```

```tsx
//tsconfig.json

{
	"compilerOptions": {
		"target": "es5", // compile 去的 Javascirpt version
		"module": "commonjs",
		"lib" [
			"dom", // control + space will popup a list
			"es6",
			"dom.iterable",
			"scripthost"
		], //  這是 tell typescript 你的 default 會有什麼(看 DOM html button解釋)
		"sourceMap": true, // 拿掉command的話 這個 會generate 多一個 file name.js.map， 你可以在 devtool裡的 soruces 也看得到 name.ts的 script 幫助 debug
		"outDir": "./dist", // compile js file into dist folder
		"rootDir": "./src", // make sure 只 compile src裡的 file
		"removeComment": true, // 拿掉 command 
		"noEmitOnError": true, // 如果ts 有 error的話 就不會 compile 全部 file了 
		"strict": true, // 他下面的 別的 strict 都是 true
		
		...
	},
	"exclude": [
		"node_modules", // this would be the default!
		"*.dev.ts", // 不compile 全部 .dev.ts 的file
	],
	"include": [
		...
	],
}
```

## DOM html

```tsx
/**
	! 的意思是 會有這個button 如果沒有放這個的話 button 會出 error 因為 它有可能會沒有這個button在dom。
	Typescript 不懂 你有沒有 ducument 這個 object的，
	因為 你也有可能 用typescript 在 nodejs 
*/
const button = document.querySelector("button")!;

const input = document.getElementById("num")! as HTMLInputElement;

function add(num: number) { ... }
```

# Typescript basic
