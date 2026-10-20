# Screen spec — ý đồ từng màn hình

Mỗi màn trả lời một câu hỏi của người dùng và có đúng một hành động chính. Mã màn là mã trong tên frame ở page `03 Final UI` của Figma (ví dụ `7s` là `Device · 7s · Giai đoạn: Chạy thực nghiệm`). Mã flow giống page 01 và 06 (xem [`ux/user-flow.md`](../ux/user-flow.md)). Cách dựng bằng Flutter ở [`handoff/flutter-handoff.md`](../handoff/flutter-handoff.md).

Đọc lại từ Figma ngày 20/10/2026.

---

## 1. Màn hình theo nhóm

### 01 · Xác thực

| Mã | Màn | Câu hỏi màn trả lời | Nội dung | Hành động chính | Flow |
|---|---|---|---|---|---|
| `1` | Đăng nhập | "Vào app bằng cách nào?" | Mascot, tên "Nốt", câu "Gom mọi deadline về một chỗ. Biết hôm nay nên làm gì trước." | Tiếp tục với Google (phụ: Đăng nhập bằng email, Đăng ký) | P1, P2 |
| `1b` | Đăng nhập bằng email | "Đăng nhập bằng email thế nào?" | Email, Mật khẩu (nút Hiện), Quên mật khẩu? | Đăng nhập | P2 |
| `1d` | Đăng nhập email — lỗi | "Sai ở đâu?" | Như `1b`, dòng lỗi "Sai email hoặc mật khẩu." | Đăng nhập lại hoặc Quên mật khẩu? | P2 |
| `1c` | Đăng ký | "Tạo tài khoản cần gì?" | Tên hiển thị, Email, Mật khẩu (gợi ý "Ít nhất 8 ký tự.") | Tạo tài khoản | P1 |
| `1e` | Quên mật khẩu | "Lấy lại mật khẩu thế nào?" | Ô email | Gửi link | P2 |
| `1f` | Kiểm tra email | "Đã gửi chưa, làm gì tiếp?" | Hướng dẫn mở email, "Chưa nhận được? Gửi lại" | Mở ứng dụng email | P2 |
| `1g` | Đặt mật khẩu mới | "Đặt mật khẩu mới ra sao?" | Mật khẩu mới, Nhập lại mật khẩu | Lưu mật khẩu | P2 |
| `1h` | Đổi mật khẩu thành công | "Xong chưa?" | "Đã đổi mật khẩu" | Vào Nốt | P2 |

### 02 · Làm quen

| Mã | Màn | Câu hỏi | Nội dung | Hành động chính | Flow |
|---|---|---|---|---|---|
| `O1` | Làm quen | "App sẽ hỏi gì?" | "Làm quen với Nốt nhé! 3 câu hỏi ngắn" | Bắt đầu (phụ: Để sau) | P1 |
| `O2` | Bạn đang là? (1/3) | "Mình thuộc nhóm nào?" | Sinh viên năm nhất, năm 2–3, năm cuối, Đang thực tập, Đã đi làm (chọn một) | Tiếp tục | P1 |
| `O3` | Tuần có gì cố định? (2/3) | "Lịch cố định của mình?" | Chọn nhiều: Lịch học, Đồ án, Họp nhóm, Freelance, Ca làm thêm, Giờ thực tập, Đi làm, Tập thể thao, Học thêm, + Thêm khác | Tiếp tục (phụ: Bỏ qua bước này) | P1 |
| `O4` | Muốn tốt hơn ở điều gì? (3/3) | "Mình muốn app giúp gì?" | Chọn nhiều: Không dồn deadline, Thấy rõ tiến bộ, Được nhắc trước hạn, Chia nhỏ bài lớn, Nộp đúng hạn, Gom tài liệu một chỗ, Mục tiêu riêng, + Thêm khác | Xong (phụ: Bỏ qua bước này) | P1 |

### 03 · Hôm nay

| Mã | Màn | Câu hỏi | Nội dung | Hành động chính | Flow |
|---|---|---|---|---|---|
| `2` | Hôm nay | "Hôm nay làm gì trước?" | Ngày ("Thứ Tư, 7/10"), chuông thông báo; thẻ **Hạn hôm nay** (Lab 2: Thiết kế UI · Còn 1 việc · Hoàn thiện và nộp); thẻ chuỗi "3 ngày liên tiếp đúng hạn"; dải 7 ngày tới theo độ nặng; mục **Cần để ý** (Tiểu luận chương 3 hay bị dời, Thứ Sáu đang quá nặng) | Xem việc cần làm | C2, C3, C4, P5, P7 |
| `2c0` | Chia nhỏ — 1/3 Vì sao bị dời | "Vì sao việc này cứ bị dời?" | Tiểu luận chương 3 · Hạn T6 9/10 · Đã dời 3 lần; lý do: Việc quá to, Không có giờ trống, Chưa rõ đề bài | Tiếp | P7, P4 |
| `2c` | Chia nhỏ — 2/3 Chia bước | "Chia thành những bước nào?" | "Nốt gợi ý 3 bước, mỗi bước khoảng 45 phút. Bạn sửa hoặc thêm được." Đọc lại chương 3, Viết bản nháp, Soát lỗi và nộp, + Thêm bước | Tiếp: chọn giờ | P7 |
| `2c2` | Chia nhỏ — thêm bước | (biến thể của `2c`) | Ô "Nhập tên bước…" | Tiếp: chọn giờ | P7 |
| `2c3` | Chia nhỏ — 3/3 Xếp giờ | "Làm mỗi bước lúc nào?" | Mỗi bước một giờ: T4 20:00, T5 19:30, T6 10:00 (người dùng chọn) | Xếp vào lịch | P7 |
| `3c` | Kế hoạch — đã xếp 3 buổi | (biến thể của `3`) | Lịch tháng có 3 buổi mới | — | P7 |
| `2f` | Bảng thành tích tuần này | "Tuần này mình làm được gì?" | Số ngày liên tiếp đúng hạn, "3/3 deadline nộp đúng hạn", số giai đoạn đã xong; danh sách theo ngày (Nộp Báo cáo tuần 4 · sớm 1 ngày, Giai đoạn 2/3 Thiết kế UI…); "Tự ghi lại khi bạn nộp deadline hoặc tick xong một giai đoạn" | Chạm một việc đã làm | P5 |

### 04 · Kế hoạch

| Mã | Màn | Câu hỏi | Nội dung | Hành động chính | Flow |
|---|---|---|---|---|---|
| `3` | Kế hoạch — Tháng | "Ngày nào quá nặng?" | Nút Tháng / Tuần; "Tháng 10, 2026"; lưới 7 cột, mỗi ô có ngày, màu nhiệt, số độ nặng và khuôn mặt mascot | Chạm một ngày | C4, P8 |
| `4` | Chi tiết ngày | "Ngày này có gì, dời bớt được không?" | "Thứ Sáu, 9/10 · Rất nặng · 5 việc · 3 việc đến hạn ngày này"; gợi ý "Dời 2 việc để thứ Sáu nhẹ hơn · Sang T5 và T7 · Rất nặng → Nặng"; danh sách việc, việc dời được ghi "dời được" | Xem trước (giãn việc) | C4 |
| `4b` | Xem trước dời việc | "Dời việc nào, sang ngày nào?" | Thay đổi độ nặng từng ngày (T6 Rất nặng → Nặng, T5 Nhẹ → Vừa); việc chọn để dời và ngày đề xuất; 3 việc đến hạn ngay thứ Sáu (không dời được); "Đề xuất là ngày gần nhất còn nhẹ trước hạn nộp" | Dời 2 việc | C4, C3 |
| `4c` | Chọn ngày dời (sheet) | "Muốn ngày khác thì sao?" | Lịch chọn ngày; màu là độ nặng nếu thêm việc vào ngày đó; hạn nộp của việc | Chọn ngày | C4 |
| `3d` | Kế hoạch — đã dời | (biến thể của `3`) | Lịch đã đổi màu, snackbar có Hoàn tác | — | C4 |
| `4d` | Chi tiết ngày — không dời được | "Không dời được thì làm gì?" | "Chưa có ngày đủ nhẹ để dời. Các ngày trước hạn nộp đều đã từ mức Vừa trở lên." | Chia nhỏ một việc | C4, P4 |
| `9` | Kế hoạch — Tuần | "Tuần này bận lúc nào?" | Lưới giờ T2–CN: giờ bận (Freelance: landing page, Họp nhóm đồ án), giai đoạn (Paper · Chạy thực nghiệm), việc đã xong | Nút + (thêm giờ bận) | P8 |
| `9d` | Thêm giờ bận (sheet) | "Thêm giờ bận thế nào?" | Tên ("Làm thêm ở quán cà phê"), Từ 18:00, Đến 22:00, Mỗi tuần | Lưu giờ bận | P8 |
| `9e` | Nhấn giữ để hoãn | "Hoãn việc này thế nào?" | Việc "Đã dời 3 lần"; Để mai, Chia nhỏ việc này | Để mai | P8, P7 |

### 05 · Thông báo

| Mã | Màn | Câu hỏi | Nội dung | Hành động chính | Flow |
|---|---|---|---|---|---|
| `13` | Thông báo | "Có gì mới cần làm?" | Tất cả / Chưa đọc · 3; Đọc hết; mỗi dòng một loại (Tới giờ làm: Chạy thực nghiệm; Quiz ITE302c hết hạn 23:59; Thứ Sáu đang quá nặng; 3 ngày liên tiếp đúng hạn; Tiểu luận chương 3 quá hạn; Đã nộp Lab 2 đúng hạn) | Chạm một thông báo | C3 |
| `13A`, `13B` | Hai phương án của `13` | — | Nền nhạt cho tin chưa đọc / kiểu hộp thư. Nhóm chọn một phương án khi dựng | — | C3 |
| `13p` | Thông báo đẩy (màn khoá) | "Bây giờ cần làm gì?" | "NỐT · Nhắc giai đoạn · bây giờ"; "Tới giờ làm: Chạy thực nghiệm"; "Paper · ngày 3/7 · 20:00 mỗi ngày" | Mở giai đoạn (phụ: Nhắc lại 15 phút) | C1, C3 |

### 06 · Deadline

| Mã | Màn | Câu hỏi | Nội dung | Hành động chính | Flow |
|---|---|---|---|---|---|
| `5` | Deadline — Sắp đến hạn | "Việc nào gấp nhất?" | Nút Sắp đến hạn / Môn học; "1 quá hạn"; nhóm Quá hạn, Hôm nay, Tuần này (mỗi nhóm có MascotMini); mỗi dòng: tên, mã môn · x/y giai đoạn, nhãn hạn ("Trễ 1 ngày", "Còn 6 giờ") | Nút + thêm deadline | C2, P3, S1, S2 |
| Rỗng | Trạng thái rỗng của `5` | "Chưa có gì thì làm gì?" | "Chưa có deadline nào. Nốt sẽ nhắc bạn trước hạn." | Thêm deadline | S1 |
| Đang tải | Trạng thái đang tải của `5` | — | "Đang đồng bộ deadline…" | — | S2 |
| Lỗi mất mạng | Trạng thái lỗi của `5` | "Sao không thấy gì?" | "Mất kết nối. Kiểm tra kết nối rồi thử lại." | Thử lại | S2 |
| `10b` | Deadline — Môn · Dự án | "Môn nào còn bao nhiêu việc?" | PRM393 (1/4), WDP301 (1/2), MLN111, PAPER (1 deadline · 4 giai đoạn), ITE302c (0/2) | Chạm một môn | P6 |
| `10c` | Chi tiết môn học | "Môn này còn gì?" | PRM393 · Lập trình di động · 3 còn lại · 1 đã nộp; Lab 2 (Còn 6 giờ), Lab 3 (Còn 9 ngày), Quiz giữa kỳ (Còn 2 tuần) | Chạm một deadline | P6 |
| `6b` | Thêm môn học | "Thêm môn thế nào?" | Tên môn, Mã môn, Màu nhận diện | Lưu môn học | C1, P6 |
| `6` | Thêm deadline — B1/5 | "Deadline này thuộc môn hay dự án?" | Môn học / Dự án; danh sách (PAPER Paper hội nghị, ĐATN Đồ án tốt nghiệp, WORK Làm thêm, KHÁC Việc phát sinh, ITE302c…); Thêm dự án mới | Tiếp · nhập deadline | C1, S1 |
| `6b2` | Thêm deadline — B2/5 | "Deadline tên gì, hạn khi nào?" | Tên deadline; Loại (Báo cáo, Bài báo, Đồ án, Thuyết trình, Công việc, Khác) kèm độ nặng; Hạn chót ("CN, 15/11 · còn 31 ngày để chia giai đoạn"); Nhắc trước | Tiếp | C1 |
| `6b2a` | Thêm deadline — B3/5 Mô tả | "Việc này cần làm gì?" | Mô tả (không bắt buộc, tối đa 500 ký tự): việc cần làm và ai làm phần nào. "AI dùng mô tả này để gợi ý giai đoạn" | Tiếp · chia giai đoạn | C1 |
| `6b3` | Thêm deadline — B4/5 Giai đoạn | "Chia 31 ngày thế nào?" | Thanh từ hôm nay tới hạn chót; danh sách giai đoạn (tên, từ → đến, số ngày). 4 trạng thái: **Chưa có giai đoạn** (AI gợi ý giai đoạn / Thêm giai đoạn), **AI đang chia** ("AI đang chia 31 ngày theo mô tả…"), **Đề xuất của AI** (Chạm để sửa, Tạo lại), **AI lỗi** ("Mất kết nối khi gọi AI. Mô tả của bạn vẫn được giữ." Thử lại / Tự nhập tay) | Dùng 4 giai đoạn · xem lại | C1 |
| `6b4` | Thêm giai đoạn (sheet) | "Giai đoạn này từ ngày nào, nhắc lúc mấy giờ?" | Tên, từ ngày, đến ngày, giờ nhắc mỗi ngày; "Đã chia 31/31 ngày" | Lưu giai đoạn | C1 |
| `6b5` | Thêm deadline — B5/5 Xem lại | "Đúng chưa trước khi lưu?" | Tóm tắt deadline; 4 giai đoạn; **Lịch thông báo** (4 mốc nhắc) | Lưu và bật nhắc | C1 |
| `7c` | Deadline vừa tạo | (biến thể của `7`) | "Còn 31 ngày · Hạn CN 15/11 · Nhắc 3 ngày, 1 ngày trước"; 0/4 xong; Thêm link nộp (không bắt buộc); snackbar "Đã thêm Nộp paper hội nghị" | Chạm giai đoạn | C1 |
| `7` | Chi tiết deadline | "Việc này đang tới đâu?" | Lab 2 · PRM393 · Còn 6 giờ · 23:59 hôm nay; Giai đoạn 2/3 xong (tên, ngày, giờ làm); link nộp; Ghi chú; "Tick đủ 3 giai đoạn để hoàn thành" | Hoàn thành deadline (tắt tới khi đủ giai đoạn) | C2, C3 |
| `7d` | Chi tiết — đủ 3/3 | (biến thể của `7`) | "Đã xong cả 3 giai đoạn" | Hoàn thành deadline (bật) | C2 |
| Overlay | Hoàn thành deadline | "Chắc chắn hoàn thành?" | "Hoàn thành Lab 2? Bạn đã xong cả 3 giai đoạn…" | Hoàn thành (phụ: Huỷ) | C2 |
| `8` | Đã nộp | "Xong chưa, tiếp theo là gì?" | Mascot Nốt Xong; "Lab 2: Thiết kế UI · Sớm hơn hạn 6 giờ · Chuỗi 3 ngày đúng hạn" | Xem việc tiếp theo (phụ: Về Deadline) | C2 |
| `7s` | Chi tiết giai đoạn | "Hôm nay làm gì cho giai đoạn này?" | "Paper · Giai đoạn 1/4 · Ngày 3/7 · Chạy thực nghiệm · T6 16/10 → T5 22/10 · Nhắc 20:00 mỗi ngày"; Tài liệu (DOCX, PDF, XLSX); Ghi chép ("Tuấn lo phần chạy. Xong 2/5 cấu hình, F1 tăng 3%.") | Tải lên hoặc Thêm ghi chép | C1, C2, C3 |
| `7s1`, `7s2` | Giai đoạn đã xong | (biến thể của `7s`) | "Đã xong · Hoàn thành T2 5/10 · đúng ngày dự kiến"; ghi chép kèm link và ảnh | Thêm ghi chép | C2, P5 |
| `7t` | Thêm ghi chép và tài liệu (sheet) | "Ghi lại gì, đính kèm gì?" | Ghi chép; "Tài liệu đã làm · 5"; Tải lên tệp (DOCX, PDF, XLSX, ZIP…), ảnh, link | Lưu ghi chép | C1, C2 |
| `7b` | Sửa deadline | "Sửa gì?" | Môn (Đổi môn), Tên, Loại, Hạn chót, Nhắc trước (1 ngày, 3 giờ, 1 giờ, Không nhắc) | Lưu (phụ: Xoá deadline) | C2 |
| Overlay | Xoá deadline | "Chắc chắn xoá?" | "Xoá cả 3 giai đoạn, ghi chép và lời nhắc. Không hoàn tác được." | Xoá (phụ: Huỷ) | C2 |
| `5e` | Đã xoá deadline | (biến thể của `5`) | Snackbar "Đã xoá deadline" | — | C2 |
| `7o` | Quá hạn | "Trễ rồi, giờ làm gì?" | Quiz ITE302c tuần 1 · Trễ 1 ngày · Chưa nộp; "Vì sao bị tính quá hạn"; giai đoạn 0/1; 3 lựa chọn: Đã nộp muộn, Dời hạn, Bỏ deadline | Chọn một cách xử lý | P3, C3 |
| `7o2` | Dời hạn | (biến thể của `7o`) | Chọn hạn mới, giữ các giai đoạn | Lưu hạn mới | P3 |
| Overlay | Bỏ deadline | "Chắc chắn bỏ?" | "Deadline sẽ ẩn khỏi danh sách và không còn nhắc." | Bỏ deadline (phụ: Huỷ) | P3 |
| `5o1`, `5o2`, `5o3` | Sau khi xử lý quá hạn | (biến thể của `5`) | Snackbar "Đã nộp muộn" / "Đã dời hạn" / "Đã bỏ deadline" | — | P3 |

### 07 · Hồ sơ, Cài đặt

| Mã | Màn | Câu hỏi | Nội dung | Hành động chính | Flow |
|---|---|---|---|---|---|
| `10` | Hồ sơ | "Mình đang làm tốt không?" | Tên, email; Chuỗi, Đã nộp 3/3, Đúng hạn; tuần này T2–CN; Bảng thành tích nhỏ | Cài đặt | P5, P6 |
| `10f` | Đã nộp tuần này | "Tuần này đã nộp gì?" | Theo môn: Lập trình di động 3 bài · đúng hạn; danh sách bài đã nộp theo ngày | — | P6 |
| `10e` | Cài đặt | "Chỉnh app thế nào?" | Thông báo nhắc hạn, Nhắc trước hạn (1 ngày), Môn học của tôi (5 môn), Mục tiêu riêng, Xuất báo cáo tuần (PDF), Hướng dẫn sử dụng, Công cụ demo | Đăng xuất (cuối màn) | P6, S3 |
| `11` | Hướng dẫn sử dụng | "Dùng app thế nào?" | 4 mẹo: Thêm môn học, Thêm deadline, Xem ngày nào nặng, Đánh dấu đã nộp; Xem ý nghĩa các icon | Bắt đầu dùng | P6 |
| `12` | Ý nghĩa icon | "Màu và mặt này nghĩa là gì?" | Trạng thái deadline; màu ngày (Rất nhẹ 1 → Rất nặng 8+); độ nặng từng loại việc | — | P6 |
| `14` | Cấu hình ứng dụng | "App đang dùng giá trị nào?" | Giá trị Remote Config: `today_max_tasks` (mặc định 5), `show_study_tip`, `reminder_hours_before` (mặc định 12); thời điểm tải | Tải lại cấu hình | S3 |
| `15` | Kiểm tra lỗi | "Báo cáo lỗi có chạy không?" | Crashlytics đang bật; lần gửi gần nhất | Gây lỗi thử (phụ: Ghi lỗi, không đóng app) | S3 |
| `15b` | Dialog đóng app | "Chắc chắn đóng app?" | "Đóng app để thử lỗi? App đóng ngay. Mở lại để gửi báo cáo." | Đóng app (phụ: Để sau) | S3 |

---

## 2. Dữ liệu mẫu dùng trên các màn

Lấy đúng từ Figma để màn này khớp màn kia.

### 2.1 Deadline dài nhiều giai đoạn (Minh)

**Nộp paper hội nghị** · dự án PAPER · loại Bài báo · hạn CN 15/11, 23:59 · tạo ngày T6 16/10 · 31 ngày · nhắc 3 ngày và 1 ngày trước hạn.

| Giai đoạn | Từ → đến | Số ngày | Nhắc mỗi ngày |
|---|---|---|---|
| Chạy thực nghiệm | T6 16/10 → T5 22/10 | 7 | 20:00 |
| Viết báo | T6 23/10 → CN 01/11 | 10 | theo `6b4` |
| Check đạo văn | T2 02/11 → T5 05/11 | 4 | 09:00 |
| Chỉnh sửa và nộp | T6 06/11 → CN 15/11 | 10 | theo `6b4` |

Tài liệu ở giai đoạn 1: `Thiet-ke-thuc-nghiem.docx` (248 KB), `Baseline-paper.pdf` (1,2 MB), `Ket-qua-thuc-nghiem.xlsx` (1,2 MB), `bieu-do-F1.png` (860 KB). Ghi chép: "Tuấn lo phần chạy. Xong 2/5 cấu hình, F1 tăng 3%."

### 2.2 Deadline của tuần (màn Hôm nay, Deadline, Kế hoạch)

| Deadline | Môn | Hạn | Giai đoạn | Ghi chú |
|---|---|---|---|---|
| Lab 2: Thiết kế UI | PRM393 | Hôm nay T4 7/10, 23:59 | 2/3 (Wireframe, Thiết kế UI, Hoàn thiện và nộp) | Link nộp `lms.fpt.edu.vn/prm393/lab2` |
| Quiz ITE302c tuần 1 | ITE302c | T3 6/10, 23:59 (trễ 1 ngày) | 0/1 | Dùng cho P3 |
| Báo cáo sprint 2 | WDP301 | T6 9/10 | 1/3 | |
| Tiểu luận chương 3 | MLN111 | T6 9/10 | 0/3 | Đã dời 3 lần, dùng cho P7 |
| Quiz ITE302c tuần 2 | ITE302c | T6 9/10 | 1/2 | |
| Slide thuyết trình nhóm | WDP301 | T3 13/10 | — | Dời được |
| Đề cương đồ án | Đồ án | CN 19/10 | — | Dời được |

### 2.3 Môn và dự án

PRM393 Lập trình di động · WDP301 Phát triển web · MLN111 Triết học Mác–Lênin · ITE302c Đạo đức nghề nghiệp · PAPER Nghiên cứu · viết Paper · ĐATN Đồ án tốt nghiệp · WORK Làm thêm · KHÁC Việc phát sinh.

### 2.4 Giờ bận

Freelance: landing page · Họp nhóm đồ án · Làm thêm ở quán cà phê 18:00–22:00, lặp mỗi tuần.

> **Lưu ý:** dữ liệu mẫu có hai "hôm nay": nhóm màn Lab 2 lấy ngày T4 7/10, nhóm màn Paper lấy ngày T6 16/10 (và `13p` là CN 18/10). Khi dựng app ở Lab 3, seed data nên dùng ngày tương đối so với ngày chạy.
