---
sidebar_position: 4
---

# src/services/menuServices.ts

## Tổng quan

```tsx title="src/services/menuServices.ts"
import { MenuItem } from "@/types";
import { apiGet } from "@/lib/api";

export class MenuService {
  static async getMenu(locale: string = "en"): Promise<MenuItem[]> {
    try {
      return await apiGet<MenuItem[]>(`/api/menu?locale=${locale}`);
    } catch (err) {
      console.error("MenuService Error:", err);
      return [
        { name: "Home", href: "/" },
        { name: "About Us", href: "/about" },
      ];
    }
  }
}
```

## Chi tiết

### Vì sao dùng class mà không dùng function

Cả class và function đều dùng được. Ưu điểm class:

- Gom nhóm theo domain: `MenuService.getMenu()`
- Dễ mở rộng về sau
- Nếu api nhiều domain thì cách này sẽ giúp có cái nhìn rõ ràng hơn

### Vì sao dùng static cho method

Nếu không dùng static code của bạn sẽ trông như này:

```tsx
const menuService = new MenuService();
await menuService.getMenu();
```

Còn nếu dùng static:

```tsx
await MenuService.getMenu();
```

Có thể thấy cú pháp ngắn gọn hơn nhiều.
