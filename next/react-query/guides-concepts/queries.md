---
sidebar_position: 1
---

# Queries

- Query là một dependency khai báo (declarative dependency) tới một nguồn dữ liệu bất đồng bộ.
- Query được xác định bằng một unique key (`queryKey`) và một query function (`queryFn`)
  trả về Promise.
- Dùng query để fetch data từ server (GET, POST,...).
- Nếu thao tác thay đổi dữ liệu (insert, update, delete), nên dùng Mutation thay vì Query.

```ts title="App.tsx"
import { useQuery } from "@tanstack/react-query";

function App() {
  const info = useQuery({
    queryKey: ["todos"], // unique key
    queryFn: fetchTodoList, // hàm fetch dữ liệu (Promise)
  });
}
```
