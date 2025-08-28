---
id: paginated-queries
title: Paginated Queries
sidebar_position: 12
---

**Paginated / Lagged Queries**

### Tóm tắt

- Phân trang bằng cách thêm **page** (hoặc cursor) vào `queryKey`.
- Vấn đề: mỗi trang được xem như query mới → UI nhảy giữa `success` và `pending`.
- Giải pháp: dùng `placeholderData` (thường là `keepPreviousData`) để:
  - Giữ **dữ liệu trang trước** hiển thị trong khi fetch trang mới.
  - Tự động thay thế khi dữ liệu mới về.
  - Có cờ `isPlaceholderData` để biết dữ liệu hiện tại có phải placeholder không.

- Áp dụng cả với `useInfiniteQuery`.

### Tác dụng

- Tránh **giật UI** khi chuyển trang.
- Giúp phân trang và load vô hạn mượt mà hơn, giữ trải nghiệm liền mạch.

👉 Ngắn gọn: **`placeholderData` giúp UI hiển thị mượt khi phân trang, không nhấp nháy trạng thái loading.**
