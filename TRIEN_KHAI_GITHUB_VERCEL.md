# Triển khai GitHub + Vercel + CMS mini

Website đã được chuyển sang mô hình:

- `content/site.json`: thông tin chung, trang chủ, giới thiệu, liên hệ.
- `content/projects.json`: toàn bộ danh sách và nội dung chi tiết dự án.
- `scripts/build.js`: sinh lại HTML tĩnh từ dữ liệu JSON.
- `admin/`: giao diện quản trị nội dung.
- `api/`: Vercel Functions để lưu thay đổi bằng cách commit về GitHub.

## 1. Đưa mã nguồn lên GitHub

Tạo một repository mới trên GitHub, ví dụ:

```bash
git init
git add .
git commit -m "Initial CMS site"
git branch -M main
git remote add origin https://github.com/<OWNER>/<REPO>.git
git push -u origin main
```

Nếu máy hiện tại chưa có Git, có thể cài Git rồi chạy các lệnh trên, hoặc upload toàn bộ thư mục lên repository GitHub bằng giao diện web.

## 2. Tạo GitHub token cho CMS

Tạo token GitHub có quyền ghi nội dung repository:

- Repository access: chỉ chọn repository của website.
- Permissions: `Contents` → `Read and write`.

Không đưa token này vào JavaScript, HTML hoặc GitHub public file. Token chỉ đặt trong biến môi trường của Vercel.

## 3. Kết nối Vercel

Trong Vercel:

- Import repository GitHub của website.
- Framework Preset: `Other`.
- Build Command: `node scripts/build.js`.
- Output Directory: `.`.

Thêm Environment Variables:

```text
ADMIN_PASSWORD=<mật khẩu đăng nhập /admin>
GITHUB_TOKEN=<token GitHub có quyền Contents read/write>
GITHUB_OWNER=<tên GitHub owner hoặc organization>
GITHUB_REPO=<tên repository>
GITHUB_BRANCH=main
```

Deploy lần đầu. Sau khi deploy xong:

- Website chính: `https://ten-du-an.vercel.app`
- Trang quản trị: `https://ten-du-an.vercel.app/admin`

## 4. Quy trình cập nhật nội dung

1. Vào `/admin`.
2. Nhập mật khẩu `ADMIN_PASSWORD`.
3. Sửa thông tin chung, trang chủ, liên hệ hoặc từng dự án.
4. Bấm `Lưu & xuất bản`.
5. API Vercel commit thay đổi vào `content/site.json`, `content/projects.json` và ảnh mới nếu có.
6. GitHub nhận commit mới.
7. Vercel tự build lại bằng `scripts/build.js` và xuất bản HTML mới.

## 5. Lưu ý ảnh

Ảnh upload từ admin sẽ được ghi vào `assets/img/`.

Khuyến nghị:

- Dùng ảnh `.jpg`, `.png`, `.webp`.
- Nén ảnh dưới 4 MB trước khi upload.
- Ảnh quá lớn có thể vượt giới hạn body của Vercel Function.

## 6. Kiểm tra local

Sau khi sửa trực tiếp JSON ở máy local:

```bash
node scripts/build.js
```

Lệnh này sinh lại toàn bộ HTML từ `content/*.json`.
