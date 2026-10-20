## Project `typescript-library` setup

### 1. Create the project

```bash
mkdir typescript-library
cd typescript-library
pnpm init
pnpm add -D typescript tsup @types/node
touch tsconfig.json
touch tsup.config.ts
mkdir src
touch src/index.ts
touch .gitignore
touch README.md
```

- `typescript` → compiler
- `tsup` → bundler (esbuild-based, very fast)
- `@types/node` → Node types

### 2. Configure `package.json`

```json
{
  "name": "atari-monk-typescript-library",
  "version": "0.0.1",
  "description": "Minimal TypeScript library template",
  "main": "./dist/index.cjs",
  "module": "./dist/index.js",
  "types": "./dist/index.d.ts",
  "exports": {
    ".": {
      "types": "./dist/index.d.ts",
      "import": "./dist/index.js",
      "require": "./dist/index.cjs"
    }
  },
  "files": ["dist"],
  "scripts": {
    "build": "tsup",
    "dev": "tsup --watch",
    "clean": "rm -rf dist"
  },
  "keywords": [],
  "license": "MIT"
}
```

Key points:

- ESM + CJS support
- Clean `exports` field (modern npm best practice)
- Only publishes `dist/`

### 3. Initialize TypeScript config

`tsconfig.json`

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "Bundler",
    "declaration": true,
    "strict": true,
    "skipLibCheck": true,
    "outDir": "dist",
    "noEmit": true
  },
  "include": ["src"]
}
```

Why `noEmit: true`?

- tsup handles actual output
- TypeScript only validates + generates types

### 4. Configure tsup

`tsup.config.ts`

```ts
import { defineConfig } from "tsup";

export default defineConfig({
  entry: ["src/index.ts"],
  format: ["esm", "cjs"],
  dts: true,
  clean: true,
  sourcemap: true,
  outDir: "dist",
  minify: false,
});
```

This ensures:

- ESM + CJS builds
- Type definitions generated
- Clean output every build

### 5. Add example `hello` function

`src/index.ts`

```ts
export function hello(name: string): string {
  return `Hello, ${name}!`;
}
```

### 6. Add `.gitignore`

```gitignore
node_modules
dist
```

### 7. Add README

````md
# typescript-library

Minimal TypeScript library template.

## Install

pnpm add atari-monk-typescript-library

### Usage

```ts
import { hello } from "typescript-library";

console.log(hello("world"));
```
````
