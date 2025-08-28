---
sidebar_position: 1
---

# Queries

## Query cơ bản

- Query là một dependency khai báo (declarative dependency) tới một nguồn dữ liệu
  bất đồng bộ.
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

`useQuery` tại một thời điểm sẽ trả về 1 trong 3 giá trị:

- `isPending` hoặc `status === 'pending'`: Query chưa có dữ liệu.
- `isError` hoặc `status === 'error'`: Query gặp phải lỗi.
- `isSuccess` hoặc `status === 'success'`: Query đã thành công và dữ liệu khả dụng.

Hay nói cách khác: `{'pending' | 'error' | 'success'} = status`, do đó có thể
lược bỏ đi `isPending, isError, isSuccess` nếu cần.

### `fetchStatus`

Ngoài trường status thì chúng ta có thể lấy thêm thuộc tính `fetchStatus` cùng
với các tùy chọn sau.

- `fetchStatus === 'fetching'`: Query đang lấy dữ liệu
- `fetchStatus === 'fause'`: Query muốn lấy dữ liệu, nhưng nó đang tạm dừng
  [Xem thêm chi tiết tại đây](https://tanstack.com/query/latest/docs/framework/react/guides/network-mode).
- `fetchStatus === 'idle'`: Query đang không thực thi

### Tại sao 2 state khác nhau?

Có 2 trạng thái cùng tồn tại là `status` và `fetchStatus`.

- `status`: Trạng thái **dữ liệu**.
- `fetchStatus`: Trạng **hàm fetch**.

Do cơ chế **background refetch** và **stale-while-revalidate** nên một query có thể
đồng thời ở nhiều tình huống.

| **status** | **fetchStatus** | Ý nghĩa                                                                 |
| ---------- | --------------- | ----------------------------------------------------------------------- |
| `pending`  | `fetching`      | Query mới mount, chưa có data, đang fetch lần đầu.                      |
| `pending`  | `paused`        | Query mới mount, chưa có data, muốn fetch nhưng bị tạm dừng (offline).  |
| `pending`  | `idle`          | Ít gặp. Query chưa có data, chưa chạy fetch (ví dụ `enabled: false`).   |
| `success`  | `idle`          | Đã có data hợp lệ, không fetch thêm. Trạng thái phổ biến nhất.          |
| `success`  | `fetching`      | Đã có data, nhưng đang refetch nền để làm mới (stale-while-revalidate). |
| `success`  | `paused`        | Đã có data, muốn refetch nhưng bị tạm dừng (offline).                   |
| `error`    | `idle`          | Query fetch thất bại, không retry thêm.                                 |
| `error`    | `fetching`      | Query gặp lỗi và đang retry lại.                                        |
| `error`    | `paused`        | Query gặp lỗi, muốn retry nhưng bị tạm dừng (offline).                  |
