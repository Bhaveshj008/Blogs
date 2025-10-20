---
title: "Stop Writing Repetitive Zod Validation: Introducing zod-fragments"
seoTitle: "zod-fragments: TypeScript Validation Library That Cuts Zod Boilerplate"
seoDescription: "A TypeScript validation library built on Zod that cuts boilerplate by 50%. Features pre-built fragments and consistent error handling, npm package."
datePublished: Fri Jul 25 2025 19:29:32 GMT+0000 (Coordinated Universal Time)
cuid: cmdj7tj2f000k02l7gksd2vo6
slug: zod-fragments
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1753471119856/032f9e7d-b3cb-4018-baa5-19364ebf24c6.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1753471443781/fe20dd9b-90c8-4079-995a-0ba2500f5309.png
tags: express, javascript, angularjs, react-native, nodejs, boilerplate, reactjs, typescript, validation, mern, form-validation, nextjs, nestjs, zod, zod-library

---

I recently published my first npm package — **zod-fragments** — and I wanted to share the story behind it, along with how it can make your Zod validation cleaner and more maintainable.

## The Problem That Started It All

I was working on a project that required extensive form validations across multiple modules. This was actually my **first time using Zod** — I'd heard great things about it being type-safe, flexible, and reliable, but I'd never implemented it in a real project before.

As the backend lead for my team, I needed to ensure our validation approach would be consistent, easy to implement, and maintainable for everyone. But as I started writing Zod schemas, I quickly realized I was spending way too much time on repetitive boilerplate:

```javascript
// This pattern repeated everywhere
const userSchema = z.object({
  name: z.string({
    required_error: "Name is required",
    invalid_type_error: "Name must be a string"
  }).min(1, "Name cannot be empty"),
  
  email: z.string({
    required_error: "Email is required",
    invalid_type_error: "Email must be a string"
  }).email("Invalid email format"),
  
  userId: z.string({
    required_error: "User ID is required",
    invalid_type_error: "User ID must be a string"
  }).uuid("User ID must be a valid UUID"),
});
```

After writing just a few schemas, I was already feeling bored and frustrated. The same patterns kept repeating across dozens of forms and API endpoints. As a team lead, I was concerned about:

* **Developer productivity** - This boilerplate was eating up valuable development time
    
* **Code consistency** - Team members might write validations differently
    
* **Maintainability** - Schema changes would require updates across multiple files
    
* **Developer experience** - Nobody wants to copy-paste validation chains all day
    

I needed a centralized solution that would make adding validations effortless while keeping our codebase consistent.

## The Search for a Solution

I looked around for existing solutions — something lightweight that could plug into Zod and handle the most common validation patterns. While there are some great libraries out there, I couldn't find anything that was both simple enough and comprehensive enough for my needs.

Most solutions were either too opinionated, too heavy, or didn't address the specific pain points I was experiencing with team consistency and developer experience.

## Building the Solution

So I decided to build my own abstraction. I started by implementing it directly in our project to solve our immediate needs. The results were immediate — validation code became cleaner, team members could implement new schemas quickly, and our codebase stayed consistent.

But as I researched more, I realized that **this kind of solution had never been implemented for Zod validation** in the way I envisioned it. There was a genuine gap in the ecosystem for a lightweight, fragment-based approach that made adding validations effortless while preserving all of Zod's power.

That's when I decided to extract it into a proper npm package and share it with the community.

## Introducing zod-fragments

**zod-fragments** is a collection of reusable validation helpers built on top of Zod. It's designed to eliminate boilerplate while keeping all of Zod's power and flexibility.

Here's how the same schema looks with zod-fragments:

```javascript
import { z, requiredString, emailOrMobile, uuid } from "zod-fragments";

const userSchema = z.object({
  name: requiredString("Name"),
  contact: emailOrMobile("Email or Phone"),
  userId: uuid("User ID"),
});
```

That's it. Clean, readable, and consistent error messages out of the box.

## Key Features That Solve Real Problems

### 1\. Pre-built Common Patterns

Instead of rewriting the same validations, you get ready-to-use fragments that handle the most common validation scenarios:

```javascript
// String validations with proper error handling
name: requiredString("Full Name")      // Non-empty string, required
bio: optionalString("Bio")             // Optional string  
slug: slug("URL Slug")                 // Lowercase alphanumeric + hyphens only

// Number validations
age: requiredNumber("Age")             // Required number
score: positiveNumber("Score")         // Must be > 0  
count: optionalNumber("Count")         // Optional number

// Specialized formats with built-in validation
id: uuid("User ID")                    // Valid UUID format required
contact: emailOrMobile("Contact")      // Email OR 10-digit mobile number
website: fileUrl("Website URL")        // Valid URL format
avatar: imageUrl("Avatar")             // Valid URL for images

// Boolean handling
isActive: boolean("Active Status")
notifications: optionalBoolean("Email Notifications")

// Enum with clear error messages
role: Enum(["admin", "user", "moderator"], "User Role")

// Date handling
createdAt: dateString("Created Date")  // ISO date string validation
updatedAt: optionalDate("Updated Date")
```

Each fragment handles multiple error scenarios (required, type validation, format validation) with contextual error messages.

### 2\. Schema Blocks for Complex Forms

For larger applications, you can use pre-built field collections that handle common patterns:

```javascript
import { seoFields, paginationFields, listQueryFields } from "zod-fragments";

// SEO-enabled content schema  
const pageSchema = z.object({
  title: requiredString("Page Title"),
  content: requiredString("Content"),
  ...seoFields  // Adds: seo_title, seo_description, seo_image
});

// API endpoint with complete query functionality
const listUsersSchema = z.object({
  ...listQueryFields  // Adds: page (default: 1), limit (default: 10), 
                      //       filters (object), sort (object), search (string)
});

// Just pagination
const simpleListSchema = z.object({
  ...paginationFields  // Just page and limit with sensible defaults
});
```

These blocks solve the common problem of recreating the same field groups across different endpoints and forms.

### 3\. Smart Validation Logic

What makes zod-fragments powerful is the intelligent validation logic built into each fragment. For example, the `emailOrMobile` function uses sophisticated regex patterns:

```javascript
// Handles both email and mobile number formats
contact: emailOrMobile("Contact Info")

// Under the hood, it validates against:
// Email: /^[^\s@]+@[^\s@]+\.[^\s@]+$/
// Mobile: /^[0-9]{10}$/
```

The `slug` fragment ensures URL-safe formatting:

```javascript
// Only allows lowercase letters, numbers, and hyphens
urlSlug: slug("URL Slug")
// Regex: /^[a-z0-9-]+$/
```

The `positiveNumber` fragment combines type checking with value validation:

```javascript
// Must be a number AND greater than 0
price: positiveNumber("Price")
```

All fragments provide user-friendly error messages that work great with form libraries:

```javascript
// With React Hook Form
const MyForm = () => {
  const { register, handleSubmit, formState: { errors } } = useForm({
    resolver: zodResolver(formSchema)
  });

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("name")} />
      {errors.name && <span>{errors.name.message}</span>}
    </form>
  );
};
```

### 4\. Consistent Error Handling

All fragments provide user-friendly error messages that work seamlessly with form libraries:

One of the key architectural decisions I made was implementing a centralized error system. All error messages are defined in a single `FIELD_ERRORS` constant:

```javascript
const FIELD_ERRORS = {
  REQUIRED: "is required",
  STRING: "must be a string", 
  NUMBER: "must be a number",
  UUID: "must be a valid UUID",
  EMAIL: "must be a valid email address",
  // ... and more
};
```

This ensures consistent messaging across your entire application. But you can still customize when needed:

```javascript
// Simple custom message
password: requiredString("Password", "Please enter your password")

// Advanced custom messages for different validation types
password: requiredString("Password", {
  required: "Password is required",
  invalid: "Must be a string", 
  validation: "Password cannot be empty"
})
```

### 5\. Full Zod Compatibility & TypeScript Support

Since fragments return standard Zod schemas with full TypeScript support, you maintain all of Zod's power:

```javascript
const schema = z.object({
  // Chain additional validations seamlessly
  password: requiredString("Password")
    .min(8, "Must be at least 8 characters")
    .regex(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)/, "Must contain uppercase, lowercase, and number"),
  
  age: positiveNumber("Age")
    .max(120, "Age cannot exceed 120")
    .int("Age must be a whole number"),

  // Mix fragments with native Zod
  customField: z.string().transform(val => val.toUpperCase()),
  
  // Use with conditional logic
  accountType: Enum(["personal", "business"], "Account Type"),
  businessName: z.string().optional()
});

// Full TypeScript inference works perfectly
type FormData = z.infer<typeof schema>;
// TypeScript knows all field types automatically
```

The package also exports common pre-built fields:

```javascript
import { title, description } from "zod-fragments";

const articleSchema = z.object({
  title,        // Pre-configured requiredString("Title")
  description,  // Pre-configured optionalString("Description") 
  content: requiredString("Content")
});
```

## Real-World Impact

After implementing zod-fragments in our original project and then in subsequent ones, the impact was significant:

* **50% less validation code** in typical forms
    
* **Faster team onboarding** - new developers could write schemas immediately
    
* **More consistent error messages** across the entire application
    
* **Faster development** when adding new forms or API endpoints
    
* **Easier maintenance** when updating validation logic
    
* **Improved developer satisfaction** - no more copy-paste validation chains!
    

As a team lead, seeing developers actually enjoy writing validation code instead of dreading it was probably the biggest win.

## Framework Integration

The package works seamlessly with popular frameworks:

### Express.js APIs

```javascript
app.post("/users", (req, res) => {
  try {
    const userData = createUserSchema.parse(req.body);
    // Process validated data
  } catch (error) {
    if (error instanceof z.ZodError) {
      const errors = {};
      error.errors.forEach(err => {
        errors[err.path.join(".")] = err.message;
      });
      return res.status(400).json({ errors });
    }
  }
});
```

### React Hook Form (shown above)

### Next.js API Routes

### And any framework that uses Zod!

## TypeScript Support

Full type inference means your IDE will autocomplete and catch errors:

```javascript
type User = z.infer<typeof userSchema>;
// TypeScript automatically knows the shape of your validated data
```

## Getting Started

Installation is simple — Zod is bundled, so you don't need to install it separately:

```bash
npm install zod-fragments
```

Then start using it immediately:

```javascript
import { z, requiredString, emailOrMobile } from "zod-fragments";

const schema = z.object({
  name: requiredString("Name"),
  contact: emailOrMobile("Contact"),
});
```

## What's Next

This started as an internal solution for my team's productivity and consistency needs, but publishing it as my first npm package has been incredibly rewarding. The response from the developer community has been encouraging, and I'm already planning new features based on feedback:

* More specialized fragments for common use cases
    
* Integration helpers for popular form libraries
    
* Additional schema blocks for different application types
    
* Enhanced TypeScript utilities for better DX
    

The fact that this approach to Zod validation didn't exist before makes me excited about the possibilities ahead.

## Try It Out

If you're using Zod in your projects and find yourself writing repetitive validation code, give zod-fragments a try:

* **NPM**: [zod-fragments](https://www.npmjs.com/package/zod-fragments)
    
* **GitHub**: [View source and documentation](https://github.com/Bhaveshj008/zod-fragments)
    

The GitHub repository has comprehensive examples, complete API documentation, and contribution guidelines if you'd like to help improve the package.

## Final Thoughts

What started as a frustration during my first experience with Zod turned into a solution that's now helping developers worldwide. Building zod-fragments taught me a lot about npm publishing, TypeScript library development, and most importantly, how to identify and solve real developer problems.

From leading a team that was struggling with repetitive validation code to publishing a package that fills a genuine gap in the Zod ecosystem — it's been an incredible journey. The fact that this approach to making validations effortless didn't exist before makes it even more rewarding.

If you find it useful, I'd love a GitHub star ⭐ or any feedback you might have. The developer community's support means everything, especially for someone publishing their first package!

What validation patterns do you find yourself repeating? As a team lead, what consistency challenges do you face? Let me know in the comments — they might become the next zod-fragments feature.

---

*Have you built your first npm package? I'd love to hear about your experience and what problem you solved!*

#zod #typescript #npm #validation #reactjs #webdev #opensource #developerexperience #zodfragments