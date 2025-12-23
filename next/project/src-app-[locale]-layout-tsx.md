---
sidebar_position: 3
---

# src/app/[locale]/layout.tsx

## Tổng quan

```tsx title="src/app/[locale]/layout.tsx"
import pick from "lodash/pick";
import { hasLocale, NextIntlClientProvider } from "next-intl";
import { getMessages } from "next-intl/server";
import { routing } from "@/i18n/routing";
import { notFound } from "next/navigation";
import Header from "@/components/Header/Header";
import Footer from "@/components/Footer/Footer";
import { MenuService } from "@/services/menuServices";
import { MenuItem } from "@/types";

type Props = {
  children: React.ReactNode;
  params: Promise<{ locale: string }>;
};
export default async function LocaleLayout({ children, params }: Props) {
  const { locale } = await params;
  const messages = await getMessages({ locale });

  if (!hasLocale(routing.locales, locale)) {
    notFound();
  }

  const menu: MenuItem[] = await MenuService.getMenu(locale);

  return (
    <html lang={locale}>
      <body className="flex flex-col min-h-screen text-gray-900 bg-gray-50">
        <NextIntlClientProvider locale={locale} messages={pick(messages, ["Error", "Header"])}>
          <Header locale={locale} menu={menu}></Header>
          <main className="flex-1 mx-0 mt-0">{children}</main>
          <Footer></Footer>
        </NextIntlClientProvider>
      </body>
    </html>
  );
}
```

## Chi tiết

### lodash

`import pick from "lodash/pick";`

`pick` dùng để lấy ra một số thuộc tính trong 1 object để tạo ra 1 object mới.

Vì khi truyền object cho các component đôi khi dữ liệu gốc khá lớn nên có thể chọn lọc một số
thuộc tính cần thiết để giảm thiểu độ trễ khi tải trang.

Ví dụ trong project này có chứa các bản dịch của `locale` nên dữ liệu là khá lớn.

### next-intl

`import { hasLocale, NextIntlClientProvider } from "next-intl";`

`NextIntlClientProvider` cung cấp translation + locale cho cả app. Vì client không lấy được
bản dịch từ server nên `NextIntlClientProvider` sẽ lấy dữ liệu từ server rồi truyền cho các
component.

`locale` được lấy từ param (Next route)

`messages` được lấy từ locale và chỉ lấy những bản dịch cần thiết để truyền cho các component.

`import { routing } from "@/i18n/routing";`

`import { notFound } from "next/navigation";`
