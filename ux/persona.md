# Persona và vấn đề

**Đề tài:** Study Planner "Nốt" cho sinh viên và người trẻ bận rộn có lịch trình dày đặc (môn học, đồ án, nghiên cứu khoa học, việc làm thêm). App giúp gom deadline từ nhiều nguồn về một chỗ, chia việc dài hạn thành các giai đoạn khớp số ngày, cho thấy ngày nào đang quá tải qua lịch nhiệt, và sắp xếp lại kế hoạch trong vài giây khi có việc phát sinh hoặc đổi ca đột xuất.

Nguồn thiết kế: Trang **00 Persona** trong file Figma [`PRM393-LAB2-Study-Planner`](https://www.figma.com/design/OkTRYkrsoJ0nkluNO4mrHz/PRM393-LAB2-Study-Planner?node-id=644-2).

---

## 1. Tổng quan hệ thống Persona

Hệ thống thiết kế gồm 4 persona đại diện cho sinh viên các năm và người đi làm: **1 persona chính, 2 persona phụ và 1 persona hỗ trợ**. Mọi quyết định thiết kế lớn ưu tiên persona chính (Minh).

### Ma trận ánh xạ Persona sang User Flow (Kiểm tra trên Prototype trang 06)

| PERSONA | Vai trò | C1 | C2 | C3 | C4 | P1 | P6 | P7 | P8 | S1 |
|---|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Minh** | Primary Persona | ● | ● | ● | | | | | | |
| **Đăng Khoa** | Secondary Persona | | | ● | ● | | | | ● | |
| **Bảo Ngọc** | Secondary Persona | ● | | | | ● | | ● | | ● |
| **Quốc Huy** | Supporting (Đi làm) | ● | | ● | | | | | ● | |

*Ghi chú:*
- **C** = Flow chính (*Core Flows*: C1, C2, C3, C4)
- **P** = Flow phụ (*Peripheral Flows*: P1, P6, P7, P8...)
- **S** = Trạng thái & xử lý lỗi (*State & Error Recovery*: S1, S2, S3)
- Ô có ● là flow dùng để kiểm tra persona đó (chấm lớn trên page 00). Định nghĩa từng flow ở `ux/user-flow.md`, cùng mã với page 01 và 06 trong Figma.
- Các flow không có cột ở đây (P2, P3, P4, P5, S2, S3) là flow chung. Riêng P3 · Trễ deadline cũng dùng để kiểm tra Minh.

---

## 2. Chi tiết từng Persona

### 2.1 Persona chính: Minh (Primary Persona) — "Người điều phối nhiều app"

> *"Mình mệt vì lúc nào cũng phải chuyển qua lại giữa Calendar, Notion, ClickUp và Linear."*

Theo frame `Persona · Minh (template chuẩn)` ở page 00.

| Mục | Chi tiết |
|---|---|
| **Bio** | Sinh viên năm cuối, đang học nhiều môn, làm trưởng nhóm nghiên cứu khoa học 4 người và đi làm thêm. Đang chuẩn bị nộp paper hội nghị hạn 15/11 |
| **Tuổi** | 22 tuổi (giả định) |
| **Thiết bị & nền tảng** | iPhone 12 (chính), laptop |
| **Công cụ hiện dùng** | Google Calendar, Notion, ClickUp, Linear |

#### Vị trí trên các thang đo (ước lượng của nhóm)
- **Thiết bị dùng:** gần hẳn về phía điện thoại.
- **Mỗi lần mở app:** vài giây.
- **Lịch tuần:** hay thay đổi.
- **Công nghệ:** thành thạo.

#### Mục tiêu và nhu cầu
- Không lỡ mốc giữa chừng của các deadline dài như paper hội nghị.
- Mở app là biết hôm nay mình và nhóm cần làm gì.
- Thôi chuyển qua lại giữa nhiều app để theo dõi một việc.

#### Khó khăn (pain point)
- Ghi lịch ở Calendar, theo dõi ở Notion, giao việc ở ClickUp và Linear.
- Chuyển qua lại nhiều app nên mệt và dễ sót việc.
- Không nhớ đã ghi chú, đã làm gì ở từng giai đoạn.

#### Hành vi và thói quen
- Dùng iPhone cả ngày, mở app vài giây giữa giờ học và ca làm.
- Việc phát sinh thêm gần như mỗi tuần.
- Lưu bài ở nhiều loại tệp: DOCX, PDF, XLSX, ZIP.

#### Động lực (theo thứ tự ưu tiên)
1. Gọn một chỗ
2. Đúng hạn
3. Theo dõi được nhóm
4. Kiểm soát được tiến độ

#### Ràng buộc
- Một deadline có nhiều người cùng làm (nhóm 4 người).
- Deadline kéo dài cả tháng (paper 15/11: 31 ngày).
- Lịch tuần thay đổi, phải sắp lại thường xuyên.

#### Nhu cầu accessibility
Minh không có nhu cầu accessibility riêng. Giới hạn theo tình huống: thường dùng một tay và chỉ liếc vài giây giữa hai việc, nên nút chính phải ở nửa dưới màn hình và trạng thái phải đọc được trong một lần nhìn.

#### Job To Be Done
> *"Khi có deadline dài như nộp paper hội nghị 15/11, tôi muốn chia từ hôm nay tới hạn chót thành các giai đoạn có ngày, ghi chú và tệp, để không phải mở thêm app nào khác."*

#### Kịch bản một ngày của Minh
- **08:00:** nhận nhắc "hôm nay là ngày 3/7 của giai đoạn Chạy thực nghiệm" (C3).
- **12:30 [C1]:** thêm deadline Paper 15/11, chia 4 giai đoạn khớp 31 ngày.
- **16:00 [C1]:** ghi chú "Lan lo phần Check đạo văn".
- **23:00 [C2]:** ghi chú kết quả, tải file XLSX và PDF lên giai đoạn.

#### Tiêu chí thành công
- **1 app:** thay Calendar, Notion, ClickUp, Linear cho mọi deadline.
- **31/31 ngày:** giai đoạn phủ kín từ hôm nay tới hạn chót.
- **< 60 giây:** tạo một deadline 4 giai đoạn bằng AI gợi ý (mục tiêu, giả định).
- **Kiểm tra bằng flow:** C1, C2, C3, P3.

#### Nguồn và giả định
- Nguồn: lời kể của một sinh viên năm cuối (Minh), 17/10/2026, chuyển qua nhóm.
- Giả định chưa kiểm chứng: tuổi, mức trên các thang đo, mục tiêu "< 60 giây". Cần phỏng vấn thêm 2–3 sinh viên năm cuối.
- Giả thuyết UI: nếu AI gợi ý giai đoạn từ mô tả, Minh tạo deadline 4 giai đoạn trong dưới 60 giây. Kiểm chứng: test usability với 3 sinh viên năm cuối, bấm giờ flow C1.

---

### 2.2 Persona phụ: Đăng Khoa (Secondary Persona)

> *"Đổi ca một cái là cả tuần học của mình phải xếp lại."*

| Mục | Chi tiết |
|---|---|
| **Độ tuổi** | 20 tuổi |
| **Vai trò** | Sinh viên năm 2 ngành Công nghệ Thông tin · Làm ca tối tại quán cà phê |
| **Thiết bị & Môi trường** | Android, kết nối 4G chập chờn khi di chuyển |
| **Khối lượng việc** | 2–4 deadline/tuần, làm ca tối 18:00–22:00 (4 tối/tuần) |

#### Mục tiêu & Nỗi đau
- **Mục tiêu:**
  - Nộp bài đúng hạn mà không phải thức trắng đêm chạy deadline.
  - Khi bị quản lý đổi ca đột xuất, sắp xếp lại việc học trong vài giây.
  - Lời nhắc thông báo kín đáo, không để lộ việc riêng tư.
- **Khó khăn:**
  - Quản lý thường báo đổi ca trước chỉ 1 ngày, làm đảo lộn toàn bộ lịch học tập.
  - Lập lại lịch bằng tay tốn nhiều công sức nên hay bỏ dở kế hoạch.
  - Mạng 4G yếu hoặc mất mạng khi ngồi trên xe buýt.
- **Thói quen:**
  - Dùng app chớp nhoáng vài giây, thao tác bằng một tay trên xe buýt.
  - Về phòng trọ lúc 22:30, lướt điện thoại xem lại việc đến khuya.

#### Job To Be Done
> *"Khi quản lý báo đổi ca, tôi muốn thêm giờ bận và lùi giai đoạn bị trùng ngay trên điện thoại, để không bỏ luôn kế hoạch tuần."*

#### Tiêu chí đo lường thành công
- **≤ 3 chạm:** Thêm xong một khung giờ bận mới.
- **< 10 giây:** Lùi một giai đoạn bị trùng sang ngày khác.
- **Offline:** lời nhắc vẫn đến đúng giờ khi mất mạng.
- **Kiểm tra bằng flow:** P8, C4, C3.

---

### 2.3 Persona phụ: Bảo Ngọc (Secondary Persona)

> *"Mình không biết nên bắt đầu học từ đâu."*

| Mục | Chi tiết |
|---|---|
| **Độ tuổi** | 18 tuổi |
| **Vai trò** | Sinh viên năm 1 ngành Thiết kế Đồ họa · Sống tại ký túc xá |
| **Thiết bị & Kinh nghiệm** | Android · Lần đầu sử dụng app quản lý thời gian |
| **Khối lượng việc** | 3–5 bài tập vẽ / đồ án môn học mỗi tuần |

#### Mục tiêu & Nỗi đau
- **Mục tiêu:**
  - Làm bài đều đặn mỗi ngày, tránh dồn ứ sát hạn nộp.
  - Biết một bài tập lớn gồm những bước nào để làm theo thứ tự.
  - Giao diện dễ hiểu, dùng được ngay từ lần mở đầu tiên mà không bị ngợp.
- **Khó khăn:**
  - Không biết bắt đầu từ đâu nên hay lần lữa, trì hoãn.
  - Bài vẽ dài hơi, chưa có kỹ năng chia nhỏ công việc.
  - Các thuật ngữ trong app năng suất truyền thống quá phức tạp và khó hiểu.
- **Thói quen:**
  - Dùng app vào buổi tối ở phòng ký túc xá.
  - Hay bị gián đoạn giữa chừng khi gia đình gọi điện về nhà.
  - Thường chỉ bắt đầu làm bài khi sát đến hạn nộp.

#### Job To Be Done
> *"Khi nhận một bài lớn đầu kỳ, tôi muốn được hướng dẫn chia thành các bước nhỏ có giờ làm, để biết hôm nay nên làm gì."*

#### Tiêu chí đo lường thành công
- **< 2 phút:** tới được deadline đầu tiên (gồm làm quen 3 câu ở P1).
- **< 1 phút:** chia một bài thành bước (P7).
- **0** thuật ngữ khó hiểu như "sprint" trên các màn Ngọc dùng.
- **Kiểm tra bằng flow:** P1, C1, P7, S1.

---

### 2.4 Persona hỗ trợ: Quốc Huy (Supporting Persona · Đi làm)

> *"Nhắc mình thì được, nhưng đừng nhắc lúc đang họp."*

| Mục | Chi tiết |
|---|---|
| **Độ tuổi** | 24 tuổi |
| **Vai trò** | Lập trình viên đi làm toàn thời gian (8:00–17:00), học thêm buổi tối |
| **Thiết bị & Trợ năng** | Android · Cài đặt hiển thị chữ lớn 130% |
| **Khối lượng việc** | 4–6 deadline công việc/tuần + các khóa học chuyên môn |

#### Mục tiêu & Nỗi đau
- **Mục tiêu:**
  - Giao đúng hạn các task và báo cáo công việc.
  - Lời nhắc đến lúc không họp.
  - Tách việc công ty và khoá học buổi tối.
- **Khó khăn:**
  - Nhắc kêu giữa cuộc họp nên anh tắt hết thông báo.
  - Deadline công việc nằm rải rác trong email, chat.
  - Phóng to chữ thì nhiều app vỡ layout.
- **Thói quen:**
  - Ngồi máy khoảng 9 tiếng mỗi ngày.
  - Dùng app lúc nghỉ trưa và trên đường về.
  - Học một khoá online vào buổi tối.

#### Job To Be Done
> *"Khi một giai đoạn công việc sắp đến giờ làm mà tôi đang họp, tôi muốn lùi lời nhắc bằng một chạm, để không phải tắt hết thông báo."*

#### Tiêu chí đo lường thành công
- **1 chạm:** lùi một lời nhắc ("Nhắc lại 15 phút" trên thông báo `13p`).
- **130%:** cỡ chữ 130% vẫn đọc tốt trên màn 360 dp (giả định, chưa kiểm tra trên Figma).
- **2 nhóm:** việc công ty và khoá học tách riêng (hai dự án ở bước B1 của Thêm deadline).
- **Kiểm tra bằng flow:** C1, C3, P8.

---

## 3. Phát biểu vấn đề (Problem Statement)

> Sinh viên và người trẻ bận rộn thường bị vỡ kế hoạch khi công việc bất ngờ chen vào hoặc lịch trình thay đổi, vì họ phải chuyển qua lại giữa quá nhiều ứng dụng rời rạc, không thấy ngày nào đang quá tải, không biết cách chia nhỏ deadline dài thành từng chặng, và việc sắp xếp lại kế hoạch bằng tay tốn quá nhiều công sức.

---

## 4. Persona dẫn tới các quyết định thiết kế quan trọng

| Đặc điểm Persona | Hệ quả thiết kế trong Nốt | Màn hình |
|---|---|---|
| **Minh** — Deadline dài cả tháng, nhóm 4 người | Thêm deadline 5 bước: môn hoặc dự án, deadline, mô tả, giai đoạn, xem lại. Giai đoạn phải phủ kín số ngày tới hạn ("Đã chia 31/31 ngày"); mỗi giai đoạn có giờ nhắc mỗi ngày | `6`, `6b2`, `6b2a`, `6b3`, `6b4`, `6b5`, `7c` |
| **Minh** — Mô tả việc rồi mới chia | Bước B3 Mô tả: AI dùng mô tả để gợi ý giai đoạn. Người dùng sửa, xoá, tạo lại, hoặc tự nhập. AI lỗi thì mô tả vẫn được giữ | `6b2a`, `6b3` (4 trạng thái) |
| **Minh** — Không nhớ đã làm gì ở từng giai đoạn | Mỗi giai đoạn có ghi chép và tài liệu (DOCX, PDF, XLSX, ZIP, ảnh, link) | `7s`, `7s1`, `7s2`, `7t` |
| **Minh** — Chuyển qua lại 4 app | Gom deadline, giai đoạn, tài liệu và lời nhắc vào một app; thông báo mở thẳng đúng giai đoạn | `13p`, `13`, `7s` |
| **Đăng Khoa** — Bị đổi ca đột xuất | Thêm giờ bận ở lịch tuần; nhấn giữ một việc để Để mai hoặc Chia nhỏ | `9`, `9d`, `9e` |
| **Đăng Khoa** — Một ngày quá nặng | Lịch nhiệt theo độ nặng; chạm ngày đỏ để xem gợi ý giãn việc sang ngày nhẹ hơn trước hạn, có Hoàn tác | `3`, `4`, `4b`, `4c`, `3d` |
| **Đăng Khoa** — 4G chập chờn | Trạng thái lỗi mất mạng có Thử lại; lời nhắc là thông báo trên máy | Trạng thái Lỗi mất mạng của `5`, `13p` |
| **Bảo Ngọc** — Lần đầu dùng app | Làm quen 3 câu hỏi ngắn (có Để sau, Bỏ qua); màn rỗng chỉ có một nút Thêm deadline | `O1`–`O4`, trạng thái Rỗng của `5` |
| **Bảo Ngọc** — Không biết chia bài lớn | Chia nhỏ việc hay bị dời: chọn lý do, Nốt gợi ý 3 bước khoảng 45 phút, Ngọc tự chọn giờ cho từng bước | `2c0`, `2c`, `2c2`, `2c3`, `3c` |
| **Quốc Huy** — Bị nhắc lúc đang họp | Thông báo có nút "Nhắc lại 15 phút"; giờ làm 8:00–17:00 thêm làm giờ bận | `13p`, `9d` |
| **Quốc Huy** — Phóng to chữ 130% | Màn dùng Auto Layout để chữ dài xuống dòng thay vì bị cắt. Chưa có frame kiểm tra 130% trong Figma | Mọi màn |
| **Tất cả** — Dùng một tay, liếc nhanh | Nút chính, nút + và thanh điều hướng ở nửa dưới màn hình; thẻ "Hạn hôm nay" ở đầu `2` | `2`, `3`, `5` |

---

## 5. Phạm vi sản phẩm (App không làm gì)

- Không đồng bộ trực tiếp tin nhắn từ Zalo/Slack (người dùng thêm deadline hoặc dùng tính năng chia việc nhanh).
- Không xây dựng tính năng mạng xã hội hoặc chat trực tiếp trong app.
- Không thay thế phần mềm kế toán hoặc quản lý tiền bạc freelance.
- Không tập trung vào giao diện web/desktop (ưu tiên điện thoại Android khung 360 × 800 dp, kiểm tra thêm ở 412 dp).

