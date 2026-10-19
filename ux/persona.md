# Persona và vấn đề

**Đề tài:** Study Planner "Nốt" cho sinh viên và người trẻ bận rộn có lịch trình dày đặc (môn học, đồ án, nghiên cứu khoa học, việc làm thêm). App giúp gom deadline từ nhiều nguồn về một chỗ, chia việc dài hạn thành các giai đoạn khớp số ngày, cho thấy ngày nào đang quá tải qua lịch nhiệt, và sắp xếp lại kế hoạch trong vài giây khi có việc phát sinh hoặc đổi ca đột xuất.

Nguồn thiết kế: Trang **00 Persona** trong file Figma [`PRM393-LAB2-Study-Planner`](https://www.figma.com/design/OkTRYkrsoJ0nkluNO4mrHz/PRM393-LAB2-Study-Planner?node-id=767-1906).

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
- **S** = Trạng thái & xử lý lỗi (*State & Error Recovery*: S1, S2)

---

## 2. Chi tiết từng Persona

### 2.1 Persona chính: Minh (Primary Persona)

> *"Mình mệt vì lúc nào cũng phải chuyển qua lại giữa Calendar, Notion, ClickUp và Linear."*

| Mục | Chi tiết |
|---|---|
| **Độ tuổi / Giới tính** | 21–22 tuổi · Nam (giả định) |
| **Vai trò** | Sinh viên năm cuối, Trưởng nhóm nghiên cứu khoa học (nhóm 4 người), làm thêm |
| **Bối cảnh học tập** | Đang học nhiều môn, làm đề tài NCKH cấp trường, chuẩn bị nộp paper hội nghị (hạn 15/11), làm thêm ngoài giờ |
| **Thiết bị & Nền tảng** | iPhone 12 (chính, dùng cả ngày giữa các môn và ca làm), Laptop |
| **Công cụ hiện dùng** | Google Calendar, Notion, ClickUp, Linear |

#### Thang đo đặc tính người dùng
- **Thiết bị:** Nghiêng hẳn về Điện thoại (90% trên di động)
- **Mỗi lần mở app:** Vài giây (mở nhanh giữa các tiết học hoặc chuyển ca)
- **Lịch tuần:** Hay thay đổi (nhiều việc phát sinh mỗi tuần)
- **Trình độ công nghệ:** Thành thạo công nghệ

#### Động lực thúc đẩy
1. Gọn một chỗ (5/5)
2. Đúng hạn (5/5)
3. Theo dõi nhóm (4/5)
4. Kiểm soát tiến độ (4/5)

#### Mục tiêu & Khó khăn
- **Mục tiêu:**
  - Ghi deadline theo môn học hoặc theo từng dự án / đề tài.
  - Chia deadline dài thành các giai đoạn cụ thể khớp đúng số ngày tới hạn chót.
  - Ghi chú lại ai đang làm phần nào ở từng giai đoạn; lưu trữ kết quả và tệp đính kèm.
- **Khó khăn:**
  - Phải ghi lịch ở Calendar, theo dõi tiến độ ở Notion, giao việc ở ClickUp và Linear.
  - Chuyển qua lại nhiều app gây mệt mỏi, phân mảnh thông tin và rất dễ sót đầu việc.
  - Không nhớ đã ghi chú gì, đã hoàn thành gì ở từng giai đoạn.
- **Thói quen:**
  - Dùng điện thoại cả ngày giữa các môn học và giờ làm thêm.
  - Việc phát sinh thêm gần như mỗi tuần.
  - Lưu trữ và nộp bài làm ở nhiều định dạng tệp: DOCX, PDF, XLSX, ZIP.

#### Job To Be Done
> *"Khi có một deadline dài như nộp paper hội nghị 15/11, tôi muốn chia từ hôm nay tới hạn chót thành các giai đoạn có số ngày, ghi chú và tệp, để không phải mở thêm app nào khác."*

#### Một ngày điển hình của Minh
- **08:00:** Nhận thông báo nhắc: *"Hôm nay là ngày 3/7 của giai đoạn Chạy thực nghiệm"*.
- **12:30 [C1]:** Thêm deadline Paper 15/11, chia làm 4 giai đoạn khớp đúng 31 ngày.
- **16:00 [C1]:** Ghi chú tiến độ: *"Lan lo phần Check đạo văn"*.
- **23:00 [C2]:** Ghi chú kết quả thực nghiệm, tải file XLSX và PDF lên giai đoạn.

#### Tiêu chí đo lường thành công
- **1 app duy nhất:** Thay thế hoàn toàn Calendar, Notion, ClickUp trong việc theo dõi học tập.
- **31/31 ngày:** Các giai đoạn phủ kín lịch trình từ lúc bắt đầu tới hạn chót.
- **Mọi loại tệp:** Đính kèm trực tiếp DOCX, PDF, XLSX, ZIP vào từng giai đoạn.
- **Kiểm tra bằng flow:** C1, C2, C3, P3.

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
- **Offline:** Lời nhắc và danh sách deadline vẫn hoạt động chính xác khi mất mạng.
- **Kiểm tra bằng flow:** P8, C4, C3.

---

### 2.3 Persona phụ: Bảo Ngọc (Secondary Persona)

> *"Mình không biết bắt đầu từ đâu."*

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
- **< 2 phút:** Hoàn thành onboarding làm quen và tạo được deadline đầu tiên có chia bước.
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
  - Giao nộp đúng hạn các task và báo cáo tiến độ công việc.
  - Lời nhắc thông minh: chỉ nhắc vào lúc không có lịch họp.
  - Tách bạch rõ ràng giữa việc ở công ty và khóa học buổi tối.
- **Khó khăn:**
  - Chuông nhắc việc vang lên giữa cuộc họp quan trọng khiến anh phải tắt toàn bộ thông báo.
  - Deadline công việc bị phân tán trong nhiều kênh: Slack, Jira, email, chat nhóm.
  - Khi bật chế độ phóng to chữ 130% trên điện thoại, rất nhiều ứng dụng bị vỡ layout, tràn chữ, che mất nút bấm.

#### Tiêu chí đo lường thành công
- **1 chạm:** Lùi một buổi làm khi có việc đột xuất.
- **Text scale 130%:** Giao diện co giãn chuẩn xác, không vỡ layout, không cụt chữ.
- **Cài đặt không làm phiền:** Thông báo tôn trọng khung giờ bận/họp.
- **Kiểm tra bằng flow:** P8, C1, C3.

---

## 3. Phát biểu vấn đề (Problem Statement)

> Sinh viên và người trẻ bận rộn thường bị vỡ kế hoạch khi công việc bất ngờ chen vào hoặc lịch trình thay đổi, vì họ phải chuyển qua lại giữa quá nhiều ứng dụng rời rạc, không thấy ngày nào đang quá tải, không biết cách chia nhỏ deadline dài thành từng chặng, và việc sắp xếp lại kế hoạch bằng tay tốn quá nhiều công sức.

---

## 4. Persona dẫn tới các quyết định thiết kế quan trọng

| Đặc điểm Persona | Hệ quả thiết kế trong Nốt | Màn hình tương ứng |
|---|---|---|
| **Minh** — Đề tài dài hạn, nhiều môn, NCKH | Deadline hỗ trợ chia thành nhiều giai đoạn khớp số ngày; cho phép đính kèm tệp (DOCX, PDF, XLSX, ZIP) và ghi chú ai làm phần nào | Chi tiết deadline (Device 7d), Chi tiết giai đoạn (Device 7s, 7s1, 7s2), Thêm ghi chép (Device 7t) |
| **Minh** — Chuyển qua lại 4 app (Calendar, Notion, ClickUp, Linear) | Tích hợp "All-in-one": vừa có lịch bận (Calendar), vừa có quản lý giai đoạn & tệp (Notion), vừa có theo dõi deadline (ClickUp/Linear) | Toàn bộ 7 phân hệ của app |
| **Khoa** — Bị quản lý đổi ca đột xuất | Thêm giờ bận trong ≤ 3 chạm; tự động phát hiện giai đoạn bị trùng và hỗ trợ lùi ngày trong < 10 giây; có nút Hoàn tác ngay | Lịch tuần & Giờ bận (Device 4.2), Chi tiết ngày (Device 4a, 4b, 3d) |
| **Khoa** — Mạng 4G chập chờn trên xe buýt | Hỗ trợ lưu trữ offline, thông báo đẩy cục bộ, trạng thái lỗi mạng rõ ràng với nút Thử lại | Trạng thái lỗi (S1), Thông báo đẩy màn hình khóa (Device 13c) |
| **Bảo Ngọc** — Sinh viên năm 1, lần đầu dùng app | Onboarding 3 câu hỏi ngắn gọn, ngôn ngữ gần gũi, tính năng AI chia nhỏ bài lớn thành các phiên làm 45 phút | Làm quen · Cá nhân hóa (Device 2a, 2b, 2c), Chia nhỏ việc -> Xếp giờ (Device 2c0, 2c3) |
| **Quốc Huy** — Chỉnh font chữ to 130% | Layout thiết kế co giãn linh hoạt bằng Auto Layout, kiểm thử riêng trên màn hình phóng to 130%, đảm bảo vùng chạm ≥ 48dp | Công cụ demo & Kiểm tra lỗi (Device 7.4), Toàn bộ màn hình |
| **Quốc Huy** — Tránh nhắc chuông khi đang họp | Tùy chọn nhắc nhở thông minh: rung nhẹ hoặc hiển thị trong danh sách thông báo thay vì phát âm thanh trong giờ bận | Cài đặt thông báo (Device 7.2), Danh sách thông báo (Device 13A, 13B) |
| **Tất cả** — Thao tác bằng một tay, liếc nhanh | Nút chính, FAB, thanh điều hướng nằm ở nửa dưới màn hình; lịch nhiệt 5 mức giúp nhận biết ngày nặng chỉ trong 1 lần liếc | Hôm nay (Device 3), Lịch nhiệt (Device 4), Deadline (Device 6.1) |

---

## 5. Phạm vi sản phẩm (App không làm gì)

- Không đồng bộ trực tiếp tin nhắn từ Zalo/Slack (người dùng thêm deadline hoặc dùng tính năng chia việc nhanh).
- Không xây dựng tính năng mạng xã hội hoặc chat trực tiếp trong app.
- Không thay thế phần mềm kế toán hoặc quản lý tiền bạc freelance.
- Không tập trung vào giao diện web/desktop (ưu tiên tối ưu cho thiết bị di động Android màn hình 360 × 800 dp, mở rộng 412 dp).

