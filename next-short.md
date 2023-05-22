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
2.  Add Api 
3.  explain repo
4.  Implement Add
5.  Implement Change
6.  Implement Delete
7.  Show query language
8.  Add live query
9.  Validation
10. Authentication
11. Authorization

- Fix, Pay, Run, Buy, Eat, 
- Go, Do, Read, Cook, Walk
- Call, Plan,Clean, Study, Sleep
- Rest, Work, Relax, Learn, Play



> Here we have a front-end react app written with next JS.
> I've configured remult as a catch all route in next js, 
> And use postgresql as database, and get the user from nextauth
>
> In this Todo app, we can add tasks, complete tasks and delete.
>
> It uses the Task type. 
>
> Let's have remult expose a full CRUD API for tasks
>
> It's as easy as adding these four decorators
>
> Register it as an entity - and test our api.
>
> Now let's use it in the front add
>
> First we'll define a task repository
> 
> And we'll use it to get tasks, add, complete and delete
> 
> Four lines of code is all this react component needs to query and update tasks on the server..