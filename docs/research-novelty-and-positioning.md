# Khoảng trống nghiên cứu & Định hướng điểm mới (Novelty & Positioning)

> **Nguyên tắc cho nghiên cứu khoa học sinh viên:** Không cần một đột phá làm thay đổi cả ngành, nhưng cần **một đóng góp mới, rõ ràng và có thể tự kiểm chứng được bằng đo đạc kỹ thuật.**

---

## 1. Phân tích hệ thống chuẩn mực hiện tại (Baseline: Stanford 2023)
Bài báo mục tiêu: Jiang et al., *"Wireless, closed-loop, smart bandage with integrated sensors and stimulators for advanced wound care and accelerated healing"*, **Nature Biotechnology** (2023).

**Họ đã làm gì:**
- Mạch in dẻo (FPCB) dày ~100 µm ghép từ nhiều IC thương mại (MCU, RF/NFC không pin, mạch kích thích điện, mạch đo trở kháng, cảm biến nhiệt độ).
- Điện cực hydrogel dẫn điện có khả năng bám/nhả theo nhiệt độ.
- Thử nghiệm tiền lâm sàng trên mô hình chuột: tốc độ lành nhanh hơn ~25%, tái cấu trúc mô cải thiện ~50%.

**Khoảng trống còn lại (cơ hội cho Thiết kế Vi mạch):**
1. **Chưa tích hợp đơn chip (Single-Chip ASIC):** Hệ thống vẫn dùng nhiều IC rời trên FPCB → kích thước, công suất tiêu thụ và giá thành còn cao.
2. **Đặt dòng cố định (Fixed-Current Open-Dose):** Trong quá trình lành, trở kháng vết thương thay đổi mạnh theo độ ẩm, dịch tiết, nhiễm trùng và tái biểu mô hóa. Nếu giữ nguyên biên độ dòng $I$, **điện trường thực tế trong mô ($E = J/\sigma$) sẽ bị trôi theo từng ngày**.

---

## 2. Năm hướng điểm mới tiềm năng

| # | Hướng điểm mới | Mức độ mới | Độ khó | Phù hợp với Thiết kế Vi mạch |
| :--- | :--- | :--- | :--- | :--- |
| **A** | **Tích hợp toàn hệ lên 1 ASIC công suất cực thấp** (kích thích + đo trở kháng + cân bằng điện tích + NFC) | Trung bình | Vừa → Khó | Rất cao (đúng chuyên ngành) |
| **B** | **Định liều theo điện trường (Electric-Field-Regulated)** dựa trên đo trở kháng thời gian thực ⭐ | **Khá mới** | Vừa | Cao (kết hợp điều khiển vòng kín + analog) |
| **C** | **Mảng đa điện cực**: lập bản đồ trở kháng không gian (Spatial EIS) & **lái hướng điện trường (Field Steering)** | Cao | Khó | Rất cao (phù hợp mở rộng thành ĐATN) |
| **D** | **Tối ưu chi phí cực thấp / dùng 1 lần** cho bài toán loét tiểu đường tại Việt Nam | Thực tiễn cao | Vừa | Tốt cho NCKH & cuộc thi sáng tạo |
| **E** | **Tự phát hiện khô/bong điện cực** bằng phép đo trở kháng để ngắt an toàn | Nhỏ, hữu ích | Dễ | Tốt làm tính năng phụ trợ |

---

## 3. Phân tích sâu Hướng B (Khuyến nghị làm trọng tâm)

### Luận điểm kỹ thuật
- Tế bào phản ứng với **điện trường ($E$)** (mức mục tiêu ~100–200 mV/mm), chứ không phản ứng trực tiếp với con số µA đặt trên mạch.
- Vì $E = J/\sigma$ và độ dẫn $\sigma$ (hay trở kháng $Z_{\text{wound}}$) thay đổi hàng ngày, hệ thống vòng kín cần:
  1. Đo $Z_{\text{wound}}$ định kỳ bằng xung sin nhỏ (EIS / giải điều chế I/Q).
  2. Tính toán lại biên độ dòng kích thích $I_{\text{stim}}$ sao cho điện trường hiệu dụng trong vùng vết thương được giữ ổn định trong ngưỡng mục tiêu (và không vượt giới hạn an toàn).

### Cách tự kiểm chứng trong phòng lab (không cần thử trên người/động vật)
- Chế tạo **mô hình vết thương giả lập (tissue phantom)** bằng gel agar / nước muối pha theo các nồng độ khác nhau để mô phỏng sự thay đổi trở kháng của vết thương theo thời gian.
- Cắm cặp đầu dò vi sai đo điện thế trực tiếp trong gel để tính điện trường thực tế $E = \Delta V / d$.
- Chứng minh hệ thống vòng kín giữ $E$ ổn định hơn hẳn so với mạch đặt dòng cố định khi trở kháng phantom thay đổi.

---

## 4. Câu định vị đề tài đề xuất

> *"Thiết kế hệ thống/vi mạch kích thích vết thương vòng kín, tự động điều chỉnh liều theo điện trường dựa trên phép đo trở kháng thời gian thực, hướng tới tích hợp trên ASIC công suất cực thấp cấp nguồn không dây."*

### Kế hoạch chia chặng theo năm học (HCMUT)
- **Năm 2:** Chứng minh nguyên lý **Hướng B** bằng mạch rời trên breadboard/PCB + MCU, kiểm chứng trên tải giả RC và mô hình gel phantom.
- **Năm 3:** Thiết kế các khối lõi (**Hướng A**) ở mức transistor trên PDK mã nguồn mở (SKY130 / GF180): gương dòng cascode, DAC dòng, cầu H cân bằng điện tích, khối I/Q.
- **Năm 4 / Đồ án tốt nghiệp:** Hoàn thiện chip (hoặc hệ lai), mở rộng sang mảng nhiều điện cực (**Hướng C**), đánh giá khả năng tape-out qua Tiny Tapeout.
