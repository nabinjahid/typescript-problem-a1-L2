## 1. Difference between interface and type in TypeScript:

To define a type in Typescript interface and type are used. though they are used for the same purpose, they have some key differences.

### First of all, interface:
Interface is mainly used with objects because it’s not used with primitive data types. To create an interface, we don’t need to use the equal sign. Interface can extend other interfaces or even classes. One important thing is that interface supports merging, which means we can declare the same interface multiple times and it will combine them automatically.

### Now, types:
Type has a bit more flexibility. It can be used with both primitive and non-primitive data types. Type can’t extend other types directly, but it can use intersection types to combine multiple types. It doesn’t support merging like interface, but it can define any kind of type — that makes it more versatile. However, in some cases, it can be harder to read, especially when the type is too complex.

---

## 2. Use of keyof keyword and example:

`keyof` is a TypeScript keyword. It’s very important because we use it to extract the keys from a type or interface. When we need a union of string literal types from an interface or type, we just use the `keyof` keyword. It gives us only the keys as a union but does not give the values.

This is helpful when we want to create types based on the property names of an object. It’s also commonly used with generic types and utility types to build more dynamic and flexible code.

```ts
interface Person {
  name: string;
  age: number;
  email: string;
}

type PersonKeys = keyof Person;
PersonKeys will be "name" | "age" | "email"


here keyof Person gives us all the keys from Person interface. Now we can use it in other part of our code

keyof with generic type:
ts
Copy
Edit
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = {
  name: "Nabin",
  age: 23,
  email: "nabin@example.com",
};
here T is the object type and K hold the keys of that type as union. and T[K] is the type of the property. so now it is fully type safe.

```
## 3. The difference between any, unknown, and never types in TypeScript:

### any:
any is like turning off TypeScript to check the type. It gives you flexibility to declare and assign values exactly like JavaScript. You can reassign any value to a variable. For example, if you declare a variable and assign a number to it, you can reassign the value to a string in the next line.

### unknown:
unknown is something like "I do not know what will be the type of the data." It is similar to any but enforces type safety. You must use type assertion or type guard to narrow it down before performing any operation on an unknown type.

### never:
Most of the time, never is used with functions. It represents a value that never occurs. For example, a function that always throws an error or has an infinite loop will have a return type of never, because it never successfully finishes. It is mainly used in advanced type scenarios, especially in functions where a value can never be returned.

### Summary:
We will use any when you want full flexibility, but it turns off type checking. When you don't know the type yet but still want type safety, we can use unknown. Use never when a function never returns a value, like throwing an error or running forever.
