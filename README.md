# Next.js TypeScript Template

> **Current Versions:**
>
> - Next.js: ^16.2.4
> - React: ^19
> - Node.js: 24.14.1

This project is a highly extensible Next.js + TypeScript template, bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app). It is designed for rapid project initialization and best practices out of the box.

## Features & Tech Stack

- **Framework**: Next.js (App Router)
- **Language**: TypeScript
- **Tooling**: ESLint, Prettier
- **Internationalization**: Built-in i18n support with typesafe-i18n (`src/i18n/`)
- **Structure**: Modular components (`src/components/`), context, and utilities for scalable development
- **Package Manager Support**: npm, yarn, pnpm, bun
- **Easy Customization**: Suitable for enterprise, personal, or prototyping needs

## Recommended Use Cases

- Enterprise web applications
- Personal websites and blogs
- MVPs and rapid prototyping

## Getting Started

1. **Create a new project from this template**
   - Click "Use this template" on GitHub, or run:
     ```bash
     npx degit <your-github-username>/nextjs-template-ts your-project-name
     cd your-project-name
     ```
2. **Install dependencies**
   - We use pnpm for this template:
     ```bash
     pnpm install
     ```
3. **Start the development server**

   ```bash
   pnpm dev
   ```

   Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

4. **Recommended customizations**
   - Update project info in `package.json` (name, description, etc.)
   - Replace `src/app/page.tsx` with your own homepage content
   - Adjust the structure in `src/components`, `src/context`, `src/utils` as needed
   - Edit language files in `src/i18n/` for your own translations

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

## Internationalization (i18n)

This template includes full internationalization support using [typesafe-i18n](https://github.com/ivanhofer/typesafe-i18n), providing type-safe translations with excellent developer experience.

### Supported Languages

- **English (en)** - Base locale
- **Chinese (zh)** - Simplified Chinese

### Project Structure

```
src/i18n/
├── en/                 # English translations
│   └── index.ts
├── zh/                 # Chinese translations
│   └── index.ts
├── i18n-types.ts       # Auto-generated type definitions
├── i18n-react.tsx      # React context and hooks
├── I18nProvider.tsx    # Provider component
├── i18n-util.ts        # Core i18n utilities
├── i18n-util.sync.ts   # Synchronous utilities
├── i18n-util.async.ts  # Asynchronous utilities
└── formatters.ts       # Custom formatters
```

### Adding New Translations

1. **Edit translation files** in `src/i18n/{locale}/index.ts`:

   ```typescript
   const en = {
     welcome: "Welcome",
     greeting: "Hello {name:string}!",
     page: {
       home: "Home",
       about: "About",
     },
   } satisfies BaseTranslation;
   ```

2. **Generate types** to ensure type safety:

   ```bash
   pnpm i18n:types
   ```

3. **Use translations** in your components:

   ```typescript
   import { useI18n } from '@/i18n/i18n-react';

   function MyComponent() {
     const { LL } = useI18n();

     return (
       <div>
         <h1>{LL.welcome()}</h1>
         <p>{LL.greeting({ name: "John" })}</p>
       </div>
     );
   }
   ```

### Type Generation and Validation

The project includes several scripts for managing i18n types:

- **Generate types**: `pnpm i18n:types`
  - Generates TypeScript definitions from translation files
  - Updates `src/i18n/i18n-types.ts`

- **Watch mode**: `pnpm i18n:watch`
  - Automatically regenerates types when translation files change
  - Useful during development

- **Type checking**: `pnpm i18n:check`
  - Runs TypeScript compiler to check for type errors
  - Ensures all translations are properly typed

- **Full validation**: `pnpm i18n:lint`
  - Combines type generation and checking
  - Use this before commits to ensure type safety

### Adding New Languages

1. **Create a new locale directory**:

   ```bash
   mkdir src/i18n/fr
   ```

2. **Add translation file** `src/i18n/fr/index.ts`:

   ```typescript
   import type { BaseTranslation } from "../i18n-types";

   const fr = {
     welcome: "Bienvenue",
     greeting: "Bonjour {name:string}!",
     // ... other translations
   } satisfies BaseTranslation;

   export default fr;
   ```

3. **Update locale types** in `src/i18n/i18n-types.ts` (auto-generated):

   ```typescript
   export type Locales = "en" | "zh" | "fr";
   ```

4. **Generate types**:
   ```bash
   pnpm i18n:types
   ```

### Using the I18nProvider

Wrap your app with the `I18nProvider` in your root layout:

```typescript
// app/layout.tsx
import I18nProvider from '@/i18n/I18nProvider';

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>
        <I18nProvider>
          {children}
        </I18nProvider>
      </body>
    </html>
  );
}
```

### Language Switching

Use the `useI18n` hook to switch languages:

```typescript
import { useI18n } from '@/i18n/i18n-react';

function LanguageSwitcher() {
  const { locale, setLocale } = useI18n();

  return (
    <div>
      <button onClick={() => setLocale('en')}>English</button>
      <button onClick={() => setLocale('zh')}>中文</button>
    </div>
  );
}
```

### Best Practices

1. **Always run type generation** after adding new translations
2. **Use the `i18n:lint` script** before committing changes
3. **Keep translation keys consistent** across all languages
4. **Use nested objects** for better organization (e.g., `page.home`, `page.about`)
5. **Leverage TypeScript** for compile-time translation validation

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.
- [typesafe-i18n Documentation](https://github.com/ivanhofer/typesafe-i18n) - learn about type-safe internationalization.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
