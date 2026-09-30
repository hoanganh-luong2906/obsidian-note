Nguồn: đọc chỉ báo kỹ thuật (5/9), RS so với thị trường (20/9), chỉ báo chính xác nhất cho VN (24/9), MA50×MA200 và MA20×MA50 (25/9).

# 1. Bản chất chỉ báo

- Mọi chỉ báo tính từ giá và khối lượng → không tạo thông tin mới, hầu hết **trễ hơn giá**. Dùng nhiều chỉ báo cùng nhóm tạo **đồng thuận giả**.
- Theo xu hướng (MA, MACD): trễ, đúng khi có xu hướng, sai liên tục khi đi ngang. Dao động (RSI, Stochastic): giả định hồi về trung bình, báo "quá mua" suốt sóng tăng mạnh.
- Chỉ báo không dự đoán, chúng mô tả. Giá trị thật: buộc biến quan sát thành quy tắc trước khi vào lệnh.

|Nhóm|Trả lời câu hỏi|Ví dụ|
|---|---|---|
|Xu hướng|Đang tăng hay giảm?|MA, EMA, MACD, ADX|
|Động lượng|Nhanh cỡ nào?|RSI, Stochastic|
|Khối lượng|Có tiền thật không?|Volume, OBV, MFI|
|Biến động|Tích luỹ hay bung?|Bollinger Bands, ATR|

# 2. MA — đường trung bình động

- MA20 = giá vốn trung bình của người mua 20 phiên gần nhất. Giá trên MA20 = phần lớn người mua tháng qua đang lãi.
- **Độ dốc quan trọng hơn việc giá cắt đường.** MA đi ngang thì tín hiệu cắt gần như vô nghĩa.
- Thứ tự MA20 trên MA50 trên MA200, cả ba dốc lên = cấu trúc tăng đầy đủ.
- MA là hỗ trợ động: trong uptrend, hồi về MA20 rồi bật thường có xác suất tốt hơn mua đuổi đỉnh.
- EMA nhanh hơn SMA nhưng nhiễu hơn. MA10/MA20 cho lướt sóng, MA50/MA200 cho trung hạn.
- Ba tầng: **MA200 = mùa (Stage)**, **MA50 = xu hướng trung hạn**, **MA20 = nhịp ngắn hạn**.

## Golden Cross / Death Cross (MA50 × MA200)

- Là tín hiệu **xác nhận xu hướng đã đổi**, không phải điểm mua/bán: mua đúng Golden Cross thường là mua sau pivot đẹp nhất; bán đúng Death Cross thường là bán gần vùng quá bán ngay trước nhịp hồi. Khi đi ngang hai đường quấn vào nhau → nhiễu.
- Dùng làm **đèn trạng thái**: Golden Cross thường xuất hiện _sau_ khi giá đã vượt nền (cuối Stage 1 → đầu Stage 2); Death Cross thường _sau_ khi giá đã thủng nền phân phối (đầu Stage 4).
- Quan trọng hơn điểm cắt: **độ dốc MA200** (Golden Cross khi MA200 vẫn dốc xuống rất hay thất bại); vị trí giá so với hai đường (giá đã rơi dưới MA50 thì tín hiệu gần như vô hiệu); khoảng cách giá–MA200 (quá xa = căng, dễ rũ).
- Golden Cross ở cổ phiếu khi VN-Index vừa Death Cross thì rủi ro cao hơn nhiều.

## MA20 × MA50

- Nhanh hơn, nhiều tín hiệu hơn, nhiễu hơn nhiều; chỉ đọc khi đã biết "mùa".
- **Stage 2:** MA20 cắt xuống MA50 thường chỉ là nhịp điều chỉnh/tạo nền (theo dõi MA50 còn dốc lên và vol điều chỉnh thấp); cắt lên lại hay đi cùng thoát nền, nhưng điểm mua vẫn là breakout có vol.
- **Stage 3:** MA20 cắt xuống khi MA50 bắt đầu dẹt = cảnh báo sớm, thường trước Death Cross vài tuần đến vài tháng.
- **Stage 4:** MA20 cắt lên MA50 thường chỉ là sóng hồi ("sóng hồi phân phối nốt").
- Chờ xác nhận 2–3 phiên (T+2 và phiên rũ dễ tạo cắt giả). Khi chỉ số rung lắc, mã nào **không** cắt xuống mới đáng chú ý.

# 3. RSI (14)

- Sai lầm phổ biến: "RSI trên 70 = phải bán". Trong uptrend mạnh RSI có thể trụ 70–90 nhiều tuần — **RSI cao là biểu hiện sức mạnh**.
- **Vùng vận hành:** uptrend khoảng 40–80, downtrend 20–60. Lần đầu thủng 40 sau chuỗi dài giữ trên 40 = đổi chế độ. Đường 50 là ranh giới.
- **Phân kỳ:** giá đỉnh cao hơn, RSI đỉnh thấp hơn = động lượng cạn — là cảnh báo, có thể kéo dài rất lâu trước khi đảo chiều. Phân kỳ dương: giá đáy thấp hơn, RSI đáy cao hơn.
- Giữ chu kỳ 14: chu kỳ 7–9 bão hoà sau 2–3 phiên trần.
- Tự xác định vùng vận hành riêng: kéo lại 2 năm, ghi RSI thường chạm đáy ở đâu trong các nhịp điều chỉnh của uptrend (mỗi mã một khác, vd 42 hay 38) — kẻ hai đường ngang thay cho 70/30 mặc định.

# 4. MACD & Bollinger Bands

- **MACD** = EMA12 − EMA26, tín hiệu EMA9; đo gia tốc xu hướng. Đáng nhìn nhất: histogram co lại (mất đà trước khi giá đảo chiều). Rất nhiễu trong sideway.
- **Bollinger** = MA20 ± 2 độ lệch chuẩn. Squeeze = tích luỹ, thường trước cú bung mạnh nhưng **không cho biết hướng**. Chạm band trên không phải tín hiệu bán; xu hướng mạnh giá "đi men theo band".

# 5. Bộ chỉ báo tối giản cho thị trường Việt Nam

|Chỉ báo|Tham số|Vai trò|Vì sao chọn|
|---|---|---|---|
|MA|SMA 20, 50, 200 (khung ngày)|Chế độ thị trường, hỗ trợ động|Không bão hoà với biên ±7%; độ dốc vẫn đọc được khi trần 5 phiên|
|Khối lượng|• MA volume|Xác nhận thật/giả|Chỉ báo độc lập duy nhất, tốn tiền thật để tạo ra|
|RSI|14|Cảnh báo động lượng cạn, phân kỳ|Cảnh báo, không phải tín hiệu|

**Setup TradingView:** khung ngày, 3 panel — (1) nến + SMA20/50/200; (2) volume + MA volume; (3) RSI(14) giữ đường 50 + hai đường vùng vận hành riêng.

**Thứ tự đọc biểu đồ:** khung tuần trước khung ngày → cấu trúc giá (quan trọng nhất) → MA → khối lượng → RSI/MACD tinh chỉnh thời điểm → cắt lỗ và R:R. Trước cả ba chỉ báo: VN-Index so với MA50/MA200 và giá trị khớp toàn thị trường so với TB20 của chính nó (thanh khoản co lại thì breakout khó bền).

**Chủ động bỏ:** Stochastic, CCI, Williams %R (trùng nhóm RSI → đồng thuận giả) · Parabolic SAR (bị đá liên tục trong sideway) · Ichimoku (thiết kế cho thị trường không biên, dựa vào gap và độ trễ 26 phiên) · mọi chỉ báo/mẫu dựa vào gap (island reversal…). Tối đa hai chỉ báo khác họ + khối lượng.

# 6. Xếp hạng độ tin cậy công cụ tại Việt Nam

|Cấp|Công cụ|Lý do|
|---|---|---|
|1 — Nền tảng|Khối lượng khớp lệnh & quan hệ giá–KL · Xu hướng VN-Index (Stage, FTD, ngày phân phối) · Cấu trúc MA (MA50/150/200, Trend Template) · RS line|Dòng tiền thật; độ đồng pha cao nên bối cảnh chỉ số là bộ lọc quan trọng nhất; MA để lọc xu hướng, không để tìm điểm mua|
|2 — Mẫu hình|VCP, nền phẳng, cốc tay cầm, 3WT · Vùng hỗ trợ/kháng cự từ volume (vùng kẹt hàng)|Hiệu quả khi có cạn cung và breakout kèm vol; người mua đỉnh ở VN hay bán hoà vốn|
|3 — Hỗ trợ|RSI, MACD, Bollinger squeeze · Nến Nhật|Xác nhận, không đứng một mình; nến chỉ có nghĩa tại vùng giá quan trọng kèm volume|
|4 — Nhiễu cao|Đếm sóng Elliott chi tiết, Fibonacci chính xác từng điểm, harmonic, Stochastic trong trend mạnh|Chủ quan, dễ "vẽ cho khớp"|

"Chính xác" chỉ có ý nghĩa khi tự đo: ghi nhật ký mỗi setup (bối cảnh VN-Index, loại nền, vol breakout, kết quả sau 10–20 phiên); sau 30–50 mẫu sẽ biết công cụ nào hiệu quả với chính mình.

# 7. Sức mạnh tương đối (RS)

RS = **tỷ số giá cổ phiếu / chỉ số tham chiếu**, không phải % tăng tuyệt đối. RS chỉ giúp **chọn đúng chỗ để tìm**, không phải điểm mua.

## Ba cách đo

1. **RS line trên TradingView (web):** gõ `HOSE:PNJ/HOSE:VNINDEX`. RS hướng lên = mạnh hơn thị trường kể cả khi giá đi ngang. **Tín hiệu mạnh nhất: RS lập đỉnh mới trước khi giá phá nền.**
2. **Mansfield RS (chuẩn Stage Analysis):** trên chart tỷ số khung tuần thêm MA30; `(RS / MA30(RS) − 1) × 100`. Cắt lên 0 ≈ bắt đầu Stage 2; cắt xuống 0 dù giá còn cao = cảnh báo sớm Stage 3.
3. **Xếp hạng kiểu IBD:** `2×(%3T) + %6T + %9T + %12T`, xếp phần trăm vị thứ toàn sàn (Excel/Python, dữ liệu Fireant/vnstock); chỉ xét top 20% (RS ≥80).

- Cách đo thủ công khác: so % giảm từ đỉnh của mã với của VN-Index trong cùng nhịp rũ; thứ tự phục hồi (mã hồi trước, lập đỉnh sớm nhất thường dẫn sóng kế tiếp).
- Bẫy: "không giảm" có thể do không ai giao dịch — kiểm tra thanh khoản khớp lệnh trước.

## Cấp ngành — bộ chỉ số VNAllshare (HOSE)

VNFIN (tài chính), VNREAL (BĐS), VNIND (công nghiệp), VNENE (năng lượng), VNHEAL (y tế), VNMAT (nguyên vật liệu), VNIT (CNTT), VNUTI (tiện ích), VNCOND (tiêu dùng không thiết yếu). So từng chỉ số ngành với VN-Index.

## RRG — Vietstock "Sức mạnh giá RRG"

- Đường dẫn: [finance.vietstock.vn/suc-manh-gia-rrg](http://finance.vietstock.vn/suc-manh-gia-rrg) (Công cụ đầu tư). Chạy cả cấp mã và cấp ngành.
- Hai trục: VS-RS trên 100 = mạnh hơn thị trường; VS-Mom trên 100 = đà mạnh vẫn được đẩy. Bốn góc: **Tăng trưởng** (cả hai trên 100) · **Suy yếu** (RS trên, Mom dưới) · **Giảm giá** (cả hai dưới) · **Tích luỹ** (RS dưới, Mom trên).
- Vòng quay chiều kim đồng hồ: Tích luỹ → Tăng trưởng → Suy yếu → Giảm giá. **Điểm cần săn: mã/ngành từ Tích luỹ bò sang Tăng trưởng**, không phải mã đã nằm sâu trong Tăng trưởng.
- Đối chiếu trạng thái cổ phiếu với ngành: cổ tốt trong ngành xấu khó hiệu quả.
- Hạn chế: RRG đã làm mượt nên trễ, không bắt được "RS lập đỉnh trước giá"; Vietstock dùng phân ngành riêng, đừng trộn với VNAllshare. Vị trí góc phần tư là trạng thái, không phải tín hiệu mua.

## SSI iBoard

Chart iBoard là TradingView nhúng ([iboard.ssi.com.vn/analysis/trading-view](http://iboard.ssi.com.vn/analysis/trading-view)) nhưng gần như chắc **không xử lý được cú pháp tỷ số** (bản nhúng dùng datafeed SSI). Dùng Compare → thêm VNINDEX → thang Percent để so tương đối (không phải ratio chart thật).

**Quy trình kết hợp:** iBoard đặt lệnh/bảng giá → Vietstock RRG quét ngành/mã hàng tuần → TradingView web soi RS line trước khi quyết định.

## Ma trận VN-Index × RS của mã (khung quyết định giữ/giảm)

- Thị trường yếu + RS yếu → giảm tỷ trọng rõ ràng (trường hợp PNJ 24/9/2026: PNJ −9,4% so với VN-Index −2,2%).
- Phần lớn cổ phiếu đi theo xu hướng chung; khi chỉ số phá hỗ trợ dài hạn, mã RS yếu gần như không có lợi thế để giữ nguyên vị thế.
- Mua lại chỉ khi **cả hai** điều kiện cùng có: VN-Index có FTD hợp lệ **và** mã có tín hiệu riêng (vượt kháng cự kèm vol, RS hướng lên, hoặc đáy cạn cung).