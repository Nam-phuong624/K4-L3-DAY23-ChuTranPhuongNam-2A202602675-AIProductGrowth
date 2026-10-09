# OPERATING DASHBOARD — DocuFreight AI

**Loại mô hình:** B2B SaaS Workflow Automation · **Cập nhật:** 09/10/2026 · **Chử Trần Phương Nam – 2A202602675**  
**NORTH STAR:** Weekly Validated Document Packets (WVDP) — **Hiện tại:** 1.200 bộ/tuần — **Mục tiêu Q4/2026:** 5.000 bộ/tuần

---

### Đèn báo sớm (Leading — nhìn hằng ngày/tuần)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| **Time-to-First-Value (TTFV)** ⭐ | 5.5 ngày | 🟢 < 7 ngày · 🟡 7–14 ngày · 🔴 > 14 ngày | [TB] baseline | POC → Paid (sau 4 tuần) & NRR (sau 12T) |
| **Pipeline Coverage (SMB/Mid-Market)** | 3.8× | 🟢 ≥ 3.5× · 🟡 2.5–3.5× · 🔴 < 2.5× | [BM] [Bessemer / Skok](https://www.forentrepreneurs.com/saas-metrics-2/) (27/08/2026) | New Bookings ARR & Sales Cycle (sau 8–12 tuần) |

---

### Đèn vận hành (Operating — nhìn hằng tuần/tháng)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| **POC → Paid Conversion** | 52% | 🟢 ≥ 50% · 🟡 35–50% · 🔴 < 35% | [BM] [ICONIQ GTM 2026](https://www.iconiq.com/growth/reports/state-of-go-to-market-2026) (27/08/2026) | New ARR & CAC Payback (sau 1–2 quý) |
| **Chi phí AI Inference ÷ Doanh thu** 🤖 | 10.8% | 🟢 < 12% · 🟡 12–18% · 🔴 > 18% | [MH] suy từ Cost/Job | Gross Margin tầng Lagging (sau 1 quý) |
| **Chi phí triển khai ÷ ACV** | 11.5% | 🟢 < 10% · 🟡 10–20% · 🔴 > 20% | [MH] suy từ CAC/PB | Gross Margin & CAC Payback (sau 2 quý) |
| **Usage Depth (% Seats Active)** | 68% | 🟢 ≥ 65% · 🟡 40–65% · 🔴 < 40% | [TB] baseline | Annual Retention & Account Churn (sau 6–12T) |

---

### Đèn kết quả (Lagging — nhìn hằng quý)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn |
|---|---|---|---|
| **Gross Margin** | 76.2% | 🟢 ≥ 75% · 🟡 65–75% · 🔴 < 65% | [BM] [Benchmarkit 2025](https://www.benchmarkit.ai/2025benchmarks) (27/08/2026) / [MH] |
| **CAC Payback Period** | 4.8 tháng | 🟢 < 6.0 tháng · 🟡 6.0–9.0 tháng · 🔴 > 9.0 tháng | [BM] [Bessemer Atlas](https://www.bvp.com/atlas/scaling-to-100-million) (27/08/2026) / [MH] |

---

### 5 luật quyết định (⏹ = luật dừng)

1. ⏹ **NẾU** TTFV > 14 ngày **TRÊN** 3 khách POC liên tiếp **THÌ** đóng băng nhận POC mới 2 tuần, cắt phạm vi xuống đúng 1 loại chứng từ (B/L đường biển) cho 1 phòng ban **KHÔNG THÌ** không tuyển thêm Sales nạp deal vào phễu tắc.
2. ⏹ **NẾU** Chi phí AI Inference ÷ Doanh thu > 18% **TRONG** 2 tuần liên tiếp **VÀ** volume ≥ 2.000 bộ **THÌ** dừng xử lý file scan mờ bằng model LLM đắt tiền, chuyển sang OCR cục bộ và áp trần token per packet **KHÔNG THÌ** không tự động giảm giá gói cước để bù volume.
3. **NẾU** Chi phí triển khai ÷ ACV > 20% **TRÊN** 3 hợp đồng liên tiếp **THÌ** đóng gói chuẩn hóa trường dữ liệu thành 5 bộ template mẫu cho khách tự cấu hình (Self-serve Mapping) **KHÔNG THÌ** không ký thêm cam kết viết code tùy biến miễn phí.
4. **NẾU** Usage Depth < 40% **TRONG** 30 ngày đầu sau go-live **THÌ** cử trực tiếp Chuyên viên CS đến tận văn phòng khách hàng đào tạo lại và phỏng vấn rào cản trong 5 ngày **KHÔNG THÌ** không chào bán thêm module Báo giá hay đề xuất nâng gói.
5. **NẾU** POC → Paid Conversion < 35% **TRONG** 1 quý **VÀ** tổng số POC ≥ 6 khách **THÌ** dừng đàm phán riêng lẻ, gửi Evidence Pack (đối soát độ chính xác & số giờ tiết kiệm) trực tiếp cho CEO/MD của khách **KHÔNG THÌ** không giảm giá quá 15% khi chưa chứng minh được giá trị.

---

### Cổng gác 90 ngày

| Ngày | Metric (1) | Ngưỡng qua cổng | Bằng chứng | Nếu trượt |
|---|---|---|---|---|
| **30** | Tỷ lệ bóc tách chính xác Evidence Pack v1 | ≥ 98% trên mẫu ≥ 50 chứng từ thật của ≥ 3 khách POC | Báo cáo đối soát Benchmark Accuracy ký xác nhận 2 bên | **FIX** (cải tiến parser 30 ngày; trượt lần 2 → **PIVOT**) |
| **60** | Time-to-First-Value (TTFV) | ≥ 3 khách POC đạt TTFV < 7 ngày | Log Audit Event trên hệ thống (Signed vs First Export) | **PIVOT** (chuyển sang Chrome Extension/Email Parser) |
| **90** | Paid Accounts & Conversion | ≥ 3 HĐ trả tiền mới (ARR ≥ $10,800) **VÀ** POC → Paid ≥ 50% | Hợp đồng kinh tế ký số + Hóa đơn VAT kỳ đầu thanh toán | **KILL** (nếu < 2 khách trả tiền hoặc POC→Paid < 25%) |

**KILL CRITERIA:** Nếu sau 90 ngày (tới 09/01/2027), không đạt tối thiểu 2 khách hàng trả phí chính thức với ACV ≥ $3,600 và POC-to-Paid < 30%, toàn bộ dự án sẽ dừng lại để bảo toàn vốn.

**CHƯA ĐO ĐƯỢC:** NRR và Churn Rate chu kỳ 12 tháng (Cần: Hệ thống hóa đơn định kỳ Stripe/Kế toán và đủ 12 tháng vận hành; Khi nào có số: Sơ bộ 6T ngày 09/04/2027, đủ 12T ngày 09/10/2027).
