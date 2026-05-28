# B7A1

## Assignment: Advanced Problem Solving with TypeScript & OOP

This assignment comprises various problems that demonstrate fundamental TypeScript concepts, including data typing, interfaces for objects, class usage with inheritance, type checking, and manipulation of data structures. The solutions aim to showcase efficient and clear problem-solving techniques using TypeScript, adhering to best coding practices.

## 💻 Problem Solving (50 Marks)

All coding solutions must be implemented in a **single file** named `solutions.ts`.

## Problem 1:
Create a TypeScript function `filterEvenNumbers` that accepts an array of numbers and returns a new array containing only the even numbers.

```tsx
// Sample Input:
filterEvenNumbers([1, 2, 3, 4, 5, 6])

// Sample Output:
[2, 4, 6]
```

## Problem 2:
Write a function `reverseString` that takes a string as input and returns the reversed version of that string.

```tsx
// Sample Input:
reverseString("typescript");

// Sample Output:
"tpircsepyt";
```

## Problem 3:
Define a union type `StringOrNumber` and create a function `checkType` that uses type guards to return "String" if the input is a string or "Number" if the input is a number.

```tsx
// Sample Input 1:
checkType("Hello");

// Sample Output 1:
"String";

// Sample Input 2:
checkType(42);

// Sample Output 2:
"Number";
```

## Problem 4:
Write a generic function `getProperty` that takes an object and a key, then returns the value of that key. Use constraints to ensure the key exists on the object.

```tsx
// Sample Input:
const user = { id: 1, name: "John Doe", age: 21 };
getProperty(user, "name");

// Sample Output:
"John Doe";
```

## Problem 5:
Define an interface `Book` with properties `title`, `author`, and `publishedYear`. Create a function `toggleReadStatus` that accepts a `Book` object and returns a new object with an added `isRead` property (boolean), defaulting to `true`.

```tsx
// Sample Input:
const myBook = { title: "TypeScript Guide", author: "Jane Doe", publishedYear: 2024 };
toggleReadStatus(myBook);

// Sample Output:
{
  title: "TypeScript Guide",
  author: "Jane Doe",
  publishedYear: 2024,
  isRead: true
}
```

## Problem 6:
Create a class `Person` with a name and age. Then, create a subclass `Student` that adds a `grade` property. Include a method `getDetails` in the `Student` class that returns a string with the student's name, age, and grade.

```tsx
// Sample Input:
const student = new Student("Alice", 20, "A");
student.getDetails();

// Sample Output:
"Name: Alice, Age: 20, Grade: A";
```

## Problem 7:
Create a function `getIntersection` that takes two arrays of numbers and returns a new array containing only the elements that are `present in both arrays`.

```tsx
// Sample Input:
getIntersection([1, 2, 3, 4, 5], [3, 4, 5, 6, 7])

// Sample Output:
[3, 4, 5]
```

---

## Blog Writing (Choose any two: 10 Marks)

Write an impactful and technically sound blog post covering **two** of the following topics. Your blog should be clear, concise, and include code examples where necessary to illustrate your points.


### Blog Topics:

1.  Why is `any` labeled a "type safety hole," and why is `unknown` the safer choice for handling unpredictable data? Explain the concept of type narrowing.

2.  How do `Pick` and `Omit` utility types prevent code duplication while creating specialized "slices" of a master interface? Discuss how this keeps your code **DRY** (Don't Repeat Yourself).

3.  How do `Generics` allow you to build reusable components and functions that stay strictly typed regardless of the data structures passed in?

4.  How do the four pillars of **OOP—Inheritance, Polymorphism, Abstraction, and Encapsulation**—help manage logic and reduce complexity in large-scale TypeScript projects?

---

## 💻 Coding Requirements

All solutions must be placed in a single file named `solutions.ts`.

* **Function Names:** Use the exact names specified in the problem descriptions.
* **Exact Output:** Your return values must match the sample output exactly, including spaces, punctuation, and capitalization.
    * *Correct:* `'Name: John Doe, Age: 30'`
    * *Incorrect:* `'name: John Doe, age: 30'`
* **Clean Code:** Use meaningful variable and class names.
* **No Noise:** * Do **not** include unnecessary comments.
* Do **not** include any `console.log` statements; return the values instead.

---

## 📝 Blog Instructions

Submit each blog post in its own Markdown file:
* **Format:** Use a separate Markdown (`.md`) file for each blog (e.g., `blog-1.md`, `blog-2.md`).
* **Structure:** Each post should have a clear **Title**, an **Introduction**, **Body Paragraphs** with code snippets, and a **Conclusion**.
* **Language:** English/Bangla.
* **Clarity:** Use proper Markdown headers and code blocks to make the post readable.
  
---

## 📁 File Structure

```text
├── solutions.ts
├── blog-1.md
├── blog-2.md
└── README.md
```

## 🚀 Submission Instructions

1. **Repository Setup:** Create a personal GitHub repository and push your completed files.
2. **Visibility:** Set the repository to **Public**.
3. **Submission:** Paste the **direct repository URL** into the assignment submission box. Do not submit individual files or archives.

### Assignment Deadlines:

* **60 marks:** May 07, 2026, 11:59 PM
* **50 marks:** May 08, 2026, 11:59 PM
* **30 marks:** After May 08, 11.59 PM

---

The code & content must be your own. Avoid `copy-pasting` from documentation or `AI generators
