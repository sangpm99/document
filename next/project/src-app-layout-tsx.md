---
sidebar_position: 2
---

# src/app/layout.tsx

Layout tổng của project

```tsx title="src/app/layout.tsx"
import "./globals.css";

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return <>{children}</>;
}
```
