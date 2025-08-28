---
id: query-keys
title: Query Keys
sidebar_position: 2
---

# Query Keys

- React Query quản lý cache dựa trên các khóa.
- Khóa có thể là mảng chuỗi hoặc đối tượng lồng nhau.
- Các khóa này phải thuộc dạng có thể `JSON.stringify`.
- Các khóa yêu cầu phải là duy nhất không trùng lặp.

## Query Keys Đơn giản

Các kiểu key đơn giản nhất là mảng chứa giá trị hằng số (string, number).

- Danh sách chung, index cơ bản.
- Không phân tầng, không phụ thuộc tham số.

[//]: # "Example"

```tsx title="tsx"
useQuery({ queryKey: ['todos'], ... })

useQuery({ queryKey: ['something', 'special'], ... })
```

[//]: # "Example"

## Mảng Keys Cùng Với Biến

khi dữ liệu cần mô tả chi tiết hơn để tránh cache trùng nhau, bạn dùng
queryKey dạng mảng có biến số (variables), gồm string + giá trị động
(id, object tham số).

- Tài nguyên phân cấp hoặc có quan hệ cha–con.
- Cần phân biệt từng item.
- Queries có tham số bổ sung: filter, sort, paging, option.

[//]: # "Example2"

```tsx title="tsx"
// An individual todo
useQuery({ queryKey: ['todo', 5], ... })

// An individual todo in a "preview" format
useQuery({ queryKey: ['todo', 5, { preview: true }], ...})

// A list of todos that are "done"
useQuery({ queryKey: ['todos', { type: 'done' }], ... })
```

[//]: # "Example2"

## Query Keys Được Băm Một Cách Xác Định

### Đối với Object

- Thứ tự thuộc tính trong object không quan trọng.
- `JSON.stringify({ status, page })` và `JSON.stringify({ page, status })` coi là giống nhau.
- Thuộc tính `undefined` cũng bị bỏ qua.

VD: Trong trường hợp dưới đây được cả 3 được coi là 1 key, catche được chia sẻ.

[//]: # "Example3"

```tsx title="tsx"
useQuery({ queryKey: ['todos', { status, page }], ... })
useQuery({ queryKey: ['todos', { page, status }], ...})
useQuery({ queryKey: ['todos', { page, status, other: undefined }], ... })
```

[//]: # "Example3"

### Đối với mảng

- Thứ tự phần tử quan trọng.
- `[ 'todos', status, page ]` khác `[ 'todos', page, status ]`.
- Thêm phần tử undefined cũng khác.

[//]: # "Example4"

```tsx title="tsx"
useQuery({ queryKey: ['todos', status, page], ... })
useQuery({ queryKey: ['todos', page, status], ...})
useQuery({ queryKey: ['todos', undefined, page, status], ...})
```

[//]: # "Example4"

## Nếu như hàm query phụ thuộc vào biến, hãy cho biến đó vào query key

Khi biến thay đổi, fetch sẽ được gọi là tự động.

[//]: # "Example5"

```tsx title="tsx"
function Todos({ todoId }) {
  const result = useQuery({
    queryKey: ["todos", todoId],
    queryFn: () => fetchTodoById(todoId),
  });
}
```

[//]: # "Example5"
