---
id: dependent-queries
title: Dependent Queries
sidebar_position: 7
---

đảm bảo các query phụ thuộc dữ liệu chạy đúng thời điểm, không chạy thừa khi chưa có input.

Điều khiển thứ tự query: query B chỉ chạy khi query A có dữ liệu.

Tránh gọi API khi chưa đủ điều kiện (nhờ enabled).

Cho phép tạo query động phụ thuộc dữ liệu trước (dùng useQueries).
