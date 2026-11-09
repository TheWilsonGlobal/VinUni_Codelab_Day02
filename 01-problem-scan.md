# 01 — Problem Scan (Cá nhân)

**Tên nhóm:** Không có — làm cá nhân (solo)
**Thành viên:** Phạm Ngọc Sơn — MSSV: 2A202603533

> **Trạng thái:** bản nháp, soạn cùng AI (xem `03-ai-log.md`). Các bài toán dưới đây là giả thuyết dựa trên hiểu biết chung về hoạt động của các công ty thành viên, **chưa** qua khảo sát thực địa. Mọi con số thời gian là **ước tính giả định**, cần kiểm chứng trước khi dùng làm baseline.

---

## Phase 1 — SCAN (tối thiểu 5 bài toán, 4 lenses)

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | Xanh SM | Tốn thời gian | Điều phối viên xử lý thủ công sự cố pin yếu của tài xế: tra vị trí và % pin, tìm trạm còn trụ trống trong tầm pin, soạn tin chỉ đường, hoặc gọi xe sạc di động. Ước tính 8–15 phút/lượt. |
| 2 | Xanh SM | Pain từ người khác | Khách để quên đồ trên xe: tổng đài nhận báo, tra lại chuyến theo số điện thoại và giờ đi, gọi tài xế, hẹn trả đồ. Nhiều lần chuyển giao giữa khách, tổng đài và tài xế, khách phải gọi lại nhiều lần để hỏi tiến độ. |
| 3 | VinFast | AI có thể tốt hơn | Cố vấn dịch vụ ở xưởng đọc mô tả lỗi tự do của khách (ví dụ "đi qua gờ giảm tốc kêu lục cục bánh trước") và tự gán nhóm lỗi để xếp lịch kỹ thuật viên. Phân loại phụ thuộc kinh nghiệm từng người, dễ xếp sai chuyên môn. |
| 4 | Vinhomes | Lặp lại | Ban quản lý trả lời các câu hỏi lặp lại của cư dân (phí dịch vụ, đăng ký gửi xe, giờ mở tiện ích, thủ tục thi công) qua hotline và nhóm chat. Phần lớn câu trả lời đã có trong quy định nhưng vẫn soạn tay từng lượt. |
| 5 | Vinmec | Tốn thời gian | Điều dưỡng bàn giao ca: tổng hợp tình trạng từng bệnh nhân từ bệnh án, y lệnh và ghi chú trong ca để bàn giao cho ca sau. Ước tính 3–5 phút/bệnh nhân. Lĩnh vực nhạy cảm, AI chỉ được soạn nháp. |
| 6 | VinWonders | Pain từ người khác | Khi thời tiết xấu khiến khu trò chơi ngoài trời đóng cửa, lượng yêu cầu đổi/hoàn vé tăng đột biến. Nhân viên CSKH đọc từng tin nhắn, đối chiếu chính sách và soạn phản hồi, khách phải chờ lâu. |

---

## Phase 2 — QUICK-ASSESS (3 Quick Problem Cards)

Chọn top 3: **#1 (Xanh SM sự cố pin)**, **#2 (Xanh SM đồ thất lạc)**, **#6 (VinWonders đổi/hoàn vé do thời tiết)**.

### Card #1
- **Bài toán (1 câu):** Điều phối viên Xanh SM mất nhiều thời gian và dễ quyết định sai khi xử lý tài xế báo pin yếu giữa ca.
- **Công ty thành viên:** Xanh SM
- **Actor (ai đang đau):** Điều phối viên (quá tải giờ cao điểm), tài xế (xe đứng, mất cuốc).
- **Workflow thủ công hiện tại (5 bước):** 1. Tài xế gọi tổng đài báo pin yếu → 2. Tổng đài chuyển cho điều phối viên → 3. Tra vị trí xe và % pin → 4. Tìm trạm còn trụ trống, đúng chuẩn sạc, trong tầm pin → 5. Soạn tin chỉ đường, hoặc gọi xe sạc di động nếu pin quá thấp.
- **Bước tốn thời gian/lỗi nhất:** Bước 4 (ước tính 3–5 phút/lượt) là chậm nhất. Quyết định ở bước 5 khi pin dưới 5% là rủi ro nhất: chọn trạm quá xa có thể làm xe hết pin giữa đường.
- **Bước AI có thể hỗ trợ:** Bước 3–4 là tra cứu có cấu trúc, phù hợp với code/rule. Bước 5 (soạn tin chỉ đường bằng tiếng Việt) phù hợp với LLM, dưới dạng nháp chờ điều phối viên duyệt.
- **Metric thành công (có số):** Giảm thời gian xử lý trung vị từ khoảng 11 phút (ước tính, cần đo baseline) xuống **dưới 4 phút**. **0 lần** đề xuất trạm xa hơn 5 km khi pin dưới 5%, trên bộ kiểm thử tối thiểu 50 kịch bản.
- **Quick Architecture:** [ ] No AI  [x] Rule  [x] LLM  [ ] Agent. Rule quyết định ngưỡng 5% / 5 km, LLM chỉ soạn tin nháp.

### Card #2
- **Bài toán (1 câu):** Khách để quên đồ trên xe Xanh SM phải chờ lâu và gọi lại nhiều lần vì việc tra chuyến và liên lạc tài xế làm thủ công.
- **Công ty thành viên:** Xanh SM
- **Actor (ai đang đau):** Khách hàng (lo lắng, chờ đợi), tổng đài viên (nhiều cuộc gọi lặp lại).
- **Workflow thủ công hiện tại (4 bước):** 1. Khách gọi báo mất đồ → 2. Tổng đài tra chuyến theo số điện thoại và giờ đi → 3. Gọi tài xế xác nhận có đồ hay không → 4. Hẹn lịch trả đồ và gọi lại báo khách.
- **Bước tốn thời gian/lỗi nhất:** Bước 3–4 (ước tính 10–20 phút tính cả thời gian chờ tài xế nghe máy), cộng thêm các cuộc gọi hỏi tiến độ.
- **Bước AI có thể hỗ trợ:** Bước 2 là tra cứu dữ liệu, rule là đủ. LLM có thể tóm tắt mô tả món đồ và soạn tin cập nhật trạng thái gửi khách.
- **Metric thành công (có số):** Giảm số cuộc gọi hỏi tiến độ mỗi vụ từ khoảng 2–3 (ước tính) xuống **dưới 1**. **90%** vụ có tin xác nhận gửi khách trong vòng 15 phút.
- **Quick Architecture:** [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent. Phần lớn giá trị đến từ tra chuyến tự động và thông báo trạng thái. LLM chỉ là phần thêm, nên chưa chọn.

### Card #3
- **Bài toán (1 câu):** Khi thời tiết xấu khiến khu trò chơi ngoài trời đóng cửa, CSKH VinWonders bị dồn yêu cầu đổi/hoàn vé và phản hồi chậm.
- **Công ty thành viên:** Khác — VinWonders (Vinpearl)
- **Actor (ai đang đau):** Nhân viên CSKH (quá tải đột biến), khách đã mua vé.
- **Workflow thủ công hiện tại (4 bước):** 1. Đọc tin nhắn hoặc email của khách → 2. Tra mã vé và loại vé → 3. Đối chiếu chính sách đổi/hoàn theo loại vé và lý do → 4. Soạn phản hồi và tạo yêu cầu hoàn tiền nếu đủ điều kiện.
- **Bước tốn thời gian/lỗi nhất:** Bước 3–4 (ước tính 5–8 phút/yêu cầu). Dễ trả lời sai chính sách khi quá tải.
- **Bước AI có thể hỗ trợ:** Phân loại ý định (đổi / hoàn / hỏi thông tin), trích mã vé, soạn phản hồi nháp theo đúng điều khoản chính sách.
- **Metric thành công (có số):** Thời gian phản hồi đầu tiên trong ngày cao điểm từ vài giờ (ước tính) xuống **dưới 30 phút**. **≥ 95%** phản hồi nháp được CSKH duyệt mà không phải sửa nội dung chính sách.
- **Quick Architecture:** [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent. LLM soạn nháp. Mọi quyết định hoàn tiền phải qua nhân viên duyệt.

---

## Lựa chọn cho Deep-Dive

Chọn **Card #1 (Xanh SM sự cố pin)**:
- Có ranh giới an toàn rõ ràng, kiểm thử được (ngưỡng 5% / 5 km). Đây cũng là bài toán của prompt prototype (`starter-code/prompt_prototype.py`), nên phần code và phần phân tích khớp nhau.
- Card #2 có giá trị, nhưng phần lớn giải quyết được bằng rule và tích hợp dữ liệu, không cần LLM.
- Card #3 chỉ đột biến theo thời tiết, khó có dữ liệu ổn định để đo baseline.
