---
marp: true
style: |
  .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
---

```sh
npx  create-next-app@latest
```

```sh
npm i remult
```

```json
{
  "compilerOptions": {
    "experimentalDecorators": true // add this
  }
}
```

- Create components/todo.tsx

```tsx
"use client";
export default function Todo() {
  return (
    <div>
      <h1>Todos</h1>
    </div>
  );
}
```

- clear default page.tsx and css and call Todo

---

- define the entity src/shared
- bootstrap remult on the server

```ts
// src/app/api/[...remult]/route.ts
import { remultNextApp } from "remult/remult-next";
import { Task } from "../../../shared/Task";
const api = remultNextApp({
  entities: [Task],
});
export const { GET, POST, PUT, DELETE } = api;
```

- Tasks: Fix, Pay, Run, Eat, Buy
- Demo find

---

- add task
- Go, Do, Read, Cook, Walk

---

```css
body {
  font-family: Arial, Helvetica, sans-serif;
  background-color: whitesmoke;
  margin: 0;
}
h1 {
  color: #ef4444;
  font-style: italic;
  font-size: 4rem;
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
  padding: 0.5rem 1rem;
  border-bottom: 1px solid lightgray;
  display: flex;
  align-items: center;
  gap: 0.25rem;
}
input[type="checkbox"] {
  width: 1.5rem;
  height: 1.5rem;
}
input {
  font-size: 100%;
  width: 100%;
  padding: 8px;
  border: 0;
}
```

---

```css
input:placeholder-shown {
  font-style: italic;
}
span {
  flex-grow: 1;
}
button {
  background-color: white;
  border: 2px solid #0000001a;
  border-radius: 0.5rem;
  padding: 0.5rem;
  white-space: nowrap;
  font-size: 100%;
  cursor: pointer;
}
```

---

- validation
- live query
  - REMEMBER TO REMOVE THE ADD CODE TO PREVENT THE ARRAY PLAY
- update multiple rows

---

# Next Auth

- on Layout.tsx
  ```ts
  return (
    <html lang="en">
      <SessionProvider> <!-- this is what we need-->
        <body className={inter.className}>{children}</body>
      </SessionProvider>
    </html>
  );
  ```
- Add use client

---

# Todo tsx

```tsx
const session = useSession();
useEffect(() => {
  if (session.status === "unauthenticated") signIn();
  else if (session.status === "authenticated")
    return taskRepo...
}, [session]);
if (session.status !== "authenticated") return <></>;
return
<main>
  <div>
    {JSON.stringify(session.user)}
    <button onClick={() => signOut()}>Sign Out</button>
  </div>
```

---

# /src/app/api/auth/[...nextauth]/route.ts

```ts
import NextAuth from "next-auth/next";
import Credentials from "next-auth/providers/credentials";
import { UserInfo, remult } from "remult";
const nextAuth = NextAuth({
  providers: [
    Credentials({
      credentials: {
        name: {
          placeholder: "Try Steve or Jane",
        },
      }, // build slowly

      authorize: (info) => findUser(info?.name) || null,
    }),
  ],
});
export { nextAuth as GET, nextAuth as POST };
const validUsers: UserInfo[] = [
  // build slowly
  { id: "1", name: "Jane" },
  { id: "2", name: "Steve" },
];
function findUser(name?: string | null) {
  return validUsers.find((user) => user.name === name);
}
//.env.local
//NEXTAUTH_SECRET=
```

---

get user for remult

```ts
export async function getUserOnServer() {
  const session = await getServerSession();
  return findUser(session?.user?.name);
}
```

---

add role

add callback

```ts
callbacks: {
  session: ({ session }) => ({
    ...session,
    user: findUser(session.user?.name),
  }),
},
```

in front:

```
remult.user = session.data.user as UserInfo
```

---

Add database

- npm i pg
- DATABASEURL=postgres://postgres:MASTERKEY@localhost/postgres

---

# deploy

## Railway

```json
"start": "next start -p $PORT",
```

Railway up
Define url

Define variables:
NEXTAUTH_SECRET
NEXTAUTH_URL
DATABASE_URL

---

## Deploy Vercel

```ts
  dataProvider: createPostgresDataProvider({
    connectionString:
      process.env["POSTGRES_URL"] || process.env["DATABASE_URL"],
    configuration: {
      ssl: Boolean(process.env["POSTGRES_URL"]),
    },
  }),
```

- Disable live query

---

## Ably

- npm i ably

```ts
import ably from "ably/promises"
import { AblySubscriptionServer } from "remult/ably"
import { DataProviderLiveQueryStorage } from "remult/server"
const api = remultNextApp({{
  //...
  subscriptionServer: new AblySubscriptionServer(
    new ably.Rest(process.env["ABLY_API_KEY"]!)
  ),
  liveQueryStorage: new DataProviderLiveQueryStorage(dataProvider),
}})
```

---

```ts
import ably from "ably/promises";
import { NextResponse } from "next/server";

export async function POST() {
  const token = await new ably.Rest(
    process.env["ABLY_API_KEY"]!
  ).auth.createTokenRequest({ capability: { "*": ["subscribe"] } });
  return NextResponse.json(token);
}
```

---

# Front end

RETURN LIVE QUERY
```ts
useEffect(() => {
remult.apiClient.subscriptionClient = new AblySubscriptionClient(
new ably.Realtime({ authUrl: "/api/getAblyToken", authMethod: "POST" })
)
}, [])
```