# Persona và vấn đề

**Đề tài:** Study Planner "Nốt" cho sinh viên năm cuối có tuần học đã kín bởi nhiều môn, đồ án và nghiên cứu. App giúp gom deadline từ nhiều nhóm Zalo về một chỗ, cho thấy ngày nào đang quá tải, và sắp lại kế hoạch trong vài giây khi một việc bất ngờ chen vào.

---

## 1. Persona chính

### Nguyễn Võ Khả Hân

| Mục | Chi tiết |
|---|---|
| **Độ tuổi** | 21 (nhóm 20–22) |
| **Vai trò** | Sinh viên năm 4, kỳ 8, ngành Kỹ thuật Phần mềm, Đại học FPT TP.HCM |
| **Việc làm thêm** | Freelance theo đơn: làm web, app, landing page khi có người thuê, không có lịch cố định |

### Bối cảnh hằng ngày

Kỳ này Hân học 5 môn: 3 môn offline và 2 môn online.

| Môn | Hình thức | Lịch học |
|---|---|---|
| MLN111 | Offline | Thứ Ba và thứ Sáu, 9:30–11:45 |
| PRM393 | Offline | Thứ Ba và thứ Sáu, 12:30–14:45 |
| WDP301 | Offline | Thứ Ba và thứ Sáu, 15:00–17:15 |
| EXE201 | Online | Thứ Năm, 15:00–17:15 |
| ITE302c | Online (Coursera) | Thứ Hai, 17:45–19:45, chỉ 2 buổi trong kỳ (tuần đầu và tuần cuối) |

- Thứ Ba và thứ Sáu kín lịch từ 9:30 đến 17:15. Nghỉ giữa các môn chỉ 15–45 phút.
- Ngoài 5 môn, Hân còn chạy song song hai việc dài hạn: đồ án liên kỳ (kỳ 8 và kỳ 9) và nghiên cứu khoa học. Hân cũng đang chuẩn bị CV và profile để ra trường.
- Mỗi tuần có khoảng 7–8 deadline.
- Mỗi môn có một nhóm Zalo của cả lớp và một nhóm làm việc 5–6 người. Tổng cộng Hân theo dõi 10 nhóm Zalo.
- Việc bất ngờ đến từ ba nguồn: task mới giao trong nhóm Zalo, lịch họp nhóm, và đơn freelance.
- Hệ quả: thời gian ngoài giờ lên lớp đã chia hết. Một việc mới gần như luôn phải lấy chỗ của một việc khác.

### Mục tiêu

1. Đạt điểm 8–10 ở các môn.
2. Nộp mọi bài đúng hạn, không quên deadline nào.
3. Mở app là biết ngay hôm nay cần làm việc nào trước.
4. Khi có việc bất ngờ, sắp lại kế hoạch trong vài giây thay vì bỏ luôn kế hoạch.
5. Theo dõi tiến độ từng deadline mà không phải mở từng nhóm chat.

### Nỗi đau (pain point)

1. **Nỗi đau trung tâm:** kế hoạch tuần bị vỡ mỗi khi một việc bất ngờ chen vào. Lần gần nhất kế hoạch vỡ đúng là vì một task bất ngờ.
2. Khi đó Hân không biết nên lùi việc nào, vì không thấy rõ việc nào quan trọng hơn và ngày nào còn trống.
3. Sắp lại kế hoạch bằng tay tốn công, nên Hân thường bỏ luôn kế hoạch.
4. 7–8 deadline mỗi tuần nằm rải rác trong 10 nhóm Zalo. Không có một chỗ để xem tất cả.
5. Thông báo quan trọng bị trôi trong tin nhắn nhóm, nên dễ sót thông tin và quên lịch.
6. Không biết một deadline cần bao nhiêu buổi làm, nên hay bắt đầu trễ.

### Thói quen dùng thiết bị

- Dùng cả laptop và điện thoại. Điện thoại là iPhone, dùng hằng ngày.
- App được thiết kế cho Android theo yêu cầu môn học. Đây là ràng buộc nền tảng, không phải lựa chọn theo thiết bị của Hân.
- Mở app nhiều lần trong ngày, mỗi lần dưới một phút: giữa hai môn, trên đường đi học.
- Thường thao tác bằng một tay.
- Hay xem lại kế hoạch lúc khuya.

### Nhu cầu accessibility

Hân không có khuyết tật, nhưng có giới hạn theo tình huống:

| Tình huống | Yêu cầu thiết kế |
|---|---|
| Đọc lúc khuya, lúc mệt | Chữ nội dung tối thiểu 14 sp. Contrast chữ tối thiểu 4.5:1 |
| Dùng một tay | Hành động chính ở nửa dưới màn hình. Vùng chạm tối thiểu 48 × 48 dp |
| Liếc nhanh giữa hai môn | Mức gấp và mức nặng luôn có chữ hoặc hình đi kèm, không chỉ bằng màu |

---

## 2. Phát biểu vấn đề

> Sinh viên năm cuối có tuần đã kín bởi 5 môn, đồ án và nghiên cứu thường vỡ kế hoạch học khi một việc bất ngờ chen vào, vì họ không thấy ngày nào còn trống, không biết nên lùi việc nào, và việc sắp lại kế hoạch bằng tay tốn quá nhiều công.

---

## 3. Tiêu chí thành công đo được

**Tiêu chí chính (gắn với nỗi đau trung tâm, Flow 4):**

> Khi một việc bất ngờ chen vào, Hân xếp được việc đó vào một khung giờ trống trong **dưới 30 giây**, tính từ lúc mở tab Lịch bận đến lúc việc mới hiện trên màn Hôm nay.

**Tiêu chí phụ:**

| # | Tiêu chí | Flow |
|---|---|---|
| 2 | Thêm một deadline mới chép từ nhóm Zalo trong **dưới 20 giây** | Flow 1 |
| 3 | Dời một việc khỏi ngày quá tải sang ngày khác trong **tối đa 4 lần chạm** và **dưới 15 giây** | Flow 3 |

**Cách đo:** bấm giờ trên prototype Figma (page 06), mỗi tiêu chí đo 3 lần, lấy trung bình. Điểm bắt đầu và kết thúc lấy đúng theo flow tương ứng trong `ux/user-flow.md`.

---

## 4. Persona dẫn tới quyết định thiết kế nào

| Đặc điểm của Hân | Hệ quả thiết kế | Màn hình |
|---|---|---|
| Mở app dưới một phút | Màn đầu tiên là Hôm nay: việc làm tiếp, lịch bận hôm nay, deadline gần nhất | S02 |
| Việc bất ngờ chen vào tuần đã kín | Tab Lịch bận cho thấy khung giờ trống của từng ngày. Chạm khung trống là thêm việc vào đó | S05, S06 |
| Không thấy ngày nào quá tải | Lịch nhiệt: mỗi ngày có màu theo mức nặng, kèm số việc và khuôn mặt mascot | S03, S09 |
| Không biết lùi việc nào | Mỗi deadline có mức quan trọng (Thấp, Vừa, Cao). Chi tiết ngày cho dời từng việc, không cho dời sau hạn nộp | S06, S09 |
| 7–8 deadline trong 10 nhóm Zalo | Form Thêm deadline chỉ bắt buộc 3 trường: tên, nhóm việc, hạn nộp | S06 |
| Không chỉ có môn học | "Môn" mở rộng thành "Nhóm việc": Môn học, Đồ án, Nghiên cứu, Khác | S04, S06 |
| Không biết một deadline cần bao nhiêu buổi | Lưu deadline xong, app tự xếp buổi làm 45 phút vào khung trống trước hạn nộp | S06, S07 |
| Hay quên hạn | Nhắc trước hạn, chỉnh trong Hồ sơ | S10 |
| Dùng một tay, đọc lúc khuya | FAB và thanh điều hướng ở cuối màn hình. Contrast và cỡ chữ theo mục accessibility | Tất cả |
| Mục tiêu điểm 8–10 | Mỗi deadline hiện tiến độ theo số buổi đã xong ("2/3 buổi") | S04, S07 |

---

## 5. App không làm gì

- Không đọc hay đồng bộ tin nhắn Zalo. Mục tiêu là chép vào đủ nhanh.
- Không quản lý việc freelance và CV. Chúng chỉ xuất hiện dưới dạng lịch bận hoặc nhóm việc Khác.
- Không chia sẻ deadline giữa các thành viên nhóm.
- Không có bản laptop. Hành vi trên màn hình rộng từ 600 dp chỉ được mô tả trong `handoff/flutter-handoff.md`.
