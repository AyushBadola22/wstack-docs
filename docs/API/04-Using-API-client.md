# Using Api Client

This app supports various HTTP methods, and all requests are handled in `src/app/api/[...routes]/route.tsx`. It exports all the related HTTP methods so you only need to make the api call using your preferred method and you are good to go.

## Available Methods
```ts
export const GET = handle(app);
export const POST = handle(app);
export const PUT = handle(app);
export const DELETE = handle(app);
export const PATCH = handle(app);
export const OPTIONS = handle(app);
```

Each exported method is responsible for handling the corresponding HTTP request and routing it to the appropriate logic within the app.

## Example GET Request using TanStack Query

TanStack Query is a powerful library for managing server state in React applications. You can use it to call API endpoints like the one you’ve defined in your route.tsx file.

Using TanStack Query in combination with your Hono API client allows you to manage server-state in a declarative way while handling various HTTP methods such as GET, POST, PUT, DELETE, and PATCH. By leveraging TanStack Query, It can simplify state management, automatically handle caching and refetching.

Here’s how you can perform a GET request to fetch data using TanStack Query:

```ts
import { useQuery } from '@tanstack/react-query';

const fetchHello = async () => {
  const res = await fetch("/api/hello");
  if (!res.ok) {
    throw new Error("Failed to fetch data");
  }
  return res.json();
};

const HelloComponent = () => {
  const { data: helloData, error, isLoading } = useQuery({
    queryKey: ["hello"],
    queryFn: fetchHello, 
  });

  if (isLoading) {
    return <div>Loading...</div>;
  }

  if (error instanceof Error) {
    return <div>Error: {error.message}</div>;
  }
  return <div>{helloData?.message}</div>;
};

export default HelloComponent;

```
## Handling POST, PUT, DELETE Requests with TanStack Query

Just like with GET requests, you can also use TanStack Query for making POST, PUT, DELETE, or PATCH requests to your API. Below are some examples of how to handle these HTTP methods.

### Example: Making a POST Request

For sending data (e.g., creating a new resource), use the `mutate` function from the `useMutation` hook:

```ts
import { useMutation } from '@tanstack/react-query';

const createUser = async (userData: { name: string }) => {
  const res = await fetch("/api/users", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(userData),
  });

  if (!res.ok) throw new Error("Failed to create user");
  return res.json();
};

const UserCreationComponent = () => {
  const mutation = useMutation({
    mutationFn: createUser,
  });

  const handleCreateUser = () => {
    const newUser = { name: "John Doe" };
    mutation.mutate(newUser);
  };

  return (
    <div>
      <button onClick={handleCreateUser}>Create User</button>
      {mutation.isLoading && <div>Creating user...</div>}
      {mutation.isError && <div>Error: {mutation.error.message}</div>}
      {mutation.isSuccess && <div>User created successfully!</div>}
    </div>
  );
};

export default UserCreationComponent;
```

### Example: Making a PUT Request

For updating a resource:

```ts
const updateUser = async (userId: string, userData: { name: string }) => {
  const res = await fetch(`/api/users/${userId}`, {
    method: "PUT",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(userData),
  });

  if (!res.ok) throw new Error("Failed to update user");
  return res.json();
};
```

### Example: Making a DELETE Request

For deleting a resource:

```ts
const deleteUser = async (userId: string) => {
  const res = await fetch(`/api/users/${userId}`, {
    method: "DELETE",
  });

  if (!res.ok) throw new Error("Failed to delete user");
  return res.json();
};
```
