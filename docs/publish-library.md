## Publish library

### 1. Build

```bash
pnpm build
# sanity check file after building
node -e "import('./dist/index.js').then(m => console.log(m.hello('world')))"
```

You should get:

```
dist/
  index.js      (ESM)
  index.cjs     (CommonJS)
  index.d.ts    (types)
```

### 2. Publish

```bash
npm login
npm publish --access public
```
