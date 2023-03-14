# typescript=lib-vite

Original source code is based on:
Blog post: https://jivancic.com/posts/build-a-component-library.html
Git repository: https://github.com/josip2312/typescript-lib-vite

This template should help to get started developing components with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar) (and disable Vetur).

## Type Support for `.vue` Imports in TS

Since TypeScript cannot handle type information for `.vue` imports, they are shimmed to be a generic Vue component type by default. In most cases this is fine if you don't really care about component prop types outside of templates.

However, if you wish to get actual prop types in `.vue` imports (for example to get props validation when using manual `h(...)` calls), you can run `Volar: Switch TS Plugin on/off` from VSCode command palette.

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

### Step #1:

```sh
npm install
```

Note: if you get an error:

```
npm WARN tarball tarball data for my-component-lib@file:/Users/igorvasiliev/Projects/typescript-lib-vite/my-component-lib-0.0.0.tgz (sha512-0y8KvDSaNQLyLM2TS/GyhPjm3YqfcqjYxeYA2MhaAjzJtYP0koC3C5uGLNT4C92ogf3j/o4VA3KID91TKmRhlg==) seems to be corrupted. Trying again.
npm WARN tarball tarball data for my-component-lib@file:/Users/igorvasiliev/Projects/typescript-lib-vite/my-component-lib-0.0.0.tgz (sha512-0y8KvDSaNQLyLM2TS/GyhPjm3YqfcqjYxeYA2MhaAjzJtYP0koC3C5uGLNT4C92ogf3j/o4VA3KID91TKmRhlg==) seems to be corrupted. Trying again.
npm ERR! code ENOENT
npm ERR! syscall open
npm ERR! path /Users/igorvasiliev/Projects/typescript-lib-vite/my-component-lib-0.0.0.tgz
npm ERR! errno -2
npm ERR! enoent ENOENT: no such file or directory, open '/Users/igorvasiliev/Projects/typescript-lib-vite/my-component-lib-0.0.0.tgz'
npm ERR! enoent This is related to npm not being able to find a file.
npm ERR! enoent

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/igorvasiliev/.npm/_logs/2023-03-14T09_31_15_735Z-debug-0.log
```

### Step #2

Go to `package.json` and temporary remove following line:

```
"dependencies": {
    //"my-component-lib": "my-component-lib-0.0.0.tgz", // <- remove this line (do not comment it out! remove it)
    "vue": "^3.2.20"
  },

```

Then run `npm install` again

### Step #3:

Execute:

```
npm run build
```

Output:

```
> my-component-lib@0.0.0 build
> vite build && vue-tsc --emitDeclarationOnly && mv dist/src dist/types

vite v2.6.14 building for production...
✓ 4 modules transformed.
dist/my-component-lib.es.js   0.89 KiB / gzip: 0.48 KiB
dist/style.css                0.11 KiB / gzip: 0.11 KiB
dist/my-component-lib.umd.js   0.75 KiB / gzip: 0.49 KiB
src/App.vue:2:26 - error TS2307: Cannot find module 'my-component-lib' or its corresponding type declarations.

2 import { MyButton } from 'my-component-lib';
                           ~~~~~~~~~~~~~~~~~~


Found 1 error.
```

It's ok, the file `my-component-lib-0.0.0.tgz` is still missing

### Step #4:

Execute:

```
npm pack
```

Command output:

```
npm notice
npm notice 📦  my-component-lib@0.0.0
npm notice === Tarball Contents ===
npm notice 1.1kB README.md
npm notice 4.3kB dist/favicon.ico
npm notice 910B  dist/my-component-lib.es.js
npm notice 764B  dist/my-component-lib.umd.js
npm notice 403B  dist/src/App.vue.d.ts
npm notice 521B  dist/src/components/MyButton.vue.d.ts
npm notice 65B   dist/src/index.d.ts
npm notice 11B   dist/src/main.d.ts
npm notice 112B  dist/style.css
npm notice 82B   dist/vite.config.d.ts
npm notice 849B  package.json
npm notice === Tarball Details ===
npm notice name:          my-component-lib
npm notice version:       0.0.0
npm notice filename:      my-component-lib-0.0.0.tgz
npm notice package size:  3.4 kB
npm notice unpacked size: 9.1 kB
npm notice shasum:        8829dd97ab936662e1690a69559956f2930895f4
npm notice integrity:     sha512-BuWbZdhgOCwR4[...]GN3sl3gG9g7fg==
npm notice total files:   11
npm notice
```

Note: after this step you'll get `my-component-lib-0.0.0.tgz` and now it's time to return removed line to `package.json` file:

```
"dependencies": {
    "my-component-lib": "my-component-lib-0.0.0.tgz", // <- put it back
    "vue": "^3.2.20"
  },
```

### Step #5:

```
npm install
```

Output:

```
added 1 package, and audited 113 packages in 997ms

15 packages are looking for funding
  run `npm fund` for details

2 moderate severity vulnerabilities

To address all issues, run:
  npm audit fix

Run `npm audit` for details.
```

Installation shall pass now w/o any errors

You are free to run any command from package.json without errors

## List of available commands to execute:

### Typecheck

```sh
npm run typecheck
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Create zipped file of component library

```sh
npm pack
```
