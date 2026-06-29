# VCOMP - Vietnamese Compression Protocol
**Giao thức nén tiếng Việt tối ưu cho Kỷ nguyên AI & Dữ liệu lớn**

VCOMP là một thư viện mã nguồn mở giúp ánh xạ, mã hóa và nén ngữ nghĩa tiếng Việt một cách triệt để. Thay vì nén theo từng byte ngẫu nhiên (như Gzip hay Zip), VCOMP phân tích cấu trúc âm tiết tiếng Việt và mã hóa chúng thành một hệ thống Base60 siêu tối ưu.

## 🚀 Điểm nhấn (Features)
- **Lossless Phonetics Compression:** Ép 1 từ tiếng Việt (ví dụ: `nghiêng`) thành đúng 3 ký tự alphanumeric (ví dụ: `5A4`).
- **Giảm 60%-70% Dung lượng:** Cực kỳ hữu ích cho Database, hệ thống Log, chat app, hoặc truyền tải IoT. Gắn VCOMP trước khi chạy GZIP sẽ cho ra dung lượng nhỏ nhất thế giới cho các tin nhắn siêu ngắn.
- **AI Token Optimization:** Chuẩn hóa toàn bộ độ dài của từ tiếng Việt, dọn đường cho việc ánh xạ 1-1 token, giúp vượt qua rào cản "Thuế Token" (Token Tax) trên các mô hình AI lớn (ChatGPT, Claude).

## 📦 Cài đặt
```bash
npm install vcomp-js
```

## 🛠 Cách sử dụng (Usage)

```javascript
import { encodeWord, decodeWord, timeToBase60, base60ToTime } from 'vcomp-js';

// 1. Mã hóa tiếng Việt sang Mã thời gian (TimeCode)
const timeCode = encodeWord("trường");
console.log(timeCode); // Đầu ra: 6 chữ số (hhmmss) đại diện cho tọa độ ma trận

// 2. Chuyển Mã thời gian sang Mã Base60 siêu nén (3 ký tự)
const compressed = timeToBase60(timeCode);
console.log(compressed); // Ví dụ: "hK2"

// 3. Giải mã ngược lại
const originalTimeCode = base60ToTime(compressed);
const originalWord = decodeWord(originalTimeCode);
console.log(originalWord); // "trường"
```

## 🧠 Nguyên lý hoạt động
Tiếng Việt có độ phân mảnh rất cao do dấu câu (UTF-8 multibyte). VCOMP sử dụng một Ma trận Phụ âm (Consonants) x Vần (Rhymes) gồm `1440 tổ hợp`. Cùng với hệ thống "Bánh đà" (S1, S2 state machine), thuật toán có khả năng bao quát toàn bộ từ điển tiếng Việt tự nhiên và gom gọn nó lại bằng công thức:
`[Phụ âm (Base60)] + [Vần (Base60)] + [Dấu/State (Base60)]`

## ⚖️ Bản quyền (License)
Dự án được phân phối dưới giấy phép **MIT**. Bạn hoàn toàn tự do sử dụng nó trong các dự án cá nhân, phi thương mại lẫn thương mại (ví dụ: nhúng vào phần mềm công ty bạn để nén database).

---
*Phát triển bởi một khối óc người Việt, vì một tương lai tiếng Việt không còn bị bỏ lại phía sau trong kỷ nguyên Trí tuệ Nhân tạo.*
