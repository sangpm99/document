---
id: network-mode
title: Network Mode
sidebar_position: 5
---

# Network Mode

React Query cung cấp 3 chế độ network để quyết định cách **Query** và **Mutation** hoạt động
khi không có kết nối mạng.

Mặc định là `online`.

## Network Mode: online

- Không fetch nếu mất mạng.
- Giữ nguyên `state` hiện tại (`pending`, `error`, `success`).
- Có thêm `fetchStatus`:
  - `fetching`: đang request.
  - `pause`: bị tạm dừng do mất mạng.
  - `idle`: không fetch và không pause.
- Khi online lại, query tiếp tục từ chỗ dừng (không phải refetch).
