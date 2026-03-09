# Hướng dẫn Clone và Sử dụng Template cho Dự án Mới

Tài liệu này hướng dẫn chi tiết các bước để tự nhân bản (clone) source code từ bộ Boilerplate này ra thành một dự án độc lập, hoàn toàn mới (có lịch sử Git sạch) để bạn bắt đầu lập trình.

## Cách 1: Sử dụng Github "Use this template" (Dành cho Repo được thiết lập trên Github)

Nếu repository template này đã được đẩy lên Github và cấu hình là một template, đây là cách nhanh nhất:

1. Truy cập vào trang web của repository này trên GitHub.
2. Tìm và bấm vào nút màu xanh có nội dung **"Use this template"** ở góc phải phía trên.
3. Chọn **"Create a new repository"**.
4. Điền tên mới cho dự án của bạn (VD: `my-awesome-project`) và khởi tạo kho lưu trữ.
5. Máy chủ Github sẽ tự chép mã nguồn sang repository mới tinh của bạn. Giờ bạn chỉ cần clone URL của repo mới về máy và sử dụng.

---

## Cách 2: Setup Thủ công qua Git CLI (Dành cho Local repo / Bất kỳ nền tảng Git nào)

Trong trường hợp bạn muốn tạo thủ công, hãy làm theo tuần tự các bước dưới đây trên màn hình Terminal (Command Prompt / PowerShell / Git Bash):

### Bước 1. Nhân bản (Clone) Template này về thư mục mới

Thay `d:\template_nextjs` (hoặc URL git gốc) và `my-new-app` bằng tên dự án của bạn:

```bash
# Cú pháp: git clone <nguồn-repo-gốc> <tên-thư-mục-dự-án-mới>
git clone d:\template_nextjs my-new-app
cd my-new-app
```

### Bước 2. Dọn sạch và khởi tạo lịch sử Git mới

Bạn không nên giữ lại lịch sử commit của template cũ để tránh rối rắm. Hãy xóa hẳn hệ thống `.git` đang có.

```bash
# Xóa thư mục .git (Trên Linux/MacOS/Git Bash)
rm -rf .git

# (Hoặc nếu dùng Windows Command Prompt/PowerShell)
# rmdir /s /q .git  hoặc  Remove-Item -Recurse -Force .git
```

Sau khi dọn sạch, hãy "khai sinh" hệ thống quản lý git mới tinh cho dự án của bạn:

```bash
git init
```

### Bước 3. Khởi tạo một Repository mới trên Git Server

Hãy đăng nhập vào Github (hoặc Gitlab/Bitbucket v.v.) và tạo một repository trực tuyến trống (blank project) với tên là `my-new-app`.
Nền tảng sẽ cấp cho bạn một URL Repository (ví dụ: `https://github.com/username/my-new-app.git`).

Thực hiện liên kết và đẩy (push) code local đó lên Remote server:

```bash
# Nối liên kết vào máy chủ mới
git remote add origin <URL-Repository-mới-của-bạn>

# Tạo commit gốc đầu tiên
git add .
git commit -m "Init: Khởi tạo mã nguồn từ cấu trúc Next.js Template"

# Đẩy code lên branch main
git branch -M main
git push -u origin main
```

---

## Các thao tác Cài đặt Môi trường Bắt buộc cho dự án mới

Sau khi hoàn tất việc kết nối Git và bắt đầu làm việc, hoặc nếu có một Lập trình viên khác trong team clone dự án mới của bạn về máy tính của họ, người đó sẽ cần chạy các lệnh sau ở lần mở máy đầu tiên:

**1. Cài đặt các gói thư viện (Dependencies):**

```bash
npm install
```

**2. Khởi tạo biến môi trường ở Local:**

```bash
# Copy file mẫu sang file thực (.env.local sẽ được ignore bảo mật khi push code)
cp .env.example .env.local
```

**3. Khởi tạo lại Git Hook (Kích hoạt quá trình bắt lỗi Linter trước mỗi lệnh commit):**
Để các công cụ như `Husky` chèn kiểm tra vào git ở máy tính mới, lập trình viên cần kích hoạt chúng qua lệnh sau:

```bash
npx husky init
git config core.hooksPath .husky/_
```

_(Nếu là HĐH Windows, bạn cũng có thể cần phải vào file `.husky/pre-commit` và sửa dòng chạy thành `npx.cmd lint-staged` để sửa lỗi thiếu bash npx)._

**4. Chạy dự án:**
Thử nghiệm chạy local server ở môi trường phát triển:

```bash
npm run dev
```

Mở trình duyệt tại địa chỉ [http://localhost:3000](http://localhost:3000) để xem mã nguồn hiển thị.
