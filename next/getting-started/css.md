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
