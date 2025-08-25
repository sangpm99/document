---
sidebar_position: 2
---

# Cấu trúc cơ bản

## Tạo Component Wrapper

Để sử dụng **React Query** trong toàn bộ ứng dụng, cần tạo một component wrapper cung cấp `QueryClientProvider`.  
Component này có thể được khai báo trong layout tổng:

```tsx title="src/components/ReactQueryWrapper.tsx"
"use client";

import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

const queryClient = new QueryClient();

export default function ReactQueryWrapper({ children }: { children: React.ReactNode }) {
  return <QueryClientProvider client={queryClient}>{children}</QueryClientProvider>;
}
```

Sau khi cấu hình, các component con trong ứng dụng có thể truy cập hook và API của React Query.

## Sử dụng tại Function Component

Ví dụ sử dụng trong một function component:

```tsx title="src/app/page.tsx"
"use client";

import { useQuery } from "@tanstack/react-query";

export default function Home() {
  const { isPending, error, data } = useQuery({
    queryKey: ["repoData"],
    queryFn: () => fetch("https://api.github.com/repos/TanStack/query").then((res) => res.json()),
  });

  if (isPending) return "Loading...";

  if (error) return "An error has occurred: " + error.message;

  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.description}</p>
      <strong>👀 {data.subscribers_count}</strong>
      <strong>✨ {data.stargazers_count}</strong>
      <strong>🍴 {data.forks_count}</strong>
    </div>
  );
}
```

Trong đó:

- `useQuery`: dùng để fetch dữ liệu
- `queryKey`: dùng để định danh cho query này
- `queryFn`: hàm gọi api

## Tự động gọi query

Mặc định khi khai báo query sẽ tự động check xem trong catche có dữ liệu của `queryKey` chưa,
nếu chưa sẽ tự động gọi, có thể ngăn việc ngọi này bằng thuộc tính `enabled`

```tsx title="tsx"
const { isPending, error, data } = useQuery({
  queryKey: ["repoData"],
  queryFn: () => fetch("https://api.github.com/repos/TanStack/query").then((res) => res.json()),
  enabled: false,
});
```

Và có thể biến nó thành `invalidate` để nó đánh dấu dữ liệu cũ không còn hợp lệ và phải cập
nhật dữ liệu mới.

```tsx title="tsx"
const query = useQuery({ queryKey: ["todos"], queryFn: getTodos });
queryClient.invalidateQueries({ queryKey: ["todos"] });
```

## Mutation

Mutation là dành cho các thao tác có side-effect thường là POST, PUT, PATCH, DELETE, ... mà
sẽ không lưu catche như query, trong khi query chỉ GET và catche dữ liệu, ngoài ra mutation
có thể tác động đến query để chạy.

Đối với những phương thức không phải GET như trên, mà có dữ liệu trả về, thường sẽ không
lưu catche mà chỉ dùng 1 lần để xử lý dữ liệu tạm thời thì ta vẫn dùng mutation.

VD:

```tsx title="tsx"
const mutation = useMutation({
  mutationFn: async ({ username, password }) => {
    const res = await fetch("/api/login", {
      method: "POST",
      body: JSON.stringify({ username, password }),
      headers: { "Content-Type": "application/json" },
    });
    if (!res.ok) throw new Error("Login failed");
    return res.json();
  },
  onSuccess: (data) => {
    // Lưu token / user info vào localStorage hoặc state management
    localStorage.setItem("token", data.token);
    // Có thể invalidate query nếu cần fetch user profile tiếp
    queryClient.invalidateQueries({ queryKey: ["me"] });
  },
});
```
