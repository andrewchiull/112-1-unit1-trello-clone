# Web Programming HW#1


## Reference

- (Frontend linter init settings for React) [ntuee-web-programming/112-1-unit1-trello-clone](https://github.com/ntuee-web-programming/112-1-unit1-trello-clone)
    - [local README](./../refcode/112-1-unit1-trello-clone/README.md)

- ~~[ntuee-web-programming/112-1-unit1-todo-list](https://github.com/ntuee-web-programming/112-1-unit1-todo-list)~~ // DEPRECATED
    - [local README](./../refcode/112-1-unit1-todo-list/README.md)

## Run the project

If you only want to run the project, you can follow the steps below.

### 1. Clone the project

Please find the `.zip` download link of `HW1: My Diary` at https://wp.ee.ntu.edu.tw/.

![picture 3](../images/25177c34dca1d13f856b44adc2bc1cca7ff1646a520a57548cd5e28f23f4204a.png)  


### 2. Install dependencies

```bash
cd backend
yarn
```

### 3. Run the server

```bash
yarn start
```

### 4. Open the frontend

Open `frontend/index.html` by clicking it in your file explorer.

Or if you're on ubuntu, you can run the following command to open it in your browser.

```bash
cd frontend
xdg-open index.html
```

If you're on macOS, you can run the following command to open it in your browser.

```bash
cd frontend
open index.html
```


## Notes

### Coding with MongoDB

[ref](https://www.notion.so/02-More-on-Full-Stack-Apps-e98a20066c974d9d858cb0878364f391?pvs=4#22aa044897164309ba273526586100ec)

### `export const getTodos` const method
[ref](https://www.notion.so/02-More-on-Full-Stack-Apps-e98a20066c974d9d858cb0878364f391?pvs=4#0282d331a6ec4d8fb65ddd84ce4d6d6d)

要用 `const` 來保證這個 method 沒有 side effects，即不會更動到 caller。

### Destructuring Assignments

[ref](https://www.notion.so/02-More-on-Full-Stack-Apps-e98a20066c974d9d858cb0878364f391?pvs=4#e37c0026cf81474b84f3213e29d9de60)

```javascript
const { title, description } = req.body;

// equals to

const title = req.body.title;
const description = req.body.description;
```

### `(req, res)` 怎麼知道 caller method 是 `put`?

[ref](https://www.notion.so/02-More-on-Full-Stack-Apps-e98a20066c974d9d858cb0878364f391?pvs=4#1f6f2d65925040f980450b7c3d9214b3)

![picture 2](../images/4b5327aeddd920d5c85bbe4f1292fbc4bd438d621445559b09d27acda86e4462.png)  

> 因此，只要前端打過來的是，例如：…/api/todos/12345，那 id 就會收到 12345




### 建立一個 “Promise” 的 MongoDB 連線！

其實應該可以用 `async/await` ，老師說之後示範。

### [Git 版本控制教學 - submodule - MyApollo](https://myapollo.com.tw/blog/git-tutorial-submodule/)

### [[前端筆記] 使用 Node.js 時噴錯 -Error: listen EADDRINUSE: address already in use 127.0.0.1:3000 | by Bonnie Wang | Medium](https://bonnieyf.medium.com/%E5%89%8D%E7%AB%AF%E7%AD%86%E8%A8%98-%E4%BD%BF%E7%94%A8-node-js-%E6%99%82%E5%99%B4%E9%8C%AF-error-listen-eaddrinuse-address-already-in-use-127-0-0-1-3000-e9f14532ad50)

## Problems

1. lint 的部分應該放在 setup 後面？
2. [這裡 merge 有問題](https://github.com/ntuee-web-programming/112-1-unit1-todo-list#5-install-dependencies-week-2)

# Setup

## Frontend Setup

### 1. Create a vite project

```bash
$ yarn create vite
yarn create v1.22.17
✔ Project name: … frontend
✔ Select a framework: › React
✔ Select a variant: › TypeScript

cd frontend
yarn
yarn dev
```


## Backend Setup

### 1. Create a `backend` folder

```bash
mkdir backend
```

### 2. Create a `package.json` file

```bash
cd backend
yarn init -y
```

### 3. Install dependencies

```bash
yarn add express cors mongoose dotenv body-parser
```

### 4. Typescript setup

```bash
yarn add -D ts-node typescript @types/cors @types/node @types/express
```
`-D`: dev only

Then we create a `tsconfig.json` file

```bash
yarn tsc --init
```

### 5. Create an entry point

```bash
mkdir src
touch src/index.ts
``` 


### 6. Add scripts to `package.json`

```json
"scripts": {
  "dev": "nodemon src/index.ts",
  "start": "ts-node src/index.ts",
  "lint": "eslint src",
  "format": "prettier --write src"
}
```


### Do this after the linters are set up

Add the following line to `tsconfig.json`. Now we can import from `@lib/*` instead of `../../../lib/*`.

```json
{
  "compilerOptions": {
    ...
    "@lib/*": ["../lib/*"], // <--- Do NOT add this line

    // Use This Instead // ISSUE
    "paths": {
      "@lib/*": ["../lib/*"]
    }
    ...
  }
}
```