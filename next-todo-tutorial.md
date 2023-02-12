Setup tailwind:




tasks:

- Clean Car
- Read a book
- Take a nap (completed)
- Pay bills
- Do laundry


### Configure Tailwind (optional)

1. Install Tailwind CSS

```sh
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

2. Configure your template paths

Add the paths to all of your template files in your tailwind.config.js file.

_tailwind.config.js_

```js{3}
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

3. Add the Tailwind directives to your CSS

replace the content of the `globals.css` file with:

_src/styles/global.css_

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
**External div**
```
bg-gray-50 h-screen flex items-center flex-col justify-center text-lg
```
**H1**
text-6xl text-red-500 italic

**main**
bg-white border rounded-lg shadow-lg m-5 w-screen max-w-md

**list div**
border-b px-6 p-2 gap-2 flex items-center

**checkbox**
w-6 h-6

**input**
w-full

**form**
border-b-2 p-2 px-6 flex

**button**
bg-blue-600 hover:bg-blue-700 text-white px-3 py-1 text-base font-semibold rounded-lg

**Bottom Div**
flex justify-between px-6 p-2 gap-4 border-t

**signout div**
flex justify-between px-6 p-2

