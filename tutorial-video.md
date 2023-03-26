---
marp: true
---

```sh
np create vite@latest
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

add route to server and test
add proxy

```json
  server: { proxy: { "/api": "http://localhost:3002" } }
```

test from vite

---

Add api.ts
add - experimentalDecorators

# Setup done

---

Add entity
Add tasks:

1. Clean car
2. Read a book
3. Take a nap (completed)
4. Pay bills
5. Do Laundry

---

get tasks on the front end and start with css:

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
main > div {
  padding: 0.5rem 1rem;
  border-bottom: 1px solid lightgray;
  display: flex;
  align-items: center;
  gap: 0.25rem;
}
input[type="checkbox"] {
  height: 1.5rem;
  width: 1.5rem;
  flex-shrink: 0;
}
```

---

Add task
first add state and html, then the addTask method.

```css
main > div,
main > form {
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

sign in css

```css
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px;
}
```


- skip helmet, compression etc...
- skip path - just use the static url
  ```ts
  app.use(express.static(process.cwd() + "/dist"))
  ```
- use tsx also for start
