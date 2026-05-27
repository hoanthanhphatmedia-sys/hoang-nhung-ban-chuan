# Hướng dẫn sử dụng & chỉnh sửa website — Hồng Nhung BĐS

> Cập nhật mới: dự án đã có CMS mini cho GitHub + Vercel. Ưu tiên chỉnh sửa nội dung tại `/admin`, dữ liệu nằm trong `content/site.json` và `content/projects.json`, sau đó chạy `node scripts/build.js` hoặc để Vercel tự build khi CMS commit lên GitHub. Xem chi tiết trong `TRIEN_KHAI_GITHUB_VERCEL.md`.

Website tĩnh viết bằng **HTML + CSS + JavaScript thuần**. Mở `index.html` là chạy. Đưa lên Internet xem **mục G**.

---

## A. Cấu trúc thư mục

```
web chị nhung/
├── index.html        — Trang chủ (video nền, BĐS nổi bật trượt ngang, giới thiệu, 15 cảm nhận xoay vòng)
├── about.html        — Trang giới thiệu chi tiết (câu chuyện 4 năm + khối số liệu)
├── listings.html     — Trang danh mục BĐS (21 mục, lọc theo loại hình & ô tìm kiếm)
├── contact.html      — Trang liên hệ (form + thông tin liên hệ)
├── HUONG_DAN.md      — File hướng dẫn này
├── du-an/            — 21 trang chi tiết từng dự án + _template.html
│   ├── sunshine-legend-city-canho.html
│   ├── biet-thu-vinhomes-ocean-city.html
│   ├── ... (tổng 21 file)
│   └── _template.html   — file mẫu để chị nhân bản thêm dự án mới
└── assets/
    ├── css/style.css   — Màu sắc, font, bố cục, carousel, responsive mobile
    ├── js/script.js    — Header cuộn, dropdown, menu mobile, dữ liệu 21 BĐS, slider testimonials
    ├── video/hero.mp4  — Video nền đầu Trang chủ
    └── img/            — 14 ảnh dự án + chân dung + 2 file logo
```

---

## B. Thanh menu (header) — bố cục 3 phần

Header trong suốt khi ở đầu trang, cuộn xuống thì chuyển nền navy. Hoạt động giống nhau trên tất cả các trang (kể cả 21 trang chi tiết dự án):

- **Bên trái — Menu chính:** Giới thiệu · Bất động sản · Liên hệ.
- **Chính giữa — Logo:** logo Hồng Nhung BĐS (bấm về Trang chủ).
- **Bên phải — Menu phụ "Loại hình BĐS":** dropdown 6 loại — Căn hộ, Biệt thự, Nhà phố, Đất nền, Chuyển nhượng BĐS, BĐS thương mại. Bấm vào loại nào sẽ mở trang Bất động sản và **tự lọc sẵn**. Cạnh đó là nút **Đặt lịch hẹn**.
- Trên điện thoại: menu thu vào nút **☰**.

---

## C. Hai khối trượt ngang trên Trang chủ

### C.1 — "Bất động sản nổi bật" (trượt ngang bị động)
6 card sản phẩm tiêu biểu trượt liên tục từ phải sang trái — không cần thao tác. Đưa chuột vào thì dừng để người xem đọc kỹ. Sửa danh sách 6 card này trong `index.html`, khối `<div class="marquee-track">` (nhớ chỉnh **cả hai** bản — bản gốc + bản nhân đôi để vòng lặp liền mạch).

### C.2 — "Khách hàng nói gì" (trượt ngang chủ động, 3 giây/lần)
15 cảm nhận tự động đổi mỗi 3 giây, có chấm điều hướng phía dưới, hover dừng tự động, trên điện thoại **vuốt ngang** để chuyển. Sửa cảm nhận trong `index.html` khối `<div class="testi-track">`.

---

## D. ẢNH, VIDEO & LOGO

**14 ảnh + 2 logo đã có sẵn trong `assets/img/`.** Ảnh nặng (29 MB, 7 MB) đã được nén xuống dưới 600 KB. Danh sách chi tiết xem `assets/img/_DOC_TRUOC_KHI_THEM_ANH.txt`.

Quy tắc khi thay/thêm ảnh: tên file viết thường, không dấu, không cách, đuôi `.jpg`. Ghi đè file cùng tên là ảnh trên web tự đổi.

Video nền: `assets/video/hero.mp4` (video chị đang dùng là 720×720 vuông — để nền hero đẹp hơn nên thay bằng video ngang 16:9).

Logo: `assets/img/logo.png` (trắng nền trong suốt). Muốn thay: ghi đè file cùng tên, chỉnh kích thước ở `assets/css/style.css` → `.logo-center img { height: ... }`.

---

## E. Đổi màu chủ đạo

Trong `assets/css/style.css`, khối `:root` đầu file:

```css
--bg:#0d1b2a;          /* nền tối */
--paper:#f8f6f1;       /* nền sáng */
--gold:#c8a14e;        /* vàng gold nhấn */
--gold-soft:#e3c882;   /* vàng gold nhạt */
```

---

## F. Cho form Liên hệ gửi được email

`contact.html` đang dùng form mẫu. Đăng ký formspree.io, thay `your-id-here` trong `<form action="...">` bằng mã của chị.

---

## G. Đưa website lên Internet

- **Netlify Drop** (nhanh nhất): kéo-thả nguyên thư mục vào app.netlify.com/drop.
- **Vercel / GitHub Pages**: phù hợp khi gắn tên miền riêng.

Khi deploy, **giữ nguyên cấu trúc thư mục `du-an/`** để các trang chi tiết hoạt động.

---

## H. Tối ưu hiển thị Android / màn nhỏ

Toàn bộ trang đã có breakpoint cho màn ≤680 px: hero ngắn lại, h1/h2/h3 nhỏ hơn, padding gọn 16 px, listing 1 cột, testimonial trượt 1 thẻ/lần, card marquee thu nhỏ 268 px. Logo ở header tự thu xuống ~44 px trên điện thoại.

Nếu chị thấy chỗ nào còn vỡ trên điện thoại, mở `assets/css/style.css` cuộn xuống cuối — phần `@media (max-width:680px)` chứa tất cả rule mobile, sửa hoặc thêm rule mới ở đó.

---

## I. TRANG CHI TIẾT DỰ ÁN (`du-an/`) — quan trọng

### I.1 — Đã có sẵn 21 trang

Mỗi mục trong "Bất động sản" có 1 trang chi tiết riêng trong `du-an/`. Khi khách bấm vào một thẻ ở trang chủ hoặc trang Bất động sản, sẽ tự mở đúng trang chi tiết tương ứng.

Mỗi trang gồm: hero ảnh dự án + tên + loại hình → bảng thông số (loại, vị trí, diện tích, PN, WC, giá) → 3 mục mô tả (Tổng quan / Tiện ích / Pháp lý) → khối CTA gọi/Zalo/gửi yêu cầu → footer.

### I.2 — Sửa nội dung 1 trang dự án

Mở file `du-an/<slug>.html` (ví dụ `du-an/sunshine-legend-city-canho.html`) bằng Notepad/VS Code, sửa các đoạn chữ trong các thẻ `<p>`, `<h2>`, `<li>`. Lưu lại là xong.

Một số chỗ hay sửa:
- **Thẻ `<title>`** và **`<meta description>`** ở đầu file (cho SEO).
- **`<h1>`** trong khối `.project-hero` — tên dự án hiển thị to.
- **`<p class="project-addr">`** — địa chỉ.
- **`<div class="project-specs">`** — bảng thông số. Đổi diện tích, số phòng, giá.
- **`<div class="project-content">`** — 3 mục Tổng quan / Tiện ích / Pháp lý. Viết thêm chi tiết theo từng dự án.

### I.3 — Thêm trang dự án mới

**Bước 1 — Tạo file HTML:**
1. Vào thư mục `du-an/`, copy file `_template.html`.
2. Đổi tên thành `<slug-du-an>.html` (viết thường, không dấu, không cách, dùng dấu gạch ngang). Ví dụ: `vinhomes-smart-city.html`, `the-marina-noi-bai.html`.
3. Mở file mới, dùng Find & Replace (Ctrl+H) thay:
   - `TEMPLATE_NAME` → tên dự án (ví dụ "Vinhomes Smart City")
   - `TEMPLATE_TYPE` → loại hình, **viết đúng 1 trong 6 loại**: `Căn hộ`, `Biệt thự`, `Nhà phố`, `Đất nền`, `Chuyển nhượng`, `Thương mại`
   - `TEMPLATE_ADDR` → địa chỉ
   - `TEMPLATE_AREA` → số m²
   - `TEMPLATE_BEDS` → số phòng ngủ (xoá cả block `<div><span>Phòng ngủ</span>...</div>` nếu là đất/thương mại không có phòng)
   - `TEMPLATE_BATHS` → số phòng tắm
   - `assets/img/PLACEHOLDER.jpg` → đường dẫn ảnh mới (ví dụ `assets/img/vinhomes-smart-city.jpg`)
4. Viết lại 3 mục **Tổng quan / Tiện ích / Pháp lý** cho đúng dự án.

**Bước 2 — Thêm vào danh mục Bất động sản:**

Mở `assets/js/script.js`, tìm mảng `properties`, thêm 1 dòng mới (ví dụ ở cuối mảng):

```javascript
{ id:22, slug:"vinhomes-smart-city", type:"Căn hộ", name:"Vinhomes Smart City", addr:"Đại Mỗ, Nam Từ Liêm, Hà Nội", price:"Liên hệ", beds:2, baths:2, area:75, img:"assets/img/vinhomes-smart-city.jpg" },
```

- `slug` phải **trùng đúng** tên file (không có `.html`) → để link tự nối tới trang chi tiết.
- `type` phải đúng 1 trong 6 loại.
- Với Đất nền / Thương mại / Chuyển nhượng (không có phòng): để `beds:0, baths:0` và **thêm trường `meta:"câu mô tả tự do"`**.

**Bước 3 — Thêm ảnh:**

Bỏ ảnh dự án mới vào `assets/img/` với tên trùng `img` ở bước 2. Nén ảnh dưới ~600 KB.

**Xong.** Mở `listings.html` thấy dự án mới hiện trong danh mục; bấm vào card sẽ mở `du-an/vinhomes-smart-city.html`.

### I.4 — Xoá trang dự án cũ

1. Xoá file `du-an/<slug>.html`.
2. Mở `assets/js/script.js`, xoá dòng tương ứng trong mảng `properties`.
3. (Tuỳ chọn) Nếu trang chủ có "card nổi bật" trỏ tới dự án đó, mở `index.html`, xoá khối `<a class="listing-card" href="du-an/<slug>.html">...</a>` (nhớ xoá **cả 2 bản** trong `marquee-track` để vòng lặp vẫn liền).

---

## J. Kiểm tra nhanh trước khi dùng

- Mở `index.html` → video nền chạy, header trong suốt, 6 card BĐS trượt ngang, 15 cảm nhận tự xoay 3s.
- Bấm vào 1 card → mở đúng trang chi tiết trong `du-an/`. Bấm "← Về danh mục" → quay lại `listings.html`.
- Bấm 1 loại trong menu "Loại hình BĐS" → trang Bất động sản tự lọc sẵn.
- Thu nhỏ cửa sổ → menu gom vào ☰, layout tự thu gọn cho điện thoại.
- Bấm thử nút "Gọi", "Zalo" trên trang chi tiết → mở đúng app.
