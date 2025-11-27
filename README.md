# Hướng dẫn sắp xếp cấu trúc thư mục

Tài liệu ngắn gọn để bạn dựng khung thư mục rõ ràng, dễ mở rộng, và giúp người mới vào dự án nhìn là hiểu.

## 1) Khung 4 tầng vàng (Domain → Project → Module → File)
```
/Domain (lĩnh vực lớn)
    /Project (dự án cụ thể)
        /Module (chức năng, thành phần chính)
            /File (code, tài liệu, asset)
```
Ví dụ:
- `/Programming/FastAPI-Scholarship-System/{auth,db,models,schemas,routes,services}`
- `/DataScience/{NaiveBayes-Iris,Apriori-MarketBasket,DataWarehouse-Assignment}`
- `/Work/{Reports,Presentations,Research}`

## 2) Nguyên tắc giữ folder luôn sạch
- **Mỗi folder chỉ 1 loại nội dung**: `src`, `tests`, `docs`, `assets`, `outputs`.
- **Tên mô tả rõ ràng**: tránh `temp`, `final-final-v4`; ưu tiên `analysis`, `dataset_cleaned`, `report_2025`, `api_routes`, `frontend_components`.
- **Bộ khung tối thiểu cho project code**: `src`, `tests`, `docs`, `scripts`, `assets`.
- **Bộ khung tối thiểu cho project học tập/báo cáo**: `docs`, `img`, `data_raw`, `data_cleaned`, `output`.
- **Đặt README.md trong mỗi folder lớn** để mô tả nhanh nội dung và quy ước.

## 3) Mô hình 3 tầng trực quan (UI → Logic → Data)
```
/ui        (giao diện, API entrypoint, slide, docs)
    /react-app
    /endpoints.txt
/logic     (business logic, services, domain, analysis)
    /services
    /domain
    /analysis
/data      (database, file, raw data)
    /raw
    /clean
    /models
```
Giúp người mới: nhìn là biết code nào liên quan UI, code nào xử lý, và dữ liệu nằm ở đâu.

## 4) Template theo loại dự án
- **Web (React + Backend)**
  - `/frontend/src/{components,pages,hooks,styles,utils}`
  - `/backend/src/{routes,controllers,services,models,config,utils}`
  - `/database/{schema.sql,migrations/}`
- **Data Science / Machine Learning**
  - `/notebooks`
  - `/src/{data_preprocess,feature_engineering,models,evaluation}`
  - `/data/{raw,processed}`
  - `/reports`, `/results`
- **Học tập / trường học**
  - `/CourseName/{Lectures,Assignments/Assignment1...,Exams,Notes,References}`
- **Workspace cá nhân**
  - `/Workspace/{Coding,University,Research,Blog,Notes,Career}`

## 5) Công cụ giúp nhìn nhanh cấu trúc
- Hiển thị cây thư mục: `tree -L 3`
- VS Code extensions: Project Manager, Explorer Exclude, Bookmarks, TODO Tree.
- Vẽ sơ đồ folder: https://tree.nathanfriend.io/, https://markmap.js.org/, Graphviz (GitHub plugin).

## 6) Quy tắc quản lý & đặt tên phiên bản
- Không để file rác ở root; mọi thứ phải thuộc một folder loại rõ ràng.
- Dùng version rõ: `report_v1`, `report_v2`, `report_final` (tốt hơn: dùng Git).
- Có `CHANGELOG.md` hoặc `NOTES.md` cho dự án đang phát triển.
- Khi lưu dataset hay output: ghi ngày và nguồn trong tên file hoặc README kèm theo.

## 7) Checklist áp dụng nhanh
- [ ] Đã xác định Domain → Project → Module trước khi tạo file.
- [ ] Mỗi folder chỉ chứa một loại nội dung.
- [ ] Có README.md mô tả ở folder gốc và các module lớn.
- [ ] Tên folder/file mang ngữ nghĩa, không dùng `temp/final`.
- [ ] UI/Logic/Data được tách rõ để onboarding nhanh.
- [ ] Có nơi riêng cho asset, docs, scripts, tests.

## 8) Mẹo nâng cao
- Với repo lớn: thêm `docs/architecture.md` mô tả sơ đồ module và data flow.
- Dùng `Explorer Exclude` (VS Code) để ẩn thư mục build/log/venv cho sạch sidebar.
- Với project data: giữ cấu trúc `/data/{raw,clean,processed}` và log quy trình biến đổi ở `docs/data-prep.md`.
- Thường xuyên chạy `tree -L 2` trước khi commit để kiểm tra bố cục và file rác.

## 9) Quy ước đặt tên file/folder
- **Script/backend**: snake_case (`data_loader.py`, `user_service.go`).
- **Frontend**: folder kebab-case (`user-profile`), component PascalCase (`UserCard.tsx`).
- **Docs/asset**: kebab-case (`system-architecture.md`, `landing-hero.png`).
- **Test**: bám theo file nguồn (`user_service_test.py`, `user.service.spec.ts`).

## 10) Quick start cho người mới vào repo
1. Clone repo, đọc `README.md` gốc và `docs/architecture.md` (nếu có).
2. Tạo môi trường: `python -m venv .venv && source .venv/bin/activate` hoặc `npm install`.
3. Đảm bảo khung thư mục tối thiểu (`src`, `tests`, `docs`, `assets`, `scripts`).
4. Chạy lệnh chính: ví dụ `make dev` / `npm run dev` / `python -m src.main`.
5. Chạy kiểm tra: `npm test` hoặc `pytest`, kèm format `npm run lint` / `black` / `gofmt`.

## 11) Gợi ý `.gitignore` nhanh
- **Python**: `.venv/`, `__pycache__/`, `*.pyc`, `.pytest_cache/`, `.mypy_cache/`, `.env`.
- **Node/Frontend**: `node_modules/`, `dist/`, `.next/`, `.turbo/`, `*.log`, `.env*`.
- **Java/Gradle**: `.gradle/`, `build/`, `out/`, `.idea/`, `*.iml`, `*.log`.
- **Data/outputs**: `data/raw/`, `outputs/`, `*.csv` (nếu lớn) → đặt trong `.gitignore` và mô tả ở `data/README.md`.

## 12) Lệnh “kiểm tra sạch” trước commit
- Xem bố cục: `tree -L 2`
- Rà file rác: `find . -maxdepth 2 -type f | sort`
- Quét TODO/FIXME: `rg "TODO|FIXME"`
- Kiểm tra gitignore: `git status --short` (không để file build/log/dataset lọt vào)

## 13) Quản lý dữ liệu & checksum
- Lưu `data/README.md` ghi nguồn, ngày tải, quyền sử dụng.
- Giữ các tầng dữ liệu: `data/raw`, `data/clean`, `data/processed`, `data/models`.
- Ghi checksum cho file lớn: `sha256sum data/raw/file.zip > data/raw/file.sha256`.
- Khi chia sẻ dữ liệu nội bộ, kèm checksum và hướng dẫn giải nén trong `data/README.md`.
