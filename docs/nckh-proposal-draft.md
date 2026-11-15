# Bản Nháp Đề Cương Nghiên Cứu Khoa Học Sinh Viên (HCMUT)

> **Tài liệu dùng cho MỐC 1 (Tháng 12/2026):** Mang theo bản đề cương này (cùng sơ đồ khối phần cứng) khi gặp Giảng viên hướng dẫn tại Khoa Điện – Điện tử, Trường ĐH Bách Khoa – ĐHQG-HCM.

---

## 1. Thông Tin Chung
- **Tên đề tài (Tiếng Việt):** Thiết kế hệ thống băng dán thông minh kích thích vi dòng vòng kín, tự động ổn định điện trường dựa trên phép đo trở kháng thời gian thực định hướng hỗ trợ lành vết thương mạn tính.
- **Tên đề tài (Tiếng Anh):** *Design of a Closed-Loop Microcurrent Smart Bandage System with Real-Time Impedance-Based Electric Field Regulation for Chronic Wound Healing Applications.*
- **Nhóm sinh viên thực hiện:**
  1. **Hậu** — Phụ trách mạch tương tự, nguồn dòng hai pha, thiết kế PCB.
  2. **Thành** — Phụ trách mô hình điện sinh học, giao diện điện cực, đo lường AFE và thực nghiệm Gel Phantom.
  3. **Khang** — Phụ trách vi điều khiển, thuật toán vòng kín, giao tiếp không dây NFC/BLE và phần mềm giám sát.
- **Thời gian thực hiện:** 6,5 tháng (Từ tháng 11/2026 đến tháng 05/2027).

---

## 2. Đặt Vấn Đề & Tính Cấp Thiết
- Vết thương mạn tính (loét bàn chân do tiểu đường, loét tì đè) thường bị đình trệ ở giai đoạn viêm do suy giảm **"pin da" (điện thế xuyên biểu bì)** và mất đi **điện trường nội sinh ngang ($\sim 100 - 200\,\text{mV/mm}$)** — tín hiệu định hướng sự di cư của tế bào sừng và nguyên bào sợi (*electrotaxis*).
- Các nghiên cứu gần đây (tiêu biểu là công trình băng dán thông minh của ĐH Stanford trên *Nature Biotechnology*, 2023) đã chứng minh kích thích điện kết hợp theo dõi trở kháng giúp tăng tốc độ lành vết thương.
- **Hạn chế của các hệ thống hiện hữu:** Phần lớn các mạch kích thích hiện nay hoạt động ở chế độ **đặt dòng cố định ($I = \text{const}$)**. Trong khi đó, trở kháng của vết thương thay đổi tới hàng chục lần theo độ ẩm dịch tiết và quá trình tái biểu mô hóa. Việc giữ dòng không đổi làm cho **điện trường thực tế ($E = \rho \cdot J$) bị trôi mạnh theo thời gian** (quá yếu khi vết thương ướt, hoặc quá mạnh gây kích ứng khi vết thương khô).

---

## 3. Mục Tiêu & Điểm Mới Của Đề Tài
1. **Mục tiêu tổng quát:** Xây dựng hoàn chỉnh một nguyên mẫu phần cứng – phần mềm băng dán vết thương thông minh sử dụng các vi mạch thương mại (COTS) có khả năng đo trở kháng tải và tự động điều chỉnh biên độ xung vi dòng hai pha nhằm **giữ điện trường trong vùng mục tiêu ($100 - 150\,\text{mV/mm}$) ổn định**.
2. **Ba đóng góp cụ thể:**
   - **Thuật toán điều khiển liều theo điện trường (Electric-Field-Regulated Closed-Loop):** Kết nối trực tiếp phép đo trở kháng phức $Z(f_0)$ với bộ điều khiển nguồn dòng hai pha, kèm tính năng tự phát hiện bong/hở điện cực.
   - **Phần cứng an toàn, chi phí thấp:** Thiết kế tầng nguồn dòng hai pha cân bằng điện tích ($20 - 400\,\mu\text{A}$, điện áp tuân thủ $12\,\text{V}$), có tụ chặn DC và mạch giới hạn dòng phần cứng $< 1\,\text{mA}$ tuân thủ định hướng tiêu chuẩn IEC 60601-1 / 60601-2-10.
   - **Kiểm chứng định lượng trên mô hình Gel Phantom 4 giai đoạn:** Đánh giá đối chứng sai số điện trường giữa chế độ dòng cố định (Open-loop) và chế độ điều khiển vòng kín (Closed-loop) trên hệ thống mẫu gel Agar–NaCl.

---

## 4. Phạm Vi & Phương Pháp Nghiên Cứu (Đảm Bảo An Toàn & Đạo Đức)
- **Mô phỏng mạch & tín hiệu:** Sử dụng LTspice (cho nguồn dòng 2 pha và mô hình điện cực Randles) kết hợp Python (cho thuật toán giải điều chế đồng bộ I/Q và điều khiển vòng kín).
- **Chế tạo nguyên mẫu:** Thiết kế bo mạch PCB thu nhỏ trên KiCad sử dụng vi điều khiển công suất thấp (`STM32` / `ESP32-C3`), tầng nguồn dòng `TLV9062 + BSS84`, cầu H `CD4053B` và khối đo trở kháng.
- **Thực nghiệm kiểm chứng:** Thực hiện hoàn toàn trên **mạng tải giả RC** và **mô hình vết thương giả (Agar–NaCl Gel Phantom)** với hệ 4 điện cực đo trực tiếp điện trường $E = \Delta V / d$. *Không thử nghiệm trên người hoặc động vật trong giai đoạn đề tài này.*

---

## 5. Sản Phẩm Dự Kiến Khi Nghiệm Thu (Tháng 05/2027)
1. **02 bo mạch nguyên mẫu PCB** hoàn chỉnh chạy thuật toán vòng kín kèm phần mềm Dashboard thu thập dữ liệu thời gian thực.
2. **01 bộ bàn đo kiểm chứng Gel Phantom** và bộ dữ liệu thực nghiệm đối chứng ($n \ge 3$ lần lặp cho 4 trạng thái trở kháng vết thương).
3. **01 Báo cáo tổng kết NCKH** và bài báo khoa học cấp Trường / Hội nghị sinh viên.

---

## 6. Năm Câu Hỏi Xin Ý Kiến Giảng Viên Hướng Dẫn Tại Buổi Gặp Đầu Tiên
1. Với mục tiêu nộp NCKH vào tháng 5–6/2027, phạm vi dừng ở **bo mạch PCB + đo đối chứng trên Gel Phantom 4 nồng độ** đã đủ độ sâu cho hội đồng cấp Khoa/Trường chưa, hay cần bổ sung thêm phần nào?
2. Ở khối đo trở kháng, nhóm nên ưu tiên **tự thiết kế mạch đo I/Q bằng Khuếch đại đo lường (`INA826`) + ADC của MCU** (để thể hiện rõ đóng góp thiết kế mạch), hay dùng chip chuyên dụng như `AD5933 / AD5940`?
3. Phòng thí nghiệm của Bộ môn có hỗ trợ máy đo **LCR meter** và **Oscilloscope 2 kênh** để nhóm hiệu chuẩn tải giả ở giai đoạn tháng 2–3/2027 không?
4. Về hướng liên ngành dài hạn (năm 3–4): Bộ môn có hướng kết nối với nhóm thiết kế IC tương tự (để đưa khối nguồn dòng 2 pha lên quy trình CMOS SKY130/GF180) hoặc phòng lab Y sinh không?
5. Thời hạn đăng ký chính thức và nộp quyển NCKH sinh viên của Khoa Điện – Điện tử năm học này rơi vào tuần nào để nhóm chốt cứng lịch?
