# Quy Trình Thực Nghiệm Trên Gel Phantom & Định Hướng Sinh Học

> **Phụ trách chính:** **Thành** (Tải giả RC, Gel Phantom, Đo kiểm chứng điện trường & Thiết kế giao thức Sinh học)  
> **Phối hợp:** **Hậu** (Đo dạng sóng bằng Oscilloscope) & **Khang** (Thu thập log dữ liệu CSV tự động)

---

## 1. Tại Sao Dùng Gel Phantom Và Tải Giả RC?
Trong khuôn khổ 28 tuần nghiên cứu khoa học sinh viên, nhóm **không thử nghiệm trực tiếp trên người hay động vật** (đảm bảo tuyệt đối an toàn điện và quy định của Hội đồng Đạo đức). Thay vào đó, nhóm sử dụng **2 cấp độ mô hình vật lý chuẩn hóa** được công nhận trong các bài báo IEEE TBioCAS / Biosensors:
1. **Cấp độ 1 — Mạng tải giả rời (Discrete RC Randles + Cole Phantom):** Dùng điện trở và tụ điện có giá trị chính xác ($1\%$) để kiểm chuẩn sai số của mạch nguồn dòng (Hậu) và mạch đo trở kháng (Khang).
2. **Cấp độ 2 — Mô hình vết thương giả bằng Gel Agar – NaCl (Hydrogel Tissue Phantom):** Mô phỏng môi trường dẫn điện ion 3 chiều của vết thương ở các giai đoạn khác nhau (từ tiết nhiều dịch/viêm sang khô dần/tái biểu mô hóa) để **đo trực tiếp điện trường thực tế $E = \Delta V / d$**.

---

## 2. Thiết Kế Cấp Độ 1: Bộ 3 Tải Giả RC Chuẩn (Tuần 13–17)

Mỗi tải giả gồm một nhánh nối tiếp $R_s$ (trở kháng dịch mô sâu) và một mắt song song $R_p \parallel C_p$ (trở kháng giao diện điện cực – lớp biểu mô):

| Mã tải | Trạng thái vết thương mô phỏng | $R_s$ ($\Omega$) | $R_p$ ($\text{k}\Omega$) | $C_p$ ($\text{nF}$) | $|Z|$ lý thuyết tại $1\,\text{kHz}$ | $|Z|$ ở DC ($f \to 0$) |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **Load-1 (Ướt / Viêm)** | Dịch tiết nhiều, lớp biểu bì rách hoàn toàn | $470\,\Omega$ | $2.2\,\text{k}\Omega$ | $100\,\text{nF}$ | $\approx 1.66\,\text{k}\Omega$ | $2.67\,\text{k}\Omega$ |
| **Load-2 (Trung bình)** | Đang lên mô hạt (granulation tissue) | $1.0\,\text{k}\Omega$ | $10.0\,\text{k}\Omega$ | $47\,\text{nF}$ | $\approx 4.10\,\text{k}\Omega$ | $11.0\,\text{k}\Omega$ |
| **Load-3 (Khô / Lành)** | Tái biểu mô hóa một phần, dịch tiết giảm | $1.5\,\text{k}\Omega$ | $33.0\,\text{k}\Omega$ | $22\,\text{nF}$ | $\approx 8.53\,\text{k}\Omega$ | $34.5\,\text{k}\Omega$ |

---

## 3. Thiết Kế Cấp Độ 2: Công Thức Pha 4 Mẫu Gel Phantom (Tuần 17–25)

### 3.1. Nguyên vật liệu (Dễ mua, chi phí $< 100.000\,\text{VNĐ}$)
- Bột **Agar-agar** tinh khiết (loại dùng cho vi sinh hoặc thực phẩm sạch): $2.0\,\text{g}$ cho mỗi $100\,\text{mL}$ dung dịch ($2\%\,\text{w/v}$) để tạo độ cứng tương đương mô mềm.
- **Nước cất** (hoặc nước khử ion DI water): dùng làm dung môi chuẩn để kiểm soát độ dẫn điện.
- **Muối tinh khiết $\text{NaCl}$** (hoặc viên pha dung dịch đệm **PBS** y tế mua tại hiệu thuốc/cửa hàng hóa chất).
- **Hộp khuôn nhựa chữ nhật** kích thước cố định: dài $L = 60\,\text{mm}$, rộng $W = 30\,\text{mm}$, cao độ dày lớp gel $H = 5\,\text{mm}$.

### 3.2. Bảng nồng độ 4 mẫu Gel mô phỏng diễn tiến lành vết thương

| Mẫu Gel | Trạng thái sinh lý mô phỏng | Nồng độ $\text{NaCl}$ ($\text{g/L}$) | Độ dẫn điện $\sigma$ ước tính ($\text{S/m}$) | Trở kháng dự kiến giữa 2 điện cực ($d = 20\,\text{mm}$) |
| :--- | :--- | :---: | :---: | :---: |
| **Gel-1 (Exudate-Rich)** | Vết thương mới / tiết nhiều dịch rỉ viêm | $9.0\,\text{g/L}$ ($0.9\%$ sinh lý) | $\approx 1.4 - 1.6\,\text{S/m}$ | $\approx 1.5 - 2.5\,\text{k}\Omega$ |
| **Gel-2 (Granulation)** | Giai đoạn tăng sinh / mô hạt ẩm | $4.5\,\text{g/L}$ ($0.45\%$) | $\approx 0.7 - 0.8\,\text{S/m}$ | $\approx 3.0 - 5.0\,\text{k}\Omega$ |
| **Gel-3 (Epithelializing)** | Đang đóng miệng vết thương, ít dịch | $1.8\,\text{g/L}$ ($0.18\%$) | $\approx 0.30 - 0.35\,\text{S/m}$ | $\approx 7.5 - 12\,\text{k}\Omega$ |
| **Gel-4 (Dry / Scab)** | Bề mặt khô / gần lành hoàn toàn | $0.6\,\text{g/L}$ ($0.06\%$) | $\approx 0.10 - 0.12\,\text{S/m}$ | $\approx 18 - 28\,\text{k}\Omega$ |

> **Quy trình đúc khuôn:** Đun sôi nước cất + $\text{NaCl}$ đã cân chính xác, cho bột Agar $2\%$ vào khuấy đều đến khi trong suốt, đổ vào khuôn dày $5\,\text{mm}$, để nguội đến nhiệt độ phòng ($25^\circ\text{C}$) và bọc kín bằng màng bọc thực phẩm để tránh bay hơi nước trước khi đo.

---

## 4. Bố Trí Bàn Đo 4 Điện Cực Kiểm Chứng Điện Trường (Thực Nghiệm Ăn Điểm)

```text
          Khuôn Gel Agar + NaCl (60 mm x 30 mm x 5 mm)
   ┌────────────────────────────────────────────────────────┐
   │                                                        │
   │     [ E+ ]          ( P+ )          ( P- )     [ E- ]  │
   │   Kích thích       Đầu dò 1        Đầu dò 2  Kích thích│
   │       │               │               │          │     │
   └───────┼───────────────┼───────────────┼──────────┼─────┘
           │◄─────────────►│◄─ d_p = 10mm ─►│◄────────►│
           │               │               │          │
           │               └──► ΔV_probe ◄─┘          │
           │                 (Oscilloscope /          │
           │                  In-Amp INA826)          │
           └──────► Dòng kích thích I_stim ◄──────────┘
                        (d_stim = 30 mm)
```

- **Hai điện cực ngoài ($E_+, E_-$):** Khoảng cách $d_{\text{stim}} = 30\,\text{mm}$, nối với đầu ra mạch kích thích & đo trở kháng.
- **Hai đầu dò trong ($P_+, P_-$):** Hai kim Ag/AgCl hoặc dây đồng mạ thiếc mảnh cắm cách nhau đúng $d_p = 10.0\,\text{mm}$ tại vùng trung tâm (qua nắp khuôn khoan lỗ định vị sẵn).
- **Cách tính điện trường thực tế tại tâm vết thương giả:**
  $$E_{\text{actual}} = \frac{\Delta V_{\text{probe}}}{d_p} = \frac{\Delta V_{\text{probe}}\,(\text{mV})}{10\,\text{mm}} \quad (\text{đơn vị: mV/mm})$$
- **Kịch bản đo đối chứng (Lặp lại $n = 3$ lần trên cả 4 mẫu Gel-1 $\to$ Gel-4):**
  1. **Chế độ Vòng Hở (Open-Loop, giống các mạch thông thường):** Đặt cố định $I_{\text{stim}} = 150\,\mu\text{A}$ cho cả 4 mẫu Gel $\to$ Ghi lại $E_{\text{actual}}$ bị vọt từ $\sim 40\,\text{mV/mm}$ (ở Gel-1) lên $> 400\,\text{mV/mm}$ (ở Gel-4).
  2. **Chế độ Vòng Kín (Closed-Loop của nhóm):** Đặt mục tiêu $E_{\text{target}} = 120\,\text{mV/mm}$ $\to$ Hệ thống tự đo $Z$ của từng mẫu Gel và tự hạ dòng từ $\sim 350\,\mu\text{A}$ (ở Gel-1) xuống $\sim 45\,\mu\text{A}$ (ở Gel-4), giữ $E_{\text{actual}}$ luôn nằm trong dải $120 \pm 15\,\text{mV/mm}$ (sai số $< 12\%$).

---

## 5. Thiết Kế Phần Mở Rộng Sinh Học (Cơ Chế Phân Tử & Giao Thức In-Vitro)

Báo cáo NCKH của nhóm được bổ sung thêm 2 nội dung chuyên sâu về sinh học thực nghiệm (do **Thành** phụ trách):
1. **Giải thích sâu cơ chế phân tử trong Chương 1:** Trình bày chuẩn xác đường truyền tín hiệu nội bào **PI3K$\gamma$ / PIP3 / PTEN**, sự phân cực thụ thể màng (EGFR, Integrin) và động học trùng hợp sợi **F-actin** ở mép trước tế bào sừng (keratinocyte) dưới điện trường $100-200\,\text{mV/mm}$.
2. **Xây dựng Giao thức Thử nghiệm In-Vitro Chuẩn (Đề xuất cho giai đoạn mở rộng với Phòng Lab Sinh học):**
   - Thiết kế buồng **Scratch Assay (Wound Healing Assay)** trên đĩa nuôi cấy 6 giếng với dòng tế bào nguyên bào sợi chuột (**NIH/3T3**) hoặc tế bào sừng người (**HaCaT**), sử dụng cầu muối Agarose $2\%$ để cách ly sản phẩm điện phân tại điện cực khỏi môi trường nuôi cấy DMEM.
   - Phần thiết kế chi tiết này đưa vào **Phụ lục / Hướng phát triển** của báo cáo NCKH (hoặc thực hiện thật nếu GVHD kết nối được với Bộ môn Kỹ thuật Y sinh – ĐH Quốc Tế hoặc ĐH Khoa học Tự nhiên).
