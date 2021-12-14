# React and TypeScript Review

The goal of this module is to review the basics of React before fully entering the world of React Native. The course I've set out to take recommends using TypeScript for a safer development process. I totally agree with this view. So, basically, the main topics are

> 1. Why using TypeScript on my projects?
> 1. Basic types
> 1. Objects and Interfaces
> 1. Basic React Hooks
> 1. Custom Hooks
> 1. TypeScripts generalities
> 1. Axios (HTTP protocols)
> 1. Forms

## Why Using TypeScript on my projects?

Well, most of the time, a development project requires that many modules integrate perfectly so that an application runs smoothly. Those modules consist on objects and methods whose properties correspond to an actual process o real entity to be described in a system.

> When developing a project, all models should have clearly defined properties and methods that integrate with one another for it to succeed.

Here is where TypeScript comes to the rescue. By providing strong typing, it allows the developer to clearly state what properties are associated to a particular class of objects, and specify the kind of parameters that a particular method needs to work properly. I know for a fact that being loose with the typing can lead to an app crashing horribly. Furthermore, via VSCode, TypeScript provides real time error detection and handling, which represents a major speed up o the development process.

Another advantages of using TypeScript are controlled mutation (the developer is able to state when a particular variable or property can change its type) and automatic documentation.

> TypeScript doesn't increase the size of JavaScript bundle, and provides immense support for teamwork.

Some of the problems of TypeScript are related to the specific types for a variable, property or function in a context. Inheritance of objects can accent this problems.

## Basic Types

Now, it's time to consider how to manage strong typing. Well, I already have some experience with TypeScript from my work with Angular, yet I think that this is not enough. So I review the basics and proceed to more advanced stuff.

The easiest way to use TypeScript is by defining proper file extensions. On VSCode, this leads to automatic error detection and type inference. The explicit way implies using the following syntax

```tsx
let name: string = "Diego";
```

This sets variable `name` to be of type `String` throughout the code. If the type variable is allowed to change to some other type, the pipe can be used to specify which other types are permitted for the variable.

```tsx
let name: string | number = "Diego";
```

> Any number of pipes can be used for specifying the allowed types of a given variable in TypeScript.

**Pro tip:** Using typing and VSCode allows the programmer to take full advantage of linting. This is quite useful since it prevents looking up the documentation on the browser all the time.

Something interesting happens if instead of variables, a constant is declared. In that case, the value itself seems to be the type of the entity. For constants, if a specific type is desired, it must be stated explicitly.

**Pro tip:** Project configurations for TypeScript linting and error detection are contained on `tsconfig.json`.

When working with arrays, it is important to declare the type of the elements explicitly. When calling an API, for instance, this may prevent that an empty JSON placeholder be filled with undesired data, causing errors in the app, perhaps by calling the wrong endpoint. This can be done by the syntax

```tsx
const myArray = string[]
```

Now, it may seem complicated at first, but is immensely useful when working with APIs. Usually, an API is based on a model of each of the objects that interact in a given environment. It may be clients, products, sellers, stores, etc. And each endpoint is meant to alter the properties of a given object that corresponds to a particular model. Enforcing string typing warranties that the backend models are consistent with the frontend classes used for allowing data manipulation by the final user. Since most of data is sent in JSON format, that I know of, typing arrays is paramount. Before an API call is made, the data array on the frontend is empty. Specifying a typ can prevent the app from crashing before actual compilation.

## Objects and Interfaces

I am familiar with objects from my previous work. Now, interfaces are awesome. This allow defining a sort of type for common literal objects. For instance, an interface for an object may be

```tsx
interface Person {
  name: string;
  houseNo: number;
  job?: string;
}
```

And an object that conforms to this interface may be instantiated as follows

```tsx
const person: Person = {
  name: "Diego",
  houseNo: 5,
};
```

Notice that the question mark on the interface definition means that an object that conforms to `Person` may or may not have a job. So this property can be added in next steps of the program. Nesting inside interface definition is not recommended. The ideal is to define the most important interface at the top, and derive from it auxiliary interfaces. For instance, if a person has an address, which is a complex object in general

```tsx
interface Person {
  name: string;
  houseNo: number;
  address?: Address;
  job?: string;
}

interface Address {
  city: string;
  country?: string;
}
```

And a person object that conforms to `Person` can be defined as follows

```tsx
const person: Person = {
  name: "Diego",
  houseNo: 5,
  address: {
    city: "Bogotá",
    country: "Colombia",
  },
};
person.job = "Unemployed";
```

Interfaces are not classes, they are a mean of imposing TypeScript validation rules on literal objects. To instantiate objects from a template, a class should be used.

Functions can also have a specific type. This is possible by using `:` notation on the arguments and after the parenthesis on arrow functions as follows

```tsx
const myFunction = (arg1: number, arg2: string): boolean => {
  let someBool: boolean;
  // function body
  return someBool;
};
```

This is quite useful on VSCode, since it provides in place docs of the argument and return types of the function.

## Basic React Hooks with TS

The most used and direct hook is `useState`. Now, implicitly, TypeScript sets the generic type of the state variable and setState function. However, this can be done explicitly by using the following

```tsx
const [myState, setMyState] = useState<number>(10);
```

The generic `<number>` tells TypeScript that we want the state variable to be of numeric type. This is a major help on debugging simple changes of state carried out by callbacks on a react app. It is also possible to use custom generics. Default values can be assigned to functions, which simplifies code.

**Pro tip:** It is possible to define custom hooks that manage a complicated logic inside an app. A hook can use basic React hooks and return the objects that are needed for the view. Check `hooks` directory for a reference.
