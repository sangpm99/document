---
id: initial-query-data
title: Initial Query Data
sidebar_position: 14
---

**Initial Query Data**

### Tóm tắt

Có nhiều cách để cung cấp dữ liệu ban đầu cho query:

- **Declarative**: dùng `initialData`.
- **Imperative**: `queryClient.prefetchQuery` hoặc `queryClient.setQueryData`.

### Các cách dùng `initialData`

1. **Truyền trực tiếp dữ liệu** → bỏ qua trạng thái loading ban đầu.

- ⚠️ Không nên truyền data giả/không đầy đủ (nên dùng `placeholderData` cho case này).

2. **Kết hợp với `staleTime` và `initialDataUpdatedAt`**:

- Mặc định `initialData` được coi là mới → nếu `staleTime=0` sẽ refetch ngay khi mount.
- Có thể đặt `staleTime` để kiểm soát thời gian data được coi là fresh.
- Nếu data cũ, dùng `initialDataUpdatedAt` (timestamp) để query biết chính xác lúc nào nên refetch.

3. **Dùng function** → `initialData: () => ...` chỉ chạy một lần khi query init → tiết kiệm CPU.

4. **Lấy từ cache query khác**:

- Ví dụ: lấy 1 `todo` từ cache của `['todos']` làm initial data cho `['todo', id]`.
- Khi lấy từ cache, nên truyền thêm `initialDataUpdatedAt` từ source query để refetch hợp lý.
- Có thể conditionally kiểm tra freshness bằng `queryClient.getQueryState` trước khi quyết định dùng cache hay fetch mới.

### Tác dụng

👉 Giúp hiển thị UI ngay lập tức mà không bị flash trạng thái loading, đồng thời linh hoạt kiểm soát độ “fresh” của dữ liệu để tránh refetch không cần thiết.
