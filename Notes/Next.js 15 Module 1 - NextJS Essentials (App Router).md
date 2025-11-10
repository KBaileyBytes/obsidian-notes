---
tags:
  - module
lecture_count: 
current_lecture: "0"
length: 
status: Archived
course_link: '[[Next.js 15]]'
link: 
module_number: 1
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [x] Routing
- [ ] Pages
- [ ] Components
- [ ] Requesting & Sending Data
- [ ] Stying, Images & Metadata

```

### Reserved Filenames
---

- `page.js` => Create a new page (e.g., `app/about/page.js` creates a `<your-domain>/about` page)

- `layout.js` => Create a new layout that wraps sibling and nested pages

- `not-found.js` => Fallback page for "Not Found" errors (thrown by sibling or nested pages or layouts)

- `error.js` => Fallback page for other errors (thrown by sibling pages or nested pages or layouts)

- `loading.js` => Fallback page which is shown whilst sibling or nested pages (or layouts) are fetching data

- `route.js` => Allows you to create an API route (i.e., a page which does NOT return JSX code but instead data, e.g., in the JSON format)

### Routing & Pages
---

![[Pasted image 20250220163455.png | center]]


To add new routes to your app, simply create a folder with a route name, in this case the route would be  `localhost:3000/about`.

To navigate between routes, make sure to use the built-in `<Link>` tag to prevent re-rendering pages.

````ad-code
title: Link Example

```html
<Link href="/about">About Us</Link>
```


````



### Layout and metadata
---

Each directory can have a special `layout.js` file that acts as a container for the `page.js` file. Here we can modify the exported `metadata` const to change properties such as the `title`
 and `description` of the page.

```js
import './globals.css'

export const metadata = {
  title: 'NextJS Course App',
  description: 'Your first NextJS app!',
};

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```


---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
