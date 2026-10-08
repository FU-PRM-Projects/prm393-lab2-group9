# Quyết định thiết kế

10 quyết định quan trọng nhất. Mỗi lý do gắn với persona, một heuristic của Nielsen, một tiêu chí WCAG, hoặc một ràng buộc thực tế.

| # | Quyết định | Lý do | Thấy ở đâu |
|---|---|---|---|
| 1 | Màn mở đầu là **Hôm nay**, chỉ trả lời "làm gì tiếp?" | Persona: mỗi lần mở app dưới một phút, giữa hai môn. Nielsen #6 (nhận ra thay vì phải nhớ): việc gấp nhất hiện sẵn, không phải đi tìm | S02 |
| 2 | Bỏ thẻ ba con số, chip nền màu và thanh tiến độ ở dòng việc. Mỗi dòng chỉ còn checkbox, tên, một dòng phụ, thời hạn | Nielsen #8 (tối giản): ở bản Stitch đầu, mức gấp hiện ba lần trên một dòng. Persona có 7–8 deadline mỗi tuần nên cần đọc lướt | S04, vòng lặp 1 |
| 3 | Thêm **lịch nhiệt** 5 mức, màu lạnh đến nóng | Nỗi đau trung tâm: Hân không thấy ngày nào còn trống để chèn việc mới. Màu nóng-lạnh cho thấy ngày nặng trong một lần liếc | S03 |
| 4 | Ô lịch nhiệt luôn có số việc và khuôn mặt mascot; Chi tiết ngày ghi nhãn chữ của mức | WCAG 1.4.1 (không dùng màu làm tín hiệu duy nhất). Ô mức 1 trên nền trắng chỉ đạt 1.47:1 nên màu không đủ để nhận biết | S03, S09 |
| 5 | Form Thêm deadline chỉ bắt buộc 3 trường: tên, nhóm việc, hạn nộp | Persona chép việc từ 10 nhóm Zalo; tiêu chí thêm deadline dưới 20 giây. Nielsen #7 (linh hoạt, hiệu quả): khung giờ được điền sẵn khi mở từ Lịch bận | S06 |
| 6 | Tab **Lịch bận** cho thấy khung trống giữa các khối lịch; chạm khung trống là thêm việc | Tiêu chí chính: xếp việc phát sinh dưới 30 giây. Bỏ bước "tìm giờ trống" mà Hân phải tự làm | S05, Flow 4 |
| 7 | Không cho dời việc sang sau hạn nộp: báo ngay trong bottom sheet, nút Lưu bị khóa | Nielsen #5 (phòng ngừa lỗi). Persona không phân biệt được việc nào lùi được; app phải chặn lựa chọn sai | S09, BS1, Flow 3 |
| 8 | Đánh dấu đã nộp có dialog xác nhận và snackbar Hoàn tác | Nielsen #3 (người dùng kiểm soát) và #1 (hiển thị trạng thái). Thao tác một chạm dễ bấm nhầm khi dùng một tay | S07, S08, Flow 2 |
| 9 | Mascot vẽ bằng SVG ngoài Stitch, chỉ đặt ở 8 vị trí cố định, không đặt trong dòng việc | Nielsen #4 (nhất quán): hình do Stitch vẽ khác nhau giữa các màn. Persona thấy UI "quá AI" và nhàm; mascot thêm cá tính mà không làm dày danh sách | Tất cả, `assets/mascot/` |
| 10 | Thiết kế luôn màn **Đăng nhập (Google)** và **Hồ sơ** trong Lab 2 | Ràng buộc: Lab 3 bắt buộc Google Sign-In, hồ sơ và đăng xuất. Thiết kế trước để Lab 3 không phải thêm màn ngoài thiết kế. Hồ sơ cũng chứa cài đặt nhắc hạn cho nỗi đau "hay quên hạn" | S01, S10, Flow 5 |

---

# Checklist accessibility và responsive

Trạng thái: **Đạt** là đã có bằng chứng; **Cần kiểm tra** là phải xác nhận trên page 03 Final UI trong Figma rồi dán ảnh bằng chứng vào cột cuối.

| Mục | Kết quả | Bằng chứng |
|---|---|---|
| Contrast chữ thường ≥ 4.5:1 | Đạt | `design/DESIGN.md` mục 3.3: mọi cặp chữ trên nền từ 4.71:1 đến 16.72:1. Cặp thấp nhất là warning trên warning-container (4.71:1) |
| Contrast chữ lớn và điều khiển UI ≥ 3:1 | Đạt | outline trên surface-card 3.93:1 (viền checkbox, text field); primary trên surface 5.97:1 (FAB, tab đang chọn) |
| Vùng chạm ≥ 48 × 48 dp | Cần kiểm tra | Token quy định: dòng việc ≥ 60 dp, nút 48 dp, FAB 56 dp, ô lịch nhiệt hiển thị 42 dp trong vùng chạm 48 × 48 dp (lưới 7 × 48 = 336 dp, lề 12 dp). Cần ảnh đo trong Figma của S03 (ô lịch nhiệt) và S04 (checkbox) |
| Chữ nội dung ≥ 14 sp | Đạt | `design/DESIGN.md` mục 4: chữ nội dung nhỏ nhất là bodyMedium 14 sp; 12 sp chỉ dùng cho nhãn ngắn |
| Không dùng màu làm tín hiệu duy nhất | Đạt | Mức gấp: chữ "Trễ 1 ngày", "Hôm nay 23:59" và mascot tiêu đề nhóm. Mức nặng: số việc, khuôn mặt mascot, nhãn chữ ở S09. Quyết định 4 |
| Dùng Auto Layout và constraint | Cần kiểm tra | Cần ảnh panel Auto Layout của một màn (gợi ý S04) và của component Task row |
| Đã kiểm tra ở 360 dp | Cần kiểm tra | Cần ảnh 10 màn ở khung 360 × 800 trên page 03 |
| Đã kiểm tra ở 412 dp | Cần kiểm tra | Cần ảnh ít nhất S03 và S04 ở khung 412 × 915: lịch nhiệt giãn đều 7 cột, dòng việc không vỡ chữ |
