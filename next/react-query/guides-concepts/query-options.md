---
id: query-options
title: Query Options
sidebar_position: 4
---

- Gom `queryKey` và `queryFn` vào một chỗ.
- Dễ tái sử dụng cùng một query ở nhiều nơi (`useQuery`, `useSuspenseQuery`, `useQueries`, `prefetchQuery`, `setQueryData`, ...).
- Với TypeScript: được type inference + type safety cho tất cả option của query.

[//]: # "Example1"

```ts
import { queryOptions } from "@tanstack/react-query";

function groupOptions(id: number) {
  return queryOptions({
    queryKey: ["groups", id],
    queryFn: () => fetchGroups(id),
    staleTime: 5 * 1000,
  });
}

// usage:

useQuery(groupOptions(1));
useSuspenseQuery(groupOptions(5));
useQueries({
  queries: [groupOptions(1), groupOptions(2)],
});
queryClient.prefetchQuery(groupOptions(23));
queryClient.setQueryData(groupOptions(42).queryKey, newGroups);
```

[//]: # "Example1"

Đối với Infinite Queries, có thể ghi đè các option. Một cách phổ biến và hữu dụng
là tạo mỗi một component select function.

Sử dụng bằng `useInfiniteQuery`, sử dụng trong trường hợp phân trang, tải nhiều lần, scroll, load more, ...

Đối với query bình thường thì việc fetch dữ liệu thì catche sẽ được lấy theo dữ liệu mới,
còn dữ liệu cũ sẽ mất. Đối với `useInfiniteQuery` thì dữ liệu được thêm vào list dữ liệu cũ
không bị mất đi.

[//]: # "Example2"

```ts
// Type inference still works, so query.data will be the return type of select instead of queryFn

const query = useQuery({
  ...groupOptions(1),
  select: (data) => data.groupName,
});
```

[//]: # "Example2"
