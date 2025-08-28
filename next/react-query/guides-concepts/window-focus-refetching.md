---
id: window-focus-refetching
title: Window Focus Refetching
sidebar_position: 9
---

Cơ chế này tự động làm mới dữ liệu khi app lấy lại focus, đảm bảo người dùng luôn thấy dữ liệu cập nhật.

Đảm bảo dữ liệu luôn mới nhất khi người dùng quay lại ứng dụng.

Giúp giảm rủi ro dùng dữ liệu cũ, tăng tính real-time cho UI.

Linh hoạt: cho phép tắt hoặc override khi muốn kiểm soát hành vi refetch.

Khi user rời app rồi quay lại, nếu dữ liệu query đã stale, TanStack Query sẽ tự động refetch nền.

Có thể tắt bằng refetchOnWindowFocus: false (toàn cục hoặc từng query).

Có thể tùy chỉnh sự kiện focus qua focusManager.setEventListener.

Trên React Native, thay vì window, dùng AppState để quản lý focus.

Có thể can thiệp trực tiếp trạng thái focus bằng focusManager.setFocused.
