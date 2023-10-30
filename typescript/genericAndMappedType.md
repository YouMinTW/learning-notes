# Dependant Field (ex: formValue and formConfig)

```ts
type FormValues = Record<string, any>;

// Utility type to get the value type based on the string path.
type PathValue<T, P extends string> = P extends `${infer K}.${infer Rest}`
  ? K extends keyof T
    ? PathValue<T[K], Rest>
    : any
  : P extends keyof T
  ? T[P]
  : any;

// Generate all possible paths of the object.
type Paths<T> = T extends object
  ? {
      [K in keyof T]: K extends string ? `${K}` | `${K}.${Paths<T[K]>}` : never;
    }[keyof T]
  : "";

// Adjust FormField to be generic
type FormField<V, P extends Paths<V>> = {
  name: P;
  userInput: PathValue<V, P>;
};

type Form<V extends FormValues> = {
  defaultValues: V;
  fields: Array<{ [P in Paths<V>]: FormField<V, P> }[Paths<V>]>;
};

type BasicInfo = {
  age: number;
  isSmoking: boolean;
  profile: {
    name: string;
  };
};
// Valid
const object1: Form<BasicInfo> = {
  defaultValues: { age: 18, isSmoking: true, profile: { name: "Ken" } },
  fields: [
    { name: "age", userInput: 3 },
    { name: "isSmoking", userInput: true },
    { name: "profile.name", userInput: "Kent" },
  ],
};

// Path error
const object2: Form<BasicInfo> = {
  // Error: 'nickName' is not a valid key
  defaultValues: { age: 1, isSmoking: false, profile: { nickName: "Ken" } },
  fields: [
    // Error: Type aged is not assignable to type: age, isSmoking, profile.name
    { name: "aged", userInput: 3 },
    // Error: Type isSmoke is not assignable to type: age, isSmoking, profile.name
    { name: "isSmoke", userInput: true },
    // Error: Type profile.nickName is not assignable to type: age, isSmoking, profile.name
    { name: "profile.nickName", userInput: "Kent" },
  ],
};

// Type error
const object3: Form<BasicInfo> = {
  // Error: isSmoking should be boolean
  defaultValues: { age: 1, isSmoking: 2, profile: { name: "Ken" } },
  fields: [
    // Error: Type 'string' is not assignable to type 'number'
    { name: "age", userInput: "3" },
    // Error: Type 'string' is not assignable to type 'boolean'.
    { name: "isSmoking", userInput: "true" },
    // Error: Type 'number' is not assignable to type 'string'
    { name: "profile.name", userInput: 6 },
  ],
};


```
