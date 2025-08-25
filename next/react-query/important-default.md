---
sidebar_position: 3
---

# Cấu hình mặc định quan trọng

`useQuery` hoặc `useInfiniteQuery` thì dữ liệu mặc định được coi là stale (dữ liệu cũ) ngay cả
khi mới fetch xong, chính nhờ vậy mà nó có thể tự lấy dữ liệu mới khi mở tab mới, focus
lại cửa sổ, kết nối mạng trở lại, ...

Muốn giữ lại dữ liệu lâu hơn dùng `staleTime`:

- `staleTime`: 2 \* 60 \* 1000 → dữ liệu coi như **fresh** 2 phút.
- `staleTime`: Infinity → dữ liệu luôn **fresh** cho đến khi bạn tự `invalidateQuery`.
- `staleTime`: 'static' → dữ liệu luôn **fresh**, kể cả khi invalidate cũng không refetch.

Thông thường staleTime mặc định là 0 nhưng sẽ không fetch liên tục mà chỉ rơi vào 3 trường
hợp (mở tab mới, focus lại cửa sổ, kết nối mạng trở lại).

Ngoài ra có thể cài `refetchInterval` để tự động chạy lại.

Các thiết lập staleTime được khuyến nghị để tránh gọi lại quá nhiều, tuy nhiên cũng có
thể tùy chỉnh các thiết lập này bằng: `refetchOnMount`, `refetchOnWindowFocus`,
`refetchOnReconnect`.

Nếu không có component nào dùng query hoặc unMount hết thì query sẽ thành **inactive**
nhưng dữ liệu vẫn lưu trong catche trong thời gian mặc định là 5 phút, có thể tùy
chỉnh thời gian này bằng gcTime (5 \* 60 \* 1000).

Query thất bại sẽ được retry tối đa 3 lần, với thời gian chờ theo cấp số nhân,
có thể thay đổi bằng `retry`: number | false, `retryDelay`: function.

React Query sẽ so sánh dữ liệu cũ và mới theo cấu trúc, nếu không thay đổi
giữ nguyên, hữu ích khi dùng `useMemo` và `useCallback`. Chỉ hoạt động tốt với
dữ liệu JSON-compatible, nếu dữ liệu phi JSON có thể tắt tính năng này. Nhưng
gần như chẳng bao giờ cần phải tắt, vì các dữ liệu fetch luôn có dạng JSON.

```tsx title="tsx"
config: {
  structuralSharing: false;
}
```
