---
marp: true
---


So I wanted to build a CRUD application
* Time to market is critical (I want to fail fast)
* Quick turnaround
* - a little about the monolith

---

What do I need?:
1. Types on the front end
2. Types on the backend
3. Data transfer objects
4. Validations on the front end
5. Validations on the backend
6. Authorization on the front end 
7. Authorization on the API
8. ORM / sql
9. API Routes
10. Live updates across users
11. Query language


---

Review the list:
1. ORM (prisma etc...)
2. Next JS, remix etc.. are a step right direction because we ca
4. Routes that are glued using:
   1. Graphql
   2. TRPC
   3. Rest API (open api)


--- 

I want a single source of truth because:
I want to get things done
I'm lazy
I'm error prone

---

Alternatives for app development:
1. Low code (Wix, wordpress, retool, notion, air tables, google forms etc...)
   1. Pros:
      1. Quick to get in front of users
   2. Cons:
      1. Not flexible
      2. The easy is easier, the hard is harder
      3. Vendor lock in
      4. Developer availability 
2. BAAS - Firebase, appwrite, platformatic, supabase
   1. Pros:
      1. Fast time to market
      2. 
   2. Cons:
      1. No reuse
      2. Code generation
      3. Flexibility
      4. The easy is easier, the hard is harder
      5. A different language
         1. Supabase - I write pl sql
      6. Developer experience when writing server functions or customization code.
3. Non Isomorphic
   1. Backend in .NET/php/
4. Node JS backend
   1. custom writing routes etc...
