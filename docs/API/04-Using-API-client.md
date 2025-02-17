# Using Api Client

This app supports various HTTP methods, and all requests are handled in `src/app/api/[...routes]/route.tsx`.

## Available Methods
```ts
export const GET = handle(app);
export const POST = handle(app);
export const PUT = handle(app);
export const DELETE = handle(app);
export const PATCH = handle(app);
export const OPTIONS = handle(app);
```

## Example GET Request using TanStack Query

To call a GET request using TanStack Query, you can use the `useQuery` hook as shown below:

```ts
import { useQuery } from '@tanstack/react-query';

const fetchHello = async () => {
    const res = await fetch("/api/hello");
    if (!res.ok) throw new Error("Failed to fetch data");
    return res.json();
  };

const { data: helloData } = useQuery({
    queryKey: ["hello"],
    queryFn: fetchHello,
});
```