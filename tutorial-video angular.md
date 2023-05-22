---
marp: true
---

```sh
ng new
```

```sh
npm i express remult tsx
npm i --save-dev @types/express
```

```sh
npm run dev
```

add src/server/index.ts

```json
"dev-node":"tsx watch src/server"
```
```json
"allowSyntheticDefaultImports":true
```

---

```json
// proxy.conf.json
{
  "/api": {
    "target": "http://localhost:3002",
    "secure": false
  }
}
```
```sh
"dev": "ng serve --proxy-config proxy.conf.json --open",
```

---

Add entity
Add tasks:

1. Clean car
2. Read a book
3. Take a nap (completed)
4. Pay bills
5. Do Laundry

---

get tasks on the front end

Add form for new task

import FormsModule

 and start with css:

```css
body {
  font-family: Arial;
  background-color: whitesmoke;
  margin: 0;
}
h1 {
  color: #ef4444;
  font-style: italic;
  font-size: 3.75rem;
  font-weight: inherit;
  text-align: center;
  margin: 0;
}
main {
  background-color: white;
  max-width: 500px;
  min-width: 300px;
  margin: auto;
  border: 1px solid lightgray;
  border-radius: 0.5rem;
  box-shadow: 0 2px 4px #0003, 0 25px 50px #0000001a;
}
```

---

```css
main > form,
main > div {
  padding: 0.5rem;
  border-bottom: 1px solid lightgray;
  display: flex;
  align-items: center;
  gap: 0.25rem;
}
input {
  font-size: 100%;
  width: 100%;
  padding: 8px;
  border: 0;
}
input:placeholder-shown {
  font-style: italic;
}
input[type="checkbox"] {
  height: 1.5rem;
  width: 1.5rem;
  flex-shrink: 0;
}
```

---

```css
button {
  background-color: white;
  border: 2px solid #0000001a;
  border-radius: 0.5rem;
  padding: 0.5rem 0.5rem;
  white-space: nowrap;
  font-size: 100%;
  cursor: pointer;
}

```

---



## Live Query
* ## REMEMBER LIVE QUERY ADD ISSUE
## Validation
etc..

## remember retry when talking about signin

- skip helmet, compression etc...
- skip path - just use the static url
  ```ts
  app.use(express.static(process.cwd() + "/dist"));
  ```
- use tsx also for start
