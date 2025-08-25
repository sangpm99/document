---
sidebar_position: 3
---

# Khung Và Trang

## Trang (Page)

Để tạo trang chúng ta sẽ tạo trong thư mục `src/app`, ví dụ trang index (trang chủ)

Lúc này khi truy cập địa chỉ có url là: / thì sẽ là trang chủ

Còn đối với những trang khác sẽ có dạng: `src/app/about/page.tsx`,
`src/app/contact/page.tsx`

## Khung (Layout)

Layout là giao diện được chia sẻ giữa nhiều trang, khi chuyển hướng các layout
sẽ được bảo tồn duy trì không render lại.

Layout sẽ nhận 1 prop children có thể là 1 page hoặc 1 layout khác, đối với
layout root phải có html và body.

Layout có thể lồng nhau, các layout con không cần html và body

```tsx title="src/app/layout.tsx"
export default function DashboardLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <body>
        {/* Layout UI */}
        {/* Place children where you want to render a page or nested layout */}
        <main>{children}</main>
      </body>
    </html>
  );
}
```

## Định tuyến lồng nhau (Nesting Routes)

Ví dụ: `app/blog/blog1/page.tsx`

Khi bạn truy cập đường dẫn /blog/blog1 sẽ xuất hiện trang này, trang blog1
sẽ được lồng bởi trang page

## Định tuyến động (Dynamic Routes)

Ví dụ: `app/blog/[slug]/page.tsx`

Khi bạn truy cập đường dẫn /blog/blog1 hay /blog/blog2 đều hướng tới
trang app/blog/[slug]/page.tsx vì [slug] là tham số tuỳ bạn truyền vào,
bạn có thể bắt logic để nó hiển thị ra sao theo tham số truyền vào để
quyết định cái gì sẽ hiển thị.

## Liên kết (Link)

Giống như thẻ a trong html tuy nhiên thì nó sẽ chuyển trang mượt hơn không
bị reload cả trang mà chỉ reload 1 thành phần đó

```tsx title="tsx"
import Link from "next/link";

<Link href="/blogs/blog1">Go to blog1</Link>;
```
