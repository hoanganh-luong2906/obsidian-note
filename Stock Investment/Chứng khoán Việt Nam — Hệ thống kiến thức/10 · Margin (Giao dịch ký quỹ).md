## 1. Tổng quan

Margin là khoản vay từ công ty chứng khoán (CTCK) để mua thêm cổ phiếu. Toàn bộ cổ phiếu trong tài khoản trở thành tài sản bảo đảm cho khoản vay. Đòn bẩy phóng đại cả lãi lẫn lỗ, và lãi vay chạy mỗi ngày dù giá đi đâu.

Margin không tạo ra lợi thế. Nó chỉ phóng to một vị thế: vị thế đúng thì lời nhiều hơn, vị thế sai thì mất vốn nhanh hơn.

Mục tiêu bài học:

- Tự tính được tỷ lệ ký quỹ, ngưỡng call và ngưỡng force sell của tài khoản ngay lúc mở vị thế.
- Biết chi phí thật của lãi vay theo thời gian nắm giữ.
- Biết quy trình và cách xử lý khi bị call margin.
- Đặt margin vào khung quyết định chung: chỉ dùng khi vị thế đã được xác nhận.

Liên hệ bài trước: Lesson 2 ghi "thanh khoản cao → dấu hiệu bán tháo" và bài học FOMO với PNJ. Margin là cơ chế khiến hai điều đó trở nên đắt giá hơn nhiều: FOMO bằng tiền vay, và bán tháo do bị ép bán.

## 2. Khái niệm cốt lõi

Con số quan trọng nhất trên màn hình là tỷ lệ ký quỹ thực tế (Rtt). Mọi quy tắc call và force sell đều so sánh Rtt với các ngưỡng của CTCK.

|   |   |
|---|---|
|Thuật ngữ|Ý nghĩa|
|Tổng tài sản (TS)|Giá trị thị trường của cổ phiếu + tiền trong tài khoản|
|Nợ|Gốc vay + lãi cộng dồn + phí|
|Tài sản thực có (NAV)|TS − Nợ, phần thật sự là của bạn|
|Tỷ lệ ký quỹ thực tế (Rtt)|NAV / TS|
|Sức mua|Tiền mặt + hạn mức vay còn dùng được, tính theo tỷ lệ cho vay từng mã|

```latex
R_{tt} = \frac{TS - N\text{ợ}}{TS}
```

Ba ngưỡng cần biết (mức cụ thể khác nhau theo từng CTCK):

|   |   |   |
|---|---|---|
|Ngưỡng|Mức phổ biến|Khi Rtt chạm mức này|
|Ký quỹ ban đầu|≥ 50% (Thông tư 120/2020/TT-BTC)|Vốn tự có tối thiểu khi mở vị thế, tức vay tối đa 1:1|
|Duy trì (call)|Khoảng 30–40%|Bị call margin, phải nộp tiền hoặc bán bớt|
|Xử lý (force sell)|Khoảng 25–30%|CTCK có quyền tự bán cổ phiếu, không cần bạn đồng ý|

Tỷ lệ cho vay khác nhau theo từng mã. Bluechip có thể được vay 50%, mã yếu hơn 20–30%, có mã 0%. Chỉ mã nằm trong danh mục chứng khoán ký quỹ của sàn và của CTCK mới được vay.

Rủi ro hay bị bỏ qua: CTCK có thể hạ tỷ lệ hoặc cắt margin một mã bất cứ lúc nào. Mã bị cảnh báo, báo lỗ hay có tin xấu thường bị cắt trước. Khi đó Rtt tụt ngay dù giá chưa giảm.

## 3. Khi mua bằng margin

Dùng hết sức mua nghĩa là bắt đầu với Rtt = 50%, chỉ cách ngưỡng call vài bước giá. Không phải vì được vay 1:1 thì nên vay 1:1.

Ví dụ xuyên suốt bài: vốn 100 triệu, mã được vay 50%. Sức mua tối đa là 200 triệu: 100 triệu của bạn và 100 triệu vay.

1. Ngày T: đặt lệnh mua trong giới hạn sức mua. Khoản vay chỉ phát sinh phần vượt quá tiền mặt.
2. Khoảng T+2: tiền được thanh toán, khoản vay được giải ngân thực tế. Lãi thường tính từ ngày giải ngân.
3. Cổ phiếu về tài khoản và trở thành tài sản bảo đảm cho toàn bộ dư nợ.

Mỗi CTCK quy định ngày bắt đầu tính lãi hơi khác nhau. Kiểm tra trong hợp đồng ký quỹ của SSI.

## 4. Lãi vay

Chi phí thật của margin nằm ở thời gian ôm hàng, không phải con số %/năm. Lãi tính mỗi ngày, kể cả thứ Bảy, Chủ Nhật và ngày lễ.

```latex
L\text{ãi} = D\text{ư nợ} \times L\text{ãi suất năm} \times \frac{S\text{ố ngày vay}}{365}
```

Một số CTCK dùng 360 thay vì 365. Lãi suất margin phổ biến khoảng 9–14%/năm, thường có ưu đãi 30 ngày đầu rồi tăng dần.

Chi phí lãi khi vay 100 triệu ở 12%/năm (vị thế 200 triệu):

|   |   |   |   |
|---|---|---|---|
|Thời gian giữ|Tiền lãi (triệu đồng)|% trên vị thế 200 triệu|% trên vốn 100 triệu|
|30 ngày|0,99|0,49%|0,99%|
|60 ngày|1,97|0,99%|1,97%|
|90 ngày|2,96|1,48%|2,96%|
|180 ngày|5,92|2,96%|5,92%|

Cổ phiếu đi ngang 3 tháng vẫn khiến vốn của bạn mất gần 3%, chưa kể phí giao dịch và thuế bán.

Thời hạn và cách trả:

- Mỗi khoản vay thường có thời hạn khoảng 90 ngày, có thể gia hạn.
- Quá hạn thì bị lãi phạt (thường khoảng 150% lãi suất thường) và có thể bị xử lý tài sản.
- Lãi cộng dồn vào nợ và thu định kỳ, ví dụ cuối tháng.
- Tiền nộp vào tài khoản hoặc tiền bán cổ phiếu thường được tự động cấn trừ nợ.

## 5. Khi bán và hiệu ứng đòn bẩy

Vay 1:1 thì mỗi 1% giá cổ phiếu thành 2% trên vốn của bạn, cả chiều lãi lẫn chiều lỗ. Lỗ càng sâu thì phần cần tăng để hòa vốn càng lớn.

Cơ chế khi bán:

1. Lệnh bán khớp ngày T.
2. Tiền bán về tài khoản khoảng T+2 và được tự động cấn trừ vào nợ gốc và lãi.
3. Trong thời gian chờ tiền về, lãi có thể vẫn tiếp tục chạy. Có thể ứng trước tiền bán nhưng mất phí ứng.

Phóng đại lãi/lỗ với vốn 100 triệu, vay 100 triệu (trước lãi vay, phí và thuế):

|   |   |   |   |   |
|---|---|---|---|---|
|Giá cổ phiếu|Tổng TS (triệu)|NAV (triệu)|Lãi/lỗ trên vốn|Cần tăng để hòa vốn|
|+20%|240|140|+40%|—|
|+10%|220|120|+20%|—|
|−10%|180|80|−20%|+25%|
|−20%|160|60|−40%|+67%|
|−30%|140|40|−60%|+150%|

Dòng −30% là lý thuyết: trước khi giá xuống tới đó, tài khoản đã bị force sell (mục 6).

## 6. Call margin và force sell

Vay 1:1 thì cổ phiếu chỉ cần giảm khoảng 23% là bị call, khoảng 29% là bị force sell. Trên HOSE, đó là 4–5 phiên sàn liên tiếp, đúng kịch bản PNJ vừa trải qua.

Cách đọc trạng thái tài khoản:

- Rtt ≥ ngưỡng duy trì: an toàn.
- Ngưỡng xử lý ≤ Rtt < ngưỡng duy trì: bị call margin.
- Rtt < ngưỡng xử lý: bị force sell.

### Tự tính ngưỡng ngay lúc mua

Tổng tài sản mà tại đó Rtt chạm một ngưỡng R:

```latex
TS_{ng\text{ưỡng}} = \frac{N\text{ợ}}{1 - R}
```

Mức giảm cần để chạm ngưỡng, giả định ngưỡng call 35% và force sell 30%, vốn 100 triệu:

|   |   |   |   |   |   |
|---|---|---|---|---|---|
|Mức vay|Vị thế (triệu)|Giảm đến call|Phiên sàn HOSE đến call|Giảm đến force sell|Phiên sàn HOSE đến force sell|
|Vay 100 triệu (1:1)|200|−23,1%|4|−28,6%|5|
|Vay 50 triệu (0,5:1)|150|−48,7%|10|−52,4%|11|
|Vay 25 triệu (0,25:1)|125|−69,2%|17|−71,4%|18|

Giảm mức vay một nửa thì vùng an toàn rộng gấp đôi. Lãi cộng dồn làm nợ tăng mỗi ngày, nên các ngưỡng này nhích dần lên theo thời gian.

### Quy trình khi bị call

1. CTCK gửi thông báo call, thường sau phiên.
2. Bạn có hạn bổ sung, thường đến một giờ nhất định của phiên sau.
3. Không bổ sung kịp thì cổ phiếu bị bán, thường ngay đầu phiên.
4. Nếu Rtt rơi xuống dưới ngưỡng xử lý trong phiên, cổ phiếu có thể bị bán ngay. CTCK chọn mã nào để bán, không phải bạn.

### Hai cách xử lý

Nộp tiền luôn tốn ít hơn bán bớt, vì tiền nộp trừ thẳng vào nợ.

Nộp tiền, số tiền tối thiểu X:

```latex
X \geq N\text{ợ} - TS \times (1 - R_{dt})
```

Bán bớt cổ phiếu, giá trị bán tối thiểu S:

```latex
S \geq TS - \frac{NAV}{R_{dt}}
```

Ví dụ: TS còn 150 triệu, nợ 100 triệu, Rtt = 33,3% < 35%. Nộp tiền cần tối thiểu 100 − 150 × 0,65 = 2,5 triệu. Bán bớt cần tối thiểu 150 − 50 / 0,35 ≈ 7,1 triệu.

Một số CTCK yêu cầu đưa Rtt về mức cao hơn ngưỡng duy trì, nên số thực tế có thể lớn hơn. Mỗi phiên chần chừ, con số cần bù tăng rất nhanh.

### Bẫy call chéo

Khi mã A nằm sàn trắng bên mua, CTCK không bán được A. Họ bán mã B, C còn thanh khoản để thu hồi nợ. Cổ phiếu tốt của bạn bị bán đúng đáy vì mã xấu kéo cả tài khoản xuống.

## 7. Margin trong đọc thị trường

Force sell là bán bắt buộc, không phải bán do đánh giá lại doanh nghiệp. Vì vậy các đợt giảm có force sell thường quá đà, tạo cơ hội cho người còn tiền mặt.

- **Thanh khoản cao + giá giảm sâu nhiều phiên**: dấu hiệu bán tháo (Lesson 2), thường có force sell dây chuyền. Phiên bán tháo cực đại có thể là Selling Climax theo Wyckoff, nhưng cần xác nhận thêm.
- **Force sell thường diễn ra đầu phiên**: áp lực bán dồn vào ATO và đầu phiên sáng sau những phiên giảm mạnh liên tiếp.
- **Fibonacci quá đà**: margin bị ép bán đẩy các nhịp điều chỉnh sâu tới 70–78,6% thay vì dừng ở 50–61,8%.
- **Dư nợ margin toàn thị trường**: CTCK công bố theo quý. Dư nợ ở đỉnh lịch sử nghĩa là thị trường dễ tổn thương trước một cú sốc; dư nợ đã giảm mạnh sau đợt bán tháo nghĩa là nguồn cung bắt buộc đã cạn bớt.
- **CTCK hết room margin hoặc cắt margin một nhóm mã**: sức mua giảm đột ngột, nhóm mã đó dễ bị bán giảm vị thế hàng loạt.

## 8. Nguyên tắc sử dụng margin an toàn

Nguyên tắc gốc: stop loss của mình phải kích hoạt rất lâu trước khi CTCK kịp gọi call.

1. **Ngưỡng riêng cao hơn ngưỡng CTCK.** Không để Rtt dưới 60–70%, tức vay ít hơn nhiều so với hạn mức được phép.
2. **Cắt lỗ −7 đến −8% trên giá cổ phiếu.** Với mức này, tài khoản không bao giờ đến gần vùng call.
3. **Không dùng margin ở lệnh đầu tiên.** Chỉ nhồi bằng margin khi vị thế đã có lãi và vượt qua đủ khung xác nhận 5 lớp (thị trường, giai đoạn, sức mạnh tương đối, nền giá, điểm kích hoạt).
4. **Không dùng margin để bình quân giá xuống.** Đây là con đường ngắn nhất dẫn tới force sell.
5. **Không margin khi thị trường chung mập mờ.** Thị trường chưa vào Stage 2 rõ ràng thì đi bằng tiền mặt, vị thế nhỏ.
6. **Tránh mã có rủi ro sự kiện.** Sắp ĐHCĐ bất thường, phát hành thêm, bị cảnh báo hay có tin xấu đều dễ bị cắt margin.
7. **Tránh mã thanh khoản thấp.** Khi cần thoát có thể không bán được, hoặc chính mã đó gây call chéo.
8. **Giới hạn thời gian giữ.** Margin dành cho vị thế đang chạy; cổ phiếu đi ngang quá vài tuần thì trả bớt nợ.

## 9. Checklist và bài tập

Trước mỗi lệnh dùng margin, đi qua đủ checklist này. Một ô không tick được thì đi bằng tiền mặt.

- Đã biết ngưỡng call, ngưỡng xử lý và lãi suất hiện hành của SSI
- Mã nằm trong danh mục ký quỹ, đã biết tỷ lệ cho vay của mã
- Vị thế đã có lãi và qua đủ khung xác nhận 5 lớp
- Đã tính giá chạm call và force sell, cách xa điểm cắt lỗ
- Rtt sau lệnh vẫn ≥ 60%
- Không có sự kiện rủi ro sắp tới (ĐHCĐ bất thường, phát hành, cảnh báo)
- Có nguồn tiền mặt dự phòng nếu bị call

### Bài tập tự tính

Giả định ngưỡng call 35%, force sell 30%.

1. Vốn 80 triệu, vay 40 triệu, mua 120 triệu cổ phiếu. Giá giảm bao nhiêu % thì bị call? Bao nhiêu % thì bị force sell?
2. TS 190 triệu, nợ 130 triệu. Tài khoản đang ở trạng thái nào? Cần nộp bao nhiêu, hoặc bán bao nhiêu?
3. Vay 150 triệu ở 13%/năm, giữ 45 ngày. Tiền lãi là bao nhiêu?

### Đáp án

1. Call tại TS = 40 / 0,65 ≈ 61,5 triệu, tức giảm khoảng 48,7%. Force sell tại TS = 40 / 0,7 ≈ 57,1 triệu, tức giảm khoảng 52,4%.
2. Rtt = 60 / 190 ≈ 31,6%, nằm giữa 30% và 35% nên bị call. Nộp tối thiểu 130 − 190 × 0,65 = 6,5 triệu, hoặc bán tối thiểu 190 − 60 / 0,35 ≈ 18,6 triệu.
3. 150 × 13% × 45 / 365 ≈ 2,4 triệu.

Các ngưỡng và lãi suất trong bài là mức phổ biến trên thị trường. Con số áp dụng cho tài khoản của bạn nằm trong hợp đồng ký quỹ và biểu phí của SSI.