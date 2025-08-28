---
id: background-fetching-indicators
title: Background Fetching Indicators
sidebar_position: 8
---

giúp báo hiệu khi query đang refetch nền, cả ở mức component và toàn ứng dụng.

Phân biệt loading lần đầu (status: 'pending') với refetch nền (isFetching).

Cho phép hiển thị trạng thái cập nhật dữ liệu mà không chặn UI.

Có thể hiển thị indicator toàn cục bằng useIsFetching khi bất kỳ query nào đang fetch.
