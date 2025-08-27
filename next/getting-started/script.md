---
sidebar_position: 7
---

# Script

Bạn muốn nhúng một đoạn JavaScript bên ngoài (CDN) — ví dụ như
Google Analytics, chatbot, v.v… — và nó cần hoạt động trên nhiều trang (multiple routes).

```tsx title="tsx"
import Script from "next/script";

export default function DashboardLayout({ children }: { children: React.ReactNode }) {
  return (
    <>
      <section>{children}</section>
      <Script src="https://example.com/script.js" />
    </>
  );
}
```

Script từ next/script đảm bảo script được:

- Tải chỉ 1 lần duy nhất.
- Tự động tải khi người dùng vào route có layout này.
- Không tải lại nếu người dùng chuyển giữa các route con trong cùng layout.

## Strategy

Thuộc tính strategy giúp bạn kiểm soát khi nào script được tải và thực thi.

### `beforeInteractive`

Tải script ngay lập tức, trước cả khi Next.js bắt đầu chạy.

Không chờ React hydrate (khởi tạo).

Dùng khi script rất quan trọng và cần chạy ngay lập tức (ví dụ:
polyfill, tag manager, A/B testing).

```tsx title="tsx"
import Script from "next/script";

<Script src="..." strategy="beforeInteractive" />;
```

### `afterInteractive`

Tải ngay sau khi trang bắt đầu hydrate (React bắt đầu hoạt động).

Phù hợp với đa số trường hợp: analytics, chatbot, pixel, ...

```tsx title="tsx"
import Script from "next/script";

<Script src="..." />; // hoặc strategy="afterInteractive"
```

### `lazyOnload`

Tải khi trình duyệt rảnh (idle), sau khi tải xong trang.

Ưu tiên hiệu năng (performance), nhưng script chạy chậm hơn.

Dùng cho script ít quan trọng, hoặc chỉ phục vụ tracking phụ.

```tsx title="tsx"
import Script from "next/script";
<Script src="..." strategy="lazyOnload" />;
```

## Inline Script

Là các đoạn JavaScript viết trực tiếp trong HTML thay vì được tải từ file bên ngoài.

C1: Dùng dấu { } trực tiếp

```tsx title="tsx"
<Script id="show-banner">{`document.getElementById('banner').classList.remove('hidden')`}</Script>
```

C2: dangerouslySetInnerHTML

```tsx title="tsx"
<Script
  id="show-banner"
  dangerouslySetInnerHTML={{
    __html: `document.getElementById('banner').classList.remove('hidden')`,
  }}
/>
```

Lưu ý bảo mật: `dangerouslySetInnerHTML` là một cách để chèn code có thể nguy
hiểm nếu không kiểm soát nội dung. Bắt buộc phải có id.
Nên sử dụng khi cần nhúng script từ bên thứ 3 (ví dụ: Google Analytics,
Facebook Pixel, Chat Widget...) hoặc chạy 1 lần duy nhất.

## Self Host
