# Worksheet — DocuFreight AI

Họ tên: Chử Trần Phương Nam · MHV: 2A202602675 · Ngày làm: 09/10/2026

---

## Trạm 1 — Loại mô hình

**Câu chốt loại:**  
Chúng tôi là **B2B** vì tiền đến từ các **Công ty Giao nhận Vận tải (Freight Forwarders) và Đại lý Hải quan (Customs Brokers)**; người dùng trực tiếp là **Nhân viên chứng từ (Documentation Ops) & Nhân viên Báo giá (Pricing Ops)** của chính doanh nghiệp đó để xử lý các bộ chứng từ vận tải (Bill of Lading, Invoice, Packing List, Tờ khai Hải quan), không có bên thứ ba trung gian sở hữu dữ liệu người dùng.

---

### Bảng đèn §3.2 (B2B) của loại mình — Đánh giá hiện trạng đo lường

| Đèn | ✅ / 🔧 / ❌ | Số nằm ở đâu / Cần gì để đo |
|---|---|---|
| **Time-to-first-value (TTFV)** | ✅ | Đo từ Timestamp ký hợp đồng/POC trong CRM (HubSpot) đến Timestamp khách upload & xác thực thành công bộ chứng từ đầu tiên trên hệ thống (Postgres Event Log). |
| **Pipeline coverage** | ✅ | Đo trong CRM: Tổng value các deal ở stage Qualified trở lên ÷ Quota doanh thu quý. |
| **% deal chết ở khâu security/procurement** | 🔧 | Cần gắn thêm trường "Lost Reason" chuẩn hóa trên CRM (phân loại: Security, IT Integration, Price, Ghosting) — 1 tuần cấu hình. |
| **POC → Paid conversion** | ✅ | Đo trên CRM: Số hợp đồng trả tiền đã ký ÷ Tổng số POC đã khởi động trong quý. |
| **Sales cycle (tuần)** | ✅ | Đo trên CRM: Thời gian từ khi tạo Deal Qualified đến khi Closed-Won. |
| **Usage depth trong tài khoản** | ✅ | Đo trên Product Analytics (PostHog): Số seats active hàng tuần có ≥5 actions ÷ Tổng số seats đã cấp phép. |
| **Chi phí triển khai ÷ ACV** | 🔧 | Cần bảng theo dõi giờ công Customer Success/AI Engineer tích hợp webhook/custom template cho mỗi khách nhân với đơn giá giờ ÷ ACV — 1 tuần chuẩn hóa sheet. |
| **Tập trung doanh thu** | ✅ | Đo từ phần mềm kế toán/Stripe: Doanh thu của khách hàng lớn nhất ÷ Tổng MRR/ARR. |
| **NRR (Net Revenue Retention)** | ❌ | Chưa đo được vì sản phẩm mới dưới 6 tháng vận hành; cần tối thiểu 12 tháng dữ liệu gia hạn và expansion/upsell. |
| **Gross Margin** | ✅ | Đo từ Báo cáo tài chính quản trị: (Doanh thu − Chi phí OpenAI/Anthropic/OCR API − Chi phí Cloud AWS) ÷ Doanh thu. |
| **CAC Payback** | 🔧 | Cần chốt phân bổ chi phí Marketing/Sales chia cho Lãi gộp ròng mỗi tháng để tính chính xác thời gian hoàn vốn — 2 tuần để khớp dữ liệu kế toán. |

---

## Trạm 2 — Thẻ đèn

**North Star:** **Số bộ chứng từ chuẩn hóa được xử lý thành công hàng tuần (Weekly Validated Document Packets - WVDP)** — Hiện tại: **1.200 bộ/tuần** — Mục tiêu Q4/2026: **5.000 bộ/tuần**.

| # | Tầng (L/O/G) | Đèn | Định nghĩa (Đếm gì · **KHÔNG** đếm gì) | Công thức | Nhịp · Ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | **L** | **Time-to-First-Value (TTFV)** ⭐ | Đếm số ngày từ khi ký HĐ/POC đến khi khách hàng nhận được bộ chứng từ đầu tiên được AI bóc tách & export thành công vào hệ thống nghiệp vụ (VNACCS/Excel/TMS) với độ chính xác >98%. **KHÔNG** đếm ngày tạo tài khoản test, không đếm tài khoản chỉ upload file mẫu của hệ thống. | `Ngày (First Validated Export) − Ngày (Signed Contract)` | Từng khách · Lead CS | POC → Paid (sau 4–6 tuần) và NRR (sau 12 tháng) |
| 2 | **L** | **Pipeline Coverage (SMB & Mid-Market)** | Đếm tổng giá trị ACV của các deal đã qua vòng Discovery & Demo thành công (Qualified Pipeline) chia cho target doanh thu quý. **KHÔNG** đếm các lead lạnh chỉ điền form website hoặc chưa xác nhận ngân sách. | `Tổng ACV Deals Qualified ÷ Target ACV Quý` | Hàng tuần · Head of Sales | Doanh thu mới & Sales Cycle (sau 8–12 tuần) |
| 3 | **O** | **POC → Paid Conversion Rate** | Đếm % khách hàng kết thúc giai đoạn POC chuyển đổi thành hợp đồng thuê bao trả phí chính thức. **KHÔNG** đếm các hợp đồng gia hạn POC thử nghiệm miễn phí. | `(Số POC Closed-Won) ÷ (Tổng số POC kết thúc trong kỳ) × 100%` | Hàng tháng · Head of Sales | Doanh thu ARR mới & CAC Payback (sau 1–2 quý) |
| 4 | **O** | **Chi phí AI Inference ÷ Doanh thu (AI Cost/Job Ratio)** 🤖 | Đếm tổng chi phí token LLM + API OCR phát sinh để xử lý toàn bộ jobs trong kỳ chia cho tổng doanh thu từ việc xử lý tài liệu. **KHÔNG** đếm chi phí máy chủ web app (AWS EC2 cơ bản), không đếm chi phí môi trường Dev/Staging. | `(Chi phí API LLM + OCR trong kỳ) ÷ (Doanh thu xử lý tài liệu trong kỳ) × 100%` | Hàng tuần · Lead AI Engineer | Gross Margin tầng Lagging (sau 1 quý) |
| 5 | **O** | **Chi phí triển khai & Onboarding ÷ ACV** | Đếm toàn bộ chi phí nhân công kỹ thuật + CS thiết lập template/mapping hệ thống riêng cho mỗi khách hàng chia cho Giá trị hợp đồng năm (ACV). **KHÔNG** đếm chi phí hỗ trợ ticket kỹ thuật thông thường sau khi đã go-live. | `(Tổng giờ công Onboarding × Đơn giá giờ 250.000đ) ÷ ACV` | Từng khách · Lead CS | Gross Margin & CAC Payback (sau 2 quý) |
| 6 | **O** | **Usage Depth (Tỷ lệ Active Seats)** | Đếm % nhân viên chứng từ được cấp tài khoản thực hiện xử lý ≥10 bộ chứng từ/tuần. **KHÔNG** đếm tài khoản Admin của ban giám đốc chỉ vào xem báo cáo tổng quan. | `(Số Seats active ≥10 jobs/tuần) ÷ (Tổng số Seats được cấp) × 100%` | Hàng tuần · Lead CS | Churn Rate & Account Expansion / NRR (sau 6–12 tháng) |
| 7 | **G** | **Gross Margin (Biên lợi nhuận gộp)** | Đếm doanh thu thuần trừ toàn bộ COGS (Cloud, OpenAI/Anthropic token, OCR, Server hosting, Nhân công hỗ trợ vận hành cấp 1). **KHÔNG** trừ chi phí R&D phần mềm lõi và chi phí Sales/Marketing. | `(Doanh thu thuần − COGS) ÷ Doanh thu thuần × 100%` | Hàng tháng/Quý · Kế toán trưởng | Runway & Lợi nhuận ròng (sau 2–4 quý) |

> **Đèn chi phí AI là đèn số:** **4 (Chi phí AI Inference ÷ Doanh thu / AI Cost per Job Ratio)**.

---

## Trạm 3 — Ngưỡng

| # | Đèn | 🟢 Xanh | 🟡 Vàng | 🔴 Đỏ | Nguồn | Lý do (1 câu) & Ngày kiểm tra |
|---|---|---|---|---|---|---|
| 1 | **Time-to-First-Value (TTFV)** ⭐ | < 7 ngày | 7–14 ngày | > 14 ngày | **[TB]** | Tự đo baseline: Sản phẩm bóc tách tài liệu nếu quá 14 ngày chưa export được file đầu tiên thì 80% khách bỏ cuộc trước khi hết hạn POC. |
| 2 | **Pipeline Coverage** | ≥ 3.5× | 2.5×–3.5× | < 2.5× | **[TB]** / **[BM]** | Với Win Rate mục tiêu 30% ở phân khúc Forwarder vừa và nhỏ, cần pipeline tối thiểu 3.3× (đặt 3.5× để có biên an toàn). Kiểm tra benchmark B2B: 27/08/2026. |
| 3 | **POC → Paid Conversion Rate** | ≥ 50% | 35%–50% | < 35% | **[BM]** | Benchmark ICONIQ State of GTM 2026 (kiểm tra 27/08/2026): Trung vị POC-to-paid của SaaS AI B2B đạt ~50% (tăng từ 36% năm 2025). |
| 4 | **Chi phí AI Inference ÷ Doanh thu** 🤖 | < 12% | 12%–18% | > 18% | **[MH]** | Suy từ mô hình Day 25: Giá gói $0.40/bộ chứng từ, chi phí AI (OCR + LLM) tối đa $0.048/bộ để giữ biên COGS AI an toàn bảo vệ Gross Margin ≥75%. |
| 5 | **Chi phí triển khai ÷ ACV** | < 10% | 10%–20% | > 20% | **[MH]** | Suy từ mô hình Day 24: Với ACV $4,800 (Mid-Market), chi phí onboarding không được vượt quá $720 (tương đương 72 giờ công) để đảm bảo Payback < 6 tháng. |
| 6 | **Usage Depth (% Seats Active)** | ≥ 65% | 40%–65% | < 40% | **[TB]** | Baseline nội bộ: Nếu <40% nhân viên chứng từ dùng AI sau 30 ngày go-live, khách hàng sẽ hạ gói (downgrade seats) khi tái ký hợp đồng năm. |
| 7 | **Gross Margin** | ≥ 75% | 65%–75% | < 65% | **[BM]** / **[MH]** | Target Day 24 cho SaaS B2B AI Workflow đạt 75% (neo theo benchmark Benchmarkit 2025: 77% và ICONIQ 2026: 53% AI-native, kiểm tra 27/08/2026). |

---

### Phụ lục [MH] — Phép tính chi tiết suy từ mô hình tài chính & Cost/Job (3 phép tính)

#### [MH] 1 — Ngưỡng Chi phí AI Inference ÷ Doanh thu (Đèn số 4)

* **Đầu vào (từ Unit Economics Day 25):**
  * Giá bán trung bình (ARPU): Gói Professional $300/tháng bao gồm 750 bộ chứng từ $\rightarrow$ Đơn giá $0.40$/bộ chứng từ.
  * Mỗi bộ chứng từ tiêu chuẩn gồm: 1 Bill of Lading (1 trang), 1 Commercial Invoice (2 trang), 1 Packing List (2 trang), 1 Tờ khai hải quan (2 trang) = 7 trang tài liệu PDF.
  * Kiến trúc AI Pipeline: OCR Vision trích xuất text/table ($0.0015$/trang $\times$ 7 = $0.0105$) + LLM Schema Mapping (Prompt + Completion: 4.000 tokens input + 1.500 tokens output qua Claude 3.5 Sonnet / GPT-4o mini: ~$0.025/lần) + Validation retry rate 15% ($0.005$) $\rightarrow$ **Cost per Job cơ sở = $0.0405$/bộ chứng từ**.
  * Mục tiêu Gross Margin của toàn sản phẩm $\ge 75\%$, trong đó trần ngân sách cho toàn bộ COGS AI (Inference + OCR API) là $\le 15\%$ doanh thu.

* **Phép tính suy ngược:**
  $$\text{Tỷ lệ Chi phí AI} = \frac{\text{Cost per Job}}{\text{Đơn giá doanh thu per Job}} = \frac{\$0.0405}{\$0.4000} = 10.125\%$$
  * Ngưỡng Xanh (🟢): $< 12\%$ (Chi phí AI $\le \$0.048$/bộ chứng từ, biên gộp AI $\ge 88\%$).
  * Ngưỡng Vàng (🟡): $12\% - 18\%$ (Chi phí AI từ $\$0.048 - \$0.072$/bộ chứng từ $\rightarrow$ do tài liệu phức tạp, retry nhiều hoặc model fallback).
  * Ngưỡng Đỏ (🔴): $> 18\%$ (Chi phí AI $> \$0.072$/bộ chứng từ $\rightarrow$ ăn mòn Gross Margin mục tiêu, đe dọa bài toán tài chính).

---

#### [MH] 2 — Ngưỡng Chi phí Triển khai & Onboarding ÷ ACV (Đèn số 5)

* **Đầu vào (từ Mô hình tài chính Day 24):**
  * Phân khúc khách hàng mục tiêu: Freight Forwarders quy mô vừa (Mid-Market) có ACV = $4,800/năm ($400/tháng).
  * Mục tiêu CAC Payback $\le 6$ tháng.
  * Tỷ suất Lãi gộp (Gross Margin) = $75\% \rightarrow$ Lãi gộp hàng tháng $= \$400 \times 75\% = \$300/\text{tháng}$.
  * Tổng ngân sách CAC tối đa $= \$300 \times 6 = \$1,800$.
  * Trong đó, cơ cấu chi phí CAC: Sales & Marketing chiếm $60\%$ ($\$1,080$), Chi phí Triển khai kỹ thuật & Onboarding (CS/Solutions Engineer) chiếm tối đa $40\%$ ($\$720$).
  * Đơn giá giờ công triển khai của Solutions Engineer / Onboarding Specialist: $250.000\text{đ} \approx \$10/\text{giờ}$.

* **Phép tính suy ngược:**
  $$\text{Chi phí triển khai tối đa cho phép} = \$720 \text{ (tương đương } 72 \text{ giờ công)}$$
  $$\text{Tỷ lệ Chi phí triển khai ÷ ACV} = \frac{\$720}{\$4,800} = 15.0\%$$
  * Ngưỡng Xanh (🟢): $< 10\%$ (Chi phí triển khai $\le \$480 \approx 48$ giờ công $\rightarrow$ Onboarding mượt mà, self-serve template tốt, Payback rút ngắn còn $<4.5$ tháng).
  * Ngưỡng Vàng (🟡): $10\% - 20\%$ (Chi phí triển khai từ $\$480 - \$960 \approx 48 - 96$ giờ công $\rightarrow$ Cần theo dõi các khâu custom mapping kéo dài).
  * Ngưỡng Đỏ (🔴): $> 20\%$ (Chi phí triển khai $> \$960 \approx 96$ giờ công $\rightarrow$ Biến sản phẩm thành "dịch vụ outsource gia công", phá vỡ trần Payback 6 tháng).

---

#### [MH] 3 — Ngưỡng Thời gian Hoàn vốn CAC Payback (Đèn số 7 phụ trợ)

* **Đầu vào (từ Mô hình tài chính Day 24 & Runway):**
  * Runway hiện tại của công ty: 14 tháng.
  * Chu kỳ bán hàng B2B (Sales Cycle): 8 tuần ($\approx 2$ tháng).
  * Thời gian an toàn còn lại để tái đầu tư tăng trưởng: $14 - 2 = 12$ tháng.
  * Để đạt hiệu quả vốn và duy trì tăng trưởng bền vững, thời gian thu hồi chi phí bán hàng (CAC Payback) không được chiếm quá 50% thời gian an toàn còn lại ($\le 6$ tháng).

* **Phép tính suy ngược:**
  $$\text{CAC Payback tối đa cho phép} = \frac{\text{CAC}}{\text{ARPU} \times \text{Gross Margin}} = \frac{\$1,800}{\$400 \times 75\%} = \frac{\$1,800}{\$300} = 6.0 \text{ tháng}$$
  * Ngưỡng Xanh (🟢): $< 6.0$ tháng (Thu hồi vốn nhanh, tối ưu dòng tiền).
  * Ngưỡng Vàng (🟡): $6.0 - 9.0$ tháng (Chấp nhận được đối với deal Mid-Market quy mô lớn).
  * Ngưỡng Đỏ (🔴): $> 9.0$ tháng (Vượt ngưỡng an toàn, đe dọa làm cạn kiệt Runway trước khi đạt điểm hòa vốn).

---

## Trạm 4 — 5 Luật Quyết định

> Đánh dấu **⏹** cho luật DỪNG (có 2 luật dừng bắt buộc).

1. ⏹ **[LUẬT DỪNG - TRIỂN KHAI]**  
   **NẾU** Time-to-First-Value (TTFV) $> 14$ ngày  
   **TRÊN** 3 khách hàng POC liên tiếp  
   **THÌ** đóng băng toàn bộ hoạt động nhận POC mới trong 2 tuần, cắt phạm vi thử nghiệm xuống đúng 1 loại chứng từ duy nhất (Bill of Lading đường biển) cho 1 phòng ban chứng từ duy nhất để tối ưu quy trình onboarding  
   **KHÔNG THÌ** không được tuyển thêm Sales B2B để nạp thêm khách vào phễu đang tắc.

2. ⏹ **[LUẬT DỪNG - ĐƠN GIÁ & CHI PHÍ AI]**  
   **NẾU** Chi phí AI Inference ÷ Doanh thu $> 18\%$  
   **TRONG** 2 tuần liên tiếp  
   **VÀ** tổng số chứng từ xử lý $\ge 2.000$ bộ  
   **THÌ** dừng ngay việc xử lý các file scan chất lượng thấp (mờ/nghiêng) bằng model LLM đắt tiền, chuyển sang quy trình OCR cục bộ và áp dụng trần token per packet  
   **KHÔNG THÌ** không được tự động giảm giá bán gói cước để thu hút thêm volume bù đắp doanh thu.

3. **[LUẬT TỐI ƯU HÓA CHI PHÍ ONBOARDING]**  
   **NẾU** Chi phí triển khai $\div$ ACV $> 20\%$  
   **TRÊN** 3 hợp đồng liên tiếp  
   **THÌ** đóng gói chuẩn hóa toàn bộ các trường dữ liệu tùy biến thành 5 bộ template mẫu cho khách hàng tự cấu hình (Self-serve Mapping UI) trong sprint tiếp theo  
   **KHÔNG THÌ** không được ký thêm các phụ lục cam kết "viết code tùy biến miễn phí" (custom development) cho khách hàng mới.

4. **[LUẬT CỨU VÃN CHURN SỚM]**  
   **NẾU** Usage Depth (Tỷ lệ Active Seats) $< 40\%$  
   **TRONG** 30 ngày đầu sau khi go-live bàn giao hệ thống  
   **THÌ** cử trực tiếp 1 Chuyên viên Customer Success đến tận văn phòng khách hàng đào tạo lại quy trình thao tác và phỏng vấn rào cản thao tác của nhân viên chứng từ trong vòng 5 ngày làm việc  
   **KHÔNG THÌ** không được gửi email chào bán thêm module Báo giá (Quotation Module) hoặc đề xuất nâng gói người dùng.

5. **[LUẬT XỬ LÝ NGHẼN PHỄU CHUYỂN ĐỔI POC]**  
   **NẾU** Tỷ lệ POC $\rightarrow$ Paid Conversion $< 35\%$  
   **TRONG** 1 quý  
   **VÀ** tổng số POC đã hoàn thành $\ge 6$ khách  
   **THÌ** dừng đàm phán thương mại riêng lẻ, rà soát lại Evidence Pack (bản báo cáo đối soát độ chính xác thực tế và số giờ làm việc tiết kiệm được) gửi thẳng cho Giám đốc Điều hành (CEO/Managing Director) của khách hàng  
   **KHÔNG THÌ** không được giảm giá hợp đồng quá 15% để cố ép chốt deal khi khách chưa nhìn thấy giá trị đo lường được.

---

## Trạm 5 — Cổng gác 90 ngày

| Cổng | Metric gác cổng (Đúng 1 metric) | Ngưỡng qua cổng | Bằng chứng vật lý | Quyết định nếu trượt |
|---|---|---|---|---|
| **Ngày 30** | Tỷ lệ bóc tách chính xác của Evidence Pack v1 | $\ge 98\%$ trên mẫu $\ge 50$ chứng từ thật của $\ge 3$ khách hàng POC | File Báo cáo đối soát Benchmark Accuracy ký xác nhận giữa 2 bên | **FIX:** Cải tiến prompt/parser cho 1 dạng chứng từ chính trong 30 ngày. (Trượt lần 2 $\rightarrow$ **PIVOT**) |
| **Ngày 60** | Time-to-First-Value (TTFV) | $\ge 3$ khách hàng POC đạt TTFV $< 7$ ngày (tự trích xuất & export thành công bộ chứng từ đầu tiên) | Log Audit Event trên hệ thống (Timestamp Signed vs First Valid Export) | **PIVOT:** Đổi từ Web Portal sang Chrome Extension / Nhúng Email Parser nếu khách ngại đăng nhập portal riêng. |
| **Ngày 90** | Hợp đồng trả tiền chính thức (Paid Accounts) & POC Conversion | $\ge 3$ hợp đồng trả tiền chính thức ký mới với tổng ARR $\ge \$10,800$ ($\ge \$300$/tháng/khách) **VÀ** POC $\rightarrow$ Paid $\ge 50\%$ | Bản hợp đồng kinh tế có chữ ký số + Hóa đơn VAT kỳ đầu tiên đã thanh toán | **KILL:** Đóng dự án nếu sau 90 ngày không có nổi 2 khách trả tiền hoặc POC $\rightarrow$ Paid $< 25\%$. |

### KILL CRITERIA
> **Nếu sau 90 ngày kể từ ngày khởi động (tới ngày 09/01/2027), dự án không có ít nhất 2 khách hàng Forwarder trả phí chính thức với ACV $\ge \$3,600$ và POC-to-Paid conversion $< 30\%$, toàn bộ dự án sẽ dừng lại để bảo toàn vốn.**

### CHƯA ĐO ĐƯỢC
> **NRR (Net Revenue Retention) và Churn Rate hàng năm:** Hiện tại sản phẩm mới triển khai dưới 6 tháng nên chưa đủ chu kỳ 12 tháng để tính toán NRR và tỷ lệ tái ký hợp đồng năm.  
> * **Cần gì để đo:** Cần hệ thống theo dõi hóa đơn định kỳ (Stripe Billing / Phần mềm kế toán) và thời gian vận hành tối thiểu 12 tháng.  
> * **Khi nào có số:** Dự kiến có số liệu NRR sơ bộ chu kỳ 6 tháng vào ngày **09/04/2027** và đủ số liệu chu kỳ 12 tháng vào ngày **09/10/2027**.
