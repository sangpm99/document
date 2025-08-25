---
sidebar_position: 5
---

# Phông Chữ

Có 2 cách sử dụng font

## Dùng font tĩnh đã tải trong project `next/font/local`

Tải font từ bên ngoài về mục `src/fonts`

```tsx title="src/app/page.tsx"
import localFont from "next/font/local";

const poppins = localFont({
  src: [
    { path: "../fonts/Poppins-Black.ttf", weight: "900", style: "normal" },
    { path: "../fonts/Poppins-BlackItalic.ttf", weight: "900", style: "italic" },
    { path: "../fonts/Poppins-Bold.ttf", weight: "700", style: "normal" },
    // ...
  ],
  variable: "--font-poppins",
  display: "swap",
});

<body className={`${poppins.variable} ${poppins.className} font-sans antialiased`}>
  {children}
</body>;
```

Nếu dùng tailwind

```tsx title="tailwind.config.js"
import type { Config } from "@tailwindcss/react";

const config: Config = {
  content: ["./src/**/*.{js,ts,jsx,tsx,css}"],
  corePlugins: {},
  plugins: [],
  theme: {
    extend: {
      fontFamily: {
        sans: ["var(--font-poppins)", "sans-serif"],
      },
    },
  },
  important: true,
};
```

Nếu dùng Ant Design, tại mục wrapper component của Ant Design

```tsx title="src/components/AntdWrapper.tsx"
<ConfigProvider
  theme={{
    token: {
      fontFamily: "var(--font-poppins, sans-serif)",
    },
  }}
>
  {children}
</ConfigProvider>
```

## Dùng font từ google `next/font/google`

```tsx title="src/app/page.tsx"
import { Geist } from "next/font/google";

const geist = Geist({
  subsets: ["latin"],
});

export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={geist.className}>
      <body>{children}</body>
    </html>
  );
}
```
