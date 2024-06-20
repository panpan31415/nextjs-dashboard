# Adding Search and Pagination

## Why use URL search params?
As mentioned above, you'll be using URL search params to manage the search state. This pattern may be new if you're used to doing it with client side state.

There are a couple of benefits of implementing search with URL params:

- Bookmarkable and Shareable URLs: Since the search parameters are in the URL, users can bookmark the current state of the application, including their search queries and filters, for future reference or sharing.
- Server-Side Rendering and Initial Load: URL parameters can be directly consumed on the server to render the initial state, making it easier to handle server rendering.
- Analytics and Tracking: Having search queries and filters directly in the URL makes it easier to track user behavior without requiring additional client-side logic.

## Adding the search functionality

- `useSearchParams`- Allows you to access the parameters of the current URL. For example, the search params for this URL /dashboard/invoices?page=1&query=pending would look like this: {page: '1', query: 'pending'}.
- `usePathname` - - Lets you read the current URL's pathname. For example, for the route /dashboard/invoices, usePathname would return `/dashboard/invoices`.
- `useRouter` - Enables navigation between routes within client components programmatically. There are multiple methods you can use.

1. Capture the user's input
   - "use client" - This is a Client Component, which means you can use event listeners and hooks.
   - <input> - This is the search input.
  
2. Update the URL with the search params
Import the useSearchParams hook from 'next/navigation', and assign it to a variable:
` const searchParams = useSearchParams();`


`URLSearchParams` is a Web API that provides utility methods for manipulating the URL query parameters. Instead of creating a complex string literal, you can use it to get the params string like ?page=1&query=a.

```
'use client';
 
import { MagnifyingGlassIcon } from '@heroicons/react/24/outline';
import { useSearchParams, usePathname, useRouter } from 'next/navigation';
 
export default function Search() {
  const searchParams = useSearchParams();
  const pathname = usePathname();
  const { replace } = useRouter();
 
  function handleSearch(term: string) {
    const params = new URLSearchParams(searchParams);
    if (term) {
      params.set('query', term);
    } else {
      params.delete('query');
    }
    replace(`${pathname}?${params.toString()}`);
  }
}
```
- `${pathname}` is the current path, in your case, "/dashboard/invoices".
- As the user types into the search bar, `params.toString()` translates this input into a URL-friendly format.
- `replace(${pathname}?${params.toString()})`updates the URL with the user's search data. For example,`/dashboard/invoices?query=lee`if the user searches for "Lee".
- The URL is updated without reloading the page, thanks to Next.js's client-side navigation (which you learned about in the chapter on navigating between pages.)

3. Keeping the URL and input in sync
To ensure the input field is in sync with the URL and will be populated when sharing, you can pass a defaultValue to input by reading from searchParams:

```
<input
  className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
  placeholder={placeholder}
  onChange={(e) => {
    handleSearch(e.target.value);
  }}
  defaultValue={searchParams.get('query')?.toString()}
/>
```

`defaultValue` vs. `value` / Controlled vs. Uncontrolled
If you're using state to manage the value of an input, you'd use the `value` attribute to make it a controlled component. This means React would manage the input's state.

However, since you're not using state, you can use `defaultValue`. This means the native input will manage its own state. This is okay since you're saving the search query to the URL instead of state.

The defaultValue property sets or returns the default value of a text field.

Note: The default value is the value specified in the HTML value attribute.

The difference between the defaultValue and value property, is that defaultValue contains the default value, while value contains the current value after some changes have been made. If there are no changes, defaultValue and value is the same (see "More Examples" below).

The defaultValue property is useful when you want to find out whether the contents of a text field have been changed.

4. Updating the table

When to use the `useSearchParams()` hook vs. the `searchParams` prop?

You might have noticed you used two different ways to extract search params. Whether you use one or the other depends on whether you're working on the client or the server.

- `<Search>` is a Client Component, so you used the useSearchParams() hook to access the params from the client.
- `<Table>` is a Server Component that fetches its own data, so you can pass the searchParams prop from the page to the component.
As a general rule, if you want to read the params from the client, use the useSearchParams() hook as this avoids having to go back to the server.


### Best practice: Debouncing

## Adding pagination