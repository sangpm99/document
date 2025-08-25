---
sidebar_position: 2
---

# Tổ Chức Thư Mục

## Thư mục gốc

- app: Ứng dụng định tuyến (nơi viết các page)
- pages: Trang định tuyến (tùy chọn)
- public: Tài nguyên công khai (ảnh, phông chữ, ...)
- src: Các thư mục code tùy chọn

## Các file gốc

- next.config.js: Cấu hình cho Next.js
- package.json: Các phụ thuộc và tập lệnh của dự án
- instrumentation.ts: Tệp OpenTelemetry và Instrumentation
- middleware.ts: Phần mềm trung gian yêu cầu Next.js
- .env: Biến môi trường
- .env.local: Biến môi trường cục bộ
- .env.production: Biến môi trường product
- .env.development: Biến môi trường dev
- .eslintrc.json: Tệp cấu hình cho ESLint
- .gitignore: Git các tập tin và thư mục để bỏ qua
- next-env.d.ts: Tệp khai báo TypeScript cho Next.js
- tsconfig.json: Tệp cấu hình cho TypeScript
- jsconfig.json: Tệp cấu hình cho JavaScript

## File định tuyến

- layout: .js .jsx .tsx Layout
- page: .js .jsx .tsx Page
- loading: .js .jsx .tsx Loading UI
- not-found: .js .jsx .tsx Not found UI
- error: .js .jsx .tsx Error UI
- global-error: .js .jsx .tsx Global error UI
- route: .js .ts API endpoint
- template: .js .jsx .tsx Re-rendered layout
- default: .js .jsx .tsx Parallel route fallback page

## Định tuyến lồng nhau

- folder: Định tuyến phân khúc
- folder/folder: Định tuyến phân khúc lồng nhau

## Định tuyến động

- [folder]: Định tuyến phân khúc động
- [...folder]: Lấy toàn bộ định tuyến phân khúc
- [[...folder]]: Tuỳ chọn lấy toàn bộ định tuyến phân khúc

## Định tuyến nhóm và thư mục riêng tư

- (folder): Nhóm routes không ảnh hưởng đến routing
- \_folder: Thư mục tuỳ chọn và tất cả các phân đoạn con ra khỏi định tuyến

Lưu ý: (folder) sẽ không ảnh hưởng đến slug

VD: `app/(blog)/hello-world/page.tsx` => [https://localhost:3000/hello-world](https://localhost:3000/hello-world)

## Các routes song song và bị chặn

- @folder: Vị trí đặt tên
- (.)folder: Chặn cùng cấp độ
- (..)folder: Chặn 1 cấp độ bên trên
- (..)(..)folder: Chặn 2 cấp độ bên trên
- (...)folder: Chặn từ gốc

## Quy ước tệp metadata

- favicon: Favicon file (.ico)
- icon: App Icon file (.ico .jpg .jpeg .png .svg)
- icon: Generated App Icon (.js .ts .tsx)
- apple-icon: Apple App Icon file (.jpg .jpeg, .png)
- apple-icon: Generated Apple App Icon (.js .ts .tsx)
