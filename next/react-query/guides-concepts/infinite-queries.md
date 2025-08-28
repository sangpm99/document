---
id: infinite-queries
title: Infinite Queries
sidebar_position: 13
---

**Infinite Queries**

### Tóm tắt

- Dùng `useInfiniteQuery` để hỗ trợ **infinite scroll** hoặc **Load More**.
- Khác với `useQuery`:
  - `data` có cấu trúc `{ pages, pageParams }`.
  - Có `fetchNextPage`, `fetchPreviousPage`, `hasNextPage`, `hasPreviousPage`.
  - Bắt buộc có `initialPageParam`.
  - Cần định nghĩa `getNextPageParam` / `getPreviousPageParam` để biết khi nào còn dữ liệu.
  - Thêm cờ: `isFetchingNextPage`, `isFetchingPreviousPage`.

- Một query vô hạn chỉ có **1 request đang chạy cùng lúc** → tránh gọi song song (có thể bật `{ cancelRefetch: false }` nếu muốn).
- Khi refetch, **từng trang được gọi tuần tự từ đầu** để đảm bảo không bị trùng / thiếu dữ liệu.
- Tính năng nâng cao:
  - **Bi-directional list** → dùng `getPreviousPageParam` + `fetchPreviousPage`.
  - **Đảo ngược thứ tự trang** → dùng `select`.
  - **Chỉnh sửa thủ công** query data với `queryClient.setQueryData`.
  - **Giới hạn số trang lưu** bằng `maxPages`.
  - Nếu API không có cursor → dùng `pageParam` làm cursor.

### Tác dụng

👉 Giúp xây dựng **infinite scroll / load more UI mượt mà, có kiểm soát, dễ mở rộng** và tối ưu hiệu năng (giữ giới hạn số trang, chỉnh sửa cache linh hoạt).
