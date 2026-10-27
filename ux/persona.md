# Persona và vấn đề

**Đề tài:** "Nốt" — app ghi chú hằng ngày mang năng lượng tích cực cho sinh viên năm cuối đang kiệt sức (và người trẻ đi làm). Mỗi tối người dùng ghi một "chiến thắng nhỏ" thay vì nhìn danh sách việc chưa xong. App gom 5 thói quen tốt vào một vòng lặp hằng ngày: (1) chiến thắng nhỏ, (2) nhật ký, (3) tự chủ trước "dopamine rẻ", (4) nói chuyện với người lạ, (5) vận động.

> **Đổi hướng ngày 24/10/2026.** Theo góp ý của giảng viên, Nốt chuyển từ app quản lý deadline (Study Planner) sang app ghi chú tích cực. Giữ bảng màu, font và mascot Tụi Nốt. Bản Study Planner cũ nằm ở lịch sử Git (commit `5f00bff`).

Nguồn thiết kế: file Figma [`PRM393-LAB2-Study-Planner`](https://www.figma.com/design/OkTRYkrsoJ0nkluNO4mrHz/PRM393-LAB2-Study-Planner), page `03 Final UI`, section **Final UI · Nốt tích cực (24/10)**.

---

## 1. Phát biểu vấn đề (một câu)

Sinh viên năm cuối đang kiệt sức chỉ nhớ những gì mình chưa làm được, nên mỗi tối kết thúc bằng cảm giác thất bại và không còn động lực cho ngày mai.

## 2. Tiêu chí thành công đo được

| # | Tiêu chí | Cách đo |
|---|---|---|
| **Chính** | Người dùng ghi xong một chiến thắng nhỏ (chọn tâm trạng + 1 chiến thắng) trong **dưới 30 giây** kể từ khi chạm thông báo buổi tối | Thời gian từ lúc mở `S03` (bước 1) đến lúc thấy `S04 · Nốt đã vào hũ`. Lab 3 đo bằng sự kiện Analytics và bài test ARTEMIS |
| Phụ | Ghi một lần tự chủ từ màn Hôm nay chỉ cần **2 lần chạm** ("Dừng lại" → "Mình vừa dừng lại"), không cần mở khoá | Số lần chạm từ `S02` đến khi thấy `S04` |
| Phụ | Màn hình thở 90 giây (`S10`) mở ra trong **dưới 2 giây** | Thời gian từ lúc chạm "Thở 90 giây" đến khi sóng thở bắt đầu chạy |

---

## 3. Persona chính: Minh

> *"Cuối ngày mình chỉ nhớ những việc chưa xong. Mở Notion ra là thấy mình tệ."*

| Mục | Nội dung |
|---|---|
| Tuổi, vai trò | 22, sinh viên năm 4 ngành Kỹ thuật phần mềm, trưởng nhóm nghiên cứu 4 người, làm part-time |
| Bối cảnh hằng ngày | Học, họp nhóm, đi làm thêm; về phòng trọ khoảng 22h. Đã dùng Calendar, Notion, ClickUp, Linear nên việc được quản lý đủ, nhưng tinh thần thì không. |
| Thói quen thiết bị | Điện thoại Android, dùng nhiều nhất 22h–1h sáng, nằm trên giường, một tay, độ sáng thấp. Laptop chỉ để làm việc. |
| Mục tiêu | Thấy mình có tiến bộ mỗi ngày; ngủ trước 1h; bớt lướt điện thoại vô thức; dám hỏi giảng viên khi bế tắc; quay lại đi bộ / tập thể dục. |
| Nỗi đau | Mỗi tối kết thúc bằng danh sách việc chưa xong; lướt TikTok, chơi game và xem nội dung không lành mạnh đến 1–2h sáng để trốn áp lực, rồi tự trách; ngại nhắn hỏi thầy cô; bỏ tập từ đầu kỳ; app năng suất làm anh thấy bị chấm điểm. |
| Điều anh KHÔNG muốn | Thêm một app bắt điểm danh, mất chuỗi là về 0, hay giọng điệu "cố lên nào!" sáo rỗng. |
| Nhu cầu accessibility | Chữ nội dung ≥ 16 sp, tương phản ≥ 4.5:1, nút ≥ 48 dp ở nửa dưới màn hình để chạm bằng ngón cái. Không dùng chỉ màu để báo tâm trạng (kèm icon mặt mascot + chữ). |
| Câu hỏi Nốt trả lời | "Hôm nay mình đã làm được gì?" — thay vì "Hôm nay mình còn nợ gì?" |

**Một ngày của Minh với Nốt:** 21h30 nhận thông báo "Hôm nay bạn đã làm được gì?" → chọn tâm trạng "Ổn", ghi "Dọn bàn học và gửi email hỏi thầy" → nốt rơi vào hũ (flow F1). 0h15 nhận ra đã lướt TikTok 40 phút → chạm "Dừng lại" trên `S02` rồi "Mình vừa dừng lại" ở `S09` (flow F2). Sáng hôm sau mở tab Thử thách và nhận thẻ "Hỏi thầy 1 câu sau giờ học" (flow F3).

---

## 4. Persona phụ

| | Quốc Huy | Bảo Ngọc |
|---|---|---|
| Tuổi, vai trò | 27, nhân viên văn phòng, tối tự học khoá online | 18, sinh viên năm nhất, mới lên thành phố |
| Câu nói | "Ngồi cả ngày, tối về chỉ muốn nằm lướt điện thoại." | "Mình muốn hỏi thầy mà sợ bị đánh giá." |
| Ý của Nốt dùng nhiều nhất | 5. Vận động, 3. Tự chủ (bỏ lướt mạng đêm), 2. Nhật ký | 4. Nói chuyện với người lạ, 1. Chiến thắng nhỏ |
| Mục tiêu | Có năng lượng để học sau giờ làm; ngủ đủ | Kết bạn, dám hỏi thầy cô, thấy mình đang thích nghi được |
| Nỗi đau | Mệt, ít vận động, tự hứa học rồi bỏ; thấy tuổi 27 "chưa làm được gì" | Cô đơn, ngại nói, so sánh mình với bạn trên mạng xã hội |
| Thiết bị | iPhone, mở app giờ nghỉ trưa và trước khi ngủ | Android giá rẻ, mạng ký túc xá chập chờn (lý do cho nhánh lỗi mất mạng) |
| Nhu cầu đặc biệt | Thông báo không hiện nội dung riêng tư trên màn hình khoá (công tắc "Ẩn nội dung thông báo" ở `S12`) | Thử thách bắt đầu cực nhỏ (cấp 1: chào bạn cùng phòng) |

### Ánh xạ persona sang flow

| Persona | F1 Ghi nốt | F2 Tự chủ | F3 Thử thách | Flow phụ dùng để kiểm tra |
|---|:---:|:---:|:---:|---|
| **Minh** (chính) | ● | ● | ● | P6 Ngày tệ, P7 Thông báo |
| **Quốc Huy** (phụ) | ● | ● | | P3 Vận động, P4 Nhật ký dài, P8 Cài đặt (ẩn nội dung thông báo) |
| **Bảo Ngọc** (phụ) | ● | | ● | P1 Làm quen, T1 Hũ rỗng, T2 Mất mạng |

Định nghĩa từng flow ở [`ux/user-flow.md`](user-flow.md).

---

## 5. Bài học từ app tương tự (ảnh hưởng tới persona)

| App | Học gì cho Minh |
|---|---|
| Finch | Mascot lớn lên nhờ hành động thật → Tụi Nốt nhận "năng lượng" từ mỗi nốt. Người dùng Finch phàn nàn mất dữ liệu → nhánh lưu nháp offline |
| How We Feel (Yale) | Lưới tâm trạng 2 trục → "Lịch năng lượng" 5 mức ấm/lạnh |
| Daylio | Ngày mệt chỉ cần chạm → "chip chiến thắng" có sẵn |
| one sec | Một nhịp dừng nhỏ giúp nhận ra thói quen vô thức → nút "Mình vừa dừng lại" và màn thở 90 giây. Nốt không chặn app khác |
| Opal | Lịch chặn theo giờ → "Giờ tỉnh" (23h–1h) chỉ nhắc nhẹ. Tránh streak kiểu Opal |
| Fortify, Brainbuddy | Riêng tư là tính năng chính → danh sách thói quen muốn bớt khoá bằng sinh trắc học; không làm xấu hổ khi tái phạm |
| Unmute, nghiên cứu Sandstrom (2022) | Thử thách nói chuyện với người lạ chia cấp độ, bắt đầu cực nhỏ |
