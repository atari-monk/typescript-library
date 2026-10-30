## testing a local package with pnpm pack

`pnpm pack` lets you package your library locally and install it in another project without publishing it to npm

### 1. Build the library

Inside your library project:

```bash
pnpm build
```

This generates the distributable files in `dist/`

### 2. Create a package archive

Run:

```bash
pnpm pack
```

This creates a `.tgz` archive, for example:

```text
atari-monk-engine-0.0.1.tgz
```

The archive contains files specified by the `files` field in `package.json`

### 3. Install the package locally

Inside your game project:

```bash
pnpm add ../atari-monk-engine/atari-monk-engine-0.0.1.tgz
```

Adjust the path to match your project structure

### 4. Use the library

Import it like any regular dependency:

```ts
import { something } from "atari-monk-engine";
```

### 5. Update the package

Whenever you modify the library:

1. Run `pnpm build`
2. Run `pnpm pack`
3. Reinstall the updated archive in your game project

```bash
pnpm add ../atari-monk-engine/atari-monk-engine-0.0.1.tgz
```

### Summary

- `pnpm build` — builds the library
- `pnpm pack` — creates a local package archive
- `pnpm add <path-to-tgz>` — installs the package in another project

This workflow tests the actual distributable package without publishing anything to npm
