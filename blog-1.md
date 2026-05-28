# Why `any` Quietly Destroys TypeScript Projects

In small TypeScript projects, `any` feels harmless.

In large projects, it becomes one of the fastest ways to lose the entire benefit of TypeScript.

The moment `any` enters a codebase, type safety stops propagating. Autocomplete becomes unreliable, refactoring becomes riskier, and runtime bugs start slipping through compile-time checks unnoticed.

That’s why experienced TypeScript developers prefer `unknown` whenever data comes from outside the application boundary.

 

# What `any` Actually Does

When you use `any`, TypeScript essentially disables type checking for that value.

```typescript
let response: any = fetchSomeData();

response.toUpperCase();
response.map(() => {});
response();
```

All three lines compile successfully.

The problem is that TypeScript no longer verifies whether any of those operations are valid. If `response` is not a string, array, or function, the application crashes at runtime instead of failing during development.

This is where `any` becomes dangerous. It removes the safety guarantees TypeScript is designed to provide.

Even worse, `any` spreads.

```typescript
function process(data: any) {
  return data.value;
}
```

Now every function using `process()` also loses reliable type safety. Over time, a few `any` types can silently weaken an entire codebase.

 

# Why `unknown` Is Safer

`unknown` accepts any value, just like `any`.

The difference is that TypeScript refuses to let you use that value until you prove what it actually is.

```typescript
let response: unknown = fetchSomeData();

response.toUpperCase(); // Error
```

That error is intentional.

TypeScript is effectively saying:

> “You do not know the shape of this data yet. Validate it first.”

This becomes extremely important when handling:

* API responses
* user input
* JSON parsing
* database results
* third-party SDKs
* request payloads

All of these are external data sources that cannot be fully trusted.

 

# Type Narrowing: Proving the Type

Type narrowing is the process of checking a value before using it.

Once TypeScript sees a validation check, it narrows the type inside that scope.

```typescript
let response: unknown = fetchSomeData();

if (typeof response === "string") {
  console.log(response.toUpperCase());
}
```

Inside the `if` block, TypeScript now knows `response` is a string.

You can narrow types in multiple ways.

## Using `typeof`

```typescript
if (typeof response === "number") {
  console.log(response.toFixed(2));
}
```

## Using `instanceof`

```typescript
if (response instanceof Error) {
  console.log(response.message);
}
```

## Checking Object Properties

```typescript
if (
  typeof response === "object" &&
  response !== null &&
  "name" in response
) {
  console.log(response.name);
}
```

These checks allow TypeScript to safely understand the structure of unknown data.

 

# Real-World Example: API Responses

A common mistake is trusting API responses too early.

```typescript
async function getUser(): Promise<unknown> {
  const response = await fetch("/api/user");
  return response.json();
}
```

The returned JSON could contain anything.

Instead of assuming the shape immediately, validate it first:

```typescript
const data = await getUser();

if (
  typeof data === "object" &&
  data !== null &&
  "email" in data
) {
  console.log(data.email);
}
```

This may look slightly more verbose than using `any`, but it prevents a large category of runtime failures.

 

# The Production-Level Problem with `any`

In small scripts, using `any` occasionally may not seem harmful.

In larger applications, the consequences become serious:

* unsafe refactoring
* broken autocomplete
* hidden runtime bugs
* unreliable API contracts
* weaker maintainability
* harder debugging

A single unchecked `any` can propagate incorrect assumptions across services, components, and utility functions.

That becomes expensive very quickly in production systems.

 

# The Tradeoff

`unknown` is intentionally stricter than `any`, which means writing slightly more validation code.

But that additional validation is usually far cheaper than debugging runtime crashes caused by invalid assumptions.

TypeScript’s strictness is not there to slow development down. It exists to prevent incorrect code from reaching production.

 

# The Simple Rule

If you genuinely know the type, use that type.

If you do not know the type yet, use 'unknown` and narrow it properly.

Avoid using `any` unless you intentionally want to disable type checking.

The best TypeScript codebases are not the ones with the most complicated types.

They are the ones where types make bugs difficult to write in the first place.
