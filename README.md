# Báo cáo Phân tích Doanh số Phân phối 2022–2024

**Sinh viên:** Đoàn Phúc Gia Khánh
**MSSV:** 030239230088
**Môn học:** Tin học ứng dụng (THUD) – Lớp D08
**File:** `THUD_D08_Doan_Phuc_Gia_Khanh_030239230088.xlsx`

## 1. Mục tiêu

Xây dựng một quy trình xử lý dữ liệu hoàn chỉnh trong Excel — từ dữ liệu giao dịch thô đến Dashboard trực quan — nhằm theo dõi và phân tích hiệu suất bán hàng của 4 nhà phân phối (**FPT, Viettel, VNPT, Công ty A**) đối với 10 sản phẩm (**SP 01 – SP 10**), trên 3 miền (**Bắc / Trung / Nam**), trong giai đoạn **01/01/2022 – 31/12/2024** (~4.983 giao dịch).

## 2. Cấu trúc dữ liệu & luồng xử lý

Workbook gồm 14 sheet, chia thành 4 nhóm theo luồng xử lý dữ liệu:

```
Dữ liệu gốc  →  Tính toán  →  Tổng hợp (Pivot)  →  Trực quan hóa (Dashboard)
```

| # | Sheet | Vai trò |
|---|-------|---------|
| 1 | `Giá Đầu vào` | Bảng giá đầu vào (triệu đồng) cho từng sản phẩm SP 01–SP 10 |
| 2 | `Hệ số` | Hệ số chi phí bán hàng & hệ số lợi nhuận theo từng nhà phân phối, chia 2 nhóm sản phẩm (SP01–05, SP06–10) |
| 3 | `Price` | Bảng tổng hợp tham chiếu nhanh (gộp 2 bảng trên) |
| 4 | `Data` | **Dữ liệu giao dịch gốc**: Ngày, Khu vực, Nhà phân phối, Sản phẩm, Số lượng |
| 5 | `Bảng giá` | Bảng tính trung tâm — dùng `INDEX/MATCH` (hoặc `VLOOKUP`) tra cứu Giá đầu vào & Hệ số theo Sản phẩm/Nhà phân phối, từ đó tính: `Giá bán ra`, `Doanh số`, `Lợi nhuận` cho từng giao dịch |
| 6 | `Bảng_giá(lọc)` | Bảng dữ liệu dạng "unpivot" (tách Năm/Tháng, gộp Số lượng & Doanh số vào 1 cột `SL & DS` / `Giá trị`) — nguồn cho các PivotTable |
| 7 | `PT1` | PivotTable: Doanh số theo **Năm → Tháng** × **Nhà phân phối** |
| 8 | `PT2` | PivotTable: Tỷ trọng (%) doanh số theo Năm × Nhà phân phối |
| 9 | `PT3` | PivotTable: Doanh số theo **Năm** × **Khu vực** |
| 10 | `PT4 - Top3` | PivotTable: Top 3 sản phẩm bán chạy nhất theo Số lượng, theo từng Nhà phân phối |
| 11 | `PT4 - Top3 (All)` | Bản mở rộng của PT4, chi tiết theo từng Năm |
| 12 | `Card` | Các chỉ số KPI tổng: Lợi nhuận, Doanh thu, Tỷ suất lợi nhuận, AOV (giá trị đơn hàng trung bình) |
| 13 | `lọc SL` | Bảng phụ trợ cho Slicer lọc theo Số lượng |
| 14 | `Dashboard` | **Bảng điều khiển hiệu suất** — tổng hợp biểu đồ + slicer tương tác cho giai đoạn 2022–2024 |

## 3. Công thức & kỹ thuật chính

- **Tra cứu dữ liệu:** `INDEX/MATCH` hoặc `VLOOKUP` để lấy Giá đầu vào (theo Sản phẩm) và Hệ số chi phí/lợi nhuận (theo Nhà phân phối + Nhóm sản phẩm) từ các bảng danh mục.
- **Công thức tính giá & doanh số** (sheet `Bảng giá`):
  - `Giá bán ra = Giá đầu vào / (1 − Hệ số chi phí bán hàng − Hệ số lợi nhuận)`
  - `Doanh số = Số lượng × Giá bán ra`
  - `Lợi nhuận = Doanh số × Hệ số lợi nhuận`
- **PivotTable & Slicer:** tổng hợp dữ liệu đa chiều (Năm/Tháng/Khu vực/Nhà phân phối/Sản phẩm), lọc tương tác trên Dashboard.
- **Biểu đồ (Charts):** trực quan hóa xu hướng doanh số, cơ cấu theo khu vực và nhà phân phối, Top sản phẩm.
- **Thẻ KPI (Card):** Tổng doanh thu, tổng lợi nhuận, tỷ suất lợi nhuận, AOV — cập nhật theo bộ lọc.

## 4. Chỉ số kinh doanh nổi bật (toàn giai đoạn 2022–2024)

| Chỉ số | Giá trị |
|---|---|
| Tổng doanh thu | ~794.042 triệu VND |
| Tổng lợi nhuận | ~23.544 triệu VND |
| Tỷ suất lợi nhuận | ~13,16% |
| Giá trị đơn hàng trung bình (AOV) | ~8,56 triệu VND |
| Khu vực đóng góp doanh số lớn nhất | Miền Nam |
| Doanh số tăng trưởng | 2022 → 2024 tăng đều qua từng năm |

*(Số liệu tham khảo từ sheet `Card`, `PT1`, `PT3` — đơn vị: triệu VND)*

## 5. Cách sử dụng file

1. Mở sheet **`Dashboard`** để xem tổng quan trực quan.
2. Dùng các **Slicer** (Năm, Khu vực, Nhà phân phối...) để lọc số liệu theo nhu cầu — các biểu đồ và thẻ KPI sẽ tự động cập nhật.
3. Muốn xem chi tiết số liệu gốc dùng để tính toán: vào sheet `Bảng giá` hoặc `Data`.
4. Muốn kiểm tra công thức tra cứu giá/hệ số: xem sheet `Giá Đầu vào`, `Hệ số`, `Price`.
5. Các PivotTable (`PT1`–`PT4`) có thể refresh (chuột phải → Refresh) nếu dữ liệu nguồn thay đổi.

## 6. Công cụ sử dụng

Microsoft Excel: Formulas (INDEX/MATCH), PivotTable, PivotChart, Slicer, Conditional Formatting, Dashboard design.

---
*README này được biên soạn để mô tả cấu trúc và logic xử lý của file bài tập, hỗ trợ người đọc/giảng viên nắm nhanh luồng dữ liệu mà không cần dò từng sheet.*
