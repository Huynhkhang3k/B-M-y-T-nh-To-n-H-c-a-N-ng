# Bộ Máy Tính Toán Học Đa Năng

Bộ Máy Tính Toán Học Đa Năng là một ứng dụng web tích hợp nhiều công cụ toán học hữu ích, giúp bạn giải quyết các bài toán từ biểu thức số học phức tạp đến các vấn đề hình học liên quan đến tam giác.

## 🔹 Các Thành Phần Chính

### 🧮 1. Máy Tính Số Học
**Chức năng:**
- ✅ Tính các biểu thức số học.
- ✅ Giải phương trình (bao gồm cả các phương trình có số mũ và biến số).
- ✅ Hiển thị giải thích chi tiết cho từng bước tính toán.

**Công nghệ:**
- 💻 Sử dụng HTML, CSS và JavaScript.
- 📚 Áp dụng thư viện [Nerdamer](https://nerdamer.com/) để xử lý các biểu thức và giải phương trình.

---

### 📐 2. Máy Tính Tam Giác Vuông
**Chức năng:**
- 🔢 Cho phép nhập 2 hoặc 3 cạnh (bao gồm cạnh huyền nếu có) của tam giác vuông.
- 🔎 Tự động tính cạnh còn thiếu dựa trên định lý Pythagoras.
- 🔄 Hỗ trợ hoán đổi vị trí của góc vuông qua các ô kiểm (checkbox) để thay đổi vị trí góc.
- 🖼️ Vẽ tam giác trên canvas, với canvas tự động phóng to để đảm bảo hình vẽ luôn hiển thị đầy đủ.

**Giao diện:**
- 🎨 Thiết kế trực quan, có hiệu ứng chuyển màu khi rê chuột và dễ sử dụng.

---

### 🔺 3. Máy Tính Tam Giác & Trung Điểm
**Chức năng:**
- 🔢 Cho phép nhập 8 giá trị (ví dụ: AB, AD, BD, BC, BE, EC, AC, DE) của tam giác.
- 📏 Tự động tính các giá trị còn thiếu dựa trên các ràng buộc hình học:
  - ✨ D là trung điểm của AB (→ AD = BD, AB = 2×AD).
  - ✨ E là trung điểm của BC (→ BE = EC, BC = 2×BE).
  - ✨ DE = AC/2 (đường trung bình song song với AC).
- 🖼️ Vẽ tam giác kèm theo đường trung bình trên canvas với khả năng tự động phóng to để tránh bị chồng lấn.

**Giao diện:**
- 🔍 Các ô nhập được bố trí rõ ràng, cùng với bảng kết quả hiển thị các giá trị tính được và hình vẽ trực quan.

---

## 📜 Hướng Dẫn Sử Dụng

### 🔧 Cài Đặt:
1. 📥 Clone repository này hoặc tải file `index.html` về máy.
2. 🌐 Mở file `index.html` trong trình duyệt hoặc import vào [CodeSandbox](https://codesandbox.io/).

### 🔀 Chuyển Đổi Giữa Các Máy Tính:
Ở thanh điều hướng trên cùng có 3 nút:
- 🧮 **Máy Tính Số Học**
- 📐 **Máy Tính Tam Giác Vuông**
- 🔺 **Máy Tính Tam Giác & Trung Điểm**

Nhấn nút tương ứng để chuyển đổi giữa các chế độ.

### ⌨️ Nhập Dữ Liệu & Tính Toán:
- **Máy Tính Số Học**: Nhập biểu thức vào ô nhập và bấm **“Tính Toán”** để xem kết quả và giải thích chi tiết.
- **Máy Tính Tam Giác Vuông**: Nhập các giá trị cạnh (có thể nhập 2 hoặc 3 giá trị) rồi bấm **“Tính Toán”** để vẽ tam giác; bạn có thể thay đổi vị trí góc vuông bằng cách nhấn vào các ô kiểm đi kèm.
- **Máy Tính Tam Giác & Trung Điểm**: Nhập các giá trị của tam giác theo yêu cầu và bấm **“Tính & Vẽ”** để hệ thống tự động tính các giá trị còn thiếu cũng như vẽ tam giác kèm đường trung bình.

---

## ⚙️ Công Nghệ & Phụ Thuộc
- 🏗️ **HTML/CSS/JavaScript**: Ngôn ngữ và công nghệ cơ bản để xây dựng ứng dụng web.
- 📚 **Nerdamer**: Thư viện xử lý các biểu thức toán học và giải phương trình.
- 🔤 **Google Fonts**: Sử dụng phông chữ [Lobster](https://fonts.google.com/specimen/Lobster) cho giao diện trực quan và hiện đại.

---

## 🤝 Đóng Góp & Phản Hồi
Nếu bạn có ý kiến đóng góp, đề xuất cải tiến hoặc phát hiện lỗi, hãy gửi thông tin qua mục **[Issues](#)** hoặc tạo **Pull Request** trên repository. Mọi phản hồi đều được đánh giá cao để giúp dự án ngày càng hoàn thiện hơn!

---

## 📜 Giấy Phép
Dự án này được cấp phép theo **[MIT License](https://opensource.org/licenses/MIT)**. Giấy phép này giúp bảo vệ phần mềm của bạn khỏi việc bị sao chép hoặc sử dụng trái phép mà không có sự ghi nhận công lao. Người khác có thể sử dụng, chỉnh sửa hoặc phân phối phần mềm của bạn, nhưng phải ghi nhận nguồn gốc. Đồng thời, giấy phép cũng giúp bạn tránh trách nhiệm pháp lý nếu có người sử dụng phần mềm sai mục đích.

