---
id: disabling-queries
title: Disabling Queries
sidebar_position: 10
---

Disabling Queries cho phép trì hoãn hoặc kiểm soát thủ công việc fetch dữ liệu, thay vì để query tự động chạy.

Kiểm soát khi nào query chạy, tránh fetch khi chưa đủ điều kiện.

Hữu ích cho lazy queries (ví dụ: form lọc, search, trigger thủ công).

Giúp viết code rõ ràng, an toàn với TypeScript nhờ skipToken.

Dùng enabled: false hoặc skipToken để vô hiệu hóa query.

Khi bị disable:

Nếu có cache → query khởi tạo ở success.

Nếu không có cache → status: 'pending', fetchStatus: 'idle'.

Không fetch khi mount, không refetch nền, bỏ qua invalidateQueries.

Có thể gọi thủ công bằng refetch (nhưng không dùng với skipToken).

enabled có thể bật/tắt động → hỗ trợ lazy queries (ví dụ: chỉ chạy khi user nhập filter).

Flag isLoading = isPending && isFetching dùng để hiển thị loading đúng cách khi query ở dạng lazy.
