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

Chỉ chạy khi có mạng, nếu không có mạng sẽ không gọi queryFn.

Nếu chẳng may mất mạng, query sẽ giữ nguyên state hiện tại (`pending`, `error`, `success`)
mà không chuyển sang
thành công hay lỗi gì cả, VD: pending → pending (không thay đổi).

Để biết thêm tình trạng, query có thêm biến phụ là `fetchStatus`:

- `fetching`: `queryFn` thực sự đang chạy, request đang được gửi.
- `pause`: Query lẽ ra đang phải chạy nhưng bị tạm dừng do không có mạng.
- `idle`: Query không chạy, cũng không bị pause.

Các cờ isFetching và isPaused chỉ là dạng boolean rút gọn từ fetchStatus.

Nếu chỉ check state: 'pending' để hiển thị loading → có thể sai.

Ví dụ: query mount lần đầu, nhưng không có mạng. Lúc này state = 'pending',
nhưng thực tế nó đang paused → không có request nào được gửi.
Vì vậy cần check thêm fetchStatus.

Nếu query đã bắt đầu chạy nhưng lúc fetch thì mất mạng:

- `retry` sẽ tạm dừng
- Khi có mạng sẽ tiếp tục từ chỗ dừng (không phải từ đầu).
- Nếu trong lúc chờ, query bị hủy thì nó sẽ không tiếp tục nữa.

`refetchOnReconnect = true` nghĩa là khi online lại thì sẽ tự refetch. Nhưng ở đây khác,
query đang dở thì tiếp tục chứ không refetch mới. Hai cơ chế độc lập.

VD:

```tsx title="tsx"
import { useQuery } from "@tanstack/react-query";

const login = async () => {
  const res = await fetch("https://api.com/Authorize/SignIn", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      email: "test@gmail.com",
      password: "password",
      rememberMe: true,
      reCaptcha: "string",
    }),
  });

  return res.json();
};

export default function Home() {
  const { data, error, status, fetchStatus, isFetching, isPaused } = useQuery({
    queryKey: ["signIn"],
    queryFn: login,
    refetchOnWindowFocus: false,
    refetchOnReconnect: true,
    retry: 3,
    networkMode: "online",
  });

  return (
    <div className="p-20">
      <p>status: {status}</p>
      <p>fetchStatus: {fetchStatus}</p>
      <p>isFetching: {isFetching.toString()}</p>
      <p>isPaused: {isPaused.toString()}</p>
      <p>error: {error?.message}</p>
      <p>data: {JSON.stringify(data)}</p>
    </div>
  );
}
```

|             | Khi fetch | Khi mất mạng    | khi có mạng trở lại |
| ----------- | --------- | --------------- | ------------------- |
| status      | pending   | error           |                     |
| fetchStatus | fetching  | idle            |                     |
| isFetching  | true      | false           |                     |
| isPaused    | false     | false           |                     |
| error       | null      | Failed to fetch |                     |
| data        | null      | null            |                     |

## Network Mode: always

- Luôn chạy queryFn, bỏ qua trạng thái online/offline.
- Không bao giờ bị paused.
- Nếu fail thì vào error, retries không pause.
- `refetchOnReconnect` mặc định = false (vì reconnect không còn ý nghĩa).

Thích hợp khi queryFn không cần mạng (VD: đọc từ `AsyncStorage`, hoặc trả về giá trị cứng).

## Network Mode: offline

- Hiển thị query paused nếu mất mạng.
- Có nút mô phỏng offline (chỉ thay đổi OnlineManager, không can thiệp thật vào kết nối mạng).

## Devtools

- Hiển thị query paused nếu mất mạng.
- Có nút mô phỏng offline (chỉ thay đổi OnlineManager, không can thiệp thật vào kết nối mạng).

## Signature

```tsx title="tsx"
networkMode: "online" | "always" | "offlineFirst"; // mặc định 'online'
```
