# run-ts

> A tools to use Typescript files as npm scripts

## Gist

**before**

```json
{
  "scripts": {
    "setup": "ts-node --project ./scripts/tsconfig.json ./scripts/setup.ts some-argument",
    "build": "ts-node --project ./scripts/tsconfig.json ./scripts/build.ts"
  }
}
```

**after**

```json
{
  "scripts": {
    "setup": "run-ts some-argument",
    "build": "run-ts"
  }
}
```

## How to

### 1. Install `run-ts`

```bash
npm install --save-dev run-ts
# or
yarn add --dev run-ts
```

### 2. Create a `scripts` folder

```bash
mkdir scripts
```

### 3. Create a `scripts/tsconfig.json` file

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "target": "es6",
    "baseUrl": "."
  }
}
```

### 4. Create a `scripts/my-script.ts` file

```ts
const foo: number = 42;
console.log(foo);
```

### 5. Create a `my-script` scripts in your `package.json`

```json
{
  "scripts": {
    "my-script": "run-ts"
  }
}
```

That's it, now when you run `npm run my-script` the `scripts/my-script.ts` file is executed.

## Using args

If your file export a function as `default`, `run-ts` will execute this function with the arguments as first parameter:

```ts
// scripts/setup.ts
export default function setup(args: Array<string>) {
  console.log(args);
}
```

**Note**: You can also use `process.argv` but you have to strip the first two items (`node` and `run-ts`)
