# Project Setup Guide

This guide outlines the steps to set up this project using **Yarn Berry without Zero-Install (aka Plug'n'Play)**. Please note that as of May 24, 2025, **Turbopack does not currently work with Yarn PnP**.

---

## Project Creation Process

Follow these steps to initialize your project:

1. **Create Next.js App:**

   ```bash
   npx create-next-app@latest
   ```

2. **Create a `.yarnrc.yml` file**

   Add the following configuration to specify that Yarn should keep the `node_modules` folder by setting `nodeLinker: node-modules`:

   ```yaml
   nodeLinker: node-modules
   ```

3. **Enable Corepack:**

   ```bash
   corepack enable
   ```

4. **Set Yarn Version:**

   ```bash
   yarn set version stable
   ```

5. **Install Dependencies:**

   ```bash
   yarn install
   ```

---

## Linting Setup ([Reference](https://github.com/aridanpantoja/eslint-prettier-nextjs))

This project uses **ESLint** with **Prettier** for code quality and formatting.

### Installation

Install the necessary development dependencies:

```bash
yarn add --dev eslint-config-prettier eslint-plugin-jsx-a11y eslint-plugin-prettier prettier prettier-plugin-tailwindcss
```

### Configure Eslint and Prettier

In eslint.config.mjs

```typescript
import { FlatCompat } from "@eslint/eslintrc";

const compat = new FlatCompat({
  // import.meta.dirname is available after Node.js v20.11.0
  baseDirectory: import.meta.dirname,
});

const eslintConfig = [
  ...compat.config({
    extends: [
      "next",
      "next/core-web-vitals",
      "next/typescript",
      "plugin:prettier/recommended",
      "plugin:jsx-a11y/recommended",
    ],
    plugins: ["prettier", "jsx-a11y"],
    rules: {
      "prettier/prettier": [
        "error",
        {
          trailingComma: "all",
          semi: false,
          tabWidth: 2,
          singleQuote: true,
          printWidth: 80,
          endOfLine: "auto",
          arrowParens: "always",
          plugins: ["prettier-plugin-tailwindcss"],
        },
        {
          usePrettierrc: false,
        },
      ],
      "react/react-in-jsx-scope": "off",
      "jsx-a11y/alt-text": "warn",
      "jsx-a11y/aria-props": "warn",
      "jsx-a11y/aria-proptypes": "warn",
      "jsx-a11y/aria-unsupported-elements": "warn",
      "jsx-a11y/role-has-required-aria-props": "warn",
      "jsx-a11y/role-supports-aria-props": "warn",
    },
  }),
];

export default eslintConfig;
```

### Visual Studio Code Configuration for AutoFix

To streamline your development workflow, configure VS Code to automatically fix ESLint issues on save.

1. **Install the ESLint Extension:**

   - Open VS Code and navigate to the **Extensions** view (Command + Shift + X).
   - Search for "ESLint" and **install the extension by Microsoft**.
   - _(Optional)_ Restart VS Code to ensure the extension is fully loaded.

2. **Enable Auto Fix on Save:**
   Add the following lines to your VS Code `settings.json` file. This setting tells VS Code to run ESLint's `fixAll` command whenever you save a file.

```json
"editor.codeActionsOnSave": {
    "source.fixAll.eslint": "always"
 }
```
