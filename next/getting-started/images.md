---
sidebar_position: 4
---

# Ảnh

Next cung cấp thẻ `<Image>` nâng cao của thẻ `<img>` với nhiều tính năng hơn

```tsx title="tsx"
import Image from "next/image";

export default function Page() {
  return <Image src="/logo.svg" alt="Logo" width={86} height={46}></Image>;
}
```

Lưu ý:

- Thẻ Image nếu là ảnh **local** thì cần **width** và **height**, nếu không thì
  dùng `fill`. `fill` sẽ có position là absolute nên cần 1 phần tử cha là relative
  và có width height rõ ràng.
- Nếu là ảnh url thì không cần width height.
- Mặc định sẽ tối ưu ảnh (mờ) để tắt sử dụng thuộc tính `unoptimized`.
- alt giúp SEO tốt hơn.

## Ảnh có đầy đủ width height

```tsx title="tsx"
<Image src="/logo.svg" alt="Logo" width={86} height={46}></Image>
```

## Ảnh có width còn height tự động

```tsx title="tsx"
<Image
  src="/images/pages/auth-v2-login-illustration-light.png"
  alt="Login Background"
  width={0}
  height={0}
  sizes="100vw"
  style={{ width: "800px", height: "auto" }}
></Image>
```
