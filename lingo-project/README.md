# Lingo Indonesia ↔ Việt Nam

Ứng dụng React + TypeScript + Vite và backend Node.js/Express. Hỗ trợ dịch hai chiều qua AI tương thích OpenAI Chat Completions, nhiều sắc thái bản dịch, gợi ý trả lời, OCR ảnh bằng Tesseract.js, từ điển slang, lịch sử/yêu thích cục bộ, giao diện sáng/tối và phím tắt.

## Quick start
- Node.js 20+
- `npm install`
- Sao chép `.env.example` thành `.env`, nhập API key riêng vào `AI_API_KEY`
- `npm run dev`

## Deploy công khai
Đọc `DEPLOY-RENDER-VI.md` để triển khai qua GitHub + Render bằng giao diện web.

## Giới hạn quan trọng
- Dịch AI và gợi ý trả lời không hoạt động nếu chưa cấu hình API key hợp lệ.
- OCR chạy trong trình duyệt và cần dữ liệu ngôn ngữ; lần đầu có thể cần Internet.
- Chưa có dịch neural hoàn toàn offline.
- Bộ mã nguồn chưa được xác minh bằng build production/E2E trong môi trường hiện tại; phải kiểm tra sau khi deploy.
- Không đưa API key vào frontend hoặc GitHub.
