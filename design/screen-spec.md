# Screen spec — ý đồ từng màn hình

Mỗi màn hình dùng để làm gì, hiển thị nội dung gì và thuộc flow nào. Mã màn và tên frame giống page `03 Final UI` (section **Final UI · Nốt tích cực (24/10)**). Mã flow xem [`ux/user-flow.md`](../ux/user-flow.md). Cách dựng bằng Flutter xem [`handoff/flutter-handoff.md`](../handoff/flutter-handoff.md).

---

## 1. Màn hình

### S01 · Chào mừng & Đăng nhập

- **Để làm gì:** cổng vào khi chưa đăng nhập; cho người mới thấy ngay app nói về điều gì.
- **Nội dung:** tên "Nốt", câu "Mỗi ngày một nốt tích cực.", 3 mascot động (Thong Thả, Xong, Tập Trung), nút "Tiếp tục với Google", nút "Đăng nhập bằng email", dòng "Chưa có tài khoản? Đăng ký".
- **Hành động chính:** Tiếp tục với Google.
- **Flow:** P1, P2, P8 (sau đăng xuất), P7 (khi đang đăng xuất).

### S02 · Hôm nay (tab 1)

- **Để làm gì:** trả lời "Hôm nay bạn làm được gì?" và đưa người dùng vào 1 trong 3 việc chính.
- **Nội dung:** ngày ("Thứ Bảy, 24/10"), hình hũ chiến thắng lớn với số nốt hôm nay, mascot Xong, câu hỏi chính, nút "Ghi nốt", hai lối tắt "Dừng lại" và "Thở 90 giây", thẻ gợi ý "Thử thách".
- **Hành động chính:** Ghi nốt.
- **Flow:** F1, F2, F3; P1, P2, P3, P7.

### S03 · Ghi nốt

- **Để làm gì:** ghi một chiến thắng nhỏ trong dưới 30 giây.
- **Bước 1 (`S03a`):** "Hôm nay bạn thấy thế nào?" — 5 ô tâm trạng (Vui, Ổn, Bình thường, Mệt, Rối) có mặt mascot, nút "Tiếp". Chọn "Rối" thì hiện thêm "Ngày rối: 1 chip là đủ." và thẻ "Sơ cứu 1 phút: 5-4-3-2-1" với nút "Làm cùng Nốt".
- **Bước 2 (`S03b`):** "Hôm nay bạn làm được gì?" — ô "Chiến thắng nhỏ", 6 chip chọn nhanh (Dọn phòng, Giúp ai đó, Đi bộ, Ăn đủ bữa, Ngủ trước 12h, Xong 1 việc khó), nút "Tiếp", nút chữ "Bỏ qua nhật ký".
- **Bước 3:** vài dòng nhật ký, không bắt buộc, rồi Lưu.
- **Biến thể AI (thiết kế sẵn cho Final Assignment):** tab "Kể tự do" → "Nốt AI sắp xếp giúp" → đang đọc (nút Loading, Huỷ) → "Nốt tìm thấy 3 điều tốt" (nhãn "Gợi ý từ AI · chạm để sửa", nút "Lưu 3 nốt vào hũ") → khi lỗi: "Nốt AI đang nghỉ một chút. Đoạn viết vẫn còn đây." + tự chọn loại nốt. Lần đầu dùng có sheet quyền riêng tư (Gửi đi / Không gửi / Bạn quyết).
- **Dialog:** "Giữ nốt đang ghi? Nốt sẽ chờ ở Hôm nay." — Bỏ / Giữ nháp (khi bấm Back giữa chừng).
- **Hành động chính:** Tiếp (mỗi bước).
- **Flow:** F1; P7, T1.

### S04 · Nốt đã vào hũ

- **Để làm gì:** phản hồi ngay, cho thấy nốt vừa ghi có ý nghĩa.
- **Nội dung:** "Đã vào hũ!", "Nốt thứ 24 tháng này.", tờ nốt vừa ghi (loại, tiêu đề, "Hôm nay · Ổn"), thanh "Mốc tháng 10 · 24/25 nốt", confetti, nút "Về Hôm nay", nút chữ "Viết thêm".
- **Biến thể:** lưu khi mất mạng (banner "Offline · đã lưu trên máy", "Sẽ tự đồng bộ khi có mạng."); đạt mốc tháng ("Mốc 25 nốt!", nhãn dán tháng, nút "Gắn vào hũ" / "Để sau").
- **Hành động chính:** Về Hôm nay.
- **Flow:** F1, F3; P3, T1.

### S05 · Hũ & Nhật ký (tab 2)

- **Để làm gì:** xem lại mọi điều tốt đã ghi, theo dạng lưới tờ nốt.
- **Nội dung:** "Hũ của bạn", số nốt tháng ("24 nốt tháng 10"), "2 nhãn dán ›", lưới 2 cột tờ nốt màu theo loại (Chiến thắng, Tự chủ, Thử thách, Nhật ký) có tiêu đề và ngày.
- **Trạng thái:** rỗng ("Hũ còn trống. Ghi chiến thắng đầu tiên nhé." + "Ghi nốt đầu tiên"); lỗi mất mạng ("Chưa tải được hũ. Kiểm tra Wi-Fi rồi thử lại." + "Thử lại"); vừa xoá ("Đã xoá nốt · còn 5 giây" + "Hoàn tác").
- **Hành động chính:** chạm một tờ nốt.
- **Flow:** P4, P5, P6, T1, T2.

### S06 · Chi tiết nốt

- **Để làm gì:** đọc lại, sửa hoặc viết thêm nhật ký cho một nốt.
- **Nội dung:** "Tâm trạng hôm đó: Ổn", nhãn "✓ CHIẾN THẮNG · 24/10", tiêu đề, đoạn nhật ký, mascot Thong Thả. App bar có Sửa và Xoá.
- **Dialog:** "Xoá nốt này? Bạn có 5 giây để hoàn tác." — Huỷ / Xoá (destructive).
- **Flow:** P4, P5, P6.

### S07 · Thử thách (tab 3)

- **Để làm gì:** đưa ra đúng một thẻ thử thách vừa sức.
- **Nội dung:** chủ đề và cấp ("Dũng cảm · cấp 2", "3/5"), thẻ lớn ("DŨNG CẢM · 2 PHÚT", "Hỏi thầy 1 câu sau giờ học"), mascot Tập Trung, nút "Nhận thử thách", gợi ý "Vuốt để đổi thẻ".
- **Hành động chính:** Nhận thử thách.
- **Flow:** F3; P3.

### S08 · Chi tiết thử thách

- **Để làm gì:** làm thử thách và ghi cảm giác trước/sau.
- **Nội dung:** nhãn, tên thử thách, mẹo ngắn ("Hỏi ngắn thôi, 30 giây là đủ."), thang hồi hộp 1–5 (Bình tĩnh → Run lắm), câu mẫu để nói, nút "Xong rồi", nút chữ "Đổi thẻ dễ hơn".
- **Hành động chính:** Xong rồi.
- **Flow:** F3; P3, P7.

### S09 · Tự chủ

- **Để làm gì:** ghi nhận mỗi lần dừng "dopamine rẻ", nơi riêng tư (mở bằng khoá).
- **Nội dung:** "8 lần tự chủ tháng này", nút "Mình vừa dừng lại", nút tonal "Khó dừng? Thở 90 giây", nhóm "THÓI QUEN MUỐN BỚT" (Lướt mạng xã hội, Video ngắn, Game quá giờ, Nội dung không lành mạnh, + Thêm), dòng "Giờ tỉnh · 23:00 – 01:00" có công tắc.
- **Hành động chính:** Mình vừa dừng lại.
- **Flow:** F2; P8 (khoá).

### S10 · Thở 90 giây

- **Để làm gì:** giúp vượt qua cơn thôi thúc khi khó dừng.
- **Nội dung:** "Thở cùng Nốt", sóng thở và chữ "Hít vào…", "4 giây vào · 6 giây ra", "Còn 1:12", nút "Đổi kiểu thở", nút "Cơn sóng đã hạ", nút chữ "Thở thêm 1 vòng".
- **Sau khi thở:** "Bạn đã vượt qua!", "3 lần dừng lại hôm nay", "Làm gì tiếp?" với chip Đi bộ 5 phút, Uống nước, Nhắn một người bạn, Đi ngủ; nút "Ghi vào hũ", nút chữ "Về Hôm nay".
- **Flow:** F2.

### S11 · Hành trình (tab 4)

- **Để làm gì:** nhìn lại tiến bộ, nhất là vào ngày tệ.
- **Tab con:** Con đường · Thống kê · Lịch.
- **S11a Con đường:** các chặng thử thách ("CHẶNG 2 · DŨNG CẢM · Bắt chuyện với người lạ · 3/5"), nhãn dán đã mở / chưa mở.
- **S11b Thống kê:** "Nốt tuần này 18 (↑ 20%)", "Chuỗi ngày 6 · Kỷ lục 9", biểu đồ "Năng lượng mỗi ngày" (30 ngày, thang 1–5, có tooltip), "Mục tiêu tuần 5/7", "Cân bằng 5 điều tốt" (số nốt mỗi loại + gợi ý loại đang ít), "Bạn ghi nốt ngày nào?". Thẻ tuần dạng story có nút "Lưu thẻ tuần (PDF)".
- **S11c Lịch năng lượng:** lưới tháng, mỗi ô có số ngày, màu và mặt mascot theo tâm trạng; chuyển Tháng / Năm; chú giải "Vui … Rối · Ý nghĩa màu". Trạng thái đang tải: skeleton "Đang tải lịch năng lượng…".
- **Bonus AI:** "Hỏi Nốt" ("Tháng này mình tự chủ được mấy lần?" → "9 lần", có biểu đồ nhỏ và câu "Tính từ 46 nốt tháng 10 của bạn").
- **Flow:** P6, P8, T2, T3; F4 trong prototype.

### S12 · Cài đặt

- **Để làm gì:** chỉnh giờ nhắc, quyền riêng tư và tài khoản.
- **Nội dung:** NHẮC NHỞ (Nhắc ghi nốt buổi tối 21:30, Giờ tỉnh 23:00 – 01:00); QUYỀN RIÊNG TƯ (Nốt AI sắp xếp giúp — "Không gửi tên, email, ảnh"; Khoá phần Tự chủ; Ẩn nội dung thông báo); TÀI KHOẢN (Email); nút "Đăng xuất".
- **Flow:** P1, P2, P8.

---

## 2. Dữ liệu mẫu dùng trên các màn

| Dữ liệu | Giá trị |
|---|---|
| Người dùng | Minh, `minh.ng@gmail.com`, dùng app từ 01/03, 187 nốt |
| Ngày hiện tại | Thứ Bảy, 24/10 (tuần 43) |
| Nốt tháng 10 | 24 nốt; mốc tháng 25 nốt |
| Nốt mẫu | Chiến thắng "Dọn bàn học, gửi email hỏi thầy" (Hôm nay · Ổn); Tự chủ "Dừng lướt TikTok lúc 0h15" (Hôm qua); Thử thách "Hỏi thầy Nam về đề tài" (T5); Nhật ký "Vì sao tuần này mình mệt" (T4); "Đi bộ 20 phút sau giờ học", "Tắt game lúc 23h" (T3) |
| Tự chủ | 8 lần tháng này (9 lần theo Hỏi Nốt), 3 lần dừng lại hôm nay |
| Thử thách | Dũng cảm · cấp 2 · 3/5 — "Hỏi thầy 1 câu sau giờ học" |
| Cân bằng tháng 10 | Chiến thắng 18, Nhật ký 12, Tự chủ 9, Vận động 3, Người lạ 4 |
