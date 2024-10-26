

## What is Flow:
It is an npm package that provides static type check for Javascript

## How to use it:

Development installation of flow:
```bash
npm install --save-dev flow-bin
```

Can also be installed Globally:

```bash
npm install -g flow-bin
```

Types check can also be run directly using:

```bash
npx flow
```

Flow can be used with Babel but can also be processed with the flow-remove-types package

Global installation of the dedicated flow remove types packages:

```shell
npm install --global flow-remove-types
```

## How to add types in the code:

- **Flow Comments**: Use `// @flow` at the top of your file to enable Flow type checking.

- **Add Type Annotations**: Use `:` followed by the type after variables, function parameters, and return types. For example:
```js
function add(a: number, b: number): number {
  return a + b;
}
```
- **Declare Variable Types**: Specify the type when declaring variables:
```js
let name: string = "John";
```
- **Use Object Types**: Define types for objects using `{}`:
```js
type User = {
  name: string,
  age: number,
};

let user: User = { name: "Jane", age: 30 };
```
- **Utilize Flow's Built-in Types**: Flow has built-in types like `string`, `number`, `boolean`, `Array<T>`, etc.:
```js
let ids: Array<number> = [1, 2, 3];
```
- **Type Unions**: Use `|` for union types:
```js
function formatId(id: number | string): string {
  return id.toString();
}

```
