---
sidebar_position: 1
---

# Query Client

Query Client dùng để tương tác với cache.

```tsx title="tsx"
import { QueryClient } from "@tanstack/react-query";

const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: Infinity,
    },
  },
});

await queryClient.prefetchQuery({ queryKey: ["posts"], queryFn: fetchPosts });
```

## fetchQuery

`queryClient.fetchQuery` là hàm bất đồng bộ dùng để fetch và cache dữ liệu thủ công,
thường dùng ngoài component hoặc hook.

Sẽ trả về 1 promise. Nhưng khác với `useQuery` nó không lưu state, nó chỉ fetch 1 lần.
Nếu dữ liệu đã có trong cache và còn hợp lệ theo `staleTime`, thì dùng ngay dữ liệu cache,
không fetch lại.

VD: Fetch dữ liệu trực tiếp

```tsx title="tsx"
try {
  const data = await queryClient.fetchQuery({ queryKey, queryFn });
} catch (error) {
  console.log(error);
}
```

VD: Fetch dữ liệu với staleTime

```tsx title="tsx"
try {
  const data = await queryClient.fetchQuery({
    queryKey,
    queryFn,
    staleTime: 10000,
  });
} catch (error) {
  console.log(error);
}
```
