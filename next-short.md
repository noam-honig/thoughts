# What Have I done?

1. "experimentalDecorators": true,
2. npm i remult pg next-auth
3. Added next auth code
4. Added some environment variables

```
NEXTAUTH_SECRET=something-secret
DATABASE_URL=postgres://postgres:MASTERKEY@localhost/postgres
```

6. Add some css

```css
body {
  font-family: Arial;
  background-color: whitesmoke;
  margin: 0;
}
h1 {
  color: #ef4444;
  font-style: italic;
  font-size: 3.5rem;
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
button {
  background-color: white;
  border: 2px solid #0000001a;
  border-radius: 0.5rem;
  padding: 0.5rem;
  white-space: nowrap;
  font-size: 100%;
  cursor: pointer;
  margin-left: auto;
}
```

## Do this!

4. Remove roles from nextauth starter
5. Remove console log from authorize


## Before demo:

1. del db folder
2. drop table
3. Clean cookies

A CRUD framework for fullstack TypeScript

It covers, database access, CRUD api & front-end/backend query language
Authentication, Authorization, validation and even realtime updates.

1. Clean html
2. Create task
3. Add Api
4. Create task form
5. List data
6. Update data
7. Show query language
8. Add live query
9. Add delete Task
10. Add set completed
11. Validation
12. Postgres
13. Authentication
14. Authorization

A CRUD framework for fullstack TypeScript

It covers, database access, CRUD api & front-end/backend query language
Authentication, Authorization, validation and even realtime updates.


1.  Add Decorators
2.  Add Api & Postgres
3.  Implement Add
4.  Implement Change
5.  Implement Delete
6.  Show query language
7.  Add live query
10. Validation
12. Authentication
13. Authorization

- Go, Do, Eat, Run, Buy
- Fix, Pay, Read, Cook, Walk
- Call, Plan,Clean, Study, Sleep
- Rest, Work, Relax, Learn, Play

```tsx
const session = useSession();
useEffect(() => {
  if (session.status === "unauthenticated") {
    signIn();
    return;
  }
  remult.user = session?.data?.user as UserInfo;
  //...
}, [session]);

if (session.status !== "authenticated") return <></>;
//...
<div>
  hello {remult.user?.name} <button onClick={() => signOut()}>Sign out</button>
</div>;
```

```ts
getUser: async (req) => findUserById((await getToken({ req }))?.sub),
```
