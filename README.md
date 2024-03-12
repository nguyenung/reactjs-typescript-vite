# Setup Reactjs + TypeScript + Vite + ESlint + Prettier

## Folder structure

```txt
📦react-app
 ┣ 📂dist
 ┣ 📂public
 ┃ ┗ 📜vite.svg
 ┣ 📂src
 ┃ ┣ 📂assets
 ┃ ┃ ┗ 📜react.svg
 ┃ ┣ 📜App.css
 ┃ ┣ 📜App.tsx
 ┃ ┣ 📜index.css
 ┃ ┣ 📜main.tsx
 ┃ ┗ 📜vite-env.d.ts
 ┣ 📜.editorconfig
 ┣ 📜.eslintignore
 ┣ 📜.eslintrc.cjs
 ┣ 📜.gitignore
 ┣ 📜.prettierignore
 ┣ 📜.prettierrc
 ┣ 📜index.html
 ┣ 📜package-lock.json
 ┣ 📜package.json
 ┣ 📜tsconfig.json
 ┣ 📜tsconfig.node.json
 ┗ 📜vite.config.ts
```

## Step 1: Init Vite project

```bash
npm create vite@latest
```

Input project name:

```bash
Need to install the following packages:
create-vite@5.2.2
Ok to proceed? (y) y
✔ Project name: … react-app
```

Select Framework:

```bash
✔ Select a framework: › React
```

Select template:

```bash
✔ Select a variant: › TypeScript + SWC
```

Done. Now run:

```bash
cd reactjs-typescript-vite
npm install
```

## Step 2: Install packages for ESlint and Prettier

```bash
npm i prettier eslint-config-prettier eslint-plugin-prettier -D
```

- prettier: code formatter
- eslint-config-prettier: Turns off all rules that are unnecessary or might conflict with Prettier.
- eslint-plugin-prettier: Runs Prettier as an ESLint rule and reports differences as individual ESLint issues.

## Step 3: Configure ESlint

### Update `.eslintrc.cjs` file

Add this value to the `ignorePatterns` array to avoid ESLint to check the `vite.config.ts` file.

```typescript
"vite.config.ts"
```

Add the following code snippet to the `extends` array.

```typescript
"eslint-config-prettier",
"prettier"
```

Add the following code snippet to the `plugins` array.

```typescript
"prettier"
```

Add the following code snippet to the `rules` object to add Prettier's rules.

```typescript
'prettier/prettier': [
  'warn',
  {
    arrowParens: 'always',
    semi: false,
    trailingComma: 'none',
    tabWidth: 2,
    endOfLine: 'auto',
    useTabs: false,
    singleQuote: true,
    printWidth: 120,
    jsxSingleQuote: true
  }
]
```

## Step 4: Config Prettier to format code

Create a `.prettierrc` file in the root directory with the following content.
The purpose is to configure Prettier. It's recommended to install the `Prettier - Code formatter` extension for VS Code so that it can understand it.

```json
{
  "arrowParens": "always",
  "semi": false,
  "trailingComma": "none",
  "tabWidth": 2,
  "endOfLine": "auto",
  "useTabs": false,
  "singleQuote": true,
  "printWidth": 120,
  "jsxSingleQuote": true
}
```

Create a `.prettierignore` in the root directory with the following content.

```prettierignore
node_modules/
dist/
```

## Config the editor to standardize the editor configuration.

Create a `.editorconfig` file in the root directory.

The purpose is to configure synchronized configurations across editors if multiple people are involved in the project.

To make VS Code understand this file, install the `EditorConfig for VS Code` extension.

```editorconfig
[*]
indent_size = 2
indent_style = space
```

## Step 6: Configure alias for `tsconfig.json`

Add this snippet to the `compilerOptions` section in the `tsconfig.json` file.

```json
"baseUrl": ".",
"paths": {
  "~/*": ["src/*"]
}
```

## Step 7: Configure alias for `vite.config.ts`

Install the package @types/node to use Node.js in TypeScript files without encountering errors.

```bash
npm i @types/node -D
```

Configure aliases and enable source maps in the `vite.config.ts` file.

```typescript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react-swc";
import path from "path";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
  },
  css: {
    devSourcemap: true,
  },
  resolve: {
    alias: {
      "~": path.resolve(__dirname, "./src"),
    },
  },
});
```

## Step 8: Update script in the `package.json` file.

```json
"scripts": {
    //...
    "lint:fix": "eslint --fix src --ext ts,tsx",
    "prettier": "prettier --check \"src/**/(*.tsx|*.ts|*.css|*.scss)\"",
    "prettier:fix": "prettier --write \"src/**/(*.tsx|*.ts|*.css|*.scss)\""
}
```

## Command to run the project

That's it! To run in the development environment, we'll use the command `npm run dev`.

If you want to build, use `npm run build`.

Additionally, there are some other commands:

- Preview the build result with `npm run preview`.
- Check for any ESLint-related errors in the project: `npm run lint`.
- Automatically fix ESLint-related errors (not everything can be fixed, but many can): `npm run lint:fix`.
- Check for any Prettier-related errors in the project: `npm run prettier`.
- Automatically fix Prettier-related errors: `npm run prettier:fix`.
