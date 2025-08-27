---
sidebar_position: 6
---

# CSS

Thứ tự import file css sẽ quyết định cái nào được áp dụng trước,
nếu trùng nhau thì cái sau sẽ thay thế cái trước nếu mức độ ưu tiên của chúng bằng nhau.

## CSS Module

Là các file css có đuôi `.module.css`, cú pháp vẫn giống như css.

```tsx title="src/app/blog/page.tsx"
import styles from "./blog.module.css";

export default function Page() {
  return <main className={styles.blog}></main>;
}
```

## Global CSS

Là các file css có đuôi .module.css, cú pháp vẫn giống như css.

Cách import: dùng object styles

```tsx title="src/app/blog/page.tsx"
import styles from "./blog.module.css";

export default function Page() {
  return <main className={styles.blog}></main>;
}
```

## External Stylesheets

Có thể sử dụng các file css đóng gói

```tsx title="src/app/blog/page.tsx"
import "bootstrap/dist/css/bootstrap.css";
```

## SASS

```terminaloutput
npm install --save-dev sass
```

Bạn có thể cấu hình các tùy chọn cho Sass bằng cách thêm sassOptions vào
trong file `next.config.ts`

```tsx title="next.config.ts"
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
  sassOptions: {
    additionalData: `$var: red;`, // Tự động chèn biến vào mọi file SCSS
  },
};

export default nextConfig;
```

Mỗi file SCSS khi được biên dịch sẽ tự động được thêm nội dung này ở đầu.
Ví dụ, mọi file đều có sẵn biến `$var: red;` mà không cần import thủ công.

Mặc định Next.js dùng package sass (node-sass).

Bạn có thể chỉ định rõ muốn dùng một phiên bản khác như `sass-embedded`.

```tsx title="next.config.ts"
const nextConfig: NextConfig = {
  sassOptions: {
    implementation: "sass-embedded", // Dùng trình biên dịch khác
  },
};
```

Tạo biến trong từng file:

```scss title="scss"
$primary-color: #64ff00;

:export {
  primaryColor: $primary-color;
}
```

Import

```tsx title="tsx"
import variables from "./variables.module.scss";

export default function Page() {
  return <h1 style={{ color: variables.primaryColor }}>Hello, Next.js!</h1>;
}
```
