## Don't Duplicated Your TypeScript Interfaces

In a TypeScript project, you will almost certainly end up with multiple interfaces that look almost identical.

There is a field called ‘password’. One doesn't.

One has `id`, `createdAt`. Another one takes them out for form input

On the face of it, copying the interface isn't a big deal.

And then the project expands.

You rename a field like email to primaryEmail and now you have to rename the same thing in 10 different spots, interfaces, API payloads, frontend forms, validation schemas.

This is exactly the problem TypeScript utility types such as `Pick` and `Omit` are solving.

 

# The Actual Issue with Duplicate Interfaces

Let’s take a common backend application.

You could start with a db model like this:

```typescript
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
  createdAt: Date;
  isAdmin: boolean;
}
```

It becomes the single source of truth for your user hierarchy.

But different parts of the application require different versions of that data:

Public profile responses to

* Attempts to log in
* Registration forms *
* Admin panels
* Update the endpoints
* Authentication payload

Many developers do this manually, by creating separate interfaces for each case.

That works for some time.

But duplicated interfaces are a maintenance problem in the end.

# Omit: Removing Unused Fields

`Omit` constructs a new type from an existing type by removing some properties.

```typescript
type PublicProfile = Omit<User, "password" | "isAdmin">;
```

`PublicProfile` now has:

id

* `name` *
* email
* created_at *

But it does not contain sensitive fields like:

* password
* `isAdmin`

Useful for API responses that contain some internal fields that should never be sent to the frontend.

Another common example is the user creation.

```typescript
type CreateUserDTO = Omit<User, "id" | "createdAt">;
```

The database will generate `id` and `createdAt`, and clients should not send them.

You do not re-write the interface but generate it directly from the original type.

 

# `Pick': Taking Only What You Need

`Pick` does the reverse.

It selects only certain fields. It does not strip fields.

```typescript
type LoginCredentials = Pick<User, "email" | "password">;
```

A login form does not need:

* `created_at`
  `isAdmin`
* `name`

Just the information fields for authentication.

This makes the data structures sparse and significant.

 

## Why This Matters for Real-World Applications

Duplicating interfaces might seem acceptable for small projects.

They are dangerous in bigger applications.

Suppose we change this:

```typescript
email: string;
```

to this end.

```typescript
primaryEmail: string;
```

If you have hand-duplicated interfaces in your codebase then you now need to go find each copy and update them.

One missed can create even:

* front-end/back-end mis-matches
* api invalid payloads
* broken forms
* runtime error
* inconsistent validation logic

This is fixed by utility types, which derive everything from one source of truth.

The base interface can be changed and all derived types will be updated automatically.

 

# Combining Utility Types

This can be even more powerful when utility types are composed.

As an example:

```typescript
type UpdateUserDTO = Partial<Omit<User, "id">>;
```

Here’s the scoop:

`Omit<User, "id">` removes the `id` field

* `Partial<>` makes all other properties optional

This is great for PATCH endpoints where a user wants to update only certain fields.

Without utility types you'd probably have to manually code a big interface with a bunch of optional properties.

 

# The Production Advantage

The big advantage of utility types isn't shorter code.

That's consistency.

Derived types reduce duplication and improve maintainability.  They also make refactoring a much safer task.

They also make developer intent clearer.

This one:

```typescript
Omit<User, "password">
```

and then reports to another developer:

> "This is a user object for an external user"

That clarity matters in collaborative codebases.

 

# Trade Offs

Utility types are really handy, but don’t overuse them.

Utility types with a tonne of nesting can be difficult to read:

```typescript
Partial<Omit<Pick<User, "name" | "email">, "email">>
```

Correct in technical language.

Not quite sustainable.

We don’t want to build the smartest type system in the world.

We want to create types that will still make sense when the project grows.

 

# The More Efficient Way

Instead of thinking of interfaces as things to copy and modify over and over, think of them as basic building blocks.

Single source of truth consolidation.

Then you can create specialised versions of it using utility types like:

* Select
* `Exclude`
* `Partial`
  *Required
* Read Only.

This scales much better with larger and more complex applications.

The best TypeScript codebases are not the ones with the most complex types.

These are the types that minimise duplication, avoid errors, and allow the system to be evolved over time.
