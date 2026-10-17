# Lingo Indonesia–Việt — hướng dẫn đưa lên Internet

## Trạng thái thật của dự án
- Frontend React/Vite và backend Node/Express đã có trong bộ mã nguồn.
- API dịch theo ngữ cảnh và API gợi ý trả lời đã được viết; chúng chỉ hoạt động khi cấu hình `AI_API_KEY` hợp lệ và có hạn mức.
- OCR dùng Tesseract.js trong trình duyệt với ngôn ngữ Indonesia + English. OCR cần tải dữ liệu ngôn ngữ ở lần dùng đầu, vì vậy lần đầu có thể chậm và cần Internet.
- Chưa có bản build/deploy được xác minh trong môi trường này. Chưa có URL công khai nào được tạo.
- Chưa có mô hình dịch neural offline. Dịch AI cần Internet; đừng xem từ điển cục bộ là dịch AI.

## Bạn cần chuẩn bị (không cần viết code)
1. Tài khoản GitHub để lưu mã nguồn. Có thể đặt repository ở chế độ Private.
2. Tài khoản Render để chạy website và nhận URL `*.onrender.com`.
3. API key từ nhà cung cấp AI tương thích với API Chat Completions. API key là mật khẩu kỹ thuật để backend gọi AI; nó **không** phải mật khẩu ChatGPT. Gói ChatGPT và API thường được tính phí riêng. Kiểm tra giá, hạn mức và đặt giới hạn chi tiêu trước khi dùng.

## Các bước bằng giao diện web
1. Tải file ZIP này và giải nén trên máy tính.
2. Trên GitHub, tạo repository mới (khuyến nghị Private). Chọn **Add file → Upload files**.
3. Mở thư mục đã giải nén trên máy tính, kéo toàn bộ *nội dung bên trong* vào trang upload (phải thấy `package.json`, `src/`, `server/`, `render.yaml`, `index.html` ở thư mục gốc). Bấm **Commit changes**.
4. Trên Render, chọn **New + → Blueprint**, kết nối GitHub, rồi chọn repository vừa tạo. Render đọc `render.yaml` và dựng dịch vụ.
5. Khi Render hỏi biến môi trường `AI_API_KEY`, dán key do chính bạn tạo ở nhà cung cấp AI. Không gửi key trong ChatGPT, không đặt trong `src/`, không commit file `.env` lên GitHub.
6. Chờ Render báo **Live**. URL công khai sẽ được Render tạo và hiển thị trên trang dịch vụ. Không có URL thật trước bước này.
7. Mở `https://TEN-MIEN-CUA-BAN/api/health`. Kết quả mong đợi là `ok: true` và `provider: "configured"`. Nếu hiện `not_configured`, quay lại Environment và kiểm tra `AI_API_KEY`.
8. Thử dịch một câu ngắn Indonesia → Việt và Việt → Indonesia; sau đó thử tải ảnh chat rõ nét lên OCR.

## Bảo mật và quyền riêng tư
- Khi bấm dịch hoặc tạo gợi ý trả lời, văn bản được gửi từ backend đến nhà cung cấp AI đã cấu hình.
- OCR chạy trong trình duyệt; Tesseract.js có thể tải mã và dữ liệu ngôn ngữ từ mạng. Ảnh không được gửi đến API dịch trong luồng OCR hiện tại.
- Lịch sử và yêu thích được lưu trong localStorage trên trình duyệt, trừ khi tắt lưu lịch sử. Xóa dữ liệu trình duyệt sẽ xóa dữ liệu này.
- Không nhập mật khẩu, thông tin ngân hàng hoặc dữ liệu nhạy cảm vào tin nhắn.
- Giới hạn request tích hợp trong backend chỉ là lớp bảo vệ cơ bản, chưa thay thế hệ thống chống lạm dụng cho dịch vụ quy mô lớn.

## Sự cố thường gặp
- `Chưa cấu hình AI_API_KEY`: chưa thêm key trong Render Environment hoặc chưa redeploy.
- `Nhà cung cấp AI gặp lỗi`: kiểm tra key, hạn mức, quyền truy cập model và cấu hình `AI_MODEL`.
- OCR không chạy: thử ảnh PNG/JPG/WEBP rõ hơn, dung lượng dưới 12 MB, cho phép tải dữ liệu ngôn ngữ trong trình duyệt và thử lại.
- Lần mở đầu chậm: gói Render miễn phí có thể tạm ngừng khi không hoạt động; lần gọi đầu có thể cần chờ máy chủ khởi động.

## Chạy thử trên máy tính (tùy chọn)
Cần Node.js 20 trở lên. Mở terminal trong thư mục dự án và chạy:

```bash
npm install
```

Sao chép `.env.example` thành `.env`, thêm `AI_API_KEY` riêng của bạn, rồi chạy:

```bash
npm run dev
```

Mở URL Vite hiển thị trong terminal. Không chia sẻ file `.env`.

## Kiểm thử chưa hoàn tất
Trong môi trường tạo file hiện tại không thể xác minh một bản build production hoàn chỉnh hoặc kiểm thử end-to-end với nhà cung cấp AI thật. Hãy xem việc Render báo **Live**, `/api/health` báo `configured`, và thử dịch/OCR thật là các bước xác minh bắt buộc trước khi sử dụng thường xuyên.
