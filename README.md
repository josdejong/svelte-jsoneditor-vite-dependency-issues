# svelte-jsoneditor vite dependency issues

To reproduce: clone this repo, run `npm install`, run `npm run dev`. See commented config in `svelte.config.js` for a workaround.

In reply to: https://github.com/vitejs/vite/discussions/4230

## Detailed steps to reproduce

```
> npm init svelte@next svelte-jsoneditor-vite-dependency-issues

  √ Which Svelte app template? » Skeleton project
  √ Use TypeScript? ... Yes
  √ Add ESLint for code linting? ... Yes
  √ Add Prettier for code formatting? ... Yes

> cd svelte-jsoneditor-vite-dependency-issues

> npm install

> npm install svelte-jsoneditor@0.2.1
```

Open an editor. Replace the contents of the file `src/routes/index.svelte` with the following:

```html
<script>
  import { JSONEditor } from 'svelte-jsoneditor'

  let json = {
    greeting: 'hello world!'
  }
</script>

<JSONEditor bind:json />
```

Now, start the development server:

```
> npm run dev
```

Open the application in a browser, http://localhost:3000

This will show errors like: 

```
ReferenceError: module is not defined
    at /node_modules/debug/src/index.js?v=ed804413:7:2
    at instantiateModule (...\svelte-jsoneditor-vite-dependency-issues\node_modules\vite\dist\node\chunks\dep-c1a9de64.js:73464:166)
```

## Workaround

To workaround the issue, add a list with dependencies to the vite configuration in the file `svelte.config.js`:

```js
const config = {
  // ...
  
  kit: {
    // ...
    
    vite: {
      optimizeDeps: {
        include: [
          'ace-builds/src-noconflict/ace',
          'ace-builds/src-noconflict/ext-searchbox',
          'ace-builds/src-noconflict/mode-json',
          'ajv',
          'classnames',
          'debug',
          'diff-sequences',
          'json-source-map',
          'natural-compare-lite'
        ]
      }
    }
  }
}
```

