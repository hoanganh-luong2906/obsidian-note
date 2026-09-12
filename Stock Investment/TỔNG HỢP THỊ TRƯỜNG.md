
# PHẦN I — KHUNG LÝ THUYẾT

## 1. Chu kỳ 4 giai đoạn

Ghi chú gốc viết: _Giảm giá → Tích luỹ → Tăng giá → Phân phối → Giảm giá_. Đây chính là mô hình **Stage Analysis** của Stan Weinstein và mô hình chu kỳ của Wyckoff. Cần lưu ý cách đánh số chuẩn quốc tế bắt đầu từ **tích luỹ**, không phải từ giảm giá:

| Ghi chú gốc | Weinstein               | Wyckoff      | Đặc điểm MA200                    |
| ----------- | ----------------------- | ------------ | --------------------------------- |
| Tích luỹ    | **Stage 1** — Basing    | Accumulation | Đi ngang, phẳng dần               |
| Tăng giá    | **Stage 2** — Advancing | Markup       | Dốc lên, giá nằm trên             |
| Phân phối   | **Stage 3** — Top       | Distribution | Đi ngang trở lại, giá cắt qua lại |
| Giảm giá    | **Stage 4** — Declining | Markdown     | Dốc xuống, giá nằm dưới           |

**Công cụ xác định giai đoạn nhanh nhất (Weinstein):** độ dốc của MA200 (hoặc MA30 tuần) + vị trí giá so với MA200.

- MA200 phẳng + giá dao động quanh nó → Stage 1 hoặc Stage 3. Phân biệt bằng **giai đoạn trước đó**: trước là giảm → Stage 1; trước là tăng → Stage 3.
- MA200 dốc lên + giá trên MA200 → Stage 2. Đây là giai đoạn duy nhất nên nắm giữ vị thế mua.
- MA200 dốc xuống + giá dưới MA200 → Stage 4. Tuyệt đối không "bắt đáy" ở đây.

> **Điểm quan trọng nhất của cả mô hình:** phần lớn lợi nhuận nằm ở Stage 2, nhưng phần lớn thời gian thị trường nằm ở Stage 1 và Stage 3. Kiên nhẫn không phải là đức tính — nó là điều kiện toán học.

<svg viewBox="0 0 900 600" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, -apple-system, Segoe UI, sans-serif"> <line x1="230" y1="58" x2="230" y2="340" stroke="#94a3b8" stroke-width="1" stroke-dasharray="4 4"/> <line x1="400" y1="58" x2="400" y2="340" stroke="#94a3b8" stroke-width="1" stroke-dasharray="4 4"/> <line x1="570" y1="58" x2="570" y2="340" stroke="#94a3b8" stroke-width="1" stroke-dasharray="4 4"/> <line x1="740" y1="58" x2="740" y2="340" stroke="#94a3b8" stroke-width="1" stroke-dasharray="4 4"/>

<text x="145" y="28" text-anchor="middle" font-size="13.5" font-weight="600" fill="#dc2626">GIẢM GIÁ</text> <text x="145" y="45" text-anchor="middle" font-size="10.5" fill="#94a3b8">Stage 4 · Markdown</text> <text x="315" y="28" text-anchor="middle" font-size="13.5" font-weight="600" fill="#2563eb">TÍCH LUỸ</text> <text x="315" y="45" text-anchor="middle" font-size="10.5" fill="#94a3b8">Stage 1 · Accumulation</text> <text x="485" y="28" text-anchor="middle" font-size="13.5" font-weight="600" fill="#16a34a">TĂNG GIÁ</text> <text x="485" y="45" text-anchor="middle" font-size="10.5" fill="#94a3b8">Stage 2 · Markup</text> <text x="655" y="28" text-anchor="middle" font-size="13.5" font-weight="600" fill="#ea580c">PHÂN PHỐI</text> <text x="655" y="45" text-anchor="middle" font-size="10.5" fill="#94a3b8">Stage 3 · Distribution</text> <text x="805" y="28" text-anchor="middle" font-size="13" font-weight="600" fill="#dc2626">GIẢM GIÁ</text> <text x="805" y="45" text-anchor="middle" font-size="10.5" fill="#94a3b8">Stage 4</text>

<!-- MA200 -->

<polyline fill="none" stroke="#a855f7" stroke-width="1.8" stroke-dasharray="6 3" stroke-linejoin="round" points="60,80 100,112 140,158 180,215 210,255 230,272 260,288 290,296 320,301 350,303 380,301 400,298 430,292 460,278 490,260 520,240 550,222 570,210 600,190 630,172 660,158 690,148 715,143 740,141 770,142 800,148 830,158 860,172"/> <text x="112" y="100" font-size="10.5" fill="#a855f7" font-weight="600">MA200</text>

<!-- price -->

<polyline fill="none" stroke="#dc2626" stroke-width="2.4" stroke-linejoin="round" points="60,100 95,140 85,160 130,215 120,235 165,275 155,290 200,312 215,296 230,300"/> <polyline fill="none" stroke="#2563eb" stroke-width="2.4" stroke-linejoin="round" points="230,300 255,285 280,305 305,288 330,308 352,316 365,292 380,300 400,292"/> <polyline fill="none" stroke="#16a34a" stroke-width="2.4" stroke-linejoin="round" points="400,292 435,245 425,262 465,215 455,232 495,180 485,198 525,150 515,165 555,125 570,130"/> <polyline fill="none" stroke="#ea580c" stroke-width="2.4" stroke-linejoin="round" points="570,130 595,108 615,138 640,112 665,140 690,104 705,138 715,142 740,125"/> <polyline fill="none" stroke="#dc2626" stroke-width="2.4" stroke-linejoin="round" points="740,125 770,165 760,180 795,220 785,235 820,270 860,255"/>

<!-- event markers --> <circle cx="200" cy="312" r="4" fill="#dc2626"/> <text x="196" y="333" text-anchor="middle" font-size="10" fill="#dc2626">Bán tháo đỉnh điểm</text> <circle cx="352" cy="316" r="4" fill="#2563eb"/> <text x="352" y="337" text-anchor="middle" font-size="10" fill="#2563eb">Test lại đáy, vol cạn</text> <circle cx="400" cy="292" r="4.5" fill="#16a34a"/> <text x="410" y="285" font-size="10" fill="#16a34a" font-weight="600">Điểm mua (pivot)</text> <circle cx="595" cy="108" r="4" fill="#ea580c"/> <text x="585" y="98" text-anchor="end" font-size="10" fill="#ea580c">Mua đỉnh điểm</text> <circle cx="690" cy="104" r="4" fill="#ea580c"/> <text x="700" y="96" font-size="10" fill="#ea580c">Đỉnh giả, vol lớn</text> <text x="472" y="205" text-anchor="middle" font-size="10" fill="#16a34a" transform="rotate(-38 472 205)">nhịp sau ≈ nhịp đầu</text> <!-- rule boxes --> <rect x="26" y="382" width="196" height="188" rx="8" fill="none" stroke="#dc2626" stroke-width="1.3"/> <text x="40" y="406" font-size="12.5" font-weight="600" fill="#dc2626">Giảm giá — không mua</text> <text x="40" y="430" font-size="11" fill="#475569">• MA200 dốc xuống</text> <text x="40" y="451" font-size="11" fill="#475569">• Vol bán còn lớn</text> <text x="40" y="472" font-size="11" fill="#475569">• Nhóm chu kỳ phải thủng</text> <text x="48" y="489" font-size="11" fill="#475569">đáy mới hết cung</text> <text x="40" y="510" font-size="11" fill="#475569">• "Tạo nền" ≠ đủ thấp</text> <text x="40" y="531" font-size="11" fill="#475569">• Hồi kỹ thuật ≠ đảo chiều</text> <text x="40" y="552" font-size="11" fill="#475569">• Rủi ro: bắt dao rơi</text> <rect x="248" y="382" width="196" height="188" rx="8" fill="none" stroke="#2563eb" stroke-width="1.3"/> <text x="262" y="406" font-size="12.5" font-weight="600" fill="#2563eb">Tích luỹ — chuẩn bị</text> <text x="262" y="430" font-size="11" fill="#475569">• MA200 phẳng dần</text> <text x="262" y="451" font-size="11" fill="#475569">• Ngưng giảm 2–3 phiên</text> <text x="262" y="472" font-size="11" fill="#475569">• Vol bán cạn (VDU)</text> <text x="262" y="493" font-size="11" fill="#475569">• Tin xấu mà không giảm</text> <text x="262" y="514" font-size="11" fill="#475569">• Biên độ nén dần (VCP)</text> <text x="262" y="535" font-size="11" fill="#475569">• Lập watchlist, chờ pivot</text> <text x="262" y="556" font-size="11" fill="#475569">• Chưa vào toàn bộ vị thế</text> <rect x="470" y="382" width="196" height="188" rx="8" fill="none" stroke="#16a34a" stroke-width="1.3"/> <text x="484" y="406" font-size="12.5" font-weight="600" fill="#16a34a">Tăng giá — nắm giữ</text> <text x="484" y="430" font-size="11" fill="#475569">• MA200 dốc lên</text> <text x="484" y="451" font-size="11" fill="#475569">• Breakout kèm vol lớn</text> <text x="484" y="472" font-size="11" fill="#475569">• Ưu tiên cổ dẫn đầu</text> <text x="484" y="493" font-size="11" fill="#475569">• Mã không giảm khi</text> <text x="492" y="510" font-size="11" fill="#475569">thị trường rũ hàng</text> <text x="484" y="531" font-size="11" fill="#475569">• Điều chỉnh về MA20/50</text> <text x="492" y="548" font-size="11" fill="#475569">vol thấp = mua thêm</text> <rect x="692" y="382" width="196" height="188" rx="8" fill="none" stroke="#ea580c" stroke-width="1.3"/> <text x="706" y="406" font-size="12.5" font-weight="600" fill="#ea580c">Phân phối — thoát</text> <text x="706" y="430" font-size="11" fill="#475569">• Vol lớn, giá đứng yên</text> <text x="706" y="451" font-size="11" fill="#475569">• Tin tốt mà không tăng</text> <text x="706" y="472" font-size="11" fill="#475569">• Đỉnh sau không cao hơn</text> <text x="706" y="493" font-size="11" fill="#475569">• Sóng hồi = phân phối nốt</text> <text x="706" y="514" font-size="11" fill="#475569">• Điều chỉnh "quá đẹp",</text> <text x="714" y="531" font-size="11" fill="#475569">bán quá ít → cảnh giác</text> <text x="706" y="552" font-size="11" fill="#475569">• Mất MA50 = tín hiệu</text> </svg>

**Nguyên tắc đọc sơ đồ:** vị trí trong chu kỳ quyết định ý nghĩa của tín hiệu. Cùng một cây nến, cùng một mức volume, ở Stage 1 và Stage 3 nói hai điều ngược nhau.

---

## 2. Khung phân tích 4 tầng

Bài học lớn nhất của Lesson 2: **không tầng nào tự nó đủ để ra quyết định mua**. Áp dụng theo thứ tự từ trên xuống (top-down).

|#|Tầng|Trả lời câu hỏi|Cho biết|KHÔNG cho biết|Dữ liệu ở đâu|
|---|---|---|---|---|---|
|1|**Vĩ mô**|Bối cảnh nền kinh tế thế nào?|Lãi suất, tỷ giá, lạm phát, tăng trưởng tín dụng, đầu tư công|Điểm vào, mã cụ thể|GSO, NHNN, báo cáo CTCK|
|2|**Chính sách**|Có sự kiện cấu trúc nào không?|Nâng hạng, thay đổi quy định, thuế, room ngoại|Thời điểm chính xác|Thông tư/Nghị định, UBCKNN|
|3|**Dòng tiền**|Tiền đang chảy vào đâu? Thị trường nghĩ gì về mã này?|Nhóm ngành dẫn dắt, khối ngoại, tự doanh, thanh khoản|Xu hướng dài hạn|Fireant, Vietstock|
|4|**Kỹ thuật**|Giá đang ở đâu trong xu hướng?|Giai đoạn chu kỳ, vùng cản/hỗ trợ, điểm vào, điểm cắt lỗ|Lý do đằng sau chuyển động|TradingView|

> **Chốt lại từ ghi chú gốc:** nến + trendline chỉ trả lời "xu hướng ngắn hạn là gì" — **chưa đủ cơ sở để tìm điểm mua**. Phải cộng dòng tiền (bối cảnh, tâm lý) và vĩ mô (góc nhìn ngành). Thiếu một tầng quan trọng = mất tiền trực tiếp. Đây chính xác là cái đã xảy ra với PNJ.

**Bổ sung:** ba tầng đầu trả lời câu hỏi **"MUA GÌ"**, tầng thứ tư trả lời **"MUA KHI NÀO"**. Lẫn lộn hai câu hỏi này là nguồn gốc của phần lớn sai lầm — thấy một mã tốt về cơ bản rồi mua ngay bất kể vị trí kỹ thuật.

---

# PHẦN II — BỐI CẢNH THỊ TRƯỜNG

## 3. Câu chuyện nâng hạng — dữ kiện cập nhật

Ghi chú gốc: _"Nâng hạng là tín hiệu tích cực cho thị trường trong trung/dài hạn"_ và _"tập trung vào những cổ lớn (danh sách nâng hạng)"_. Bổ sung dữ kiện thực tế để hiểu tại sao lại là **trung/dài hạn** chứ không phải tín hiệu mua ngắn hạn.

### Mốc thời gian

|Thời điểm|Sự kiện|
|---|---|
|07–08/10/2025|FTSE Russell công bố nâng hạng Việt Nam: Cận biên → **Mới nổi thứ cấp** (Secondary Emerging)|
|03/2026|Kỳ rà soát giữa kỳ — tái khẳng định lộ trình|
|21/08/2026|Công bố danh sách: **27 mã** vào FTSE All-Cap, **6 mã** vào FTSE All-World, 90 mã Micro Cap (tổng 117 mã trong FTSE Total-Cap)|
|05/09/2026|Hoàn tất kỳ rà soát, danh sách 27 mã giữ nguyên|
|07/09/2026|Danh mục chính thức|
|**18/09/2026**|**Giao dịch cơ cấu của quỹ chỉ số hoàn tất sau phiên này**|
|**21/09/2026**|**Ngày hiệu lực nâng hạng**|
|Đến 09/2027|Hoàn tất lộ trình đưa vào chỉ số qua nhiều đợt|

### 27 mã trong FTSE Global All Cap

|Nhóm|Mã|
|---|---|
|**Large Cap**|VCB, VIC, VHM|
|**Mid Cap**|BID, HPG, VPB|
|**Small Cap (21 mã)**|FPT, GEX, HDB, HCM, MCH, MSN, NVL, STB, SHB, MSB, VCK, TCX, …|

_(Danh sách Small Cap cần tra cứu lại đầy đủ trên Vietstock/công bố FTSE trước khi dùng làm watchlist.)_

### Cơ chế dòng tiền thụ động — chi tiết quan trọng nhất

**Việc đưa vào chỉ số chia theo nhiều đợt, không phải một lần.** Đợt đầu tháng 9/2026 chỉ áp dụng **10% tỷ trọng có thể đầu tư**.

|Nguồn ước tính|Con số|
|---|---|
|SSI Research — đợt đầu 09/2026|~145 triệu USD|
|SSI Research — kịch bản cơ sở (tỷ trọng 0,49%, 4 đợt)|~2,21 tỷ USD tích luỹ|
|SSI Research — kịch bản lạc quan (tỷ trọng lên 0,95% vào 09/2027)|~4,28 tỷ USD|
|Vietcap Securities — tổng tiềm năng|~78.900 tỷ đồng (~3 tỷ USD)|

> ⚠️ **Đây là chỗ dễ hiểu sai nhất.** Con số headline "vài tỷ USD" là **tổng của cả lộ trình kéo dài đến 09/2027**. Dòng tiền thực tế vào trong tháng 9/2026 chỉ khoảng 145 triệu USD — rất nhỏ so với thanh khoản hằng ngày của HOSE. Kỳ vọng ngắn hạn và dòng tiền thực tế lệch nhau rất xa.

### Hàm ý giao dịch

1. **"Buy the rumor, sell the news".** Kỳ vọng nâng hạng đã được phản ánh vào giá từ tháng 10/2025. Giao dịch cơ cấu của quỹ chỉ số **hoàn tất sau phiên 18/09** — tức là lực mua cơ học kết thúc **trước** ngày hiệu lực 21/09, không phải sau. Rủi ro "tin ra là bán" quanh mốc này là có thật.
2. **Vào rổ ≠ tăng giá.** Theo Vietstock, trong 27 mã được chọn, chỉ **9 mã** từng lập kỷ lục giá tính từ đầu 2026. VCK và TCX đã giảm khoảng 23% và 26% từ đỉnh. Nằm trong danh sách là điều kiện cần, không phải điều kiện đủ.
3. **Đây là câu chuyện cấu trúc, không phải câu chuyện nhịp sóng.** Lợi ích thật nằm ở: thanh khoản dài hạn tăng, định giá cải thiện, nền nhà đầu tư tổ chức mở rộng — tất cả đều tính bằng năm.
4. **Danh sách 27 mã vẫn hữu ích** — nhưng dùng làm **bộ lọc thu hẹp watchlist**, sau đó vẫn phải chạy qua đủ 4 tầng phân tích và xác nhận vị trí kỹ thuật.

### Ghi chú so sánh: FTSE ≠ MSCI

Đây là hai tổ chức xếp hạng độc lập với bộ tiêu chí khác nhau. Được FTSE nâng hạng **không** tự động kéo theo MSCI. Quy mô tài sản tham chiếu MSCI Emerging Markets lớn hơn đáng kể, nên nếu MSCI nâng hạng trong tương lai thì đó là một câu chuyện riêng, quy mô khác.

---

## 4. Trạng thái thị trường hiện tại

|Yếu tố|Nội dung|Hàm ý|
|---|---|---|
|Sóng cuối năm|**Phân hoá**: nền tảng vững + dẫn dắt → tăng; không đủ lực → giảm|Không mua "theo thị trường", phải chọn mã|
|Nhịp rũ|Sẽ có một nhịp rũ **trước** khi thực sự vào sóng tăng|Vào sớm = ăn trọn nhịp rũ|
|Vị trí|Đang rung lắc tại vùng cản|Giai đoạn quan sát, chưa phải giai đoạn hành động|
|Khối ngoại|Tâm lý thận trọng quanh mốc chuyển hạng|Chưa có lực đỡ rõ ràng|

**Bổ sung — cách đo "phân hoá" cho khách quan:** dùng **độ rộng thị trường (market breadth)** thay vì cảm nhận.

- Số mã tăng / số mã giảm trên HOSE (advance–decline).
- Tỷ lệ số mã nằm trên MA50 và MA200 của toàn sàn.
- **Dấu hiệu phân hoá xấu:** VN-Index tăng nhưng số mã giảm nhiều hơn số mã tăng → chỉ số bị kéo bởi vài mã vốn hoá lớn, phần còn lại đang yếu đi. Đây là tín hiệu cảnh báo sớm cho toàn thị trường.

---

# PHẦN III — KỸ NĂNG ĐỌC

## 5. Khối lượng — ma trận đầy đủ

Ghi chú gốc viết _"Thanh khoản cao → dấu hiệu bán tháo"_. **Câu này chỉ đúng một nửa** và là lỗi kiến thức cần sửa ngay. Khối lượng **không có ý nghĩa độc lập** — nó chỉ có ý nghĩa khi đọc **kèm hướng giá** và **kèm vị trí trong chu kỳ**.

<svg viewBox="0 0 760 430" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, -apple-system, Segoe UI, sans-serif"> <rect x="120" y="55" width="600" height="300" rx="6" fill="none" stroke="#94a3b8" stroke-width="1.2"/> <line x1="420" y1="55" x2="420" y2="355" stroke="#94a3b8" stroke-width="1.2"/> <line x1="120" y1="205" x2="720" y2="205" stroke="#94a3b8" stroke-width="1.2"/>

<text x="420" y="30" text-anchor="middle" font-size="13" font-weight="600" fill="#475569">KHỐI LƯỢNG (so với TB 20 phiên)</text> <text x="270" y="48" text-anchor="middle" font-size="11.5" fill="#94a3b8">THẤP</text> <text x="570" y="48" text-anchor="middle" font-size="11.5" fill="#94a3b8">CAO</text> <text x="60" y="205" text-anchor="middle" font-size="13" font-weight="600" fill="#475569" transform="rotate(-90 60 205)">GIÁ</text> <text x="103" y="130" text-anchor="end" font-size="11.5" fill="#94a3b8">TĂNG</text> <text x="103" y="285" text-anchor="end" font-size="11.5" fill="#94a3b8">GIẢM</text>

<text x="270" y="95" text-anchor="middle" font-size="12.5" font-weight="600" fill="#ea580c">Tăng yếu</text> <text x="270" y="120" text-anchor="middle" font-size="11" fill="#475569">Thiếu xác nhận của dòng tiền</text> <text x="270" y="141" text-anchor="middle" font-size="11" fill="#475569">Thường là hồi kỹ thuật</text> <text x="270" y="162" text-anchor="middle" font-size="11" fill="#475569">hoặc kéo xả</text> <text x="270" y="187" text-anchor="middle" font-size="11" font-weight="600" fill="#ea580c">→ Không đuổi giá</text>

<text x="570" y="95" text-anchor="middle" font-size="12.5" font-weight="600" fill="#16a34a">Dòng tiền vào thật</text> <text x="570" y="120" text-anchor="middle" font-size="11" fill="#475569">Breakout khỏi nền, hoặc</text> <text x="570" y="141" text-anchor="middle" font-size="11" fill="#475569">bùng nổ theo đà</text> <text x="570" y="166" text-anchor="middle" font-size="10.5" fill="#94a3b8">(nếu ở đỉnh dài hạn:</text> <text x="570" y="182" text-anchor="middle" font-size="10.5" fill="#94a3b8">có thể là mua đỉnh điểm)</text> <text x="570" y="196" text-anchor="middle" font-size="11" font-weight="600" fill="#16a34a">→ Điểm mua</text>

<text x="270" y="245" text-anchor="middle" font-size="12.5" font-weight="600" fill="#2563eb">Cung cạn</text> <text x="270" y="270" text-anchor="middle" font-size="11" fill="#475569">Điều chỉnh lành mạnh,</text> <text x="270" y="291" text-anchor="middle" font-size="11" fill="#475569">không ai muốn bán rẻ</text> <text x="270" y="312" text-anchor="middle" font-size="11" fill="#475569">Nền giá đang hình thành</text> <text x="270" y="337" text-anchor="middle" font-size="11" font-weight="600" fill="#2563eb">→ Đưa vào watchlist</text>

<text x="570" y="245" text-anchor="middle" font-size="12.5" font-weight="600" fill="#dc2626">Bán tháo / Phân phối</text> <text x="570" y="270" text-anchor="middle" font-size="11" fill="#475569">Cung áp đảo cầu</text> <text x="570" y="291" text-anchor="middle" font-size="11" fill="#475569">Tổ chức đang thoát hàng</text> <text x="570" y="316" text-anchor="middle" font-size="10.5" fill="#94a3b8">(nếu ở đáy dài hạn: có thể</text> <text x="570" y="332" text-anchor="middle" font-size="10.5" fill="#94a3b8">là bán tháo đỉnh điểm)</text> <text x="570" y="348" text-anchor="middle" font-size="11" font-weight="600" fill="#dc2626">→ Đứng ngoài</text>

<text x="120" y="390" font-size="11" fill="#94a3b8">Cùng một mức volume có thể mang ý nghĩa ngược nhau tuỳ vị trí trong chu kỳ — luôn đọc kèm hướng giá và giai đoạn.</text> </svg>

### Bảng tình huống thực chiến

|#|Giá|Khối lượng|Diễn giải|Hành động|
|---|---|---|---|---|
|1|Giảm mạnh|Vol **cao**|Bán tháo, cung áp đảo|Đứng ngoài|
|2|Ngưng giảm 2–3 phiên|Vol **thấp dần**|Cung cạn → sắp chạm đáy|Đưa vào vùng theo dõi|
|3|Tăng rồi điều chỉnh **"quá đẹp"**|Vol bán rất thấp|Chưa rũ được hàng yếu, hàng kẹt còn nguyên|Cảnh giác — dễ đảo chiều|
|4|Thị trường rũ mạnh, mã **không giảm**|—|Sức mạnh tương đối|Ưu tiên theo dõi|
|5|**Vượt nền**|Vol **cao** (≥1,5× TB20)|Breakout có xác nhận|Điểm mua chuẩn|
|6|Tăng|Vol **thấp**|Thiếu xác nhận, dễ là hồi kỹ thuật|Không đuổi giá|
|7|Đứng yên tại đỉnh|Vol **rất cao**|Có cung hấp thụ toàn bộ lực mua|Dấu hiệu phân phối|

### Ba khái niệm cần nắm chính xác

**a) Effort vs Result (Wyckoff).** Khối lượng là _nỗ lực_, biến động giá là _kết quả_. Khi nỗ lực lớn (vol cao) mà kết quả nhỏ (giá đứng yên) → có một lực đối kháng đang hấp thụ. Ở đỉnh = phân phối. Ở đáy = tích luỹ. **Đây là công cụ mạnh nhất để đọc dấu chân tổ chức.**

**b) Volume Dry-Up (VDU).** Trong nền giá, khối lượng cạn dần xuống dưới trung bình là dấu hiệu **cung đã cạn kiệt** — tiền đề của breakout. Đây chính là cái ghi chú gốc gọi là _"ngưng giảm 2–3 phiên, vol bán thấp"_. Trong hệ thống VCP của Minervini, VDU là điều kiện bắt buộc trước điểm mua.

**c) Bán tháo đỉnh điểm (Selling Climax) ≠ bán tháo kéo dài.** Phân biệt:

||Bán tháo kéo dài|Bán tháo đỉnh điểm|
|---|---|---|
|Vol|Cao đều nhiều phiên|**Cực đại một phiên** (2–3× TB20)|
|Biên độ|Vừa|Rất rộng|
|Giá đóng cửa|Gần đáy phiên|**Bật lên, đóng gần đỉnh phiên**|
|Ý nghĩa|Còn giảm tiếp|Có thể là điểm kết thúc Stage 4|

**Lưu ý:** ngay cả bán tháo đỉnh điểm cũng **không phải điểm mua**. Nó chỉ đánh dấu bắt đầu Stage 1 — sau đó thường cần nhiều tuần đến nhiều tháng xây nền và **test lại đáy** trước khi có điểm mua thật.

### Chuẩn hoá khối lượng

Không bao giờ đọc volume ở dạng số tuyệt đối. Luôn so với **trung bình 20 phiên** của chính mã đó:

- < 0,7× TB20 → thấp (cạn cung)
- 0,7–1,3× TB20 → bình thường
- 1,3–2× TB20 → cao
- > 2× TB20 → đột biến, cần tìm nguyên nhân cụ thể

### Các biến dạng đặc thù thị trường Việt Nam

|Biến dạng|Ảnh hưởng|Cách xử lý|
|---|---|---|
|**Giao dịch thoả thuận**|Một lệnh lớn làm vol tổng tăng vọt nhưng không phản ánh cung–cầu thật|**Luôn tách khối lượng khớp lệnh** khi tính TB và đánh giá|
|**Phiên ATC**|Lệnh dồn vào phút cuối, có thể bẻ nến ngày|Xem thêm dữ liệu intraday trước khi kết luận|
|**Đáo hạn phái sinh VN30**|Vol và giá nhóm VN30 bị nhiễu ngày đáo hạn (thứ Năm thứ 3 hằng tháng)|Đánh dấu ngày đáo hạn trên lịch, loại khỏi phân tích mẫu hình|
|**Biên độ ±7% (HOSE)**|Nến kịch trần/sàn bị cắt cụt, tạo Marubozu giả|Đọc kèm dư mua/dư bán trần–sàn|
|**T+2**|Người mua hôm nay không tạo được cung cho đến 2 phiên sau|Áp lực bán thường dồn vào phiên T+2 sau một nhịp tăng mạnh|
|**UPCoM thanh khoản mỏng**|Mọi chỉ báo dựa trên volume đều kém tin cậy|Hạn chế áp dụng phân tích khối lượng|

---

## 6. Sức mạnh tương đối — định lượng hoá

Ghi chú gốc: _"Các mã không giảm khi thị trường rũ hàng mạnh → ưu tiên theo dõi (cổ phiếu mạnh, đầu ngành)"_. Đây là nguyên tắc đúng và quan trọng, nhưng **"không giảm" là quan sát định tính**. Cách đo cho khách quan:

**a) Đường RS (Relative Strength line) = Giá cổ phiếu / VN-Index.** Vẽ dưới biểu đồ giá.

- RS đi lên = mã đang mạnh hơn thị trường.
- **Tín hiệu mạnh nhất:** RS lập đỉnh mới **trước khi** giá lập đỉnh mới. Trong hệ thống O'Neil đây là một trong những dấu hiệu tin cậy nhất của cổ phiếu dẫn dắt.

**b) So sánh mức giảm từ đỉnh.** Trong cùng nhịp rũ, tính % giảm của mã so với % giảm của VN-Index. Mã giảm ít hơn đáng kể → sức mạnh tương đối.

**c) Thứ tự phục hồi.** Mã hồi phục trước và lập đỉnh mới sớm nhất sau nhịp rũ thường là mã dẫn dắt sóng kế tiếp.

> ⚠️ **Bẫy cần tránh:** "không giảm" cũng có thể do **không ai giao dịch**, không phải do có lực đỡ. Trước khi kết luận là sức mạnh, kiểm tra thanh khoản khớp lệnh có đủ lớn không. Một mã UPCoM đứng giá 5 phiên với vài nghìn cổ phiếu khớp không phải là cổ phiếu mạnh.

---

## 7. Phân biệt lực bán tổ chức và lực bán nhỏ lẻ

Ghi chú gốc: _"Nếu lực bán xuất hiện sau khi thị trường đã rung lắc một vài phiên → thường sẽ là lực bán nhỏ lẻ (đặc trưng là phản ứng chậm)"_.

|Đặc điểm|Lực bán tổ chức|Lực bán nhỏ lẻ|
|---|---|---|
|**Thời điểm**|Ngay khi thị trường bắt đầu yếu, hoặc sớm hơn|**Sau** vài phiên rung lắc — phản ứng chậm|
|**Quy mô lệnh**|Lệnh lớn, đều đặn, có tổ chức|Lệnh nhỏ, rời rạc|
|**Cách thực hiện**|Thường bán vào nhịp hồi để không đánh sập giá|Bán tháo vào nhịp giảm, bán bằng mọi giá|
|**Dấu vết**|Vol cao mà giá không tăng được (hấp thụ)|Nến giảm biên độ rộng, vol trung bình|
|**Mức nguy hiểm**|Cao — báo hiệu phân phối|Thấp hơn — nhưng vẫn tạo áp lực|

**Nguồn dữ liệu để kiểm chứng (Fireant/Vietstock):**

- Khối ngoại mua/bán ròng
- Tự doanh CTCK mua/bán ròng
- Phân bổ lệnh lớn / lệnh nhỏ

> **Nguyên tắc:** dùng **dòng tiền luỹ kế** (cộng dồn nhiều phiên), không dùng số liệu từng phiên riêng lẻ. Một phiên bán ròng không nói lên điều gì; 10 phiên bán ròng liên tiếp là một xu hướng.

**Kết luận hành động:** nếu một mã còn đang chịu áp lực từ những phiên bán nhỏ lẻ → **chờ thêm, chưa vào**. Lực bán này rồi sẽ cạn, nhưng chưa cạn thì mua vào là mua đúng lúc còn cung.

---

## 8. Tin tức và phản ứng giá

Nguyên tắc gốc: **giá phản ứng thế nào quan trọng hơn nội dung tin là gì.**

|Tin|Phản ứng giá|Kết luận|Lý giải|
|---|---|---|---|
|Tốt|Tăng mạnh, vol lớn|Tích cực|Lực mua thật, chưa bị phản ánh hết|
|Tốt|**Không tăng / giảm**|**Xấu**|Có cung hấp thụ toàn bộ → đang phân phối|
|Xấu|Giảm mạnh, vol lớn|Tiêu cực|Cung áp đảo|
|Xấu|**Không giảm**|**Tốt**|Có cầu đỡ ở dưới → đang tích luỹ|

### Nền tảng lý thuyết

Đây là hệ quả của **giả thuyết thị trường hiệu quả dạng bán mạnh**: thông tin công khai được phản ánh vào giá rất nhanh. Vì vậy giá trị thông tin không nằm ở _nội dung tin_, mà ở **độ lệch giữa tin thực tế và kỳ vọng đã có sẵn trong giá**.

Cùng logic với câu trong Lesson 1:

> _"Nếu một thông tin được đưa đến một cách miễn phí, thì chắc chắn mình đã phải trả giá tại một thời điểm nào đó rồi."_

Khi tin đến tay nhà đầu tư cá nhân, giá thường đã phản ánh xong. "Giá phải trả" chính là mua ở vùng cao. **Case nâng hạng ở mục 3 là ví dụ đang diễn ra theo thời gian thực.**

> ⚠️ **Cảnh báo kỹ thuật:** không nhầm giảm giá do **ngày giao dịch không hưởng quyền (GDKHQ)** với tin xấu. Giá điều chỉnh kỹ thuật khi chia cổ tức/cổ phiếu thưởng là cơ học, không mang thông tin về cung–cầu. Kiểm tra lịch quyền trước khi diễn giải một phiên giảm bất thường.

---

# PHẦN IV — RA QUYẾT ĐỊNH

## 9. Chọn cổ phiếu

### Tiêu chí cổ phiếu dẫn đầu

Ghi chú gốc chỉ viết _"tìm được cổ phiếu dẫn đầu → mua vào"_. Bộ tiêu chí cụ thể hơn:

|Tiêu chí|Cách kiểm tra|
|---|---|
|**Sức mạnh giá tương đối**|Đường RS đi lên, RS lập đỉnh trước giá|
|**Vị trí trong ngành**|Thuộc top 1–3 về vốn hoá/thị phần của nhóm ngành đang dẫn dắt|
|**Nhóm ngành mạnh**|Ngành đó đang có dòng tiền vào (kiểm tra ở tầng vĩ mô/dòng tiền)|
|**Hành vi khi thị trường rũ**|Giảm ít hơn chỉ số, hồi phục trước|
|**Tăng trưởng lợi nhuận**|EPS quý gần nhất tăng trưởng so với cùng kỳ — nền tảng cho sóng bền|
|**Giá gần đỉnh, không gần đáy**|Cổ phiếu dẫn dắt thường phá đỉnh cũ, không nằm ở đáy 52 tuần|

> **Điểm dễ nhầm nhất:** nhiều người tìm cổ phiếu "rẻ" ở gần đáy. Cổ phiếu dẫn đầu hầu như không bao giờ rẻ. Mua ở gần đỉnh cũ đúng vào thời điểm breakout là một hành động đúng, dù nó đi ngược trực giác.

### Nhóm cổ phiếu chu kỳ — logic hoàn toàn khác

Ghi chú gốc: _"Mua nhóm Dầu khí thì phải đợi nó giảm thủng đáy → nó mới tăng lại. Tạo nền → chưa đủ thấp."_

Bổ sung lý giải:

- Cổ phiếu chu kỳ (dầu khí, thép, hoá chất, vận tải biển, phân bón) đi theo **giá hàng hoá đầu vào/đầu ra**, không theo tăng trưởng nội tại.
- **Nghịch lý P/E của cổ phiếu chu kỳ:** ở đáy chu kỳ, lợi nhuận sụt về gần 0 → P/E trông rất **cao** (hoặc âm). Ở đỉnh chu kỳ, lợi nhuận đạt kỷ lục → P/E trông rất **thấp**, có vẻ "rẻ". Mua cổ phiếu chu kỳ khi P/E thấp thường là mua đúng đỉnh.
- **Biến số cần theo dõi thực sự:** giá dầu Brent, biên lọc dầu (crack spread), giá thép HRC, giá cước vận tải — chứ không phải biểu đồ giá cổ phiếu.
- Vì vậy _"tạo nền chưa đủ thấp"_ có nghĩa: nền giá cổ phiếu chỉ có ý nghĩa khi **biến số chu kỳ nền tảng đã đảo chiều**. Nếu giá dầu vẫn đang giảm thì nền giá cổ phiếu dầu khí chỉ là nghỉ giữa nhịp.

---

## 10. Nền giá, điểm mua, mục tiêu giá

### Cần phân biệt ba khái niệm

Ghi chú gốc viết _"Nền giá = TBC(đáy cũ, đỉnh cũ,...)"_. Công thức này thực chất là cách tính một **mức tham chiếu/trung điểm**, không phải định nghĩa nền giá. Ba khái niệm khác nhau:

|Khái niệm|Định nghĩa|Vai trò|
|---|---|---|
|**Nền giá (base)**|Vùng giá đi ngang, có đáy nền và đỉnh nền rõ ràng, kéo dài tối thiểu vài tuần|Nơi tích luỹ diễn ra|
|**Mức tham chiếu / trung điểm**|Trung bình cộng của các mốc quan trọng (đáy cũ, đỉnh cũ) — gần với Fibonacci 50% hoặc pivot point cổ điển (H+L+C)/3|Vùng hỗ trợ/cản tâm lý|
|**Điểm mua (pivot / buy point)**|Đỉnh của nền + một biên nhỏ, nơi giá breakout kèm vol lớn|Nơi đặt lệnh|

**Thứ tự đúng:** xác định nền → xác định đỉnh nền → chờ breakout kèm vol → vào lệnh tại pivot. Không mua giữa nền.

### Mục tiêu giá — sửa lại cho chính xác

Ghi chú gốc: _"Nhịp đầu bao nhiêu, nhịp sau bấy nhiêu (xấp xỉ)"_. Đây là nguyên tắc **measured move**, nhưng **không áp dụng cho mọi nhịp**. Công thức đo đúng theo từng mẫu hình:

|Mẫu hình|Cách đo mục tiêu|
|---|---|
|**Cờ / Cờ đuôi nheo (flag, pennant)**|Chiều dài cán cờ (flagpole) chiếu từ điểm breakout — đây chính là "nhịp sau ≈ nhịp đầu"|
|**Cốc tay cầm (cup with handle)**|Độ sâu cốc chiếu từ pivot|
|**Vai đầu vai**|Khoảng cách từ đỉnh đầu tới đường viền cổ, chiếu xuống từ điểm phá vỡ|
|**Tam giác / nêm**|Chiều cao đáy mẫu hình chiếu từ điểm phá vỡ|
|**Hộp giá / nền đi ngang**|Chiều cao hộp chiếu từ cạnh trên|

> **Ghi nhớ:** mục tiêu giá là công cụ để **tính tỷ lệ lời/lỗ trước khi vào lệnh**, không phải dự báo. Nếu R:R không đạt yêu cầu thì bỏ qua cơ hội — đó mới là công dụng thật của phép đo này.

### Sóng hồi — phân biệt ba loại

Ghi chú gốc: _"Sóng hồi phân phối nốt"_. Đúng trong bối cảnh cuối Stage 3, nhưng cần phân biệt:

|Loại|Bối cảnh|Đặc điểm|Ý nghĩa|
|---|---|---|---|
|**Hồi kỹ thuật trong Stage 4**|Sau nhịp giảm mạnh|Vol thấp, hồi 30–50% nhịp giảm, không vượt được MA50|Bẫy — giảm tiếp|
|**Phân phối nốt cuối Stage 3**|Sau một sóng tăng dài|Đỉnh sau thấp hơn đỉnh trước, vol lớn mà không đi được|Thoát hàng|
|**Điều chỉnh lành mạnh trong Stage 2**|Giữa xu hướng tăng|Về MA20/MA50, **vol cạn dần**, giữ được hỗ trợ|Cơ hội mua thêm|

**Biến số phân biệt:** giai đoạn chu kỳ + hành vi khối lượng khi hồi + có giữ được MA quan trọng không.

---

## 11. Quản trị rủi ro — phần còn thiếu hoàn toàn trong ghi chú gốc

Cả hai bài học đều nói về **mua gì, mua khi nào**, nhưng không có dòng nào về **mất bao nhiêu nếu sai**. Đây là lỗ hổng lớn nhất, và cũng là thứ quyết định sống còn.

### Đặt điểm cắt lỗ

|Cách đặt|Vị trí|Phù hợp với|
|---|---|---|
|**Theo cấu trúc**|Dưới đáy nền hoặc dưới đáy gần nhất|Mua tại pivot sau nền|
|**Theo đường trung bình**|Mất MA20 (ngắn hạn) hoặc MA50 (trung hạn)|Nắm giữ trong Stage 2|
|**Theo % cố định**|7–8% dưới giá mua (chuẩn O'Neil)|Người mới, cần kỷ luật cứng|
|**Theo biến động**|1,5–2× ATR(14) dưới giá vào|Mã biến động cao|

**Nguyên tắc:** xác định điểm cắt lỗ **trước khi** đặt lệnh mua, không phải sau khi thua lỗ.

### Tỷ lệ lời/lỗ và khối lượng vị thế

- **R:R tối thiểu 2:1**, lý tưởng 3:1. Nếu mục tiêu giá cách điểm vào 10% mà cắt lỗ cách 8% → bỏ qua.
- **Rủi ro mỗi lệnh ≤ 1–2% tổng vốn.**
- Công thức: `Số cổ phiếu = (Tổng vốn × % rủi ro chấp nhận) / (Giá vào − Giá cắt lỗ)`
- Ví dụ: vốn 500 triệu, rủi ro 1% = 5 triệu. Mua giá 50.000, cắt lỗ 46.000 → chênh 4.000/cp → mua tối đa 1.250 cp (≈62,5 triệu).

### Ràng buộc riêng của thị trường Việt Nam

|Ràng buộc|Ảnh hưởng tới rủi ro|Cách xử lý|
|---|---|---|
|**T+2**|Mua hôm nay, sớm nhất T+2 mới bán được. Trong 2 phiên đó có thể mất tới ~14% nếu sàn liên tiếp|Điểm cắt lỗ thực tế phải rộng hơn tính toán lý thuyết, hoặc giảm khối lượng vị thế|
|**Biên độ ±7%**|Sàn liên tiếp + dư bán sàn chất đống = **không thoát được hàng** dù đã đặt lệnh|Tránh mã thanh khoản thấp; ưu tiên mã có khớp lệnh lớn|
|**Co-movement cao với VN-Index**|Đa dạng hoá nhiều mã vẫn không giảm được rủi ro hệ thống|Quản trị tỷ trọng tiền mặt, không chỉ quản trị số lượng mã|

> **Hệ quả quan trọng:** vì T+2 và biên độ, **kích thước vị thế** ở thị trường Việt Nam là công cụ quản trị rủi ro quan trọng hơn điểm cắt lỗ. Cắt lỗ có thể không thực hiện được; vị thế nhỏ thì luôn hiệu quả.

---

## 12. Kỷ luật và tâm lý

1. **Đừng đi theo thị trường** — đi theo đám đông thì "chết chùm".
2. **Mua lúc không ai dám mua**, bán lúc mọi người hăng hái.
3. **Chờ xác nhận trước khi vào** — không có lệnh nào bắt buộc phải đặt hôm nay. Chi phí của việc bỏ lỡ một cơ hội là 0; chi phí của việc vào sai là tiền thật.
4. **Quan sát khối lượng trước khi quyết định**, không quyết định rồi mới tìm lý do biện minh.
5. **Viết lý do vào lệnh ra giấy trước khi bấm.** Nếu không viết được thành câu rõ ràng thì chưa đủ cơ sở.

---

## 13. Case study: PNJ

**Đã làm gì sai:**

- FOMO theo thị trường, mua ở vùng giá cao.
- Không quan sát khối lượng trước khi vào lệnh.
- Bỏ qua dấu hiệu mã vẫn còn chịu áp lực từ các phiên bán nhỏ lẻ.
- Không xác định trước điểm cắt lỗ và tỷ lệ R:R.

**Chi phí:** 5–10% — bằng toàn bộ lợi nhuận kỳ vọng của một nhịp giao dịch bình thường.

### Checklist trước khi bấm lệnh

**A. Bối cảnh**

- [ ] VN-Index đang ở giai đoạn nào — đã rũ xong hay đang rũ?
- [ ] Độ rộng thị trường thế nào (số mã tăng/giảm)?
- [ ] Nhóm ngành của mã này có đang có dòng tiền vào không?

**B. Vị trí kỹ thuật của mã**

- [ ] Mã đang ở Stage nào? (MA200 dốc ra sao, giá nằm trên hay dưới?)
- [ ] Có nền giá rõ ràng không? Đỉnh nền ở đâu?
- [ ] Giá hiện tại cách pivot bao xa? Có đang đuổi giá không?

**C. Khối lượng**

- [ ] Khối lượng bán các phiên gần nhất đã cạn chưa (so với TB20)?
- [ ] Đã **tách giao dịch thoả thuận** chưa?
- [ ] Còn áp lực bán nhỏ lẻ trễ nhịp không?
- [ ] Dòng tiền khối ngoại/tự doanh **luỹ kế** đang vào hay ra?

**D. Tin tức**

- [ ] Có tin nào đang đẩy giá không? Giá **phản ứng ra sao** với tin đó?
- [ ] Có sắp GDKHQ không?

**E. Rủi ro — bắt buộc**

- [ ] Cắt lỗ ở giá nào? Mất bao nhiêu % nếu chạm?
- [ ] Mục tiêu giá ở đâu? R:R có ≥ 2:1 không?
- [ ] Khối lượng vị thế bao nhiêu? Rủi ro có ≤ 2% tổng vốn không?
- [ ] Nếu T+2 mà sàn 2 phiên liên tiếp thì chịu được không?

> **Nếu có bất kỳ ô nào chưa tick được → chưa vào lệnh.**

---

# PHẦN V — ĐÍNH CHÍNH VÀ MÂU THUẪN

## 14. Các mâu thuẫn nội tại trong ghi chú gốc

Một số câu trong hai bài học mâu thuẫn nhau nếu đọc tách rời. Chúng không sai — chúng **áp dụng ở các giai đoạn khác nhau của chu kỳ**. Không nhận ra điều này là nguyên nhân gây lẫn lộn khi thực chiến.

|Cặp mâu thuẫn|Cách hoà giải|
|---|---|
|_"Mua lúc không ai dám mua"_ **vs** _"Tìm cổ phiếu dẫn đầu → mua vào"_|Câu đầu áp dụng cho **Stage 1** (mua ở nền, khi tâm lý còn xấu). Câu sau áp dụng cho **Stage 2** (mua breakout, khi mã đã mạnh rõ ràng). Hai chiến lược, hai thời điểm — không trộn lẫn.|
|_"Thanh khoản cao → bán tháo"_ **vs** breakout cần vol lớn|Volume không có nghĩa độc lập. **Vol cao + giá giảm** = bán tháo. **Vol cao + giá vượt nền** = breakout. Luôn đọc kèm hướng giá.|
|_"Đừng đi theo thị trường"_ **vs** cổ phiếu Việt Nam co-movement rất cao với VN-Index|"Đừng đi theo" = đừng chạy theo **tâm lý đám đông**, không có nghĩa bỏ qua **xu hướng chỉ số**. Ngược lại: xu hướng VN-Index là bộ lọc bắt buộc, vì trong nhịp rũ mạnh thì ~80% cổ phiếu giảm bất kể tốt xấu.|
|_"Mua lúc giảm"_ **vs** _"không bắt dao rơi"_|Mua khi giá giảm **về vùng hỗ trợ đã xác định trước, kèm vol cạn**, trong một mã đang ở Stage 1 hoặc Stage 2. Không phải mua bất kỳ khi nào giá giảm.|

## 15. Những phát biểu cần gắn thêm điều kiện

|Ghi chú gốc|Điều kiện cần bổ sung|
|---|---|
|"Thanh khoản cao → dấu hiệu bán tháo"|**Chỉ đúng khi giá giảm.** Xem ma trận ở mục 5.|
|"Mua lúc không ai dám mua"|Cần kèm xác nhận: vol bán cạn + ngưng giảm 2–3 phiên + MA200 đã phẳng. Thiếu điều kiện thì đây là bắt dao rơi.|
|"Ngưng giảm 2–3 phiên → sắp chạm đáy"|Cần thêm: mã có đang trong Stage 4 không? Trong xu hướng giảm mạnh, "ngưng giảm" thường chỉ là nghỉ giữa nhịp. 2–3 phiên là **quá ngắn** để xác nhận đáy — nền giá thật thường cần nhiều tuần.|
|"Nhịp sau bằng nhịp đầu"|Chỉ áp dụng cho mẫu hình cờ/cờ đuôi nheo. Xem bảng công thức đo ở mục 10.|
|"Dầu khí phải thủng đáy mới tăng"|Biến số quyết định là **giá dầu và biên lọc dầu**, không phải biểu đồ giá cổ phiếu. Nên backtest lại bằng TradingView Bar Replay trước khi coi là quy luật.|
|"Một cổ phiếu tăng + điều chỉnh quá đẹp → dễ đảo chiều"|Cần phân biệt với **điều chỉnh lành mạnh trong Stage 2** (về MA20/50, vol cạn, giữ hỗ trợ) — trường hợp đó lại là cơ hội mua. Biến số phân biệt: mã đã tăng bao lâu, đang ở đâu trong chu kỳ.|
|"Nâng hạng là tín hiệu tích cực"|Đúng về cấu trúc dài hạn. Nhưng dòng tiền thụ động đợt đầu chỉ ~10% tỷ trọng, và giao dịch cơ cấu kết thúc trước ngày hiệu lực. Xem mục 3.|

---

## 16. Đối chiếu thuật ngữ Việt – Anh

Để đọc được tài liệu gốc (Murphy, O'Neil, Bulkowski, Minervini, Weinstein):

|Tiếng Việt|Tiếng Anh|
|---|---|
|Tích luỹ / Phân phối|Accumulation / Distribution|
|Nền giá|Base / Consolidation|
|Điểm mua, điểm phá vỡ|Pivot point / Buy point / Breakout|
|Rũ hàng|Shakeout|
|Bắt dao rơi|Catching a falling knife|
|Bán tháo đỉnh điểm|Selling climax|
|Đỉnh giả / phá vỡ giả|Upthrust / False breakout|
|Sức mạnh tương đối|Relative Strength (RS)|
|Khối lượng cạn kiệt|Volume dry-up (VDU)|
|Nỗ lực và kết quả|Effort vs Result|
|Độ rộng thị trường|Market breadth|
|Mục tiêu giá theo mẫu hình|Measured move|
|Tỷ lệ lời/lỗ|Risk/Reward ratio (R:R)|
|Khối lượng vị thế|Position sizing|
|Giao dịch thoả thuận|Negotiated / Block trade|
|Khớp lệnh|Matched order|
|Khối ngoại / Tự doanh|Foreign investors / Proprietary trading|

---

## Tóm tắt một dòng

> **Xác định giai đoạn chu kỳ (MA200) → kiểm tra khối lượng theo hướng giá (đã tách thoả thuận) → xác nhận sức mạnh tương đối so với VN-Index → tính điểm cắt lỗ và R:R → chỉ khi đó mới vào lệnh, với khối lượng vị thế phù hợp.** Bỏ qua bất kỳ bước nào là lặp lại PNJ.

---

## Việc cần làm tiếp

- [ ] Tra cứu đầy đủ danh sách 21 mã Small Cap trong rổ FTSE All-Cap
- [ ] Vẽ đường RS (giá/VN-Index) cho các mã trong watchlist trên TradingView
- [ ] Backtest quy tắc "ngưng giảm 2–3 phiên + vol cạn" bằng Bar Replay — đo tỷ lệ thắng thật
- [ ] Thiết lập bảng theo dõi dòng tiền khối ngoại/tự doanh **luỹ kế** cho watchlist
- [ ] Xây bảng tính position sizing để dùng trước mỗi lệnh