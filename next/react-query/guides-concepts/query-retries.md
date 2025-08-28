---
id: query-retries
title: Query Retries
sidebar_position: 11
---

**Query Retries**

### Tóm tắt

- Khi `useQuery` thất bại, TanStack Query sẽ tự động retry (mặc định **3 lần**).
- Cấu hình:
  - `retry: false` → tắt retry.
  - `retry: n` → thử lại `n` lần.
  - `retry: true` → retry vô hạn.
  - `retry: (failureCount, error) => boolean` → logic tùy chỉnh.

- Trên **server** mặc định `retry = 0` để SSR nhanh.
- Trạng thái lỗi: trong các lần retry, lỗi nằm ở `failureReason`; sau lần cuối, lỗi xuất hiện ở `error`.

### Retry Delay

- Mặc định **exponential backoff**: bắt đầu từ `1000ms`, nhân đôi mỗi lần, tối đa `30s`.
- Có thể override:
  - `retryDelay: fn` → logic tùy chỉnh.
  - `retryDelay: number` → thời gian cố định.

### Tác dụng

- **Tăng độ tin cậy** khi request thất bại do lỗi mạng hoặc tạm thời.
- Cho phép cân bằng giữa **UX mượt mà** (tự retry) và **kiểm soát chặt chẽ** (tắt hoặc giới hạn retry).

👉 Nói ngắn gọn: **Query Retries giúp tự động xử lý lỗi tạm thời bằng retry có giới hạn và delay thông minh, đảm bảo dữ liệu được lấy thành công mà không cần can thiệp thủ công.**
