[Vite](https://vitejs.dev/) is a fast and lightweight build tool for modern JavaScript applications. It is designed to be simple to use and easy to configure, with a focus on providing a smooth developer experience.

We love developing with Vite because it's fast and easy to work with. But we're developing a full-stack app with Express as our API server and running both Vite's dev server and a separate Node process in development is annoying. So we looked for the simplest way to have Vite run the Express server and hot-reload it as we make changes.

Let's demonstrate it by building a full-stack app, that runs simultaneously on the same machine `react-ts` and `express`.

### A Little More About Vite

Vite uses native ES module imports to build your applications and supports hot module replacement (HMR) for fast development. It also has built-in support for JSX and TypeScript, and allows you to use modern syntax such as the [optional chaining operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) `foo?.bar` and [nullish coalescing operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing) `null ?? 'bla'` without needing to set up a complicated build configuration.

Overall, Vite aims to make it easy for developers to create high-performance, modern applications with minimal setup and maintenance overhead.

## Creating A Simple Vite Project

We will start with the `react-ts` template

```sh
npm create -y vite@latest my-project-name -- --template react-ts
```

## Adding The Express Server Code

Next, we'll install `express` by running

```bash
cd my-project-name 
npm i express 
npm i -D @types/express
```

After that, we'll create the server's `index.ts` file in the `src/server` folder

```typescript
import express from 'express'; 
export const app = express();
app.get('/api/test', (_, res) => 
    res.json({ greeting: "Hello" }
))
```

**Notes**:

1. We didn't add the `app.listen` call - we'll add that later on.
    
2. We exported the `app` express application - we'll use that later for vite to run.
    

## Creating The `vite` Plugin

In the project root create a file called `express-plugin.ts` with the following code

```typescript
export default function express(path: string) {
  return {
    name: "vite3-plugin-express",
    configureServer: async (server: any) => {
      server.middlewares.use(async (req: any, res: any, next: any) => {
        process.env["VITE"] = "true";
        try {
          const { app } = await server.ssrLoadModule(path);
          app(req, res, next);
        } catch (err) {
          console.error(err);
        }
      });
    },
  };
}
```

**Notes:**

1. This code instructs `vite` to **load on its server** the path that we send it **as a parameter** (later on, in our case `src/server`).
    
2. It also sets the `VITE` process environment variable to `true` - we can use that to **differentiate** when the express server is called **using this plugin or not**. For example, as a part of making our project production-ready, we can add these lines to `server/index.ts`:
    

```typescript
if (!process.env['VITE']) {
  const frontendFiles = process.cwd() + '/dist'
  app.use(express.static(frontendFiles))
  app.get('/*', (_, res) => {
    res.send(frontendFiles + '/index.html')
  })
  app.listen(process.env['PORT'])
}
```

## Using The `vite` Plugin

Edit the `tsconfig.node.json` file to include the `express-plugin.ts` file

```json
{
  "compilerOptions": {
    "composite": true,
    "module": "ESNext",
    "moduleResolution": "Node",
    "allowSyntheticDefaultImports": true
  },
  "include": ["vite.config.ts","express-plugin.ts"] // Adjust this
}
```

Edit the `vite.config.ts` file to import the plugin and use it

```typescript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import express from './express-plugin' //Add this

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react(), express('src/server')],  // Adjust this
})
```

Now the `express` plugin is being imported from a local file `./express-plugin`. The `express` function is called with the argument `src/server` specifies the location of the server-side entry file.

When you run `vite` with this configuration, it will build the client-side application as usual and then start an Express server in the background. The Express server will use the specified server-side entry file as the starting point for setting up routes, middleware, and any other server-side logic.

## Test That It Works

Run the `vite` app using `npm run dev` .

If you navigate to [`http://127.0.0.1:5173/`](http://127.0.0.1:5173/) you see the default welcome page of `Vite + React`, but our `express` server is live too, navigate to `http://127.0.0.1:5173/api/test` to see the greeting.

Let's make a quick sanity check for the parallel running of `React & Express`. We will add a useEffect hook to get the greeting from our server. In `App.tsx` file, add these lines:

```typescript
//Add this function
const getGreeting = async function () {
  const res = await fetch("/api/test");
  return await res.json();
};

function App() {
  ...
  const [greeting, setGreeting] = useState(""); // Add this

  useEffect(() => { // Add this hook
    getGreeting().then((res) => setGreeting(res.greeting));
  }, []);

  return (
   ...
        //Add this line somewhere
        <p>Server response: {greeting}</p> 
   ...
  );
}
```

And on [`http://127.0.0.1:5173/`](http://127.0.0.1:5173/) you should see the greeting. You don't even need to refresh, thanks to the **HMR .**

![Sanity check illustration](https://cdn.hashnode.com/res/hashnode/image/upload/v1672952549415/3a6443a4-5177-420d-9cc3-78c80ae4429c.png align="center")

## Using An npm Package

To make this easier to use, we've created an `npm` package with this plugin called [`vite3-plugin-express`](https://www.npmjs.com/package/vite3-plugin-express). This plugin replaces the `express-plugin.ts` we built earlier.

Install the package via npm:

```bash
npm i vite3-plugin-express
```

and to use it, slightly change `vite.config.ts` file:

```typescript
//vite.config.ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import express from "vite3-plugin-express"

export default defineConfig({
  plugins: [vue(), express('express-server.ts')]
})
```

**Notes**:

* Make sure that the express handler is exported as `app`
    
* Make sure not to call `app.listen`.
    
    The plugin adds the `VITE` environment variable, use that to disable the call to `app.listen`
    

## Watch This Video

In this video from our BudapestJS meetup, we showed how to turn a front-end React app into a full-stack app using Node.js, Postgres, and [Remult](https://remult.dev). Of course, we used `vite` as a part of our demo. The video's timeline is positioned at the point we configured `vite`.

<iframe width="560" height="315" src="https://www.youtube.com/embed/CnCaMQCu3Kc?start=448"></iframe>