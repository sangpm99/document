---
id: query-functions
title: Query Functions
sidebar_position: 3
---

Một query function sẽ trả về 1 promise có thể là `data` hoặc `error`.

[//]: # "Example"

```tsx
useQuery({ queryKey: ["todos"], queryFn: fetchAllTodos });
useQuery({ queryKey: ["todos", todoId], queryFn: () => fetchTodoById(todoId) });
useQuery({
  queryKey: ["todos", todoId],
  queryFn: async () => {
    const data = await fetchTodoById(todoId);
    return data;
  },
});
useQuery({
  queryKey: ["todos", todoId],
  queryFn: ({ queryKey }) => fetchTodoById(queryKey[1]),
});
```

[//]: # "Example"

## Query Function Variables

`queryKey` không chỉ để định danh cache, mà còn được truyền vào queryFn thông
qua `QueryFunctionContext`. Nhờ vậy, bạn có thể viết `queryFn` tái sử dụng mà không
cần truyền biến từ ngoài.

[//]: # "Example4"

```tsx
function Todos({ status, page }) {
  const result = useQuery({
    queryKey: ["todos", { status, page }],
    queryFn: fetchTodoList,
  });
}

// Access the key, status and page variables in your query function!
function fetchTodoList({ queryKey }) {
  const [_key, { status, page }] = queryKey;
  return new Promise();
}
```

[//]: # "Example4"

### QueryFunctionContext
