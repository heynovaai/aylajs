O que eu quero da Ayla?

```ts
const objeto = ayla.object({
  name: ayla.string(),
  age: ayla.number(),
  email: ayla.string().email().providers(["gmail", "hotmail", "yahoo"]),
  password: ayla.string().min(8),
  confirmPassword: ayla.string().equals("password"),
  address: ayla.object({
    street: ayla.string(),
    number: ayla.number(),
    city: ayla.string(),
    state: ayla.string().length(2),
  }),
  phones: ayla.array(ayla.string().phone()),
  hobbies: ayla.array(ayla.string().in(["reading", "coding", "playing"])),
});

const schema = {
  type: "object",
  shape: {
    name: { type: "string" },
    age: { type: "number" },
    email: {
      type: "string",
      email: {
        is: true,
        providers: ["gmail", "hotmail", "yahoo"],
      },
    },
    password: { type: "string", min: 8 },
    confirmPassword: { type: "string", equals: "password" },
    address: {
      type: "object",
      shape: {
        street: { type: "string" },
        number: { type: "number" },
        city: { type: "string" },
        state: { type: "string", length: 2 },
      },
    },
    phones: { type: "array", of: { type: "string", phone: true } },
    hobbies: {
      type: "array",
      of: { type: "string", in: ["reading", "coding", "playing"] },
    },
  },
};

const data = {
  name: "John Doe",
  age: 25,
  email: 123,
  password: "12345678",
  confirmPassword: "123456789",
  address: {
    street: "Main St",
    number: 123,
    city: "New York",
    state: "NY",
  },
  phones: ["123456789", "987654321"],
  hobbies: ["reading", "coding", "playing", "sleeping"],
};

const parsedData = objeto.parse(data); //Throws error because of the invalid data
```
