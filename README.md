# Building Type-Safe Forms in React Native & Expo with TypeScript, React Hook Form, and Zod

One of the key aspects of any mobile application is the ability to collect and process user input effectively. This is where forms come into play, and their significance cannot be overstated. However, forms can also be a source of frustration, both for developers and users, if not implemented correctly. In this article, we will delve into the process of creating forms that are not only user-friendly but also type-safe and performant.

Integrating **TypeScript** with **React Native** has been a game-changer, providing developers with the power of static typing and the ability to catch errors at compile time. **React Hook Form** offers an elegant solution for managing form state, reducing the amount of boilerplate code, and improving performance. On the other hand, **Zod** is a TypeScript-first schema declaration and validation library that ensures the data we work with matches the expected types.

Throughout this article, we will explore the synergistic relationship between these three powerful tools. We'll start by setting up a new Expo project with TypeScript, followed by defining our form schema with Zod. Next, we'll integrate the React Hook Form to handle our form state and validation, ensuring that our forms are both type-safe and efficient.

By the end of this guide, you will have a clear understanding of how to leverage TypeScript, React Hook Form, and Zod to build forms that are robust, scalable, and maintainable. Whether you are new to React Native or looking to enhance your existing skills, this article will provide you with the knowledge and best practices needed to take your form development to the next level.

Enough talk, let's code

## Initiate the Project

```bash
# create new expo app with typescript
npx create-expo-app -t expo-template-blank-typescript rn-expo-efficient-forms

# navigate to the project directory
cd rn-expo-efficient-forms

# open vscode
code .
```

Add the following `script` in `package.json` along with other `scripts` that we can check the **TypeScript** setup:

```json
{
  "scripts": {
    ...
    "ts:check": "tsc"
  }
}
```

at this point your `package.json` full code will be as below:

```json
{
  "name": "rn-expo-efficient-forms",
  "version": "1.0.0",
  "main": "node_modules/expo/AppEntry.js",
  "scripts": {
    "start": "expo start",
    "android": "expo start --android",
    "ios": "expo start --ios",
    "web": "expo start --web",
    "ts:check": "tsc"
  },
  "dependencies": {
    "expo": "~50.0.14",
    "expo-status-bar": "~1.11.1",
    "react": "18.2.0",
    "react-native": "0.73.6"
  },
  "devDependencies": {
    "@babel/core": "^7.20.0",
    "@types/react": "~18.2.45",
    "typescript": "^5.1.3"
  },
  "private": true
}
```

Type-check the project:

```bash
# run the following command to check
npm run ts:check
```

Update the `tsconfig.json` file for the optimized development process:

```json
{
  "extends": "expo/tsconfig.base",
  "compilerOptions": {
    "strict": true
  },
  "include": ["**/*.ts", "**/*.tsx", ".expo/types/**/*.ts", "expo-env.d.ts"]
}
```

Expo CLI supports path aliases in your projects `tsconfig.json` automatically. This enables you to import modules using a custom alias instead of a relative path.

For example, if you have a file at `src/components/Button.tsx` and wish to import it using the alias `@/components/Button` as follows:

```js
import Button from '@/components/Button';
```

Then simply add the alias @/\* in the project's tsconfig.json and set it to the src directory:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```

the final `tsconfig.json` will be as below:

```json
{
  "extends": "expo/tsconfig.base",
  "compilerOptions": {
    "strict": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  },
  "include": ["**/*.ts", "**/*.tsx"]
}
```
