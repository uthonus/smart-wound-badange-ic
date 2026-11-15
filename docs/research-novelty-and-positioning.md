# Khoảng trống nghiên cứu & Định hướng điểm mới (Novelty & Positioning)

> **Nguyên tắc cho nghiên cứu khoa học sinh viên:** Không cần một đột phá làm thay đổi cả ngành, nhưng cần **một đóng góp mới, rõ ràng và có thể tự kiểm chứng được bằng đo đạc kỹ thuật.**

---

## 1. Phân tích hệ thống chuẩn mực hiện tại (Baseline: Stanford 2023)
Bài báo mục tiêu: Jiang et al., *"Wireless, closed-loop, smart bandage with integrated sensors and stimulators for advanced wound care and accelerated healing"*, **Nature Biotechnology** (2023).

**Họ đã làm gì:**
- Mạch in dẻo (FPCB) dày ~100 µm ghép từ nhiều IC thương mại (MCU, RF/NFC không pin, mạch kích thích điện, mạch đo trở kháng, cảm biến nhiệt độ).
- Điện cực hydrogel dẫn điện có khả năng bám/nhả theo nhiệt độ.
- Thử nghiệm tiền lâm sàng trên mô hình chuột: tốc độ lành nhanh hơn ~25%, tái cấu trúc mô cải thiện ~50%.

**Khoảng trống còn lại:**
- **Đặt dòng cố định (Fixed-Current Open-Dose):** Trong quá trình lành, trở kháng vết thương thay đổi mạnh theo độ ẩm, dịch tiết, nhiễm trùng và tái biểu mô hóa. Nếu giữ nguyên biên độ dòng $I$, **điện trường thực tế trong mô ($E = J/\sigma$) sẽ bị trôi theo từng ngày**.
- **Chi phí và độ phức tạp tiếp cận:** Cần một giải pháp gọn nhẹ, sử dụng các chip thương mại (COTS) phổ biến, tối ưu cho điều kiện triển khai thực tế và dễ mở rộng.

---

## 2. Năm hướng điểm mới tiềm năng

| # | Hướng điểm mới | Mức độ mới | Độ khó | Ghi chú |
| :--- | :--- | :--- | :--- | :--- |
| **B** | **Định liều theo điện trường (Electric-Field-Regulated)** dựa trên đo trở kháng thời gian thực ⭐ | **Khá mới** | Vừa | Trọng tâm chính, thực hiện được ngay bằng chip có sẵn + thuật toán trên MCU |
| **D** | **Tối ưu chi phí cực thấp / dùng 1 lần** cho bài toán loét tiểu đường tại Việt Nam | Thực tiễn cao | Vừa | Tốt cho NCKH & cuộc thi sáng tạo |
| **E** | **Tự phát hiện khô/bong điện cực** bằng phép đo trở kháng để ngắt an toàn | Nhỏ, hữu ích | Dễ | Tốt làm tính năng phụ trợ |
| **C** | **Mảng đa điện cực**: lập bản đồ trở kháng không gian (Spatial EIS) & **lái hướng điện trường (Field Steering)** | Cao | Khó | Phù hợp mở rộng thành đề tài năm 3–4 / ĐATN |
| **A** | **Thiết kế riêng 1 khối mạch tích hợp (ASIC block)** ở mức transistor (ví dụ tầng nguồn dòng hoặc khối I/Q) | Chuyên sâu IC | Cao | Có thể tách làm nhánh nghiên cứu riêng khi học lên năm 3–4 |

---

## 3. Phân tích sâu Hướng B (Trọng tâm thực hiện)

### Luận điểm kỹ thuật
- Tế bào phản ứng với **điện trường ($E$)** (mức mục tiêu ~100–200 mV/mm), chứ không phản ứng trực tiếp với con số µA đặt trên mạch.
- Vì $E = J/\sigma$ và độ dẫn $\sigma$ (hay trở kháng $Z_{\text{wound}}$) thay đổi hàng ngày, hệ thống vòng kín cần:
  1. Đo $Z_{\text{wound}}$ định kỳ bằng chip AFE (như AD5940/41) hoặc mạch giải điều chế I/Q.
  2. MCU tính toán lại giá trị dòng đặt $I_{\text{stim}}$ sao cho điện trường hiệu dụng trong vùng vết thương được giữ ổn định trong ngưỡng mục tiêu (và không vượt giới hạn an toàn).

### Cách tự kiểm chứng trong phòng lab (không cần thử trên người/động vật)
- Chế tạo **mô hình vết thương giả lập (tissue phantom)** bằng gel agar / nước muối pha theo các nồng độ khác nhau để mô phỏng sự thay đổi trở kháng của vết thương theo thời gian.
- Cắm cặp đầu dò vi sai đo điện thế trực tiếp trong gel để tính điện trường thực tế $E = \Delta V / d$.
- Chứng minh hệ thống vòng kín giữ $E$ ổn định hơn hẳn so với mạch đặt dòng cố định khi trở kháng phantom thay đổi.

---

## 4. Câu định vị đề tài đề xuất

> *"Hệ thống băng dán vết thương thông minh vòng kín, tự động điều chỉnh liều vi dòng để ổn định điện trường dựa trên phép đo trở kháng thời gian thực."*

### Kế hoạch chia chặng theo năm học (HCMUT)
- **Năm 2:** Chứng minh nguyên lý **Hướng B** bằng mạch dùng chip có sẵn (MCU + AFE/Op-amp), kiểm chứng trên tải giả RC và mô hình gel phantom.
- **Năm 3:** Thu nhỏ lên mạch in dẻo (FPCB) tích hợp NFC; mở rộng thêm tính năng an toàn (**Hướng E**) hoặc mảng nhiều điện cực (**Hướng C**).
- **Năm 4 / Đồ án tốt nghiệp:** Có thể phát triển tiếp thành sản phẩm hoàn chỉnh, hoặc chọn thiết kế ở mức transistor một khối analog cốt lõi (như khối nguồn dòng 2 pha) để gắn trực tiếp với chuyên ngành Thiết kế Vi mạch.
